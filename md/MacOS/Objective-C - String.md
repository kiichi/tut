
##Objective-C - String

###Convert NSData to NSString or vise versa

```objective-c
 aStr = [[NSString alloc] initWithData:aData encoding:NSASCIIStringEncoding];
 ```
```objective-c
 aData = [aStr dataUsingEncoding: NSASCIIStringEncoding];
 ```
###Join
```objective-c
 string = [chunks componentsJoinedByString: @","];
 ```
###Concat String
```objective-c
 for (int i=0; i<[arr count];i++){
    [theString appendString:[NSString stringWithFormat:@"%i,",[arr objectAtIndex:i]]];
 }
 ```

###Find something in between - useful for HTML Scraper
```objective-c
 {
 	NSString *answer;
 	NSScanner *myScanner = [NSScanner scannerWithString:theString];
 	BOOL found = FALSE;
 	while (! [myScanner isAtEnd]) {
 		if ([myScanner scanUpToString:@"<div class='definition'>" intoString:NULL] &&
 			[myScanner scanString:@"<div class='definition'>" intoString:NULL] &&
 			[myScanner scanUpToString:@"</div>" intoString:&answer]
 			) {
 			NSLog(@"Possible answer: %@", answer);
 			found = TRUE;
 		}
 	}
 	if (! found) NSLog(@"No definition for %@ found",WordToSearch);
 } 
 ```
###Find Substring
```objective-c
 if (range.location != NSNotFound) {
 ```
###Comparison
```objective-c
 if ([myStr compare:@"Hello"] == NSOrderedSame) { ...
 ```


###Converting String to Int or Float etc...
```objective-c
 int num = [numStr intValue]; // floatValue etc...
 ```
###Converting int or float to String
```objective-c
 ```
###Format string, and convert from other types, like sprintf
  NSString *str = [[NSString alloc] initWithFormat:@"(%.2f,%.2f,%.2f)",x,y,z];


###URL encoding
```objective-c
 ```

###Split
  NSString *string = @"oop:ack:bork:greeble:ponies";
  NSArray *chunks = [string componentsSeparatedByString: @","];



###Useful for Path Manipulation
```objective-c
 - (NSString *)stringByDeletingLastPathComponent;
 - (NSString *)stringByAppendingPathComponent:(NSString *)str;
 
 - (NSString *)pathExtension;
 - (NSString *)stringByDeletingPathExtension;
 - (NSString *)stringByAppendingPathExtension:(NSString *)str;
 
 - (NSArray *)stringsByAppendingPaths:(NSArray *)paths;
 Using the "/a/b/c/hello.txt" example:
 
  NSString *path = @"/a/b/c/hello.txt";
 
  NSString *fileName = [path lastPathComponent];
   // 'hello.txt'
 
  NSString *basePath = [path stringByDeletingLastPathComponent];
   // '/a/b/c'
 
  NSString *newPath = [basePath stringByAppendingPathComponent:@"goodbye.txt"];
   // '/a/b/c/goodbye.txt'





