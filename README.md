# SCUMSLang Language Specification

## About

SCUMSLang is a modern StarCraft User Map Settings language that has its goal to supersede the normally used language in StarEdit (nowadays superseded by ScmDraft) to define custom behaviour in maps.

## Specification

**Static variables**

```
static <var_name> = <value>;
```

**Functions**

```
function <function_name>() {
    
}
```

**Event handlers**

```
// Anonymous event handler
function() when <condition_name>(), ..., <another_condition_name>(...) {

}

// Named event handler
function <function_name>() <condition_name>(), ..., <another_condition_name>(...) {

}
```

**Attributes**

```
// Argumentless attribute
[<attribute_name>]
...
[<another_attribute_name>]

// Attribute with arguments
[<attribute_name>("arg1", 2)]
```

**Constants**

Constants are pre-defined and in-built values of StarCraft which are simply said constant names (e.g. Player1).

**Templates**

```
// A template function has template arguments that only accepts constants.
template function<template_variable, ..., another_template_variable>(<argument>, ..., <another_argument>) {

}

template (<variable_name, another_variable_name>) for (<value>, ..., <another_value>) and (<value>, ..., <another_value>) {

}
```

**Blocks**

```
ordered {
    // All event handlers in this block are fired sequentially
}
```