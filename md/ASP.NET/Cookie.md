
##Cookie

###Example
Using Single "Value"
```csharp
 HttpCookie cookie = new HttpCookie("Username", "Kiichi");
 cookie.Expires = DateTime.Now.AddDays(30);
 Response.Cookies.Add(cookie);
 
 HttpCookie cookie2 = new HttpCookie("Hash", "JDkufoafjakljdkafuoajfalfja");
 cookie2.Expires = DateTime.Now.AddDays(30);
 Response.Cookies.Add(cookie2);
 }
 ```
```csharp
 for (int i = 0; i < Request.Cookies.Count; i++) {
 	Response.Write("Name=" + Request.Cookies[i].Name + "/Value=" + Request.Cookies[i].Value +"<br/>");
 }
 }
 ```
Using Multiple Key/Value Set
```csharp
 Request.Cookies.Remove("UserSettings");
 HttpCookie cookie = new HttpCookie("UserSettings");
 cookie["Username"] = "ktakeuch";
 cookie["Key"] = "fdjaklfjaidafalfdjakfjlajaljfaljaafldjka";
 cookie.Expires = DateTime.Now.AddDays(1);
 	
 Response.Cookies.Add(cookie);
 }
 ```
```csharp
 if (Request.Cookies["UserSettings"] != null) {
 	for (int i = 0; i < Request.Cookies["UserSettings"].Values.Count; i++) {
 		Response.Write(Request.Cookies["UserSettings"].Values.Keys[i] + " = " + Request.Cookies["UserSettings"].Values[i] + "<BR/>");
 	}
 	Response.Write(Request.Cookies["UserSettings"].Expires.ToShortDateString());
 }
 }
 ```



