
##Freeze Screen - Prevent user to submit twice

###freeze.js
You can simply declare freeze function to disable the submit button or lock entire screen
  
 var mLoopCounter = 1;
 var mMaxLoop = 40;
 var mIntervalId;
 
 function HideAllDDL() {
 	var elemArr = document.getElementsByTagName("select"); // can be iframe or applet too
 	for (var i=0; i<elemArr.length; i++) {
 			elemArr[i].style.visibility="hidden"; 
 	}
 }
 
 function ShowAllDDL() {
 	var elemArr = document.getElementsByTagName("select"); // can be iframe or applet too
 	for (var i=0; i<elemArr.length; i++) {
 			elemArr[i].style.visibility="visible"; 
 	}
 }
 
 function BeginPageLoad() {	
 	mIntervalId = window.setInterval("mLoopCounter=UpdateProgress(mLoopCounter, mMaxLoop)", 200);
 	HideAllDDL();
 }
 
 function EndPageLoad() {
 	window.clearInterval(mIntervalId);	
 	ShowAllDDL();
 }
 
 function UpdateProgress(currentCounter, mMaxLoopCount) {
 
 	currentCounter += 1;
 	
 	if (currentCounter <= mMaxLoopCount) {
 		document.getElementById("ProcessMessage").innerHTML += ".";		
 		return currentCounter;
 	}
 	else {
 		document.getElementById("ProcessMessage").innerHTML = "&nbsp;";
 		return 1;
 	}
 }
 
 function FreezeScreen(msg) {
     EndPageLoad();// init
 	scroll(0,0);
 	var outerPane = document.getElementById('FreezePane');
 	var innerPane = document.getElementById('InnerFreezePane');
        // <img src="images/pix.gif" id="ProcessImage" alt="processing" />
 	//var processImage = document.getElementById('ProcessImage');
 	if (outerPane) outerPane.className = 'FreezePaneOn';
 	if (innerPane) innerPane.innerHTML = msg;
 	
 	//if (processImage) processImage.src = "images/process.gif";
 	BeginPageLoad();
 }
 
 ```


###freeze.css
    .FreezePaneOff
    {
       visibility: hidden;
       display: none;
       position: absolute;
       top: -100px;
       left: -100px;
    }
 
    .FreezePaneOn
    {
       position: absolute;
       top: 0px;
       left: 0px;
       visibility: visible;
       display: block;
       width: 100%;
       height: 100%;
       background-color: #666;
       z-index: 999;
       filter:alpha(opacity=85);
       -moz-opacity:0.85;
       padding-top: 20%;
    }
 
    .InnerFreezePane
    {
       text-align: center;
       width: 66%;
       background-color: #336699;
       color: White;
       font-size: large;
       border: dashed 2px #111;
       padding: 9px;
    }
    
    #ProcessMessage 
    {
 	font-size:30px;
 	text-align:center;
 	
    }

###HTML
```csharp
    <div id="InnerFreezePane" class="InnerFreezePane"> </div>
    <br />
    <div align="center"><div id="ProcessMessage"></div>
 </div>
 ```
###Usage
In aspx or master page
```csharp
 <script type="text/javascript" src="js/freeze.js"></script>
 ```
```csharp
 ```
###Client Side Hi-jacking for validation conflict problem
In aspx page (make sure to place in HEAD tag)
```csharp
 var refSubmit = null;
 // If IE
 if (!document.addEventListener) {
 	refSubmit = document.forms[0].onsubmit;    
 }
 
 var isSubmitButton = false;
 function SetIsSubmitButton(){
 	isSubmitButton = true;
 }
 function mySubmit()
 {
 	var blnDoSubmit = true;
 	// If IE
 	if (!document.addEventListener) { 
 		blnDoSubmit = refSubmit(); // get true or false
 	}
 	else {
 		// count how many errors on asp.net validator controls
 		var i;
 		var cnt = 0;
 		for (i = 0; i < Page_Validators.length; i++) {
 			if (!Page_Validators[i].isvalid) {
 				cnt++;
 			}
 		}
 		//alert(cnt);
 		// if no validation error, you can submit
 		if (cnt == 0) {
 			blnDoSubmit = true;
 		}
 		else {
 			blnDoSubmit = false;
 		}    
 	}
 
 	if (blnDoSubmit) {
 		if (isSubmitButton) { 
 			FreezeScreen(' Your Data is Being Processed...');
 		}
 	}
 	isSubmitButton = false;
 	return blnDoSubmit;
 }
 
 // If IE
 if (!document.addEventListener) {
 	document.forms[0].onsubmit = mySubmit;
 }
 else {
 	//alert('mysubmit was assigned');
 	window.captureEvents(Event.SUBMIT);
 	window.onsubmit = mySubmit;
 }
 </script>
 
 ```
and in cs page
```csharp
 ```
If you do not have any other refreshing mechanism (e.g. auto-postback drop down menu) or If you would like to insert splash for all postback process, you can just put like this (but this does not work on IE):
```csharp
 var refSubmit = document.forms[0].onsubmit;
 
 function mySubmit()
 {
   var blnDoSubmit = refSubmit();
   if (blnDoSubmit) ShowSplashScreen();
   return blnDoSubmit;
 }
 
 document.forms[0].onsubmit = mySubmit;
 </script>
 ```


