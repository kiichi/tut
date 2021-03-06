
##Upload

###Simple Example
:Note|In order to fit on server side program, you have to specify your file object's name. As default, flex add "Filedata" as the key. In the second argument of upload function, you can change this value to what ever you want.

```flex
 ```
This will be retrieved in django like
```flex
 ```
In PHP 
```flex
 ```
This is the default value:
  request.FILES["Filedata"]
  $_FILES['Filedata']

```flex
     <mx:Script>
         <![CDATA[
             import flash.events.*;
             import flash.net.FileReference;
             import flash.net.URLRequest;        
             import mx.controls.Alert;
             
             private var uploadReq:URLRequest;
             private var file:FileReference;
     
             public function initApp() :void  {
                 uploadReq = new URLRequest();
                // uploadReq.contentType = "multipart/form-data";
                // uploadReq.method = URLRequestMethod.POST;
                 uploadReq.url = "http://localhost:8000/webservice/uploadavatar/json/";
 
                 file = new FileReference();
                 file.addEventListener(Event.SELECT, selectHandler);
                 file.addEventListener(IOErrorEvent.IO_ERROR, ioErrorHandler);
                 file.addEventListener(ProgressEvent.PROGRESS, progressHandler);
                 file.addEventListener(Event.COMPLETE, completeHandler);
                 file.browse();
             }
     
             private function selectHandler(event:Event):void {
                 var file:FileReference = FileReference(event.target);
                 Alert.show("selectHandler: name=" + file.name + " URL=" + uploadReq.url);                
                 file.upload(uploadReq,"file",false);
             }
     
             private function ioErrorHandler(event:IOErrorEvent):void {
                 Alert.show("ioErrorHandler: " + event);
             }
     
             private function progressHandler(event:ProgressEvent):void {
                 var file:FileReference = FileReference(event.target);
                 Alert.show("progressHandler: name=" + file.name + " bytesLoaded=" 
 				+ event.bytesLoaded + " bytesTotal=" + event.bytesTotal);
             }
     
             private function completeHandler(event:Event):void {
                 Alert.show("completeHandler: " + event);
             }
                 
             ]]>
     </mx:Script>
 </mx:Application>
 ```

###Multiple File Upload Example
```flex
 <mx:Application xmlns:mx="http://www.adobe.com/2006/mxml" 
 layout="absolute" 
 creationComplete="initApp()" viewSourceURL="srcview/index.html">
     <mx:Script>
         <![CDATA[
             /*
             Examples_FileUpload
             Written by: Dustin Andrew dustin@flash-dev.com www.flash-dev.com
             */
         
             import mx.states.*;
             import mx.controls.*;
             import mx.managers.*;
             import mx.events.*;
             import flash.events.*;
             import flash.net.*;
             
             private const _strUploadDomain:String = "http://codycodingcowboy.cahlan.com/";
             private const _strUploadScript:String = _strUploadDomain + "files/upload.php";
             
             private var _arrUploadFiles:Array;
             private var _numCurrentUpload:Number = 0;
             private var _refAddFiles:FileReferenceList;    
             private var _refUploadFile:FileReference;
             
             private var _winProgress:winProgress;
             
             private function initApp():void {
                 Security.allowDomain("*");
                 _arrUploadFiles = new Array();
             }            
             
             // Called to add file(s) for upload
             private function addFiles():void {
                 _refAddFiles = new FileReferenceList();
                 _refAddFiles.addEventListener(Event.SELECT, onSelectFile);
                 _refAddFiles.browse();
             }
             
             // Called to remove selected file(s) for upload
             private function removeFiles():void {
                 var arrSelected:Array = listFiles.selectedIndices;
                 for (var i:Number = 0; i < arrSelected.length; i++) {
                     _arrUploadFiles[Number(arrSelected[i])] = null;
                 }
                 for (var j:Number = 0; j < _arrUploadFiles.length; j++) {
                     if (_arrUploadFiles[j] == null) {
                         _arrUploadFiles.splice(j, 1);
                         j--;
                     }
                 }
                 listFiles.dataProvider = _arrUploadFiles;
                 listFiles.selectedIndex = 0;
                 if (_arrUploadFiles.length == 0) {
                     btnUpload.enabled = false;
                 } else {
                     btnUpload.enabled = true;
                 }
             }
             
             // Called when a file is selected
             private function onSelectFile(event:Event):void {
                 var arrFoundList:Array = new Array();
                 // Get list of files from fileList, make list of files already on upload list
                 for (var i:Number = 0; i < _arrUploadFiles.length; i++) {
                     for (var j:Number = 0; j < _refAddFiles.fileList.length; j++) {
                         if (_arrUploadFiles[i].label == _refAddFiles.fileList[j].name) {
                             arrFoundList.push(_refAddFiles.fileList[j].name);
                             _refAddFiles.fileList.splice(j, 1);
                             j--;
                         }
                     }
                 }
                 if (_refAddFiles.fileList.length >= 1) {
                     for (var k:Number = 0; k < _refAddFiles.fileList.length; k++) {
                         _arrUploadFiles.push({label:_refAddFiles.fileList[k].name, data:_refAddFiles.fileList[k]});
                     }
                     listFiles.dataProvider = _arrUploadFiles;
                     listFiles.selectedIndex = _arrUploadFiles.length - 1;
                 }                
                 if (arrFoundList.length >= 1) {
                     Alert.show("The file(s): \n\n? " 
 + arrFoundList.join("\n? ") 
 + "\n\n...are already on the upload list. "
 + "Please change the filename(s) or pick a different file.", 
 "File(s) already on list");
                 }
                 if (_arrUploadFiles.length == 0) {
                     btnUpload.enabled = false;
                 } else {
                     btnUpload.enabled = true;
                 }
             }
             
             
             // Cancel and clear eventlisteners on last upload
             private function clearUpload():void {
                 _numCurrentUpload = 0;
                 _refUploadFile.removeEventListener(ProgressEvent.PROGRESS, onUploadProgress);
                 _refUploadFile.removeEventListener(Event.COMPLETE, onUploadComplete);
                 _refUploadFile.removeEventListener(IOErrorEvent.IO_ERROR, onUploadIoError);
                 _refUploadFile.removeEventListener(SecurityErrorEvent.SECURITY_ERROR, onUploadSecurityError);
                 _refUploadFile.cancel();
             }
             
             // Called to upload file based on current upload number
             private function startUpload(booIsFirst:Boolean):void {
                 if (booIsFirst) {
                     _numCurrentUpload = 0;
                 }
                 if (_arrUploadFiles.length > 0) {
                     _winProgress = winProgress(PopUpManager.createPopUp(this, winProgress, true));
                     _winProgress.btnCancel.removeEventListener("click", onUploadCanceled);
                     _winProgress.btnCancel.addEventListener("click", onUploadCanceled);
                     _winProgress.title = "Uploading file to " + _strUploadDomain;
                     _winProgress.txtFile.text = _arrUploadFiles[_numCurrentUpload].label;
                     _winProgress.progBar.label = "0%";
                     PopUpManager.centerPopUp(_winProgress);
                     
                     // Variables to send along with upload
                     var sendVars:URLVariables = new URLVariables();
                     sendVars.action = "upload";
                     
                     var request:URLRequest = new URLRequest();
                     request.data = sendVars;
                     request.url = _strUploadScript;
                     request.method = URLRequestMethod.POST;
                     _refUploadFile = new FileReference();
                     _refUploadFile = _arrUploadFiles[_numCurrentUpload].data;
                     _refUploadFile.addEventListener(ProgressEvent.PROGRESS, onUploadProgress);
                        _refUploadFile.addEventListener(Event.COMPLETE, onUploadComplete);
                     _refUploadFile.addEventListener(IOErrorEvent.IO_ERROR, onUploadIoError);
                       _refUploadFile.addEventListener(SecurityErrorEvent.SECURITY_ERROR, onUploadSecurityError);
                     _refUploadFile.upload(request, "file", false);
                 }
             }
             
             // Called on upload cancel
             private function onUploadCanceled(event:Event):void {
                 PopUpManager.removePopUp(_winProgress);
                 _winProgress == null;
                 _refUploadFile.cancel();
                 clearUpload();
             }
             
             // Get upload progress
             private function onUploadProgress(event:ProgressEvent):void {
                 var numPerc:Number = Math.round((Number(event.bytesLoaded) / Number(event.bytesTotal)) * 100);
                 _winProgress.progBar.setProgress(numPerc, 100);
                 _winProgress.progBar.label = numPerc + "%";
                 _winProgress.progBar.validateNow();
                 if (numPerc > 90) {
                     _winProgress.btnCancel.enabled = false;
                 } else {
                     _winProgress.btnCancel.enabled = true;
                 }
             }
             
             // Called on upload complete
             private function onUploadComplete(event:Event):void {
                 _numCurrentUpload++;
                 PopUpManager.removePopUp(_winProgress);
                 if (_numCurrentUpload < _arrUploadFiles.length) {
                     startUpload(false);
                 } else {
                     Alert.show("File(s) have been uploaded.", "Upload successful");
                 }
             }
             
             // Called on upload io error
             private function onUploadIoError(event:IOErrorEvent):void {
                 Alert.show("IO Error in uploading file.", "Error");
                 PopUpManager.removePopUp(_winProgress);
                 _winProgress == null;
                 _refUploadFile.cancel();
                 clearUpload();
             }
             
             // Called on upload security error
             private function onUploadSecurityError(event:SecurityErrorEvent):void {
                 Alert.show("Security Error in uploading file.", "Error");
                 PopUpManager.removePopUp(_winProgress);
                 _winProgress == null;
                 _refUploadFile.cancel();
                 clearUpload();
             }
             
         ]]>
     </mx:Script>
     
     <mx:Canvas top="10" bottom="10" left="10" right="10">
         <mx:Panel width="300" height="266" layout="absolute" 
 horizontalCenter="0" verticalCenter="0" 
 id="panUpload" title="Select file(s) for upload">
             <mx:VBox left="10" bottom="10" top="10" right="10">
                 <mx:List width="100%" id="listFiles" height="100%" allowMultipleSelection="true"/>
                 <mx:HBox width="100%" horizontalAlign="center">
                     <mx:Button label="Add file(s).." id="btnAdd" click="addFiles()"/>
                     <mx:Button label="Remove file(s)" id="btnRemove" click="removeFiles()"/>
                 </mx:HBox>
             </mx:VBox>
             <mx:ControlBar horizontalAlign="right">
                 <mx:Button label="Upload file(s)" id="btnUpload" click="startUpload(true)" enabled="false"/>
             </mx:ControlBar>
         </mx:Panel>
     </mx:Canvas>
 </mx:Application>
 ```
###winProgress.mxml
```flex
 <mx:TitleWindow xmlns:mx="http://www.adobe.com/2006/mxml" layout="absolute" width="400" height="145" title="Progress Bar Window">
     <mx:VBox left="10" top="10" right="10" bottom="10" horizontalAlign="center" verticalAlign="top">
         <mx:Label text="Filename" id="txtFile" enabled="true" width="100%"/>
         <mx:ProgressBar width="100%" id="progBar" mode="manual"/>
         <mx:Button label="Cancel" id="btnCancel"/>
     </mx:VBox>
 </mx:TitleWindow>
 
 ```
```flex
 $errors = array();
 $data = "";
 $success = "false";
 function return_result($success,$errors,$data) {
 	echo("<?xml version=\"1.0\" encoding=\"utf-8\"?>");
 ?>
 <results>
 <success><?=$success;?></success>
 <?=$data;?>
 <?=echo_errors($errors);?>
 </results>
 <?
 }
 
 function echo_errors($errors) {
 
 	for($i=0;$i<count($errors);$i++) {
 ?>
 <error><?=$errors[$i];?></error>
 <?
 	}
 
 }
 
 $file_temp = $_FILES['file']['tmp_name'];
 $file_name = $_FILES['file']['name'];
 
 $file_path = $_SERVER['DOCUMENT_ROOT']."/data";
 
 //checks for duplicate files
 if(!file_exists($file_path."/".$file_name)) {
 
 	//complete upload
 	$filestatus = move_uploaded_file($file_temp,$file_path."/".$file_name);
 
 	if(!$filestatus) {
 		$success = "false";
 		array_push($errors,"Upload failed. Please try again.");
 	}
 }
 else {
 	$success = "false";
 	array_push($errors,"File already exists on server.");
 }
 
 return_result($success,$errors,$data);
 
 ?>
 
 ```
In view file

```flex
 # just do print request.FILES if you do not know about the key
 # in this example, flex specify file key as fileref.upload(req,'file',false);
 file = request.FILES['file']
 
 # Other data on the request.FILES dictionary - add restriction for real usage HERE!
 
 # Sanitizing goes here ...
 # File size checking
 filesize = len(file['content'])
 if filesize > 200000:
 	raise Exception('file size is too big')
 
 # content type checking
 filetype = file['content-type']
 if filetype != 'application/octet-stream':
 	raise Exception('content type does not match')
 		
 #extention check
 filename = file['filename'] 
 ext = path.splitext(filename)[1]
 if ext != '.png' and ext != '.jpg' and ext != '.gif':
 	raise Exception('Invalid file type ' + ext)
 
 # PIL goes here, BUT try to change file size on client size!
 # maybe just check the file size is 48*48 otherwise kick
 print 'uploading ' + path.join(MEDIA_ROOT,subdir,filename)
 fd = open(path.join(MEDIA_ROOT,subdir,request.user.username+'.jpg'), 'wb')  
 fd.write(file['content'])  
 fd.close()  
 ```
###Reference
http://blog.flexexamples.com/2007/09/21/uploading-files-in-flex-using-the-filereference-class/
http://www.adobe.com/devnet/air/flex/articles/uploading_air_app_to_server_print.html




