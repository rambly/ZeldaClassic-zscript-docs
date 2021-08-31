# Global Functions

## General Functions

### Waitdraw()

void Waitdraw()
:	* ZASM Instruction: `WAITDRAW`

Halts execution of the script until ZC's internal code has been run (movement, collision detection, etc.), but before the screen is drawn. This can only be used in the active global script, not in other scripts.

See the "Instruction Processing Order" in "Misc" to determine what order scripts run in and what is performed before and after `Waitdraw()` returns.

!!! important "Waitdraw() in FFC and item scripts"
	As of 2.53.2, calling `Waitdraw()` in an FFC script or an item script is not allowed or advised. It will throw an error in the compiler and may result in unexpected behavior.
	
---

### Waitframe()

void Waitframe()
:	* ZASM Instruction: `WAITFRAME`

Temporarily halts execution of the current script. This function returns at the beginning of the next frame of gameplay.

!!! note
	Calling Waitframe() in an item script is currently effectively identical to calling `Quit()`. This behavior is different in versions after 2.53, and using Waitframe() in an item script is not advised. The same is true for global scripts in the `Init`, `onExit`, and `onContinue` slots.

	It is safe to call `Waitframe()` in the active global script. Unlike with `Waitdraw()`, it is also safe to call `Waitframe()` in FFC scripts.

	A `Waitframe()` is required in all infinite loops (like `while (true)`) so that ZC may pause to break in order to advance to the next frame, then resume the loop from the start. Without a `Waitframe()` instruction, any infinite loops will cause the game to hang.

<!-- **Example** -->
``` C++
while (true)
{
	/// Infinite loop that does stuff once per frame!!
	/// Cool stuff goes here
	Waitframe(); /// Exit the infinite loop here for one frame;
				 /// process all other code that needs to be processed
}
```

---

### Quit()

void Quit()
:	* ZASM Instruction: `QUIT`

Terminates execution of the current script. Does not return.

!!! caution
	If called from a global script, the script itself exits. *All* script processing halts.

<!-- **Example** -->
``` C++
DoSomeStuff(); // This command will run.
Quit(); 
DoSomeMoreStuff(); // This command and any subsequent commands will not run.
```

---

## Tile Modifying Functions

### CopyTile()

void CopyTile(int srctile, int desttile)
:	* ZASM Instruction: `COPYTILERR d2,d3`, `COPYTILEVV`, `COPYTILERV`, `COPYTILEVR`

Copies the tile specified by `srctile` onto the tile space specified by `desttile`. The valid tile value range is **0** to **65519**. This change is temporary within the quest file and will not be retained when saving the game.

!!! tip
	`CopyTile()` may be used to change Link's tile, by copying a tile onto whatever tile ZC is using as a source for `Link->Tile`. Thus, although you cannot write directly to `Link->Tile`, you can write to the actual tile that is being used for this Link attribute, and you can do this for any other game graphic that you need to change.

	When doing this, it is important to read `Link->Dir` or `Link->Flip` **after** `Waitdraw()`, then perform the `CopyTile()` operation immediately thereafter.  See "Instruction Processing Order" in "Misc" for more information.

<!-- **Example** -->
``` C++
CopyTile(312,11614);
// This will copy tile 314 to tilespace 11614. These tiles will then be identical.
```

---
	
### SwapTile()

void SwapTile(int firsttile, int secondtile)
:	* ZASM Instruction: `SWAPTILERR d2,d3`, `SWAPTILEVV`, `SWAPTILERV`, `SWAPTILEVR`

Swaps the two tiles specified by `firsttile` and `secondtile`. The valid tile value range is **0** to **65519**. This change is temporary within the quest file and will not be retained when saving the game.

<!-- **Example** -->  
``` C++
SwapTile(312,11614);
// These tiles will swap their graphics: Tile 312 will become tile 11614,
// and tile 11614 will become tile 312.
```
	
---

### ClearTile()

void SwapTile(int tileref)
:	* ZASM Instruction: `CLEARTILER d3`, `CLEARTILEV`

Erases the tile specified by `tileref`. The valid tile value range is **0** to **65519**. This change is temporary within the quest file and will not be retained when saving the game.

<!--

---

void OverlayTile()
:	* ZASM Instruction: `OVERLAYTILEVV`, `OVERLAYTILEVR`, `OVERLAYTILERV`, `OVERLAYTILERR`

This command is not implemented in 2.53.2.-->
	
---

## Tracing Functions

### Trace()

void Trace(float val)
:	* ZASM Instruction: `TRACER d3`, `TRACEV`

Prints a line containing a string representation of `val` to allegro.log, as well as to the debug console. This is useful for debugging scripts.

You may trace `int` and `float` types with `Trace()`. To trace boolean values, see **[TraceB()](#traceb)** below. `int` values are not truncated when printed, and will always have four zeroes after the decimal point.

Values printed to allegro.log do not, by default, incorporate any whitespace or line breaks. You must manually add these. To add new lines, see **[TraceNL()](#tracenl)** below.

<!-- **Example** -->
``` C++	
int xyz = 4;
Trace(xyz);
// Prints 4.000 to allegro.log.
```

---

### TraceB()

void TraceB(bool state)
:	* ZASM Instruction: `TRACE2R d3`, `TRACE2V`

Prints a boolean state to allegro.log (and the debug console). Similar to **[Trace()](#trace)**, above, except it outputs `true` or `false` as text.

<!-- **Example** -->
``` C++	
bool test = true;
TraceB(test);
// Prints "true" to allegro.log.
```

---

### TraceS()

void TraceS(int s[])
:	* ZASM Instruction: `TRACE6 d3`

Works as **[Trace()](#trace)** above, but prints a full string to allegro.log, using the array pointer `s` as its argument.

Maximum 512 characters. Functions from string.zh can be used to split larger strings.

<!-- **Example** -->
``` C++	
int testString[] = "This is a string.";
TraceS(testString);
// Prints 'This is a string.' to allegro.log.
```

---

### TraceToBase()

void TraceToBase(int val, int base, int mindigits)
:	* ZASM Instruction: `TRACE3`

Prints a line in allegro.log as well as the debug console representing `val` in numberical base `base`.  "mindigits` can be used to specify the minimum digits displayed in the console.

Can be usefuul for checking hex values or bitwise flags ORed together, or just to trace a true intenger value, as **[Trace()](#trace)** above always traces to four decimal places.

Unlike `Trace()`, decimal values are not printed and `TraceToBase()` does not handle floats.  If you use a floating point value for `val`, it will be floored prior to conversion.

<!-- **Example** -->
``` C++	
int val = 16;
Trace(val);            // this will trace the decimal value "16".
TraceToBase(val,2,1);  // this will trace the binary representation of 16, "10000b".
TraceToBase(val,16,8); // this will trace the hex representation of 16, "0x0000000F".
//Note that because we specified 8 for the "mindigits" input, 7 zeroes are appended.
```


---

### TraceNL()

void TraceNL()
:	* ZASM Instruction: `TRACE5`

Traces a newline to allegro.log
This inserts a line break/carriage return (as if pressing return/enter) into allegro.log and is useful for providing formatting to debugging.



---

### ClearTrace()

void ClearTrace()
:	* ZASM Instruction: `TRACE4`

Clears allegro.log of all current traces and messages from Zelda Classic/ZQuest. Works on a per-quest, per-session basis. Values recorded from previous sessions are not erased.

---

## Array Functions

### SizeOfArray()

int SizeOfArray(int array[])

:	* ZASM Instruction: `ARRAYSIZE d2`

Returns the index size of the array pointed by `array`. Works only on `int` and `float` type arrays. Boolean arrays are not supported. Useful in `for` loops. 

<!-- **Example** -->
``` C++	
int isAnArray[216];
int x;
x = SizeOfArray(isAnArray); // becomes 216
```

---

## Mathematical Functions

### Rand()

int Rand(int n)
:	* ZASM Instruction: `RNDR<><> d2,d3`, `RNDV<><>`

Computes and returns a random integer from `0` to `n-1`, or a negative value between `n+1` and `0` if `n` is negative.

!!! note
	The paramater `n` is an integer, and any floating point (ZScript float) value passed to it will be truncated (floored) to the nearest integer. `Rand(3.75)` is identical to `Rand(3)`.
	
	There is a std.zh function also named `Rand()` that accepts two inputs for a bounded random number.

<!-- **Example** -->
``` C++	
Rand(40); \\Produces a random number between 0 and 39.
Rand(-20); \\Produces a random number between -19 and 0.
```

---

### Max()

float Max(float a, float b)
:	* ZASM Instruction: `MAXR<><>`, `MAXV<><>`

Returns the greater of `a` and `b`.

<!-- **Example** -->
``` C++
int GetBigger;
GetBigger = max(5.1, 20.5); // Returns 20.5
```

---
	
### Min()

float Min(float a, float b)
:	* ZASM Instruction: `MINR<><>`, `MINV<><>`

Returns the lesser of `a` and `b`.

<!-- **Example** -->
``` C++
int GetLesser;
GetLesser = min(5.1, 20.5); // Returns 5.1
```

---
	
### Pow()

int Pow(int base, int exp)
:	* ZASM Instruction: `POWERR<><>`, `POWERV<><>`

Returns `base ^ exp`. The return value is undefined for `base = exp = 0`. Note also negative values of `exp` may not be useful, as the return value is truncated to the nearest integer.

<!-- **Example** -->
``` C++
int Power;
Power = Pow(2,5); // Returns 2^5, or 32
```

---

### InvPow()

int InvPow(int base, int exp)
:	* ZASM Instruction: `IPOWERR<><>`, `IPOWERV<><>`

Returns `base ^ (1 / exp)`. The return value is undefined for `exp = 0`, or if `exp` is even and base is negative. Note also that negative values of `exp` may not be useful, as the return value is truncated to the nearest integer.

!!! tip
	The inverse *n*th power of a number is the same as its *n*th root.  For example, `InvPow(4,2)` is equivalent to `Sqrt(4)`.  Further increments of `exp` are equivalent to the cube root, fourth root, etc.

<!-- **Example** -->
``` C++
int InversePower;
InversePower = InvPow(8,3); // Returns the cube root of 8, or 2
```

---
	
### Log10()

float Log10(float val)
:	* ZASM Instruction: `LOG10<>`

Returns the log of val to the base 10. Any value <= 0 will return 0.

---

### Ln()

float Ln(float val)
:	* ZASM Instruction: `LOGE<>`

Returns the natural logarithm of val (to the base e). Any value <= 0 will return 0.

---

### Factorial()

int Factorial(int val)
:	* ZASM Instruction: `FACTORIAL<>`

Returns val!. val < 0 returns 0.

<!-- **Example** -->
``` C++
int MyFactorial;
MyFactorial = Factorial(5); // Returns 5*4*3*2*1, or 120
```

---

### Abs()

float Abs(float val)
:	* ZASM Instruction: `ABS<>`

Return the absolute value of the parameter, if possible. If the absolute value would overflow the parameter, the return value is undefined.

<!-- **Example** -->
``` C++
Abs(-5); // Returns 5
Abs(20); // Returns 20
```

---

### Sqrt()

float Sqrt(float val)
:	* ZASM Instruction: `SQROOTV<><>`, `SQROOTR<><>`

Computes the square root of the parameter. The return value is undefined for `val < 0`.

**NOTE**
:	Passing negative values to Sqrt() will return an error. See SafeSqrt() in std.zh

<!-- **Example** -->
``` C++
int x = Sqrt(16); // x = 4
```

---
	
## Trigonometric Functions

### Sin()

float Sin(float deg)
:	* ZASM Instruction: `SINR<><> d2,d3`, `SINV<><>`

Returns the trigonometric sine of the parameter, which is interpreted as a degree value.

<!-- **Example** -->
``` C++	
float x = Sin(32); // x = 0.5299
```

---

### Cos()

float Cos(float deg)
:	* ZASM Instruction: `COSR<><> d2,d3`, `COSV<><>`

Returns the trigonometric cosine of the parameter, which is interpreted as a degree value.

<!-- **Example** -->
``` C++	
float x = Cos(40); // x = 0.7660
```

---

### Tan()

float Tan(float deg)
:	* ZASM Instruction: `TANR<><> d2,d3`, `TANV<><>`

Returns the trigonometric tangent of the parameter, which is interpreted as a degree value. The return value is undefined if `deg` is of the form `90 + 180n` for an integral value of `n`.

<!-- **Example** -->
``` C++	
float x = Tan(100); // x = -5.6712
```

---
	
### RadianSin()

float RadianSin(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric sine of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
``` C++	
float x = RadianSin(3.1416); // x = 0.0000
```

---

### RadianCos()

float RadianCos(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric cosine of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
``` C++	
float x = RadianCos(3.1416); // x = -1.0000
```

---

### RadianTan()

float RadianTan(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric tangent of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
``` C++	
float x = RadianTan(3.1416); // x = 0.0000
```

---

### ArcSin()

float ArcSin(float x)
:	* ZASM Instruction: `ARCSINR<><>`

Returns the trigonometric arcsine of `x`, which is interpreted as a radian value.  The return value is undefined for `x < -1` or `x > 1`.  

This function will return the lowest solution in the range of `-pi/2` to `pi/2`.

<!-- **Example** -->
``` C++	
float x = ArcSin(0.25); // x = 0.2526
```

---
	
### ArcCos()

float ArcCos(float x)
:	* ZASM Instruction: `ARCCOSR<><>`, `ARCCOSV<><>`

Returns the trigonometric arccosine of `x`, which is interpreted as a radian value.  The return value is undefined for `x < -1` or `x > 1`.  

This function will return the lowest solution in the range of `0` to `pi`.

<!-- **Example** -->
``` C++	
float x = ArcCos(0.25); // x = 1.3181
```
---
	
### ArcTan()

float ArcTan(int x, int y)
:	* ZASM Instruction: `ARCTANR<>`

Returns the trigonometric arctangent of the coordinates, which is interpreted as a radian value.  This is calculated from an assumed origin of `(0,0)`.

<!-- **Example** -->
``` C++	
float x = ArcTan(1,1); // x = -0.7853
```
