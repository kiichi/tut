
##JSON

###Installation
%%%In .NET%%%
This is nice stand-alone library for .NET environment
http://www.newtonsoft.com/products/json/quickstart.aspx

+Right click on project
+Add Reference
+Browse Newtonsoft.Json.dll

%%%In PHP%%%
JSON library is ready as extension of apache. 
+Download php_json.dll
http://www.aurore.net/projects/php-json/
+Copy php_json.dll in ext directory
+Modify php.ini (Add extension=php_json.dll)
+Restart Apache



###Description
First, this ASP.NET example is code to demonstrate how to achive cross-domain data transfer. Basic model is like this
+ASP.NET spit out JavaScript library which return JSON object. JSON object is just serialized string array object.
+In html page, javascript include the aspx page as library, and call the function to obtain JSON object. The object is just array of string in javascript.

Second example demonstrates JSON object's serialization/deserialization in PHP language.

###Building JSON Service - JSONTest.cs File
```javascript
 using System.Data;
 using System.Configuration;
 using System.Collections;
 using System.Web;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Web.UI.HtmlControls;
 using Newtonsoft.Json;
 
 public partial class JSONTest : System.Web.UI.Page {
 	public string mOutput;
 	protected void Page_Load(object sender, EventArgs e) {
 		string[] arr = new string[] { "apple","banana","orange","strawberry" };
 		mOutput = JavaScriptConvert.SerializeObject(arr);
 		//Response.Write(mOutput);
 		
 	}
 }
 ```

###Building JSON Service - JSONTest.aspx Page
This is assumed to be used as .js library. getObj return parsed JSON object.
```javascript
 // You do not need to wrap in JS function if you use in another language like PHP, Python, etc...
 function getObj() {
     return eval('(<%=mOutput %>)');
     //return eval('(["apple","banana","orange","strawberry"])');
 }
 ```
###Consuming JSON in JavaScript
```javascript
 <head>
 </head>
 <body>
  <script type="text/javascript" src="http://(aspx page location)/JSONTest.aspx"></script>
     <script language = "javascript" type="text/javascript" >
  var obj = getObj();
  document.write(obj[0] + "<BR>");
  document.write(obj[1] + "<BR>");
  document.write(obj[2] + "<BR>");
  document.write(obj[3] + "<BR>");
     </script>
 </body>
 </html>
 ```
###Service / Client Test in PHP

```javascript
 $arr = array ('a'=>1,'b'=>2,'c'=>3,'d'=>4,'e'=>5);
 echo json_encode($arr);
 echo '<hr>';
 ?> 
 <hr>
 <pre>
 <?php
 $json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';
 var_dump(json_decode($json));
 
 var_dump(json_decode($json, true));
 
 ?> 
 </pre>
 ```



