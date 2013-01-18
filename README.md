# 23Divide Objective-C coding conventions

# I'm adding shit to this branch called "VANJA BRAINBROKE" x2

## Whitespaces

 * Tabs, not spaces.
 * End files with a newline.
 * Make liberal use of vertical whitespace to divide code into logical chunks.
 * Always put a space between an operator and its operands.
 
``` objc
total = first + second;
```
 * Never put a space between a colon and the following value.
 
``` objc
[self updateWithDeltaTime:0.3f];
```
 * Always put a space after a semicolon inside `for` loops.
 
``` objc
for (NSUInteger i = 0; i < 10; ++i)
{
	[self doShit];
}
```
 * Put a single space after keywords and before their parentheses.
 * No spaces between parentheses and their contents.
 * Blocks should have a space between their return type and name.
 * There shouldn't be a space between a cast and the variable being cast.

``` objc
NewType newTypeVariable = (NewType)oldTypeVariable;
```

## Documentation and Organization

 * Comments should be hard-wrapped at 80 characters.
 * Comments should be Apple-style.
 * Use `#pragma mark`s to categorize methods into functional groupings and protocol implementations.

## Indentation

 * Simple rule: every time there's a open curly brace, enclosed code must be indented.
 * Always use tabs to indent; never use spaces.
 * XCode will automatically indent your code most of the time; don't fight it.

``` objc
if (isShit == YES)
{
	while (shitIsHittingTheFan == YES)
	{
		[self doShit];
	}
}
```

## Naming of variables

 * Variables (including ivars) should use camelCase
 * Prefix a variable with an underscore only if it's an ivar.
 * Only use alphanumeric characters.
 * No stupid abbreviations like "btn" for "button" or "scr" for "score".
 * No single-letter variables except for loops (like in a simple for-loop with an integer variable).
 * Be descriptive in your variable names.
 * Compose a variable name using concatenated english words.
 * Always start with a small letter for the first word.
 * Always use a capital letter for following words.
 * Don't use prefixes like "my" or "this" or "another".
 * No underscores to separate words in variable names (eg. background_image should be backgroundImage)
 * Acceptable abbreviations as per [Apple naming conventions](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/APIAbbreviations.html#//apple_ref/doc/uid/20001285-BCIHCGAE)
 
```objc
NSInteger terrorLevel = 3;
NSArray *platforms;
NSDictionary *swiftRadianceThresholds;

for (NSUInteger i = 0; i < 10; ++i)
{
	NSLog(@"Counting %d", i);
}
```

## Naming of methods

 * Be descriptive, in plain english.
 * No abbreviations.
 * Explicitly name all parameters.
 * Follow [Apple naming conventions](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html). 

## Declarations

### ivars

 * One ivar per line; don't declare multiple ivars using the comma.
 * Use empty lines to group ivars in logical chunks.
 * Never declare an ivar unless you need to change its type from its declared property.
  
### Properties

 * Declare properties after ivars and before methods.
 * Prefer exposing an immutable type for a property if it being mutable is an implementation detail. This is a valid reason to declare an ivar for a property.
 * Always declare memory-management semantics even on `readonly` properties.
 * Declare properties `readonly` if they are only set once in `-init`.
 * Declare properties `copy` if they return immutable objects and aren't ever mutated in the implementation.
 * Don't use `@synthesize` unless the compiler requires it. As of LLVM 4.3 properties no longer to be @synthesize'd. However, optional properties in protocols must be explicitly @synthesize'd in order to exist.
 * One property per line; one `@synthesize` per line.
 
### Methods

 * Start with class methods, followed by init methods.
 * Separate class methods from instance methods with an empty line.
 * Follow this style:
   - Start with `-` or `+` character
   - Space
   - Return type
   - Method name (no space between return type and this)
   - Colon
   - Parameter type (no space between colon and this)
   - Parameter name (no space between parameter type and this)
  
```objc
+ (id)terrorWithLevel:(NSUInteger)level;

- (id)initWithLevel:(NSUInteger)level;
- (id)initWithLevel:(NSUInteger)level assets:(NSArray *)assets;
- (void)updateSceneWithDeltaTime:(float)deltaTime;
```
 
### Protocols

 * Declare protocols before class interface.
 * Follow the same rules as in Methods.
 
### Miscellaneous 

 * Always use Objective-C primitive types instead of C types (i.e. use `NSUInteger` instead of `unsigned int`)
 * Use forward class declarations whenever possible with `@class`.
 * Don't put a space between an object type and the protocol it conforms to. 
 
```objc
@property (attributes) id<Protocol> object;
@property (nonatomic, strong) NSObject<Protocol> *object;
```
 
 * C function declarations should have no space before the opening parenthesis, and should be namespaced just like a class.

```objc
void GHAwesomeFunction(BOOL hasSomeArgs);
```

 * Constructors should generally return `instancetype` rather than `id`.

## Expressions

 * Use dot-syntax for "simple" getters and setters.
 * Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
 * Comparisons should always be explicit.
 * Prefer positive comparisons to negative.
 * Long form ternary operators should be wrapped in parentheses and only used for assignment and arguments.

```objc
Blah *a = (stuff == thing ? foo : bar);
```


## Control Structures

 * Always surround `if`, `while`, `for`, `do`, `switch`, `case` bodies with curly braces even if it's a single-line statement.
 * All curly braces should begin on a new line. They should end on a new line.
 * All curly braces will always live "alone" in their own line.
 
```objc
if (variable == 3)
{
	[self doSomething];
}
```
 
 * Return and break early.

```objc
if (shitIsBad == YES)
{
	return;
}

if (something == nil) 
{
	// do stuff
} 
else
{
	// do other stuff
}
```

## Blocks

 * Block definitions should omit their return type when possible.
 * Block definitions should omit their arguments if they are `void`.

```objc
void (^blockName1)(void) = ^
{
    // do some things
};

id (^blockName2)(id) = ^ id (id args) 
{
    // do some things
};
```

## Literals

 * Longer or more complex literals should be split over multiple lines (optionally with a terminating comma):

``` objc
NSArray *theShit = @[
    @"Got some long string objects in here.",
    [AndSomeModelObjects too],
    @"Moar strings."
];

NSDictionary *keyedShit = @{
    @"this.key": @"corresponds to this value",
    @"otherKey": @"remoteData.payload",
    @"some": @"more",
    @"JSON": @"keys",
    @"and": @"stuff",
};
```

## Categories

 * Categories should be named for the sort of functionality they provide. Don't create umbrella categories.
 * Category methods should always be prefixed.
 * If you need to expose private methods for subclasses or unit testing, create a class extension named `Class+Private`.
