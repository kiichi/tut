
##AJAX Framework

###Background
ASP.NET AJAX is ex-Atlas javascript wrapper & the components. This will take your HTTP request from the control with the javascript, and url handler automatically respond with dynamic url. As result, programmer might not touch any javascript like the example below.

###Installation
Go to
http://asp.net/ajax/
and download the package & install.

###UpdatePanel 
1. If you issue event (e.g. button click) inside the panel itself, you do not need any extra script. You can place components, and it automatically takes care of it.

2. If you want to trigger from outside of the UpdatePanel
You need to assign "Trigger" as if you are setting validators.
-Click UpdatePanel and Open Trigger in the property
-Add->Async ...->Set control to be picked up and event which the control uses.
e.g. If you want to update the panel by external button, you should specify the button's ID and Click event. Of course, you can add multiple triggers. 

###Sample Script
AjaxTest.aspx
```csharp
 
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
 <html xmlns="http://www.w3.org/1999/xhtml">
 <head runat="server">
     <title>AJAX Test</title>
 </head>
 <body>
     <form id="form1" runat="server">
         <asp:ScriptManager ID="ScriptManager1" runat="server" />
         <div>
             <asp:Timer ID="Timer1" runat="server" Interval="3000" OnTick="Timer1_Tick">
             </asp:Timer>
         </div>
         <asp:UpdatePanel ID="UpdatePanel1" runat="server">
             <ContentTemplate>
                 <asp:Label ID="Label1" runat="server"></asp:Label>
                 <asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Refresh" />
             </ContentTemplate>
             <Triggers>
                 <asp:AsyncPostBackTrigger ControlID="Button2" EventName="Click" />
                 <asp:AsyncPostBackTrigger ControlID="Timer1" EventName="Tick" />
             </Triggers>
         </asp:UpdatePanel>
         <asp:Button ID="Button2" runat="server" OnClick="Button2_Click" Text="Refresh from Outside" />
     </form>
 </body>
 </html> 
 ```
AjaxTest.aspx.cs
```csharp
 using System.Data;
 using System.Configuration;
 using System.Web;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Web.UI.HtmlControls;
 
 public partial class _Default : System.Web.UI.Page 
 {
     protected void Page_Load(object sender, EventArgs e)
     {
 		
     }
 	protected void Timer1_Tick(object sender, EventArgs e) {
 		Label1.Text = "Timer: " + DateTime.Now.ToString();
 	}
 	protected void Button1_Click(object sender, EventArgs e) {
 		Label1.Text = "Inside Button: " + DateTime.Now.ToString();
 	}
 	protected void Button2_Click(object sender, EventArgs e) {
 		Label1.Text = "Outside Button: " + DateTime.Now.ToString();
 	}
 }
 ```




