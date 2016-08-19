# The official Objective-C style guidelines for working on GEM's projects

## References
This guidelines references from Open-sources projects:
* [Raywenderic Coding style guidelines](https://github.com/raywenderlich/objective-c-style-guide)
* [NYTimes Style guide](https://github.com/NYTimes/objective-c-style-guide)
  
## Table of Contents
* [Dot Notation Syntax](#dot-notation-syntax)
* 

## Dot Notation Syntax

Dot notation is RECOMMENDED over bracket notation for getting and setting properties.

**For example:**
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not:**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```


