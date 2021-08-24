# ZScript: Syntax, Core Functions and Variables

The functions listed in this document are all **internal** to ZQuest. They will function in any scope with no header or other import directives required.

These functions are the basic building blocks of ZScript. All of the functions in header files (std.zh, string.zh, et al.) rely on these functions to work. You may think of the functions in this document as the **core functions** of ZScript, and functions in headers as extended functionality. In order to access these external functions, you will need to **import** the relevant function files, e.g. `#include "std.zh"` or `import "std.zh"`.

For all external functions, please read the documentation specific to each header. These are individual files (e.g. std.txt).

Nearly every ZScript function corresponds to a ZASM instruction. Where possible, the ZASM instruction corresponding to each function and the commands detailed herein are listed with the entry for the related function/command. Full ZASM documentation is currently not complete.

# Internal Objects and Classes

Internal functions and variables other than global functions are properties of **objects**, all of which are listed along the sidebar. Each object has a corresponding *typed pointer class*, and the syntax for accessing them is:

``` C++
object->property
```
	
where *object* is the object's name (e.g. Link, Game, Screen) and *property* is the object's function.

For example, the function `void GetCurDMap()` is a property of the `Game` object, and is called in ZScript as:

``` C++
Game->GetCurDMap();
```

The `Link`, `Screen` and `Game` objects are one-of-a-kind, always available, and don't need to be initialized. Other classes, such as `ffc`, `item`, and `npc` must be initialized as objects, however, as there can be multiple instances of each.

As of 2.53, it is not possible to create your own custom classes.

# Typing

ZScript variables are of the types `int`, `float`, and `bool`. As described above, they may also be pointers to objects of the following classes: `ffc`, `item`, `npc`, `lweapon`, and `eweapon`.

ZScript functions are of the types `int`, `float`, `bool`, or `void`. Of these, only `void` does not return a value. (The `void` type is normally used to run a series of instructions without returning a value.) The other types return values appropriate to their type.

!!! note
	Throughout the following documentation, `int` indicates that a parameter is truncated by a function to an integer, or that the return value will always be an integer. However, ZScript itself does not make a distiction between `int` and `float` types.