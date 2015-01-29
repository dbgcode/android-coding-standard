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

