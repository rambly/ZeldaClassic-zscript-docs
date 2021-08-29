# Syntax

## Numbers

ZScript supports numerical input of **decimal**, **hexadecimal**, and **binary** numbers.

To input hexadecimal numbers, prefix them with `0x`. To input binary numbers, append `b` to the end of the value. Example:

``` C++
int MyCoolHexNumber = 0x0F; // same as decimal 15
int MyCoolBinaryNumber = 0011b; // same as decimal 3
```

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