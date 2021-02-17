# SCUMSLang Language Specification <!-- omit in toc -->

## About <!-- omit in toc -->

SCUMSLang is a modern StarCraft User Map Settings programming language that has its goal to supersede the normally used language in StarEdit (nowadays superseded by ScmDraft) to define custom behaviour in maps.

## Table of Contents <!-- omit in toc -->

- [1. File extensions](#1-file-extensions)
- [2. Integrated types](#2-integrated-types)
- [3. Limits](#3-limits)
- [4. Language syntax](#4-language-syntax)
  - [4.1. **`import` directive**](#41-import-directive)
  - [4.2. **`typedef enum` expression**](#42-typedef-enum-expression)
  - [4.3. **`typedef` expression**](#43-typedef-expression)
  - [4.4. **`using static` directive**](#44-using-static-directive)
  - [4.5. **`static` keyword**](#45-static-keyword)
  - [4.6. **`function` keyword**](#46-function-keyword)
  - [4.7. **`function...when`**](#47-functionwhen)
  - [4.8. **`[...]` attribute**](#48--attribute)
  - [4.9. **`template function` expression**](#49-template-function-expression)
  - [4.10. **`template foreach` expression**](#410-template-foreach-expression)

## 1. File extensions

**.umsh**

> The extension `.umsh` stands for User Mapping Settings Header. It is a header file to expose an API that can be used in the actual program.

**.umsl**

> The extension `.umsl` stands for User Mapping Settings Language. It is the source file that is getting compiled.

## 2. Integrated types

SCUMSLang-Keyword | SCUMSLang-Type | StarCraft-Type
------------------|----------------|----------------
`int`             | `UInt32`       | UInt32
`byte`            | `UInt8`        | UInt32 (shared)
`enum`            | -              | -
`bool`            | `Boolean`      |
`string`          | `String`       | String

## 3. Limits

SCUMSLang-Type | Range
---------------|---------
UInt32         | 0 to 4,294,967,295 numeric
UInt8          | 0 to 255 numeric
String         | 0 to 1024 bytes ([reference](https://staredit-network.fandom.com/wiki/String#String_limits))

## 4. Language syntax

### 4.1. **`import` directive**

File `Index.umsh` may contain:

```
// Imports file "State.umsh" one folder above this file's directory.
import "../State.umsh";
```

```
// Imports file "State.umsh" in folder States of this file's directory.
import "./States/State.umsh";
```

### 4.2. **`typedef enum` expression**

```
// Makes false and true usable as constants.
// Both constants are still of type Boolean.
typedef enum { false, true } Boolean;
```

### 4.3. **`typedef` expression**

```
// A type definition where int is the alias for UInt32.
// Assumes that the type UInt32 already exists.
typedef UInt32 int;
```

### 4.4. **`using static` directive**

The `using static` directive designates a enum type whose field members you can access without specifying a enum type name. Its syntax is:

```
using static <fully-qualified-type-name>;
```

### 4.5. **`static` keyword**

The `static` keyword is used to define a variable in the global block scope. It's syntax is:

```
// Declaration without initial assignment.
static <type> <variable-name>;

// Declaration with initial assignment.
static <type> <variable-name> = <value>;
```

### 4.6. **`function` keyword**

The `function` keyword introduces a new function which has to be followed by a name and an argument list. For example:

```
// A non-generic function.
function function_name(...)
{ ... }

// A generic function
function function_name<generic_parameter_name>(...)
{ ... }
```

### 4.7. **`function...when`**

A event handler is a function with conditions. They represent the triggers in StarCraft.

```
// A named event handler.
function function_name() 
    when condition_name()
    when another_condition_name(...)
{ ... }
```

### 4.8. **`[...]` attribute**

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

### 4.9. **`template function` expression**

The `template function` expression creates a function which resolves template arguments at compile time and arguments at runtime like in non-template `function`s.

```
// A template function that specifies two variables resolved at compile time and two arguments resolved at runtime.
template function<Unit UnitId, Player PlayerId>(<type> <argument_name>, <type> <another_argument_name>)
{ ... }
```

### 4.10. **`template foreach` expression**

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