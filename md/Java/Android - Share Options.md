
##Android - Share Options

###Share Options Example
```java
 			sharingIntent.setType("text/html");
 			sharingIntent.putExtra(android.content.Intent.EXTRA_TEXT, Html.fromHtml("<p>This is the text that will be shared.</p>"));
 			startActivity(Intent.createChooser(sharingIntent,"Share using"));
 ```

```java
 Uri screenshotUri = Uri.parse(path);
 sharingIntent.setType("image/png");
 sharingIntent.putExtra(Intent.EXTRA_STREAM, screenshotUri);
 startActivity(Intent.createChooser(sharingIntent, "Share image using"));
 ```
###Reference
http://sudarmuthu.com/blog/sharing-content-in-android-using-action_send-intent





