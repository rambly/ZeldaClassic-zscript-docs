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

Increments a value by **1**. This modifies the original variable.

``` C++
int x = 17;
x++; // will be 18
```

---

Decrement (--)
:	<!-- - -->

Decrements a value by **1**. This modifies the original variable.

``` C++
int x = 8;
x--; // will be 7
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

``` C++
int a = 3;
int b;

b = a + 2; // 5

a = 5;
b = a + 2; // 7
```
	
---
	
## Comparison Operators

Equal (==)
:	<!-- - -->

Compares values `a == b` and returns `true` if they match. **Note that this is TWO equals signs, not one. One equals sign will cause a variable to be set instead!**

``` C++
if ((2 + 2) == 4) // will evaluate to true
if ((6 + 167) == 4) // will evaluate to false
```
	
---

Not Equal (!=)
:	<!-- - -->

Compares values `a != b` and returns `true` if they **do not** match.

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
	You may reference a binary value using anumeric sequence, ending in `b`.

Bitwise NOT (~)
:	* ZASM Instruction: `BITNOT`

`~a` inverts the bits in the operand.

!!! error "Known Bug"
	The bitwise `NOT` function does not return the expected correct value for non-constants. Its usage in other contexts is legal, but not recommended. (TODO) ! is this true? it seems to be the case per what emily said. check if the main factor is constants or when interacting with &=

---

Bitwise OR (|)
:	* ZASM Instruction: `ORR`, `ORV`

`a | b` returns a `1` in each bit position in which the bits of either or both operands are `1`.


``` C++
int a = 101001b; 
int b = 001011b; 
int c = a | b; // will be 101011b
```

---

Bitwise AND (&)
:	* ZASM Instruction: `ANDR`, `ANDV`

`a & b` returns a `1` in each bit position only in which the bits of both operands are `1`.


``` C++
int a = 101001b; 
int b = 001011b; 
int c = a & b; // will be 001001b
```

---

Bitwise XOR (^)
:	* ZASM Instruction: `XORR`, `XORV`

`a ^ b` returns a `1` in each bit position in which the bits of either operand are `1`, but **not** both.


``` C++
int a = 101001b; 
int b = 001011b; 
int c = a | b; // will be 100010b
```

---

Left Shift (<<)
:	* ZASM Instruction: `LSHIFTR`, `LSHIFTV`

`a << b` shifts all bits in `a` leftward by the number of bits `b`. `0` bits are filled from the right. If a `1` bit is shifted past the 18th bit place, the return value will become undefined.

``` C++
int a = 101001b; 
int b = 2; 
int c = a << b; // will be 10100100b
```

---

Right Shift (>>)
:	* ZASM Instruction: `RSHIFTR`, `RSHIFTV`

`a >> b` shifts all bits in `a` rightward by the number of bits `b`.  `0` bits are filled from the right.

``` C++
int a = 101001b; 
int b = 2; 
int c = a << b; // will be 1010b
```

---
## Control Statements

!!! error "Todo"
	(TODO) ! all your ifs, buts, and coconuts

	i mean, all your ifs, whiles, and fors 
