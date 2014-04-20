
##Response - Send Pdf, Image, etc...

###PDF Sending Over HTTP
```asp.net
 	Response.ClearContent();
 	Response.ClearHeaders();
 	Response.ContentType = "application/pdf";
 	Response.AddHeader("Content-disposition", "attachment; filename=example.pdf");		
 	Response.OutputStream.Write(byteArr, 0, byteArr.Length);
 	Response.End();	
 }
 ```
Sanitize output attachment file name
```asp.net
 ```
You can have byte array like this:
```asp.net
 ```
###Download Text File
```asp.net
 	string test = "test1\ntest2\n\ntest hello\n world";
 	SendFile(StrToByteArray(test), "test.txt");
 }
 ```

```asp.net
 	Response.ClearContent();
 	Response.ClearHeaders();
 	Response.ContentType = "application/octet-stream";
 	Response.AddHeader("Content-disposition", "attachment; filename=\""+fileName+"\"");
 	Response.OutputStream.Write(byteArr, 0, byteArr.Length);
 	//Response.WriteFile("c:\\test.txt"); // if you have physical file on server use this
 	Response.Flush();
 	Response.End();
 }
 ```
```asp.net
 	System.Text.ASCIIEncoding encoding = new System.Text.ASCIIEncoding();
 	return encoding.GetBytes(str);
 }
 ```
###Note
Try this if you have file
```asp.net
 ```


