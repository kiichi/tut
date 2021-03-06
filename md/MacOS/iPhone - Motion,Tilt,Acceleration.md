
##iPhone - Motion,Tilt,Acceleration

###3.0 update - just add this in controller

```objective-c
    if (event.type == UIEventTypeMotion) {
    }
 }
 ```

###Description
+Add UIAccelerometerDelegate as interface of the delegate
+set delegate and interval
+Implement accelerometer method to catch the tilt


###Sample Code - ShakeMe
ShakeMeAppDelegate.h
```objective-c
 
 @class MyView;
 // Add UIAccelerometerDelegate as interface here
 @interface ShakeMeAppDelegate : NSObject  <UIAccelerometerDelegate> {
     UIWindow *window;
     MyView *contentView;
 }
 
 @property (nonatomic, retain) UIWindow *window;
 @property (nonatomic, retain) MyView *contentView;
 
 @end
 ```

ShakeMeAppDelegate.m
```objective-c
 #import "MyView.h"
 
 // Additional Code ---------------------------------------------------------------
 // Constant for the number of times per second (Hertz) to sample acceleration.
 #define kAccelerometerFrequency	3
 
 @implementation ShakeMeAppDelegate
 
 @synthesize window;
 @synthesize contentView;
 
 - (void)applicationDidFinishLaunching:(UIApplication *)application {	
 	// Create window
 	self.window = [[[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]] autorelease];
     
     // Set up content view
 	self.contentView = [[[MyView alloc] initWithFrame:[[UIScreen mainScreen] applicationFrame]] autorelease];
 	[window addSubview:contentView];
 	// sometime sensor does not start, see the solution below
 	// Additional code start ---------------------------------------------------------------
 	//[[UIAccelerometer sharedAccelerometer] setUpdateInterval:(1.0 / kAccelerometerFrequency)];
 	//[[UIAccelerometer sharedAccelerometer] setDelegate:self];
     // Additional code end ---------------------------------------------------------------
 	
 	// Show window
 	[window makeKeyAndVisible];
 }
 ```
```objective-c
 //Configure and start accelerometer
 [[UIAccelerometer sharedAccelerometer] setUpdateInterval:(1.0 / kAccelerometerFrequency)];
 [[UIAccelerometer sharedAccelerometer] setDelegate:self];
 }
 ```

```objective-c
 - (void)dealloc {
 	[contentView release];
 	[window release];
 	[super dealloc];
 }
 
 // Additional code ---------------------------------------------------------------
 // UIAccelerometerDelegate method, called when the device accelerates.
 - (void)accelerometer:(UIAccelerometer *)accelerometer didAccelerate:(UIAcceleration *)acceleration {
 	[contentView setMotion:acceleration.x Y:acceleration.y Z:acceleration.z];
 }
 
 @end
 ```

```objective-c
 ```
```objective-c
 
 @interface MyView : UIView {
 	UILabel *lblShake;
 }
 -(void)setMotion:(float)x Y:(float)y Z:(float)z;
 @end
 ```
```objective-c
 ```
```objective-c
 
 @implementation MyView
 -initWithFrame:(CGRect)frame {
 	if (self = [super initWithFrame:frame]) {
 		self.backgroundColor = [UIColor darkGrayColor];	
 		CGRect lblRect = CGRectMake(10,50,300,50);
 		lblShake = [[[UILabel alloc] initWithFrame:lblRect] autorelease];
 		lblShake.backgroundColor = [UIColor lightGrayColor];
 		[lblShake setText:@"Shake Me!"];
 		[lblShake setTextAlignment:UITextAlignmentCenter];
 		[self addSubview:lblShake];
 	}
 	return self;
 }
 
 -(void)dealloc{
 	[lblShake release];
 	[self release];
 	[super dealloc];
 }
 
 -(void)setMotion:(float)x Y:(float)y Z:(float)z{
 	NSString *str = [[NSString alloc] initWithFormat:@"(%.2f,%.2f,%.2f)",x,y,z];
 	[lblShake setText:str];
 }
 
 @end
 
 
 ```






