
##iPhone - Draw 2D


###Context and Image release with large bitmap data
```objective-c
 CGContextDrawImage(context, CGRectMake(0,0, width, height), image.CGImage);
 ```
```objective-c
 // Release process here
 // VERY IMPORTANT:
 // CGContextRelease might not release whatever you assigned data if you create a bitmap.
 // get the bitmap data, and make sure call free first.
 // CGContextRelease basically decliment reference counter.
 CGImageRef iref = CGBitmapContextCreateImage(context);
 void *data = CGBitmapContextGetData(context);
 free(data);
 // then release context
 CGContextRelease(context);
 
 ```
###Include framework
CoreGraphics.Framework

###Draw Circle

```objective-c
 CGContextRef context = UIGraphicsGetCurrentContext();
 CGContextSetRGBStrokeColor(context, 1.0, 1.0, 1.0, 1.0);
 CGContextSetRGBFillColor(context, 0.0, 0.0, 1.0, 1.0);
 CGContextSetLineWidth(context, 2.0);
 CGRect circleRect = CGRectMake(30.0, 30.0, 60.0, 60.0);
 CGContextAddEllipseInRect(context, circleRect);
 CGContextStrokePath(context);	
 CGContextFillEllipseInRect(context, circleRect);
 }
 ```




