
##iPhone - ScrollView, Pinch, Scroll

###Example

.h
```objective-c
 IBOutlet UIScrollView *mResizeView;
 UIImageView *mImage;
 }
 ```
.m
```objective-c
    [super viewDidLoad];
 	
  mImage = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"fireworks.png"]];   
     [mResizeView addSubview: mImage];  
    
     mResizeView.pagingEnabled = NO;  
     mResizeView.contentSize = CGSizeMake(mImage.frame.size.width, mImage.frame.size.height);  
     mResizeView.showsHorizontalScrollIndicator = NO;  
     mResizeView.showsVerticalScrollIndicator = NO;  
     mResizeView.scrollsToTop = YES;
     mResizeView.delegate = self; 
     // Pinch	
 mResizeView.maximumZoomScale = 4.0;  
 mResizeView.minimumZoomScale = 0.4;  
    
     [mResizeView addSubview: mImage];   
 }
 
 - (UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView {  
 return mImage;  
 }  
 ```

###Passing Touch Events

Scroll View does not take touch events (it takes zoom / drag). So if you need, you have to subclass it then overwrite the touchEnded method.


MyScrollView.h
```objective-c
 }
 @end
 ```
MyScrollView.m
```objective-c
 - (void) touchesEnded: (NSSet *) touches withEvent: (UIEvent *) event {	
 if (!self.dragging) {
 	[self.nextResponder touchesEnded: touches withEvent:event]; 
 }		
 [super touchesEnded: touches withEvent: event];
 }
 @end
 ```
Then you can catch touchEnded like
:Note|it uses locationInView so that i will return coordinate within the scrollview in case of larger image.


This is in controller that uses the MyScrollView

```objective-c
 UITouch *touch = [touches anyObject];	
 CGPoint location = [touch locationInView:mMyScrollView];
 NSLog(@"Location in Resize View %f,%f",location.x,location.y);
 }
 ```



