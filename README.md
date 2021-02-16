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

**typedef enum directive**

```
// Makes false and true usable as constants.
// Both constants are still of type Boolean.
typedef enum { false, true } Boolean;
```

**typedef directive**

```
// A type definition where int is the alias for UInt32.
// Assumes that the type UInt32 already exists.
typedef UInt32 int;
```

**using static directive**

The `using static` directive designates a enum type whose field members you can access without specifying a enum type name. Its syntax is:

```
using static <fully-qualified-type-name>;
```

**static keyword**

The `static` keyword is used to define a variable in the global block scope. It's syntax is:

```
// Declaration without initial assignment.
static <type> <variable-name>;

// Declaration with initial assignment.
static <type> <variable-name> = <value>;
```

**`function` keyword**

The `function` keyword introduces a new function which has to be followed by a name and an argument list. For example:

```
// A non-generic function.
function function_name(...)
{ ... }

// A generic function
function function_name<generic_parameter_name>(...)
{ ... }
```

**function...when**

A event handler is a function with conditions. They represent the triggers in StarCraft.

```
// An anonymous event handler.
function () when condition_name(), ..., another_condition_name(...)
{ ... }

// A named event handler.
function function_name() condition_name(), ..., another_condition_name(...)
{ ... }
```

**`[...]` attribute**

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

**`template function` directive**

The `template function` directive creates a function which resolves template arguments at compile time and arguments at runtime like in non-template `function`s.

```
// A template function that specifies two variables resolved at compile time and two arguments resolved at runtime.
template function<Unit UnitId, Player PlayerId>(<type> <argument_name>, <type> <another_argument_name>)
{ ... }
```

**`template foreach` directive**

```
// A template block.
template foreach (Player PlayerId, Unit UnitId, ...)
    // Line-breaks just for visual purposes 😊
    in (Player.Player1)
    in (Unit.ZergZergling)
{
    greet_player(UnitId, PlayerId);
}
```