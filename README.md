# SCUMSLang Language Specification

## About

SCUMSLang is a modern StarCraft User Map Settings programming language that has its goal to supersede the normally used language in StarEdit (nowadays superseded by ScmDraft) to define custom behaviour in maps.

## Language Syntax

**Imports**

File `Index.umsh` may contain:

```
// Imports file "State.umsh" one folder above.
import "../State.umsh";
```

```
// Imports file "State.umsh" in folder States.
import "./States/State.umsh";
```

**Type Definitions**

```
// Makes false and true usable as constants.
// Both constants are still of type Boolean.
typedef enum { false, true } Boolean;
```

**Type Aliases**

```
// A type definition where int is the alias for UInt32.
// Assumes that the type UInt32 already exists.
typedef UInt32 int;
```

**Static Variables**

```
// Declares a variable var_name of type int.
// The value 2 is assigned.
static int var_name = 2;
```

**Functions**

```
// A non-generic function.
function function_name() {
    
}

// A generic function
function <generic_parameter_name>function_name() {
    
}
```

**Event Handlers**

A event handler is a function with conditions. They represent the triggers in StarCraft.

```
// An anonymous event handler.
function () when condition_name(), ..., another_condition_name(...) {

}

// A named event handler.
function function_name() condition_name(), ..., another_condition_name(...) {

}
```

**Attributes**

```
// Argumentless attribute
[attribute_name]
...
[another_attribute_name]

// Attribute with arguments
[attribute_name("arg1", 2)]
```

**Templates**

```
// A template function has template arguments that only accepts constants.
template function<template_variable, ..., another_template_variable>(<argument>, ..., <another_argument>) {

}

// A template block.
template (variable_name, another_variable_name) for (1, 2, 3) and (0x1, 0x2, 0x3) and ("1", "2", "3") {

}
```

**Blocks**

```
sequence {
    // All event handlers in this block are fired sequentially
}
```