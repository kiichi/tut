
##iPhone - Email

###Example
Not tested yet

```objective-c
 NSString  *body = [@"Your message Body"stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];	
 NSString *mailString = [NSString stringWithFormat: @"mailto:%@?subject=%@&body=%@",							
 						@"kiichi@test.com",							
 						subject,							
 						body];
 [[UIApplication sharedApplication] openURL: [NSURL URLWithString:mailString]];
 ```
###Attachment (Using SDK3.0)
Include MessageUI.framework

```objective-c
 #import <MessageUI/MessageUI.h>
 @interface EmailTestViewController : UIViewController  <MFMailComposeViewControllerDelegate> {
 }
 - (IBAction)buttonPressed;
 @end
 ```
```objective-c
 #import "EmailTestViewController.h"
 
 @implementation EmailTestViewController
 
 - (void)dealloc {
     [super dealloc];
 }
 
 - (IBAction)buttonPressed {
 	if (![MFMailComposeViewController canSendMail]){
 		UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"ERROR" message:@"Email is not available"
 													   delegate:self cancelButtonTitle:@"OK" otherButtonTitles: nil];
 		[alert show];	
 		[alert release];
 		return;
 	}
 
 	MFMailComposeViewController *controller = [[MFMailComposeViewController alloc] init];
 	controller.mailComposeDelegate = self;
 	[controller setSubject:@"Subject goes here"];
 	[controller setToRecipients: [NSArray arrayWithObjects: @"info@objectgraph.com",  nil]];
 	[controller setMessageBody:@"<b>Hello</b> world" isHTML:YES];
 	UIImage *image = [UIImage imageNamed:@"test.png"];
 	NSData *imageData = UIImagePNGRepresentation(image);
 	[controller addAttachmentData:imageData mimeType :@"image/jpeg" fileName:@"test.png"];
 	[self presentModalViewController:controller animated:YES];
 	[controller release];
 }
 
 - (void)mailComposeController:(MFMailComposeViewController*)controller didFinishWithResult:(MFMailComposeResult)result error:(NSError*)error {
 	[self becomeFirstResponder];
 	[self dismissModalViewControllerAnimated:YES];
 }
 
 
 @end
 ```



