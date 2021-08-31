# Syntax

## Overview

This page covers the basic syntax and structure of ZScript.  Syntactically, ZScript is similar to C languages, and many principles will cross over between each.  However, note that they are not the same and handling of certain concepts is very different, so be sure to read the documentation carefully.

## Declarations

### Variables and Datatypes

INT / FLOAT
:	<!-- - -->
Legal Range: -214748.3648, 214748.3647
		
The basic numeral datatype. In ZScript, `int` and `float` are identical.  The different tokens exist purely for local semantics and both resolve to the same type, including for the purpose of matching function signatures.  That is, all functions that accept `int` will also accept `float`, and vice-versa.
		
In this documentation, use of `int` in variable and function definitions denotes that decimal values will be floored and disregarded when used as inputs, and `float` denotes that decimal values are retained.  However, in user-defined functions, there is no such limitation and `int` return values will freely return decimals.
		
There is no unsigned numeral datatype and values will overflow or underflow if they go outside of the legal range.
		
The use of "integer" and "float" are both misnomers - numbers are always fixed point in ZScript, and always contain four decimal points of precision.  Decimal places beyond the fourth will be truncated.
		
`int` values may also be represented or defined using **binary** or **hexadecimal** notation.  To input hexadecimal numbers, prefix them with `0x`.  To input binary numbers, append `b` to the end of the value.  For example:

``` C++
int MyCoolHexNumber = 0x0F; // same as decimal 15
int MyCoolBinaryNumber = 0011b; // same as decimal 3
```

Negative values **are** stored in binary and hexadecimal notation.  For example:

``` C++
int MyVariable = -33;
TraceToBase(MyVariable,16,1); //This will print "-0x21" to the console.
```

However, the use of negative values for both operands in bitwise functions produces undefined results and is not recommended.

Decimals are **not** represented or stored in binary or hexadecimal notation.  If an `int` with decimals has a bitwise operation performed on it, the decimals will be removed.  For example:

``` C++
int MyValue = 2.64;
MyValue |= 0001b;
Trace(MyValue);
//MyValue is initialized as an int datatype with value 2.64.
//This is bitwise OR assigned with 0001b.
//Converting 2.64 to binary floors it to 2, or 0010b.
//The OR assignment combines these to 0011b and stores to MyValue.
//The Trace statement will print "3.0000" to the console.
```	

`int` tyoed arrays are used to store strings in ZScript - see **[Arrays](#arrays)** below for more information.

--- 

BOOL
:	<!-- - -->
Legal Range: false, true

A general boolean datatype.  Internally, `false` is **0** and `true` is **0.0001**.

`int` values can be typecast to `bool`.  Any non-zero value will evaluate as `true`; only zero will evaluate as `false`.  For example:

``` C++
int MyInteger = -33;
bool MyBoolean = MyInteger; //MyBoolean is true, since MyInteger is not 0
```

`bool` values cannot be typecast to `int`.

---

Pointer Datatypes
:	<!-- - -->

Additionally, ZScript uses pointer datatypes for the different objects available to scripts.  

The following are global pointers, which are always available and don't need to be initialized:

- **Game**: Contains information and functions relevant to the current game state.
- **Link**: Contains informationa nd functions relevant to the player and player's sprite. 
- **Screen**: Contains information and functions relevant to the current screen and drawing commands.

The following generic pointers need to be initialized before use, as there can be multiple objects of each that exist at a time:

- **npc**: Contains information and functions relevant to enemies on the current screen.
- **lweapon**: Contains information and functions relevant to the player's weapons and projectiles *as they exist on the screen*.  The player's inventory is contained in the `Link` pointer, and information about weapons in their inventory is stored in `itemdata` pointers.
- **eweapon**: Contains information and functions relevant to any enemy weapons and projectiles *as they exist on the screen*.
- **ffc**: Contains information and functions relevant to FFC's.
- **item**: Contains information and functions relevant to an item on the current screen.  `item` refers to pickup items such as hearts and rupees - if looking for the player's "items", see the `Link` and `lweapon` pointers.
- **itemdata**: Contains information and functions relevant to an item's internal data.

Initiailizing these pointers is performed as follows:

``` C++
npc MyEnemy = Screen->LoadNPC(1); //Loads the 1st enemy on screen into a pointer
lweapon MyWeapon = Screen->LoadLWeapon(2); //Loads the 2nd LWeapon on screen into a pointer
eweapon EnemyWeapon = Screen->LoadEWeapon(2); //Loads the 2nd EWeapon on screen into a pointer
ffc MyFFC = Screen->LoadFFC(10); //Loads FFC 10 on screen into a pointer
item myItem = Screen->LoadItem(3); //Loads the 3rd item on screen into a pointer
itemdata MyInvItem = Game->LoadItemData(45); //Loads the 45th item in the item editor into a pointer
```

The `npc`, `lweapon`, `eweapon`, `ffc`, and `item` pointers become invalid when the associated object no longer exists - for example, if an enemy dies, its `npc` pointer will no longer be valid.  All of these objects cease to exist when the player exits the screen.  If an invalid pointer is used to reference data, a console error will be logged.  Each pointer has a `->isValid()` function that can be used to determine whether it exists or not.

The `itemdata` pointer will never become invalid, since the item's data is handled on a permanent per-quest basis.

---

### Constants

`int`, `float`, and `bool` variables in global scope can be declared as constants as follows:

``` C++
const int A = 5; //A is a constant integer
```

This uses no stack space / registers and does not count against the global variable limit.

In order to declare a constant, the assigned value must be a numerical or boolean literal.  Contants, variables, or expressions cannot be used. Constants cannot be declared in any scope below global. For example:

``` C++
const int A = 5;   //A is a constant integer
const int B = A;   //This is illegal and will error on compile.
const int C = 5*3; //This is illegal and will error on compile.

void MyFunction() {
	const int D = 5; //This is illegal and will error on compile.
}
```

---

### Arrays

Arrays may be declared for any variable type or generic pointer.  Arrays are zero-indexed, meaning that the first value is accessed with **0**.

In order to declare an array, the size must be a numerical literal.  Constants, variables, or expressions cannot be used.

The maximum array size is 214748.

``` C++
int MyArray[5]; //MyArray is an array containing int variables, sized to 5.
MyArray[0] = 2;	//Stores 2 to the first (0) value of MyArray.
MyArray[4] = 3;	//Stores 3 to the fifth and last (4) value of MyArray
int GetValue = MyArray[3]; //Gets a value from MyArray and stores it to GetValue.

int value = 3;
int AnotherArray[] = {value, 5, 6.5}; 
//Alternative way to declare an array with values.
//The array will be sized to the contents.
//Variables and expressions can be passed into the array contents.

lweapon WeaponArray[3];
WeaponArray[0] = Screen->LoadLWeapon(1);
//Arrays can be declared for generic pointers.
```

Setting or accessing the contents of arrays outside of their range is syntactically correct, but will produce a console error at runtime.
``` C++
int MyArray[5]; //MyArray is an array containing int variables, sized to 5.
MyArray[30] = 3; //This will compile, but will produce an error and will not execute.

int GetValue = MyArray[5]; 
//This will compile, but will produce an error. 
//-1 will be stored to GetValue.
```

Integer arrays are used to store string data in ZScript.  See "docs/string.txt" for string functions accessible with `std.zh`.  Operations for modifying strings are not internal to ZScript.
``` C++
int MyString[] = "Hello world!";
```

!!! tip
	In 2.53, the maximum number of global variables allowed is 1024.  However, arrays only count as one variable, regardless of their length.  Use of global arrays can help reduce the number of global variables used to store data.

---

### Functions

Functions may be defined by the user in ZScript.  Functions may return any variable type or generic pointer.  Additionally, functions may have a `void` return type, indicating that they do not return a value.  Function declarations follow the format below:

``` C++
return_type function_name ( parameter_list ) {
	body of the function
}
```

Use the `return` statement to define a return value for the function and immediately end its execution.  If function reaches the end of its scope and does not encounter a return statement, the return value is **0** for `int` returns and **false** for `bool` returns.  If the return is a generic pointer, it will be undefined and invalid.  Some examples functions are shown below:

``` C++
int MyAdditionFunction (int Num1, int Num2) {
	int Sum = Num1 + Num2;
	return Sum;
}

void LaunchHero() {
	Link->Jump = 3;
}
//Void functions need no return statement

bool IsEven (int Num) {
	if ((Num % 2) == 0) {
		return true;
	}
	else {
		return false;
	}
}
//This function checks if the input variable Num is even or not.
//If the remainder of Num / 2 is 0, it returns true.
//Else, it returns false.
```

Functions may use arrays as inputs and outputs.
Functions may be **overloaded**.  This means that multiple functions may have the same name and return type as long as the input parameters are different.  For example:

``` C++
int GetWeaponX (eweapon Weapon) {
	return Weapon->X; 
}

int GetWeaponX (lweapon Weapon) {
	return Weapon->X;
}

//These functions both have the same name.
//They are legal because the input parameters are different.
//In this case, you could call "GetWeaponX()" on either type of weapon.
```

Functions adhere to scope rules - see **[Scope Rules](#scope-rules)** below for more information.

---

### Global Scripts

!!! error "TODO"
	(TODO) !

---

### FFC Scripts

!!! error "TODO"
	(TODO) !

---

### Item Scripts

!!! error "TODO"
	(TODO) !

---

## Scope Rules

Variables, arrays, and functions have limited (or unlimited) scope depending on where in the code they are declared.

- **Global Scope**: Variables declared outside of any script, function, or block.
- **Local Scope**: Variable declared inside a script, function, or block.

Local variables are only accessible inside the script, function, or loop that they are declared.  For example:

``` C++
void MyBadFunction(int Input) {
	if (Input > 5) {
		int Output = 3;
	}
	else {
		int Output = 2;
	}
	return Output;
}
//This will generate an error during compilation and is not legal.
//Output is declared inside of the if() block, and is not acessible outside of it.

void MyGoodFunction(int Input) {
	int Output;
	if (Input > 5) {
		Output = 3;
	}
	else {
		Output = 2;
	}
	return Output;
}
//Since Output is now declated in function scope, it is accessible and the function is legal.
```

Variables of the same name can be legally declared and will not interfere with each other as long as they are in different scopes. In 2.53, variables will always return at the smallest scope they are legal.  There is **no way** to resolve a variable to a larger scope.  For example:

``` C++
int a = 45;
while (true) {
	Trace(a);	//will output 45
	int a = 2;
	Trace(a);	//will output 2 - we are now reading from the block scope variable declaration
	break;
}
Trace(a);		//will output 45 - the block scope variable is no longer accessible
```

!!! tip
	Global variables are only initialized once, when the quest is first opened - this means that the values are saved between quest sessions while playing.  This makes them useful for storing persistent playthough information.  If variables need to be reset between sessions or player deaths, this needs to be manually handled in the global script.

!!! caution
	Since global variables are only initialized once, this means that reloading a save file after adding additional global variables will produce undefined errors, since these variables were not initialized properly.  Always test changes to global variables using a fresh save file.

---

## Pre-Processor Directives
Import
:	<!-- - -->

Before the script compiles, `import` will add a file to the script file as if it was directly typed into the document.  This can be used to add headers or organize scripts more easily.

`import` will check an absolute path, then a path relative to the zquest.exe file, then will check hard-coded include folders.  These are "include", "headers", and "scripts".

`#include` can also be used.  This is almost interchangeable, but will check the include folders first, then an absolute path, then a path relative to the zquest.exe file.  This only matters if there are multiple files of the same name in valid paths for inclusion.

If a compiler error occurs in an imported file, the compiler error message will note the file and line inside that file that produced the error.

The Header Guard script setting affects `import` in some cases.  See "Header Guard" in "Misc" for more information.

``` C++
import "std.zh" //std.zh is inside the "include" folder and thus does not have to be pathed to.
import "MyProject/MyScriptFile.z" //If the folder "MyProject" is in the same directory as zquest.exe.
import "C:/Users/MyUser/My Documents/MyFile.z" //To access a file by absolute path.
```

---

## Arithmetic Operators

Plus (+)
:	* ZASM Instruction: `ADDR`, `ADDV`

Adds values `a + b` together.

``` C++
int x = 2;
int y;

y = x + 3; // will be 5
```

---

Minus (-)
:	* ZASM Instruction: `SUBR`, `SUBV`

Subtracts a value from another `a - b`.

``` C++
int x = 7;
int y;

y = x - 3; // will be 4
```

---

Increment (++)
:	<!-- - -->

Increments a value by **1**.  This modifies the original variable.

If used postfix (`x++`) the operator returns the value **before** incrementing.

If used prefix (`++x`) the operator returns the value **after** incrementing.

``` C++
int x = 17;
int y = x++;

// x = 18
// y = 17, as the value was returned before incrementing x

int a = 5;
int b = ++a;

// a = 6
// b = 6, as the value was returned after incrementing a
```

---

Decrement (--)
:	<!-- - -->

Decrements a value by **1**. This modifies the original variable.

If used postfix (`x--`) the operator returns the value **before** incrementing.

If used prefix (`--x`) the operator returns the value **after** incrementing.

``` C++
int x = 8;
int y = x--;

// x = 7
// y = 8, as the value was returned before decrementing x

int a = 15;
int b = --a;

// a = 14
// b = 14, as the value was returned after decrementing a
```
	
---
	
Multiply (*)
:	* ZASM Instruction: `MULTR`, `MULTV`

Multiplies values `a * b`.

``` C++
int x = 6;
int y;

y = x * 5; // will be 30
```

---

Divide (/)
:	* ZASM Instruction: `DIVR`, `DIVV`

Divides values `a / b`.

``` C++
int x = 20;
int y;

y = x / 5; // will be 4
```
	
---
	
Modulus (%)
:	<!-- - -->
	
Returns the remainder of integer division `a % b`.

``` C++
int x = 23;
int y;

y = x % 5; // will be 3
```

---
	
## Variable Control Operators

Set (=)
:	* ZASM Instruction: `SETR`, `SETV`

Sets value `a = b`.

Using `:=` is equivalent to `=`.

``` C++
int a = 3;
int b;

b = a + 2; // 5

a = 5;
b = a + 2; // 7
```

---

Addition Assignment (+=)
:	<!-- - -->

Adds values `a += b` and assigns the result to variable `a`.

``` C++
int a = 3;
int b = 7;

a += b; // a is now 10
```

---

Subtraction Assignment (-=)
:	<!-- - -->

Subtracts values `a -= b` and assigns the result to variable `a`.

``` C++
int a = 10;
int b = 5;

a -= b; // a is now 5
```

---

Multiplication Assignment (*=)
:	<!-- - -->

Multiplies values `a *= b` and assigns the result to variable `a`.

``` C++
int a = 20;
int b = 2;

a *= b; // a is now 40
```

---

Division Assignment (/=)
:	<!-- - -->

Divides values `a /= b` and assigns the result to variable `a`.

``` C++
int a = 15;
int b = 3;

a /= b; // a is now 5
```
	
---
	
## Comparison Operators

Equal (==)
:	<!-- - -->

Compares values `a == b` and returns `true` if they match. **Note that this is TWO equals signs, not one. One equals sign will cause a variable to be set instead!**

Using `equals` is equivalent to `==`.

``` C++
if ((2 + 2) == 4) // will evaluate to true
if ((6 + 167) == 4) // will evaluate to false
```
	
---

Not Equal (!=)
:	<!-- - -->

Compares values `a != b` and returns `true` if they **do not** match.

Using `not_eq` is equivalent to `!=`.

``` C++
if ((2 + 2) != 5) // will evaluate to true
if ((10 + 10) != 20) // will evaluate to false
```
	
---
	
Less Than (<)
:	<!-- - -->

Compares values `a < b` and returns `true` if the value of `a` is smaller than the value of `b`.

``` C++
if (6 < 7) // will evaluate to true
if (3 < 1) // will evaluate to false
```
	
---

Greater Than (>)
:	<!-- - -->

Compares values `a > b` and returns `true` if the value of `a` is larger than the value of `b`.

``` C++
if (8 > 3) // will evaluate to true
if (1 > 9) // will evaluate to false
```
	
---

## Logical Operators

!!! note
	ZScript 2.53.2 does not have **LOGICAL XOR** (`^^`). It will need to be simulated using other means.

NOT (!)
:	<!-- - -->

Inverts the logic of any boolean value. That is, `false` becomes `true` and `true` becomes `false`.

``` C++
bool PlayerIsDancing = false;
if (!PlayerIsDancing)
// The player is not a disco dancer, so this will evaluate to true

int peanuts = 99;
if (!(peanuts == 0))
// This will evaluate to true because we have a non-zero amount of peanuts

if (!undeclared_variable)
// This will evaluate to true because the variable doesn't exist,
// and undeclared variables evaluate to false in if statements.
```

---

Logical OR (||)
:	<!-- - -->

`a || b` evaluates to true if either condition `a` or condition `b` is true.

Using `or` is equivalent to `||`.

``` C++
int a = 1;
if ((a + 1 == 2) || (a + 5 == 17)) {
	DoSomething();
}

/// 1 + 5 == 17 is false, but 1 + 1 == 2 is true.
/// Since only one of these conditions needs to be satisfied,
/// this evaluates to true.
```

---
	
Logical AND (&&)
:	<!-- - -->

`a && b` evaluates to true if conditions `a` and `b` are **both** true.

Using `and` is equivalent to `&&`.

``` C++
int a = 5;
if ((a * 2 == 10) && (a - 1 == 17)) {
	DoSomething();
}

/// 5 * 2 == 10 is true, but 5 - 1 == 17 is false.
/// Both of these conditions must be satsified,
/// so this evaluates to false.
```

---

## Bitwise Operators

!!! note
	You may reference a binary value using a numeric sequence, ending in `b`.
  
Bitwise NOT (~)
:	* ZASM Instruction: `BITNOT`

`~a` inverts the bits in the operand.

Using `bitnot` or `compl` is equivalent to using `~`.

!!! error "Known Bug"
	The bitwise `NOT` function does not return the expected correct value on its own. When used with the Bitwise AND Assign `&=`, it will return the expected value; in other contexts, its use is legal but not recommended.
	
``` C++
int a = 101001b; 
int b = 001011b; 
b &= (~a); 
// ~a is expected to be 010110b.
// This is AND assigned with b,
// and is returned as 000010b.
```

---

Bitwise OR (|)
:	* ZASM Instruction: `ORR`, `ORV`

`a | b` returns a `1` in each bit position in which the bits of either or both operands are `1`.

Using `bitor` is equivalent to using `|`.

``` C++
int a = 101001b; 
int b = 001011b; 
int c = a | b; // will be 101011b
```

---

Bitwise AND (&)
:	* ZASM Instruction: `ANDR`, `ANDV`

`a & b` returns a `1` in each bit position only in which the bits of both operands are `1`.

Using `bitand` is equivalent to using `&`.

``` C++
int a = 101001b; 
int b = 001011b; 
int c = a & b; // will be 001001b
```

---

Bitwise XOR (^)
:	* ZASM Instruction: `XORR`, `XORV`

`a ^ b` returns a `1` in each bit position in which the bits of either operand are `1`, but **not** both.

Using `bitxor` is equivalent to using `^`.

``` C++
int a = 101001b; 
int b = 001011b; 
int c = a ^ b; // will be 100010b
```

---

Bitwise OR Assignment (|=)
:	<!-- - -->

`a |= b` returns a `1` in each bit position in which the bits of either or both operands are `1`, then assigns the value to variable `a`.

Using `or_eq` or `or_equal` is equivalent to using `|=`.

``` C++
int a = 101001b; 
int b = 001011b; 
a |= b; // a will be 101011b
```

---

Bitwise AND Assignment (&=)
:	<!-- - -->

`a &= b` returns a `1` in each bit position only in which the bits of both operands are `1`, then assigns the value to variable `a`.

Using `and_eq` or `and_equal` is equivalent to using `&=`.

``` C++
int a = 101001b; 
int b = 001011b; 
a &= b; // a will be 001001b
```

---

Bitwise XOR Assignment (^=)
:	<!-- - -->

`a ^= b` returns a `1` in each bit position in which the bits of either operand are `1`, but **not** both. It then assigns the value to variable `a`.

Using `xor_eq` or `xor_equal` is equivalent to using `&=`.

``` C++
int a = 101001b; 
int b = 001011b; 
a |= b; // a will be 101011b
```

---

Bitwise AND Assignment (&=)
:	<!-- - -->

`a &= b` returns a `1` in each bit position only in which the bits of both operands are `1`, then assigns the value to variable `a`.

Using `and_eq` or `and_equal` is equivalent to using `&=`.

``` C++
int a = 101001b; 
int b = 001011b; 
a &= b; // a will be 001001b
```

---

Bitwise XOR Assignment (^=)
:	<!-- - -->

`a ^= b` returns a `1` in each bit position in which the bits of either operand are `1`, but **not** both. It then assigns the value to variable `a`.

Using `xor_eq` or `xor_equal` is equivalent to using `&=`.

``` C++
int a = 101001b; 
int b = 001011b; 
a ^= b; // a will be 100010b
```

---

Left Shift (<<)
:	* ZASM Instruction: `LSHIFTR`, `LSHIFTV`

`a << b` shifts all bits in `a` leftward by the number of bits `b`. `0` bits are filled from the right. 

!!! caution
	If left shifting causes a variable to exceed the maximum integer limit of 214747 (110100011011011011b), the return will become undefined.

``` C++
int a = 101001b; 
int b = 2; 
int c = a << b; // will be 10100100b
```

---

Right Shift (>>)
:	* ZASM Instruction: `RSHIFTR`, `RSHIFTV`

`a >> b` shifts all bits in `a` rightward by the number of bits `b`.  `0` bits are filled from the left.

``` C++
int a = 101001b; 
int b = 2; 
int c = a << b; // will be 1010b
```

---
## Control Statements and Loops

### If Statement

The `if` statement specifies that a block of code will only be executed if a boolean or logical condition is true.

If used on an `int` or `float` type variable, the `if` statement will return true unless the value of the variable is **0**.

If brackets are not used, only the line immediately after the `if` statement will be executed if true.

``` C++
//General Syntax
if (condition) {
	//this block of code 
	//will execute if the condition is true
}

if (condition)
	//since there are no brackets, only this line will execute if the condition is true
//this line of code will always execute

//Example
int a = 5;
if (a > 2) {
	a--;
}

//variable a is declared as 5
//it is checked to see if it is greater than 2
//it is, so it is decremented by 1
//a is now 4
```

---

### Else Statement

The `else` statement specifies that a block of code will only be executed if a condition is false.  Note that `else` cannot be used on its own- it must be used immediately after an `if` statement's block of code.

Like the `if` statement, if brackets are not used, only the line immediately after the `else` statement will be executed if false.

``` C++
//General Syntax
if (condition) {
	//this block of code will execute if the condition is true
}
else {
	//and this block will execute if it is false
}

//Example
int numberArrows = 0;
bool quiverEmpty = false;
if (numberArrows) {
	numberArrows--;
}
else {
	quiverEmpty = true;
}

//variable numberArrows is declared as 0
//it is checked to see if it is not 0
//it is, so the "numberArrows--;" line is NOT executed
//since the if statement was evaluated false, quiverEmpty is set to true
```

---

### Else If Statement

The `else if` statement specifies that a block of code will only be executed if the initial `if` condition is false, but a separate condition is true.  Like `else`, it can only be used in conjunction with `if`.

Keep in mind that `else if` statements are checked in the order they appear and only one can execute - that is, if multiple else if statements are satisfied, only the first statement appearing in the list will execute its block of code.

``` C++
//General Syntax
if (condition 1) {
	//this block of code will execute if condition 1 is true
}
else if (condition 2) {
	//and this block will execute if condition 1 is false and condition 2 is true
}

//Example
if (hour < 8) {
	TraceS("It's morning!");
}
else if (hour < 16) {
	TraceS("It's midday!");
}
else {
	TraceS("It's evening!");
}
//depending on the value of variable hour...
//different statements are traced to the console
```

---

### While Loop

The `while` loop will continue to execute as long as a condition is true.

!!! Tip
	A common use of use case of while loops is to create permanent loops with `while (true)`.  Since the boolean value of `true` naturally always returns `true`, this will continue to loop and is useful for scripts that need to continue executing indefinitely.
	
	Remember that if there is no `Waitrame()` inside a `while` loop, frames in-game will not advance until the loop is exited.  If an FFC Script contains a `while (true)` loop with no `Waitframe()`, this will freeze the program.  See the `Waitframe()` function in "Global Functions" for more information.

``` C++
//General Syntax
while (condition) {
	//This block of code will execute if the condition is true.
	//If the block of code is fully executed and the condition is still true,
	//it will execute again and again until the condition becomes false.
}

//Example
int a = 2;
while (a < 1000) {
	a *= 2;
}
Trace(a);

//Variable a is initialized as 2.
//As long as it is less than 1000,
//it will continue to be multiplied by 2.
//When the while loop ends, a will be Traced as 1024.

//Example
int a = 0;
while (a < 20) {
	//do something
	a++;
}

//Variable a is initialized as 0.
//As long as it is less than 20, the loop will continue.
//a is incremented at the end of the while loop.
//Thus, anything else inside the loop will always execute exactly 20 times.
```

---

### For Loop

The `for` loop allows you to build initilization, conditional, and looping expressions directly into the loop.

``` C++
//General Syntax
for (first-expression ; conditional-expression ; loop-expression) {
	//This block of code will execute as long as the conditional expression is true.
}
```

In the syntax above:

- The first expression will execute only once the first time that the loop is entered.
- The conditional expression will be checked every time that the loop repeats.  If it returns false, the loop will exit.
- The loop expression will execute every time that the loop repeats, before the conditional expression.

``` C++
//Example
for (int i = 0 ; i < 10 ; ++i) {
	Trace(i);
}

//When the loop is entered, the first expression executes.  This initializes variable i as 0.
//The conditional expression is then checked.  
//0 is less than 10, so the condition is true and the code block executes.
//The value of i is traced to the console.
//The loop is restarted.  Since this is not the first time entering the loop...
//The loop expression executes.  This increments the value of i by 1.
//The conditional expression is then checked.
//1 is less than 10, so the condition is true and the code block executes.
//etc.
//Once i is incremented to 10, the expression will evaluate to false and the loop ends.
//The value of i will have been traced 10 times (0 through 9) to the console.
```

---

### Break Statement

`break` can be used to immediately exit a loop regardless of its conditions.

``` C++
for (int i = 0 ; i < 10 ; ++i) {
	Trace(i);
	if (i == 6) {
		break;
	}
}

//This is the same loop as the for loop example above, but with a nested if statement.
//The for loop will continue normally, but if i equals 6, will terminate.
//This results in the value of i being traced 7 times (0 through 6) to the console.
```

--- 

### Return Statement

`return` exits a function and passes a value to its output.  `return` must be properly typed to the function output.  Use `return` with no values to exit a `void` function.

Expressions and variables may be returned.

``` C++
int MyFunction() {
	return 3;
}
```

---

## Comments

Lines or blocks of code may be specified as comments; these lines will not be compiled and have no effect on the script.  The `//` token denotes that the remainder of the current line is a comment.  The `/*` and `*/` tokens denote a comment block.

``` C++
//This line is a comment.  Anything can be written here.

/*
	This is a block of comments.
	Anything between the block symbols is ignored.
*/

int MyVariable = 3;	//Comments may also exist at the end of a line.
```
