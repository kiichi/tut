
##iPhone - Geometory Collision Detection etc

###Point vs Rect
```objective-c
 ```
###Rect vs Rect - contains or not
```objective-c
 ```
###Rect vs Rect - intersect or not
```objective-c
 ```
###Get Intersection of Rects
```objective-c
 ```
You can also check collision like this
```objective-c
 if (CGRectIsNull(r)){ ...
 ```
###Rect - Offset
```objective-c
 ```
###Rect - expand
```objective-c
 ```
###NSMutableArray and CGRect
```objective-c
 rectArray = [[NSMutableArray alloc] init];
 [rectArray addObject:[NSValue valueWithCGRect:firstRect]];
 ```
```objective-c
 ```



###Reference
http://developer.apple.com/documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html

```objective-c
 Creating a Dictionary Representation From a Geometric Primitive
 
     * CGPointCreateDictionaryRepresentation
     * CGSizeCreateDictionaryRepresentation
     * CGRectCreateDictionaryRepresentation
 
 Creating a Geometric Primitive From a Dictionary Representation
 
     * CGPointMakeWithDictionaryRepresentation
     * CGSizeMakeWithDictionaryRepresentation
     * CGRectMakeWithDictionaryRepresentation
 
 Creating a Geometric Primitive From Values
 
     * CGPointMake
     * CGRectMake
     * CGSizeMake
 
 Modifying Rectangles
 
     * CGRectDivide
     * CGRectInset
     * CGRectIntegral
     * CGRectIntersection
     * CGRectOffset
     * CGRectStandardize
     * CGRectUnion
 
 Comparing Values
 
     * CGPointEqualToPoint
     * CGSizeEqualToSize
     * CGRectEqualToRect
     * CGRectIntersectsRect
 
 Checking for Membership
 
     * CGRectContainsPoint
     * CGRectContainsRect
 
 Getting Min, Mid, and Max Values
 
     * CGRectGetMinX
     * CGRectGetMinY
     * CGRectGetMidX
     * CGRectGetMidY
     * CGRectGetMaxX
     * CGRectGetMaxY
 
 Getting Height and Width
 
     * CGRectGetHeight
     * CGRectGetWidth
 
 Checking Rectangle Characteristics
 
     * CGRectIsEmpty
     * CGRectIsNull
     * CGRectIsInfinite




