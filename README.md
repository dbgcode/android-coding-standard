# The official DBG Android code style guide.

This style guide outlines the coding conventions for DBG Android Team!

## Introduction

The reason we made this style guide was so that we could keep the code in our projects nice and consistent - even though we have many different authors working on each project.

## Table of Contents

* [File Organization](#file-organization)
 * [Java Source Files](#java-source-files)
   * [Beginning Comments](#beginning-comments)
   * [Package and Import Statements](#package-and-import-statements)
   * [Class and Interface Declarations](#class-and-interface-declarations)
* [Indentation](#indentation)
 * [Line Length](#line-length)
 * [Wrapping Lines](#wrapping-lines)
* [Comments](#comments)
 * [Implementation Comment Formats](#implementation-comment-formats)
 * [Block Comments](#block-comments)
 * [Single-Line Comments](#single-line-comments)
 * [Trailing Comments](#trailing-comments)
 * [End-Of-Line Comments](#end-of-line-comments)
 * [Documentation Comments](#documentation-comments)
* [Declarations](#declarations)
 * [Number Per Line](#number_per_line)
 * [Initialization](#initialization)
 * [Placement](#placement)
 * [Class and Interface Declarations](#class-and-interface-declarations)
* [Statements](#statements)
 * [Simple Statements](#simple-statements)
 * [Compound Statements](#simple-statements)
 * [return Statements](#return-statements)
 * [if, if-else, if else-if else Statements](#if-statements)
 * [for Statements](#for-statements)
 * [while Statements](#while-statements)
 * [do-while Statements](#do-while-statements)
 * [switch Statements](#switch-statements)
 * [try-catch Statements](#try-catch-statements)
* [White Space](#white-space)
 * [Blank Lines](#blank-lines)
 * [Blank Spaces](#blank-spaces)
* [Naming Conventions](#naming-conventions)
* [Programming Practices](#programming-practices)
 * [Providing Access to Instance and Class Variables](#access-practices)
 * [Referring to Class Variables and Methods](#referring-practices)
 * [Constants](#constants)
 * [Variable Assignments](#variable-assignments)
 * [Miscellaneous Practices](#miscellaneous-practices)
  * [Parentheses](#parentheses)
  * [Returning Values](#returning-values)
  * [ Expressions before `?' in the Conditional Operator](#expressions)
  * [Special Comments](#special-comments)



## File Organization

A file consists of sections that should be separated by blank lines and an optional comment identifying each section.
Files longer than 2000 lines are cumbersome and should be avoided. For an example of a Java program properly formatted 

## Java Source Files

Each Java source file contains a single public class or interface. When private classes and interfaces are associated with a public class, you can put them in the same source file as the public class. The public class should be the first class or interface in the file.

Java source files have the following ordering:

Beginning comments

Package and Import statements

Class and interface declarations

## Beginning Comments

All source files should begin with a c-style comment that lists the class name, version information, date, and copyright notice:

```objc
/*
 * Classname
 * 
 * Version information
 *
 * Date
 * 
 * Copyright notice
 */
 ```
## Package and Import Statements

  The first non-comment line of most Java source files is a package statement. After that, import statements can follow. For example:

package com.android.internal.foo;

import java.sql.SQLException;

## Class and Interface Declarations

* Class ( static) variables - First the public class variables, then the protected, then package level (no access modifier), and then the private.

* Instance variables - First public, then protected, then package level (no access modifier), and then private.

* Methods - These methods should be grouped by functionality rather than by scope or accessibility. For example, a private class method can be in between two public instance methods. The goal is to make reading and understanding the code easier.

## Indentation

Four spaces should be used as the unit of indentation. The exact construction of the indentation (spaces vs. tabs) is unspecified. Tabs must be set exactly every 8 spaces (not 4).

## Line Length

Avoid lines longer than 80 characters, since they're not handled well by many terminals and tools.

## Wrapping Lines

When an expression will not fit on a single line, break it according to these general principles:

* Break after a comma.

* Break before an operator.

* Prefer higher-level breaks to lower-level breaks.

* Align the new line with the beginning of the expression at the same level on the previous line.

If the above rules lead to confusing code or to code that's squished up against the right margin, just indent 8 spaces instead.

Here are some examples of breaking method calls:

```objc
someMethod(longExpression1, longExpression2, longExpression3, 
        longExpression4, longExpression5);
 
var = someMethod1(longExpression1,
                someMethod2(longExpression2,
                        longExpression3)); 
```

Following are two examples of breaking an arithmetic expression. The first is preferred, since the break occurs outside the parenthesized expression, which is at a higher level.

```objc
longName1 = longName2 * (longName3 + longName4 - longName5)
           + 4 * longname6; // PREFER

longName1 = longName2 * (longName3 + longName4
                       - longName5) + 4 * longname6; // AVOID 
```

Following are two examples of indenting method declarations. The first is the conventional case. The second would shift the second and third lines to the far right if it used conventional indentation, so instead it indents only 8 spaces.

```objc
//CONVENTIONAL INDENTATION
someMethod(int anArg, Object anotherArg, String yetAnotherArg,
           Object andStillAnother) {
    ...
}

//INDENT 8 SPACES TO AVOID VERY DEEP INDENTS
private static synchronized horkingLongMethodName(int anArg,
        Object anotherArg, String yetAnotherArg,
        Object andStillAnother) {
    ...
}
```

Line wrapping for if statements should generally use the 8-space rule, since conventional (4 space) indentation makes seeing the body difficult. For example:

```objc
//DON'T USE THIS INDENTATION
if ((condition1 && condition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) { //BAD WRAPS
    doSomethingAboutIt();            //MAKE THIS LINE EASY TO MISS
} 

//USE THIS INDENTATION INSTEAD
if ((condition1 && condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 

//OR USE THIS
if ((condition1 && condition2) || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 
```

Here are three acceptable ways to format ternary expressions:

```objc
alpha = (aLongBooleanExpression) ? beta : gamma;  

alpha = (aLongBooleanExpression) ? beta
                                 : gamma;  

alpha = (aLongBooleanExpression)
        ? beta 
        : gamma;  
```

## Comments

Java programs can have two kinds of comments: implementation comments and documentation comments. Implementation comments are those found in C++, which are delimited by /*...*/, and //. Documentation comments (known as "doc comments") are Java-only, and are delimited by /**...*/. Doc comments can be extracted to HTML files using the javadoc tool.

Implementation comments are meant for commenting out code or for comments about the particular implementation. Doc comments are meant to describe the specification of the code, from an implementation-free perspective. to be read by developers who might not necessarily have the source code at hand.

Comments should be used to give overviews of code and provide additional information that is not readily available in the code itself. Comments should contain only information that is relevant to reading and understanding the program. For example, information about how the corresponding package is built or in what directory it resides should not be included as a comment.

Discussion of nontrivial or nonobvious design decisions is appropriate, but avoid duplicating information that is present in (and clear from) the code. It is too easy for redundant comments to get out of date. In general, avoid any comments that are likely to get out of date as the code evolves.

Note:The frequency of comments sometimes reflects poor quality of code. When you feel compelled to add a comment, consider rewriting the code to make it clearer.

Comments should not be enclosed in large boxes drawn with asterisks or other characters. Comments should never include special characters such as form-feed and backspace.

## Implementation Comment Formats

Programs can have four styles of implementation comments: block, single-line, trailing, and end-of-line.

## Block Comments

Block comments are used to provide descriptions of files, methods, data structures and algorithms. Block comments may be used at the beginning of each file and before each method. They can also be used in other places, such as within methods. Block comments inside a function or method should be indented to the same level as the code they describe.

A block comment should be preceded by a blank line to set it apart from the rest of the code.

```objc
/*
 * Here is a block comment.
 */
         

      
/*-indent

<blockquote>/*-
 * Here is a block comment with some very special
 * formatting that I want indent(1) to ignore.
 *
 *    one
 *        two
 *            three
 */
 ```
 
## Single-Line Comments

 Short comments can appear on a single line indented to the level of the code that follows. If a comment can't be written in a single line, it should follow the block comment format. A single-line comment should be preceded by a blank line.

```objc
 if (condition) {

    /* Handle the condition. */
    ...
}
 ```

## Trailing Comments

 Very short comments can appear on the same line as the code they describe, but should be shifted far enough to separate them from the statements. If more than one short comment appears in a chunk of code, they should all be indented to the same tab setting.

Here's an example of a trailing comment in Java code:

```objc
if (a == 2) {
    return TRUE;            /* special case */
} else {
    return isPrime(a);      /* works only for odd a */
}
```

## End-Of-Line Comments

The // comment delimiter can comment out a complete line or only a partial line. It shouldn't be used on consecutive multiple lines for text comments; however, it can be used in consecutive multiple lines for commenting out sections of code. Examples of all three styles follow:

```objc
if (foo > 1) {

    // Do a double-flip.
    ...
}
else {
    return false;          // Explain why here.
}
//if (bar > 1) {
//
//    // Do a triple-flip.
//    ...
//}
//else {
//    return false;
//}
```
## Documentation Comments

Doc comments describe Java classes, interfaces, constructors, methods, and fields. Each doc comment is set inside the comment delimiters /**...*/, with one comment per class, interface, or member. This comment should appear just before the declaration:


```objc
/**
 * The Example class provides ...
 */
public class Example { ...
```

Notice that top-level classes and interfaces are not indented, while their members are. The first line of doc comment (/**) for classes and interfaces is not indented; subsequent doc comment lines each have 1 space of indentation (to vertically align the asterisks). Members, including constructors, have 4 spaces for the first doc comment line and 5 spaces thereafter.

If you need to give information about a class, interface, variable, or method that isn't appropriate for documentation, use an implementation block comment or single-line comment immediately after the declaration. For example, details about the implementation of a class should go in in such an implementation block comment following the class statement, not in the class doc comment.

Doc comments should not be positioned inside a method or constructor definition block, because Java associates documentation comments with the first declaration after the comment.

## Declarations

## Number Per Line

One declaration per line is recommended since it encourages commenting. In other words,

```objc
int level; // indentation level
int size;  // size of table
```

is preferred over

```objc
int level, size;
```

Do not put different types on the same line. Example:

         
```objc
                      int foo,  fooarray[]; //WRONG!
 ```     


Note: The examples above use one space between the type and the identifier. Another acceptable alternative is to use tabs, e.g.:

```objc
int     level;          // indentation level
int     size;            // size of table
Object  currentEntry;    // currently selected table entry
```

## Initialization

Try to initialize local variables where they're declared. The only reason not to initialize a variable where it's declared is if the initial value depends on some computation occurring first.

## Placement

Put declarations only at the beginning of blocks. (A block is any code surrounded by curly braces "{" and "}".) Don't wait to declare variables until their first use; it can confuse the unwary programmer and hamper code portability within the scope.

```objc
void myMethod() {
    int int1 = 0;         // beginning of method block

    if (condition) {
        int int2 = 0;     // beginning of "if" block
        ...
    }
}
</blockquote>
```

The one exception to the rule is indexes of for loops, which in Java can be declared in the for statement:

```objc
for (int i = 0; i < maxLoops; i++) { ... }
</blockquote>
```

Avoid local declarations that hide declarations at higher levels. For example, do not declare the same variable name in an inner block:

```objc
int count;
...
myMethod() {
    if (condition) {
        int count = 0;     // AVOID!
        ...
    }
    ...
}
```

## Class and Interface Declarations

When coding Java classes and interfaces, the following formatting rules should be followed:

* No space between a method name and the parenthesis "(" starting its parameter list
* Open brace "{" appears at the end of the same line as the declaration statement
* Closing brace "}" starts a line by itself indented to match its corresponding opening statement, except when it is a null statement the "}" should appear immediately after the "{"

```objc
class Sample extends Object {
    int ivar1;
    int ivar2;

    Sample(int i, int j) {
        ivar1 = i;
        ivar2 = j;
    }

    int emptyMethod() {}

    ...
}
```

* Methods are separated by a blank line
