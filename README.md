# The official Objective-C style guidelines for working on GEM's projects

## References
This guidelines references from Open-sources projects:
* [Raywenderic Coding style guidelines](https://github.com/raywenderlich/objective-c-style-guide)
* [NYTimes Style guide](https://github.com/NYTimes/objective-c-style-guide)
* [Google Objective-C Style Guide](https://google.github.io/styleguide/objcguide.xml)
  
## Table of Contents
* [Spacing](#spacing)
* [Naming](#naming)
  * [Principles](#principles)
  * [Class](#class)
  * [Variable](#variable)
  * [Constant](#constant)
  * [Properties](#properties)
  * [Method](#method)
  * [Categories](#categories)
  * [Underscores](#underscores)

## Spacing

* Method braces and other braces (`if`/`else`/`switch`/`while` etc.) always open on the same line as the statement but close on a new line.
* **Must** have exaclty 1 space between `if` and braces 

**Preferred:**
```objc
if (user.isHappy) {
    //Do something
} else {
    //Do something else
}

- (IBAction)outletAction:(id)sender {
    // sample action
}
```

**Not Preferred:**
```objc
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}

if(True){
    //Do something
}

- (IBAction)outletAction:(id)sender
{
    // sample action
}
```

* **DO NOT** add spaces between method return type and method name
* **DO NOT** add spaces between type and braces
* **DO NOT** add spaces between `*` and variable name
* Space between type and `*` **MUST exactly** 1 space
* Space between operators (`+`, `-`, `>=`, ...) **MUST exaclty** 1 space
* There **SHOULD NOT** be a space between the type identifier and the name of the protocol encased in angle brackets, applies to instance variables, and method declarations
* There **Must** have exaclty 1 space between protocol encased in angle brackets and super class (class declaration) or super protocol (protocol declaration)
* **Must** have exactly 1 space between `-` and `(return_type)`

**Preferred:**
```objc
- (void)setText:(NSString *)text {
    UILabel *label.text = text;
    id<AnProtocolName> aVariable = nil;
}

@protocol AnProtocolName <ASuperProtocol>

@end

@interface MyProtocoledClass : NSObject <NSWindowDelegate>

@property (nonatomic, week) id<AnProtocolName> aVariable;

@end


```

**Not Preferred:**
```objc
-(void) setText:( NSString * ) text {
    UILabel * label.text=text;
    UILabel* label2.text=text;
    id<AnProtocolName> aVariable = nil;
}

@protocol AnProtocolName<ASuperProtocol>

@end

@interface MyProtocoledClass : NSObject<NSWindowDelegate>

@property (nonatomic, week) id <AnProtocolName> aVariable;

@end
```

* There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.
* Prefer using auto-synthesis. But if necessary, `@synthesize` and `@dynamic` should each be declared on new lines in the implementation.
* Colon-aligning method invocation should often be avoided. There are cases where a method signature may have >= 3 colons and colon-aligning makes the code more readable. Please do **NOT** however colon align methods containing blocks because Xcode's indenting makes it illegible.
* Code inside blocks **MUST** be indented four spaces

**Preferred:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
    // something
} completion:^(BOOL finished) {
    // something
}];
```

**Not Preferred:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                   // something
                 }
                 completion:^(BOOL finished) {
                   // something
                 }];
```


## Naming
* Naming rules are very important in maintainable code. Objective-C method names tend to be very long, but this has the benefit that a block of code can almost read like prose, thus rendering many comments unnecessary

* When writing pure Objective-C code, we **SHOULD** follow standard [Apple Objective-C guidline naming rules](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html#//apple_ref/doc/uid/10000146-SW1)

  ###Principles: Clarity, Consistency and No Self Reference
  * Be both clear and brief as possible, but clarity shouldn’t suffer because of brevity. Long, descriptive method and variable names are good

  **Preferred:**

  ```objc
  UIButton *settingsButton;

  - (void)insertObject:(id)object atIndexPath:(NSIndexPath *)indexPath;
  ```

  **Not Preferred:**

  ```objc
  UIButton *setBut;

  - (void)insert:(id)object at:(NSIndexPath *)indexPath; 
  ```
  
  * **Don’t** abbreviate names of things. Spell them out, even if they’re long

  **Preferred:**

  ```objc
  id destinationSelection;

  - (void)setBackgroundColor:(UIColor)color;
  ```

  **Not Preferred:**

  ```objc
  id destSel;

  - (void)setBkgdColor:(UIColor)color;
  ```

  * Any class, category, method, or variable name may use all capitals for initialisms within the name. This follows Apple's standard of using all capitals within a name for initialisms such as `URL`, `TIFF`, and `EXIF`

  * Consistency is especially important when you have a class whose methods should take advantage of polymorphism. Methods that do the same thing in different classes should have the same name

  * Names shouldn’t be self-referential

  **Preferred:**
  ```objc
  NSString *textString;
  NSAttributedString *textAttributedString;
  ```

  **Not Preferred:**
  ```objc
  NSString *textStringObject;
  ```

  ###Class
  * Two to three letter prefix **MUST** be used for class/protocol name and constants. However can except for Core Data entity names. 

  **For example:**
  ```objc
  @interface SBAppDelegate: NSObject
  ...

  @protocol GEMSelectPhotoDelegate
  ...
  ```

  ###Variable
  * **MUST** be camel-casing, start with a lowercase letter and capitalize the first letter of embedded words. Don’t use prefixes

  **For example:**
  ```objc
  BOOL fileExists;
  ```
  * Exception: names that start with a well-known acronym, for example, `TIFFRepresentation`


  ###Constant
  * Constants created with const **MUST** be camel-case with all words capitalized and prefixed by the related class name for clarity

  **For example:**
  ```objc
  static * const NSInteger ABAddressBookMaximumSync = 10;
  ```

  * Enumerated constants **MUST** be camel-case, but have same prefix that used for classes and first letter of the word after the prefix is capitalized

  **For example:**
  ```objc
  typedef enum _NSMatrixMode {
      NSRadioModeMatrix           = 0,
      NSHighlightModeMatrix       = 1,
      NSListModeMatrix            = 2,
      NSTrackModeMatrix           = 3
  } NSMatrixMode;
  ```

  * Integer constants, **USE** enumerations
  * Floating point constants **USE** the const qualifier
  * String constants **USE** static const qualifier
  **For example:**
  ```objc
  static NSString * const SBSalesboxCalendarName = @"QASalesbox";
  ```

  * Use uppercase letters for symbols that the preprocessor evaluates in determining whether a block of code will be processed. For multiple-words symbols, use underscore to separate between words

  **For example:**
  ```objc
  #define RGBCOLOR(RED, GREEN, BLUE, ALPHA) [UIColor colorWithRed:RED/255.0f green:GREEN/255.0f blue:BLUE/255.0f alpha:ALPHA]
  ```

  ###Properties
  * **MUST** be camel-casing, start with a lowercase letter and capitalize the first letter of embedded words. Don’t use prefixes
  * Instance variables MUST be camel-case with the leading word being lowercase, and MUST be prefixed with an underscore. This is consistent with instance variables synthesized automatically by LLVM

  **For example:**
  ```objc
  @interface GEMSampleClass () {
      id _sampleInstanceVariable;
      BOOL _sampleBoolVariable;
  }
  ```

  ###Method
  * **MUST** be camel-casing, start with a lowercase letter and capitalize the first letter of embedded words. Don’t use prefixes

  ###Categories
  * **SHOULD** follow naming convention with `Class`
  * **SHOULD** concisely segment functionality and should be named to describe that functionality

  **For example:**
  ```objc
  @interface UIViewController (NYTMediaPlaying)
  @interface NSString (NSStringEncodingDetection)
  ```

  **Not**
  ```objc
  @interface NYTAdvertisement (private)
  @interface NSString (NYTAdditions)
  ```