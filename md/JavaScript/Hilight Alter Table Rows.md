
##Hilight Alter Table Rows

###Demo
http://xxki.com/file/js/alter.html

###Sample Code
```javascript
 	<head>
 		<title>Alter Color Test</title>
 		<script language="JavaScript">
 			<!--
 			function alternate(id){
 				if(document.getElementsByTagName){  
 					var table = document.getElementById(id);  
 					var rows = table.getElementsByTagName("tr");  
 					for(i = 0; i < rows.length; i++){          
 						//manipulate rows
 						if(i % 2 == 0){
 							rows[i].className = "even";
 							}else{
 							rows[i].className = "odd";
 						}      
 					}
 				}
 			}
 			// -->
 		</script>
 
 		<style>
 			table, td{ border:1px solid black;border-collapse:collapse;}
 			.odd{background-color: white;}
 			.even{background-color: gray;}
 		</style>
 	</head>
 	<body onload="alternate('mytable')">
 		<table id="mytable">
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 			<tr><td>data</td><td>data</td><td>data</td></tr>
 		</table> 
 	</body>
 </html>
 ```


