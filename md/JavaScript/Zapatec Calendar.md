
##Zapatec Calendar

###Example
Include this in <head>
```javascript
 <script type="text/javascript" src="scripts/calendar/calendar.js"></script>
 <script type="text/javascript" src="scripts/calendar/lang/calendar-en.js"></script>
 <script type="text/javascript" src="scripts/calendar/calendar-setup.js"></script>
 ```
and use it like this
```javascript
 <img src="scripts/calendar/img.gif" id="datepicker1" style="cursor: pointer;"  />
 <script type="text/javascript">
 Calendar.setup({
 inputField     :    "date1",     // id of the input field
 ifFormat       :    "%m/%d/%Y",      // format of the input field
 button         :    "datepicker1",  // trigger for the calendar (button ID)
 align          :    "Br",           // alignment (defaults to "Bl")
 singleClick    :    true
 });
 </script>
 ```

###Problem with ASP.NET Validator
If you have a conflict with ASP.NET validator components, modify
```javascript
 ```
```javascript
 //			p.inputField.value = cal.date.print(p.ifFormat);
 //			if (typeof p.inputField.onchange == "function")
 //				p.inputField.onchange();
 //		}
        if (update && p.inputField) {
          p.inputField.value = cal.date.print(p.ifFormat);
          if (typeof p.inputField.onchange == "function") {
            if (window.event && p.inputField.Validators) {
              window.event.srcElement.Validators = p.inputField.Validators;
            }
            try { p.inputField.onchange(); } catch (e) {}
          }
        }


###Integrating in GridView
Since when you hit edit, GridView Insert the row number into the input box's id, so you have to generate the part of JavaScript.
```javascript
 <asp:TextBox ID="tbEditDueDate" runat="server" Text='<%# Bind("DueDate", "{0:MM/dd/yyyy}") %>' Width="79px"></asp:TextBox>
 	<img src="scripts/calendar/img.gif" id="datepicker2" style="cursor: pointer;"  />
 	<script type="text/javascript">
 	Calendar.setup({
 	inputField     :    "ctl00_ContentPlaceHolder1_gvItems_ctl0<%=(gvItems.EditIndex+2).ToString() %>_tbEditDueDate",
 	ifFormat       :    "%m/%d/%Y",      // format of the input field
 	button         :    "datepicker2",  // trigger for the calendar (button ID)
 	align          :    "Br",           // alignment (defaults to "Bl")
 	singleClick    :    true
 	});
 	</script>
 </EditItemTemplate>
 ```

###Links
http://www.dynarch.com/projects/calendar/




