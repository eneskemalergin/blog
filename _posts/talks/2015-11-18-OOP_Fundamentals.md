---
layout: presentation
title: OOP Fundamentals
theme: blood
categories: talks
published: true
---

{{site.startvertical}}
{{site.startslide}}

# OOP Fundamentals

> Enes Kemal Ergin

{{site.nextslide}}
#### About Me

- [Personal Blog](http://eneskemalergin.github.io/)
- [Github](https://github.com/eneskemalergin)
- [Email](eneskemalergin@gmail.com)
{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}
__Outline:__

- Abstract Data Types
- Inheritance
- Dynamic Binding(Polymorphism)

{{site.nextslide}}

```All in Objective-C ```
---

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}
## 1. Abstract Data Types(ADT)

> ! Abstract is a model of a certain kind of data structure. !

{{site.nextslide}}

__Demonstration of ADT__

<img style="max-width: 100%;" src="{{site.baseurl}}/images/ADT.png"></img>

{{site.nextslide}}

### Example

> Basic Queue ADT using Objective C NSMutableArray structure.

- Two files ```one.h```,  ```two.m```

- One of them is main and other is class/method function...

- Why? .h and .m

{{site.nextslide}}

.h is for header files in objective c, like class in java

.m is for _method_ file, which is a obvious, which is main files in obj-c. If you still insist to know why m/h answer is

    "Because .o and .c were taken. Simple as that."

{{site.nextslide}}

Implementation of the ADT

```
@implementation NSMutableArray (QueueAdditions)
// Queues are first-in-first-out, so we remove objects from the head
- (id) dequeue {
    // if ([self count] == 0) return nil; // to avoid raising exception (Quinn)
    id headObject = [self objectAtIndex:0];
    if (headObject != nil) {
        [[headObject retain] autorelease]; // so it isn't dealloc'ed on remove
        [self removeObjectAtIndex:0];
    }
    return headObject;
}

// Add to the tail of the queue (no one likes it when people cut in line!)
- (void) enqueue:(id)anObject {
    [self addObject:anObject];
    //this method automatically adds to the end of the array
}
@end
```

Interface  design .h

```
@interface NSMutableArray (QueueAdditions)
- (id) dequeue;
- (void) enqueue:(id)obj;
@end
```
{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## 2. Inheritance

> !Inheritance enables new objects to take on the properties of existing objects!

{{site.nextslide}}

### Example

Here is very comprehensive and powerful example of inheritance using Objective-C: [Source](https://agilewarrior.wordpress.com/2012/03/20/simple-objective-c-inheritance-example/)

{{site.nextslide}}

__Step 1: Define the Parent Class__


_rectange.h_

```
#import <Foundation/NSObject.h>

@interface Rectangle: NSObject

@property (nonatomic) int width;
@property (nonatomic) int height;

-(Rectangle*) initWithWidth: (int) w height: (int) h;
-(void) setWidth: (int) w height: (int) h;
-(void) print;

@end
```
_rectange.m_

```
#import "Rectangle.h"
#import <stdio.h>

@implementation Rectangle

@synthesize width = _width;
@synthesize height = _height;

-(Rectangle*) initWithWidth: (int) w height: (int) h {
    self = [super init];

    if ( self ) {
        [self setWidth: w height: h];
    }

    return self;
}

-(void) setWidth: (int) w height: (int) h {
    self.width = w;
    self.height = h;
}

-(void) print {
    printf( "width = %i, height = %i", self.width, self.height );
}

@end
```
{{site.nextslide}}

__Step 2: Inherit from the Parent__


Inheriting with the ```@interface Square: Rectangle```, add this to the Square.h


_Square.h_

```
#import "Rectangle.h"

@interface Square: Rectangle
-(Square*) initWithSize: (int) s;
-(void) setSize: (int) s;
-(int) size;
@end
```

_Square.m_

```
#import "Square.h"

@implementation Square
-(Square*) initWithSize: (int) s {
    self = [super init];

    if ( self ) {
        [self setSize: s];
    }

    return self;
}

-(void) setSize: (int) s {
    self.width = s;
    self.height = s;
}

-(int) size {
    return self.width;
}

@end
```
{{site.nextslide}}

__Step 3: Write and Run the Main__

_SpikeInheritanceTests.m_

```
#import "SpikeInheritanceTests.h"
#import "Square.h"
#import "Rectangle.h"
#import <stdio.h>

@implementation SpikeInheritanceTests

- (void)testExample
{
    Rectangle *rec = [[Rectangle alloc] initWithWidth: 10 height: 20];
    Square *sq = [[Square alloc] initWithSize: 15];

    // print em
    printf( "Rectangle: " );
    [rec print];
    printf( "\n" );

    printf( "Square: " );
    [sq print];
    printf( "\n" );

    // update square
    [sq setWidth: 20];
    printf( "Square after change: " );
    [sq print];
    printf( "\n" );
}

@end
```

{{site.endslide}}
{{site.endvertical}}

{{site.startvertical}}
{{site.startslide}}

## 3. Polymorphism

> ! Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.!

{{site.nextslide}}

### Example

```
#import <Foundation/Foundation.h>

@interface Shape : NSObject

{
    CGFloat area;
}

- (void)printArea;
- (void)calculateArea;
@end

@implementation Shape

- (void)printArea{
    NSLog(@"The area is %f", area);
}

- (void)calculateArea{

}

@end


@interface Square : Shape
{
    CGFloat length;
}

- (id)initWithSide:(CGFloat)side;

- (void)calculateArea;

@end

@implementation Square

- (id)initWithSide:(CGFloat)side{
    length = side;
    return self;
}

- (void)calculateArea{
    area = length * length;
}

- (void)printArea{
    NSLog(@"The area of square is %f", area);
}

@end

@interface Rectangle : Shape
{
    CGFloat length;
    CGFloat breadth;
}

- (id)initWithLength:(CGFloat)rLength andBreadth:(CGFloat)rBreadth;


@end

@implementation Rectangle

- (id)initWithLength:(CGFloat)rLength andBreadth:(CGFloat)rBreadth{
    length = rLength;
    breadth = rBreadth;
    return self;
}

- (void)calculateArea{
    area = length * breadth;
}

@end


int main(int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    Shape *square = [[Square alloc]initWithSide:10.0];
    [square calculateArea];
    [square printArea];
    Shape *rect = [[Rectangle alloc]
    initWithLength:10.0 andBreadth:5.0];
    [rect calculateArea];
    [rect printArea];        
    [pool drain];
    return 0;
}
```
{{site.endslide}}
{{site.endvertical}}

{{site.startslide}}
# Questions

{{site.endslide}}
{{site.startslide}}
# Thank you.
{{site.endslide}}
