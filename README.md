# SCUMSLang Language Specification <!-- omit in toc -->

## About <!-- omit in toc -->

SCUMSLang is a modern StarCraft User Map Settings programming language that has its goal to supersede the normally used language in StarEdit (nowadays superseded by ScmDraft) to define custom behaviour in maps.

## Table of Contents <!-- omit in toc -->

- [1. Integrated Types](#1-integrated-types)
- [2. Language Syntax](#2-language-syntax)
  - [2.1. **`import` directive**](#21-import-directive)
  - [2.2. **`typedef enum` expression**](#22-typedef-enum-expression)
  - [2.3. **`typedef` expression**](#23-typedef-expression)
  - [2.4. **`using static` directive**](#24-using-static-directive)
  - [2.5. **`static` keyword**](#25-static-keyword)
  - [2.6. **`function` keyword**](#26-function-keyword)
  - [2.7. **`function...when`**](#27-functionwhen)
  - [2.8. **`[...]` attribute**](#28--attribute)
  - [2.9. **`template function` expression**](#29-template-function-expression)
  - [2.10. **`template foreach` expression**](#210-template-foreach-expression)

## 1. Integrated Types

SCUMSLang-Keyword | SCUMSLang-Type | StarCraft-Type
------------------|----------------|----------------
`int`             | UInt32         | UInt32
`byte`            | UInt8          | UInt32 (shared)
`enum`            | -              | -
`string`          | String         | Text

## 2. Language Syntax

### 2.1. **`import` directive**

File `Index.umsh` may contain:

```
// Imports file "State.umsh" one folder above this file's directory.
import "../State.umsh";
```

```
// Imports file "State.umsh" in folder States of this file's directory.
import "./States/State.umsh";
```

### 2.2. **`typedef enum` expression**

```
// Makes false and true usable as constants.
// Both constants are still of type Boolean.
typedef enum { false, true } Boolean;
```

### 2.3. **`typedef` expression**

```
// A type definition where int is the alias for UInt32.
// Assumes that the type UInt32 already exists.
typedef UInt32 int;
```

### 2.4. **`using static` directive**

The `using static` directive designates a enum type whose field members you can access without specifying a enum type name. Its syntax is:

```
using static <fully-qualified-type-name>;
```

### 2.5. **`static` keyword**

The `static` keyword is used to define a variable in the global block scope. It's syntax is:

```
// Declaration without initial assignment.
static <type> <variable-name>;

// Declaration with initial assignment.
static <type> <variable-name> = <value>;
```

### 2.6. **`function` keyword**

The `function` keyword introduces a new function which has to be followed by a name and an argument list. For example:

```
// A non-generic function.
function function_name(...)
{ ... }

// A generic function
function function_name<generic_parameter_name>(...)
{ ... }
```

### 2.7. **`function...when`**

A event handler is a function with conditions. They represent the triggers in StarCraft.

```
// A named event handler.
function function_name() 
    when condition_name()
    when another_condition_name(...)
{ ... }
```

### 2.8. **`[...]` attribute**

The `[...]` attribute defines an attribute which can be applied on functions. For example:

```
// COMPILER SPECIFIC, NOT PART OF EXAMPLE:
// Introduce AttributeExample as attribute.
[AttributeUsage]
function AttributeExample();

// COMPILER SPECIFIC, NOT PART OF EXAMPLE:
// Introduce AnotherAttributeExample as attribute.
[AttributeUsage]
function AnotherAttributeExample(int int_val);

[AttributeExample]
[AnotherAttributeExample(0x3)]
// Following function does now have these attributes above.
do_something();
```

### 2.9. **`template function` expression**

The `template function` expression creates a function which resolves template arguments at compile time and arguments at runtime like in non-template `function`s.

```
// A template function that specifies two variables resolved at compile time and two arguments resolved at runtime.
template function<Unit UnitId, Player PlayerId>(<type> <argument_name>, <type> <another_argument_name>)
{ ... }
```

### 2.10. **`template foreach` expression**

```
// A template block.
template 
    // Line-breaks just for visual purposes 😊
    for (Player PlayerId) in (Player.Player1)
    for (Unit UnitId) in (Unit.ZergZergling)
{
    greet_player(UnitId, PlayerId);
}
```