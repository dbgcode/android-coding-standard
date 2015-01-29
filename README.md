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
 * [Number Per Line](#number-per-line)
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
* [White Space](#white-space)
 * [Blank Lines](#blank-lines)
 * [Blank Spaces](#blank-spaces)
* [Programming Practices](#programming-practices)
 * [Providing Access to Instance and Class Variables](#access-practices)
 * [Referring to Class Variables and Methods](#referring-practices)
 * [Constants](#constants)
 * [Variable Assignments](#variable-assignments)
 * [Miscellaneous Practices](#miscellaneous-practices)
  * [Parentheses](#parentheses)
  * [Returning Values](#returning-values)
  * [ Expressions before `?' in the Conditional Operator](#expressions-before-`?'-in-the-conditional-operator)
  * [Special Comments](#special-comments)
* [Don't Ignore Exceptions](#don't-ignore-exceptions)
* [Don't Catch Generic Exception](#don't-catch-generic-exception)
* [Don't Use Finalizers](#don't-use-finalizers)
* [Fully Qualify Imports](#fully-qualify-imports)
* [Java Library Rules](#java-library-rules)
* [Java Style Rules](#Java-style-rules)
* [Define Fields in Standard Places](#define-fields-in-standard-places)
* [Limit Variable Scope](#limit-variable-scope)
* [Order Import Statements](#order-import-statements)
* [Follow Field Naming Conventions](#follow-field-naming-conventions)
* [Use Standard Brace Style](#use-standard-brace-style)
* [Use Standard Java Annotations](#use-standard-java-annotations)
* [Treat Acronyms as Words](#treat-acronyms-as-words)
* [Use TODO Comments](#use-todo-comments)
* [Log Sparingly](#log-sparingly)
* [Follow Test Method Naming Conventions](#follow-test-method-naming-conventions)



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

Each line of text in your code should be at most 100 characters long. There has been lots of discussion about this rule and the decision remains that 100 characters is the maximum.

Exception: if a comment line contains an example command or a literal URL longer than 100 characters, that line may be longer than 100 characters for ease of cut and paste.

Exception: import lines can go over the limit because humans rarely see them. This also simplifies tool writing.

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

## Statements

## Simple Statements

Each line should contain at most one statement. Example:

```objc
argv++;         // Correct
argc--;         // Correct  
argv++; argc--; // AVOID!
```

## Compound Statements

Compound statements are statements that contain lists of statements enclosed in braces "{ statements }". See the following sections for examples.

* The enclosed statements should be indented one more level than the compound statement.

* The opening brace should be at the end of the line that begins the compound statement; the closing brace should begin a line and be indented to the beginning of the compound statement.

* Braces are used around all statements, even single statements, when they are part of a control structure, such as an if-else or for statement. This makes it easier to add statements without accidentally introducing bugs due to forgetting to add braces.

## return Statements

A return statement with a value should not use parentheses unless they make the return value more obvious in some way. Example:

```objc
return;

return myDisk.size();

return (size ? size : defaultSize);
```

## if, if-else, if else-if else Statements

The if-else class of statements should have the following form:

```objc
if (condition) {
    statements;
}

if (condition) {
    statements;
} else {
    statements;
}

if (condition) {
    statements;
} else if (condition) {
    statements;
} else {
    statements;
}
```

Note: if statements always use braces, {}. Avoid the following error-prone form:

```objc
if (condition) //AVOID! THIS OMITS THE BRACES {}!
    statement;
    ```

## for Statements

A for statement should have the following form:

```objc
for (initialization; condition; update) {
    statements;
}
```

An empty for statement (one in which all the work is done in the initialization, condition, and update clauses) should have the following form:

```objc
for (initialization; condition; update);
```

When using the comma operator in the initialization or update clause of a for statement, avoid the complexity of using more than three variables. If needed, use separate statements before the for loop (for the initialization clause) or at the end of the loop (for the update clause).

## while Statements

A while statement should have the following form:

```objc
while (condition) {
    statements;
}
```

An empty while statement should have the following form:

```objc
while (condition);
```

## do-while Statements

A do-while statement should have the following form:

```objc
do {
    statements;
} while (condition);
```

## switch Statements
A switch statement should have the following form:

```objc
switch (condition) {
case ABC:
    statements;
    /* falls through */
case DEF:
    statements;
    break;
case XYZ:
    statements;
    break;
default:
    statements;
    break;
}
```

Every time a case falls through (doesn't include a break statement), add a comment where the break statement would normally be. This is shown in the preceding code example with the /* falls through */ comment.

Every switch statement should include a default case. The break in the default case is redundant, but it prevents a fall-through error if later another case is added.

## White Space

##  Blank Lines

Blank lines improve readability by setting off sections of code that are logically related.
Two blank lines should always be used in the following circumstances:

* Between sections of a source file

* Between class and interface definitions

One blank line should always be used in the following circumstances:

* Between methods

* Between the local variables in a method and its first statement

* Before a block (see section 5.1.1) or single-line (see section 5.1.2) comment

* Between logical sections inside a method to improve readability

## Blank Spaces

Blank spaces should be used in the following circumstances:

* A keyword followed by a parenthesis should be separated by a space. Example:
       while (true) {
           ...
       }

Note that a blank space should not be used between a method name and its opening parenthesis. This helps to distinguish keywords from method calls.

 

* A blank space should appear after commas in argument lists.

* All binary operators except . should be separated from their operands by spaces. Blank spaces should never separate unary operators such as unary minus, increment ("++"), and decrement ("--") from their operands. Example:

```objc
    a += c + d;
    a = (a + b) / (c * d);
    
    while (d++ = s++) {
        n++;
    }
    printSize("size is " + foo + "\n");
```

* The expressions in a for statement should be separated by blank spaces. Example:

```objc
    for (expr1; expr2; expr3)
```

* Casts should be followed by a blank space. Examples:

```objc
    myMethod((byte) aNum, (Object) x);
    myMethod((int) (cp + 5), ((int) (i + 3)) 
                                  + 1);
```

## Programming Practices

## Providing Access to Instance and Class Variables

Don't make any instance or class variable public without good reason. Often, instance variables don't need to be explicitly set or gotten-often that happens as a side effect of method calls.

One example of appropriate public instance variables is the case where the class is essentially a data structure, with no behavior. In other words, if you would have used a struct instead of a class (if Java supported struct), then it's appropriate to make the class's instance variables public.

## Referring to Class Variables and Methods

Avoid using an object to access a class (static) variable or method. Use a class name instead. For example:

```objc
classMethod();             //OK
AClass.classMethod();      //OK
anObject.classMethod();    //AVOID!
```

## Constants

Numerical constants (literals) should not be coded directly, except for -1, 0, and 1, which can appear in a for loop as counter values.

## Variable Assignments

Avoid assigning several variables to the same value in a single statement. It is hard to read. Example:

```objc
fooBar.fChar = barFoo.lchar = 'c'; // AVOID!
```

Do not use the assignment operator in a place where it can be easily confused with the equality operator. Example:

```objc
if (c++ = d++) {        // AVOID! (Java disallows)
    ...
}
</blockquote>
```

should be written as

```objc
if ((c++ = d++) != 0) {
    ...
}
```

Do not use embedded assignments in an attempt to improve run-time performance. This is the job of the compiler. Example:

```objc
d = (a = b + c) + r;        // AVOID!
</blockquote>
```

should be written as

```objc
a = b + c;
d = a + r;
```

## Miscellaneous Practices

## Parentheses

It is generally a good idea to use parentheses liberally in expressions involving mixed operators to avoid operator precedence problems. Even if the operator precedence seems clear to you, it might not be to others-you shouldn't assume that other programmers know precedence as well as you do.

```objc
if (a == b && c == d)     // AVOID!
if ((a == b) && (c == d)) // RIGHT
```

## Returning Values

Try to make the structure of your program match the intent. Example:

```objc
if (
             booleanExpression) {
    return true;
} else {
    return false;
}
```
          
should instead be written as

```objc
return  
             booleanExpression;
             ```
          
Similarly,

```objc
if (condition) {
    return x;
}
return y;
```

should be written as

```objc
return (condition ? x : y);
```

## Expressions before `?' in the Conditional Operator

If an expression containing a binary operator appears before the ? in the ternary ?: operator, it should be parenthesized. Example:

```objc
(x >= 0) ? x : -x;
```

## Special Comments

Use XXX in a comment to flag something that is bogus but works. Use FIXME to flag something that is bogus and broken.

## Don't Ignore Exceptions

Sometimes it is tempting to write code that completely ignores an exception. You must never do this.

Acceptable alternatives (in order of preference) are:

* Throw the exception up to the caller of your method.

```objc
void setServerPort(String value) throws NumberFormatException {
    serverPort = Integer.parseInt(value);
}
```

* Throw a new exception that's appropriate to your level of abstraction.

```objc
void setServerPort(String value) throws ConfigurationException {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        throw new ConfigurationException("Port " + value + " is not valid.");
    }
}
```

* Handle the error gracefully and substitute an appropriate value in the catch {} block.

```objc
/** Set port. If value is not a valid number, 80 is substituted. */

void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        serverPort = 80;  // default port for server 
    }
}
```

* Catch the Exception and throw a new RuntimeException. This is dangerous: only do it if you are positive that if this error occurs, the appropriate thing to do is crash.

```objc
/** Set port. If value is not a valid number, die. */

void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        throw new RuntimeException("port " + value " is invalid, ", e);
    }
}
```

Note that the original exception is passed to the constructor for RuntimeException. If your code must compile under Java 1.3, you will need to omit the exception that is the cause.

* Last resort: if you are confident that actually ignoring the exception is appropriate then you may ignore it, but you must also comment why with a good reason:

```objc
/** If value is not a valid number, original port number is used. */
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) {
        // Method is documented to just ignore invalid user input.
        // serverPort will just be unchanged.
    }
}
```

# Don't Catch Generic Exception

Sometimes it is tempting to be lazy when catching exceptions and do something like this:

```objc
try {
    someComplicatedIOFunction();        // may throw IOException 
    someComplicatedParsingFunction();   // may throw ParsingException 
    someComplicatedSecurityFunction();  // may throw SecurityException 
    // phew, made it all the way 
} catch (Exception e) {                 // I'll just catch all exceptions 
    handleError();                      // with one generic handler!
}
```

You should not do this. In almost all cases it is inappropriate to catch generic Exception or Throwable, preferably not Throwable, because it includes Error exceptions as well. It is very dangerous. It means that Exceptions you never expected (including RuntimeExceptions like ClassCastException) end up getting caught in application-level error handling. It obscures the failure handling properties of your code. It means if someone adds a new type of Exception in the code you're calling, the compiler won't help you realize you need to handle that error differently. And in most cases you shouldn't be handling different types of exception the same way, anyway.

There are rare exceptions to this rule: certain test code and top-level code where you want to catch all kinds of errors (to prevent them from showing up in a UI, or to keep a batch job running). In that case you may catch generic Exception (or Throwable) and handle the error appropriately. You should think very carefully before doing this, though, and put in comments explaining why it is safe in this place.

Alternatives to catching generic Exception:

* Catch each exception separately as separate catch blocks after a single try. This can be awkward but is still preferable to catching all Exceptions. Beware repeating too much code in the catch blocks.

* Refactor your code to have more fine-grained error handling, with multiple try blocks. Split up the IO from the parsing, handle errors separately in each case.

* Rethrow the exception. Many times you don't need to catch the exception at this level anyway, just let the method throw it.

## Don't Use Finalizers

Finalizers are a way to have a chunk of code executed when an object is garbage collected.

Pros: can be handy for doing cleanup, particularly of external resources.

Cons: there are no guarantees as to when a finalizer will be called, or even that it will be called at all.

Decision: we don't use finalizers. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a close() method (or the like) and document exactly when that method needs to be called. See InputStream for an example. In this case it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs.

## Fully Qualify Imports

When you want to use class Bar from package foo,there are two possible ways to import it:

import foo.*;

Pros: Potentially reduces the number of import statements.

import foo.Bar;

Pros: Makes it obvious what classes are actually used. Makes code more readable for maintainers.

Decision: Use the latter for importing all Android code. An explicit exception is made for java standard libraries (java.util.*, java.io.*, etc.) and unit test code (junit.framework.*)

## Java Library Rules

There are conventions for using Android's Java libraries and tools. In some cases, the convention has changed in important ways and older code might use a deprecated pattern or library. When working with such code, it's okay to continue the existing style. When creating new components never use deprecated libraries.

## Java Style Rules

Every file should have a copyright statement at the top. Then a package statement and import statements should follow, each block separated by a blank line. And then there is the class or interface declaration. In the Javadoc comments, describe what the class or interface does.

```objc
/*
 * Copyright (C) 2013 The Android Open Source Project 
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at 
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software 
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and 
 * limitations under the License.
 */

package com.android.internal.foo;

import android.os.Blah;
import android.view.Yada;

import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * Does X and Y and provides an abstraction for Z.
 */

public class Foo {
    ...
}
```

Every class and nontrivial public method you write must contain a Javadoc comment with at least one sentence describing what the class or method does. This sentence should start with a 3rd person descriptive verb.

Examples:

```objc
/** Returns the correctly rounded positive square root of a double value. */
static double sqrt(double a) {
    ...
}
```

or

```objc
/**
 * Constructs a new String by converting the specified array of 
 * bytes using the platform's default character encoding.
 */
public String(byte[] bytes) {
    ...
}
```

You do not need to write Javadoc for trivial get and set methods such as setFoo() if all your Javadoc would say is "sets Foo". If the method does something more complex (such as enforcing a constraint or having an important side effect), then you must document it. And if it's not obvious what the property "Foo" means, you should document it.

Every method you write, whether public or otherwise, would benefit from Javadoc. Public methods are part of an API and therefore require Javadoc.


## Define Fields in Standard Places

Fields should be defined either at the top of the file, or immediately before the methods that use them.

## Limit Variable Scope

The scope of local variables should be kept to a minimum. By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error. Each variable should be declared in the innermost block that encloses all uses of the variable.

Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. If you don't yet have enough information to initialize a variable sensibly, you should postpone the declaration until you do.

One exception to this rule concerns try-catch statements. If a variable is initialized with the return value of a method that throws a checked exception, it must be initialized inside a try block. If the value must be used outside of the try block, then it must be declared before the try block, where it cannot yet be sensibly initialized:

```objc
// Instantiate class cl, which represents some sort of Set 
Set s = null;
try {
    s = (Set) cl.newInstance();
} catch(IllegalAccessException e) {
    throw new IllegalArgumentException(cl + " not accessible");
} catch(InstantiationException e) {
    throw new IllegalArgumentException(cl + " not instantiable");
}

// Exercise the set 
s.addAll(Arrays.asList(args));
```

But even this case can be avoided by encapsulating the try-catch block in a method:

```objc
Set createSet(Class cl) {
    // Instantiate class cl, which represents some sort of Set 
    try {
        return (Set) cl.newInstance();
    } catch(IllegalAccessException e) {
        throw new IllegalArgumentException(cl + " not accessible");
    } catch(InstantiationException e) {
        throw new IllegalArgumentException(cl + " not instantiable");
    }
}

...

// Exercise the set 
Set s = createSet(cl);
s.addAll(Arrays.asList(args));
```

Loop variables should be declared in the for statement itself unless there is a compelling reason to do otherwise:

```objc
for (int i = 0; i < n; i++) {
    doSomething(i);
}
```

and

```objc
for (Iterator i = c.iterator(); i.hasNext(); ) {
    doSomethingElse(i.next());
}
```

# Order Import Statements

The ordering of import statements is:

* Android imports

* Imports from third parties (com, junit, net, org)

* java and javax

To exactly match the IDE settings, the imports should be:

* Alphabetical within each grouping, with capital letters before lower case letters (e.g. Z before a).

* There should be a blank line between each major grouping (android, com, junit, net, org, java, javax).

Originally there was no style requirement on the ordering. This meant that the IDE's were either always changing the ordering, or IDE developers had to disable the automatic import management features and maintain the imports by hand. This was deemed bad. When java-style was asked, the preferred styles were all over the map. It pretty much came down to our needing to "pick an ordering and be consistent." So we chose a style, updated the style guide, and made the IDEs obey it. We expect that as IDE users work on the code, the imports in all of the packages will end up matching this pattern without any extra engineering effort.

This style was chosen such that:

* The imports people want to look at first tend to be at the top (android)

* The imports people want to look at least tend to be at the bottom (java)

* Humans can easily follow the style

* IDEs can follow the style

The use and location of static imports have been mildly controversial issues. Some people would prefer static imports to be interspersed with the remaining imports, some would prefer them reside above or below all other imports. Additionally, we have not yet come up with a way to make all IDEs use the same ordering.

Since most people consider this a low priority issue, just use your judgement and please be consistent.

## Follow Field Naming Conventions

* Non-public, non-static field names start with m.

* Static field names start with s.

* Other fields start with a lower case letter.

* Public static final fields (constants) are ALL_CAPS_WITH_UNDERSCORES.

For example:

```objc
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

## Use Standard Brace Style

Braces do not go on their own line; they go on the same line as the code before them. So:

```objc
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```

We require braces around the statements for a conditional. Except, if the entire conditional (the condition and the body) fit on one line, you may (but are not obligated to) put it all on one line. That is, this is legal:

```objc
if (condition) {
    body(); 
}
```

and this is legal:

```objc
if (condition) body();
```

but this is still illegal:

```objc
if (condition)
    body();  // bad!
```

## Use Standard Java Annotations

Annotations should precede other modifiers for the same language element. Simple marker annotations (e.g. @Override) can be listed on the same line with the language element. If there are multiple annotations, or parameterized annotations, they should each be listed one-per-line in alphabetical order.

Android standard practices for the three predefined annotations in Java are:

* @Deprecated: The @Deprecated annotation must be used whenever the use of the annotated element is discouraged. If you use the @Deprecated annotation, you must also have a @deprecated Javadoc tag and it should name an alternate implementation. In addition, remember that a @Deprecated method is still supposed to work.
If you see old code that has a @deprecated Javadoc tag, please add the @Deprecated annotation.


* @Override: The @Override annotation must be used whenever a method overrides the declaration or implementation from a super-class.
For example, if you use the @inheritdocs Javadoc tag, and derive from a class (not an interface), you must also annotate that the method @Overrides the parent class's method.


* @SuppressWarnings: The @SuppressWarnings annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this "impossible to eliminate" test, the @SuppressWarnings annotation must be used, so as to ensure that all warnings reflect actual problems in the code.
When a @SuppressWarnings annotation is necessary, it must be prefixed with a TODO comment that explains the "impossible to eliminate" condition. This will normally identify an offending class that has an awkward interface. For example:

```objc
// TODO: The third-party class com.third.useful.Utility.rotate() needs generics 
@SuppressWarnings("generic-cast")
List<String> blix = Utility.rotate(blax);
```

When a @SuppressWarnings annotation is required, the code should be refactored to isolate the software elements where the annotation applies.

## Treat Acronyms as Words

Treat acronyms and abbreviations as words in naming variables, methods, and classes. The names are much more readable:

* Bad

 XMLHTTPRequest

 getCustomerID

 String URL

* Good

 XmlHttpRequest

 getCustomerId

 String url

Both the JDK and the Android code bases are very inconsistent with regards to acronyms, therefore, it is virtually impossible to be consistent with the code around you. Bite the bullet, and treat acronyms as words.

## Use TODO Comments

Use TODO comments for code that is temporary, a short-term solution, or good-enough but not perfect.

TODOs should include the string TODO in all caps, followed by a colon:

```objc
// TODO: Remove this code after the UrlTable2 has been checked in.
```

and

```objc
// TODO: Change this to use a flag instead of a constant.
```

If your TODO is of the form "At a future date do something" make sure that you either include a very specific date ("Fix by November 2005") or a very specific event ("Remove this code after all production mixers understand protocol V7.").

## Log Sparingly

While logging is necessary, it has a significantly negative impact on performance and quickly loses its usefulness if it's not kept reasonably terse. The logging facilities provides five different levels of logging:

* ERROR: This level of logging should be used when something fatal has happened, i.e. something that will have user-visible consequences and won't be recoverable without explicitly deleting some data, uninstalling applications, wiping the data partitions or reflashing the entire phone (or worse). This level is always logged. Issues that justify some logging at the ERROR level are typically good candidates to be reported to a statistics-gathering server.


* WARNING: This level of logging should used when something serious and unexpected happened, i.e. something that will have user-visible consequences but is likely to be recoverable without data loss by performing some explicit action, ranging from waiting or restarting an app all the way to re-downloading a new version of an application or rebooting the device. This level is always logged. Issues that justify some logging at the WARNING level might also be considered for reporting to a statistics-gathering server.


* INFORMATIVE: This level of logging should used be to note that something interesting to most people happened, i.e. when a situation is detected that is likely to have widespread impact, though isn't necessarily an error. Such a condition should only be logged by a module that reasonably believes that it is the most authoritative in that domain (to avoid duplicate logging by non-authoritative components). This level is always logged.


* DEBUG: This level of logging should be used to further note what is happening on the device that could be relevant to investigate and debug unexpected behaviors. You should log only what is needed to gather enough information about what is going on about your component. If your debug logs are dominating the log then you probably should be using verbose logging.
This level will be logged, even on release builds, and is required to be surrounded by an if (LOCAL_LOG) or if (LOCAL_LOGD) block, where LOCAL_LOG[D] is defined in your class or subcomponent, so that there can exist a possibility to disable all such logging. There must therefore be no active logic in an if (LOCAL_LOG) block. All the string building for the log also needs to be placed inside the if (LOCAL_LOG) block. The logging call should not be re-factored out into a method call if it is going to cause the string building to take place outside of the if (LOCAL_LOG) block.

There is some code that still says if (localLOGV). This is considered acceptable as well, although the name is nonstandard.

* VERBOSE: This level of logging should be used for everything else. This level will only be logged on debug builds and should be surrounded by an if (LOCAL_LOGV) block (or equivalent) so that it can be compiled out by default. Any string building will be stripped out of release builds and needs to appear inside the if (LOCAL_LOGV) block.


Notes:

* Within a given module, other than at the VERBOSE level, an error should only be reported once if possible: within a single chain of function calls within a module, only the innermost function should return the error, and callers in the same module should only add some logging if that significantly helps to isolate the issue.


* In a chain of modules, other than at the VERBOSE level, when a lower-level module detects invalid data coming from a higher-level module, the lower-level module should only log this situation to the DEBUG log, and only if logging provides information that is not otherwise available to the caller. Specifically, there is no need to log situations where an exception is thrown (the exception should contain all the relevant information), or where the only information being logged is contained in an error code. This is especially important in the interaction between the framework and applications, and conditions caused by third-party applications that are properly handled by the framework should not trigger logging higher than the DEBUG level. The only situations that should trigger logging at the INFORMATIVE level or higher is when a module or application detects an error at its own level or coming from a lower level.


* When a condition that would normally justify some logging is likely to occur many times, it can be a good idea to implement some rate-limiting mechanism to prevent overflowing the logs with many duplicate copies of the same (or very similar) information.


* Losses of network connectivity are considered common and fully expected and should not be logged gratuitously. A loss of network connectivity that has consequences within an app should be logged at the DEBUG or VERBOSE level (depending on whether the consequences are serious enough and unexpected enough to be logged in a release build).


* A full filesystem on a filesystem that is acceessible to or on behalf of third-party applications should not be logged at a level higher than INFORMATIVE.


* Invalid data coming from any untrusted source (including any file on shared storage, or data coming through just about any network connections) is considered expected and should not trigger any logging at a level higher then DEBUG when it's detected to be invalid (and even then logging should be as limited as possible).

* Keep in mind that the + operator, when used on Strings, implicitly creates a StringBuilder with the default buffer size (16 characters) and potentially quite a few other temporary String objects, i.e. that explicitly creating StringBuilders isn't more expensive than relying on the default '+' operator (and can be a lot more efficient in fact). Also keep in mind that code that calls Log.v() is compiled and executed on release builds, including building the strings, even if the logs aren't being read.

* Any logging that is meant to be read by other people and to be available in release builds should be terse without being cryptic, and should be reasonably understandable. This includes all logging up to the DEBUG level.


* When possible, logging should be kept on a single line if it makes sense. Line lengths up to 80 or 100 characters are perfectly acceptable, while lengths longer than about 130 or 160 characters (including the length of the tag) should be avoided if possible.


* Logging that reports successes should never be used at levels higher than VERBOSE.


* Temporary logging that is used to diagnose an issue that's hard to reproduce should be kept at the DEBUG or VERBOSE level, and should be enclosed by if blocks that allow to disable it entirely at compile-time.


* Be careful about security leaks through the log. Private information should be avoided. Information about protected content must definitely be avoided. This is especially important when writing framework code as it's not easy to know in advance what will and will not be private information or protected content.


* System.out.println() (or printf() for native code) should never be used. System.out and System.err get redirected to /dev/null, so your print statements will have no visible effects. However, all the string building that happens for these calls still gets executed.

* The golden rule of logging is that your logs may not unnecessarily push other logs out of the buffer, just as others may not push out yours.

## Follow Test Method Naming Conventions

When naming test methods, you can use an underscore to seperate what is being tested from the specific case being tested. This style makes it easier to see exactly what cases are being tested.

For example:

```objc
testMethod_specificCase1 testMethod_specificCase2

void testIsDistinguishable_protanopia() {
    ColorMatcher colorMatcher = new ColorMatcher(PROTANOPIA)
    assertFalse(colorMatcher.isDistinguishable(Color.RED, Color.BLACK))
    assertTrue(colorMatcher.isDistinguishable(Color.X, Color.Y))
}
```
