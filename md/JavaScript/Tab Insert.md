
##Tab Insert

###Example
Note: Do not forget to put id on textarea.
```javascript
 <head>
 <SCRIPT>
 
 function CheckTab(el) {
   // Run only in IE
   // and if tab key is pressed
   // and if the control key is pressed
   if ((document.all) && (9==event.keyCode)) {
     // Cache the selection
     el.selection=document.selection.createRange();
     setTimeout("ProcessTab('" + el.id + "')",0)
   }
 }
 
 function ProcessTab(id) {
   // Insert tab character in place of cached selection
   document.all[id].selection.text=String.fromCharCode(9)
   // Set the focus
   document.all[id].focus()
 }
 </SCRIPT>
 </head>
 <body>
 
 <textarea cols=70 rows=25 name=content wrap=OFF id=tabbing onkeydown="CheckTab(this)">
 </textarea>
 
 </body>
 </html>
 ```


