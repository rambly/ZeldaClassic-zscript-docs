# Global Functions

## General Functions

### Waitdraw()

void Waitdraw()
:	* ZASM Instruction: `WAITDRAW`

Halts execution of the script until ZC's internal code has been run (movement, collision detection, etc.), but before the screen is drawn. This can only be used in the active global script. `Waitdraw()` should only be called from the global active script, not from FFC scripts.

The sequence of ZC draw actions is as follows:

1. FFCs (in numerical sequence, from FFC 01, to FFC 32)
2. Enemies
3. EWeapons
4. Link
5. LWeapons
6. Hookshot
7. Collision Checking
8. Store Link->Input / Link->Press
9. Waitdraw()
10. Drawing
11. Rendering of the Screen
12. Screen Scrolling
13. Drawing from FFCs

!!! note
	Drawing from FFCs technically occurs with other Drawing, but as it is issued after `Waitdraw()`, it is offset (a frame late) and renders after screen scrolling, and after any other drawing in the same frame as draw instructions from FFCs are called. To ensure that drawing done by FFCs is in sync with other drawing, it is imperative to call it from your global script, using the FFC to trigger global conditions that cause global drawing instructions that are called before `Waitdraw()` in your global active script to evaluate true. 

	Anything placed after `Waitdraw()` will not present graphical effects until the next frame.  It is possible to read/store `Link->Tile`, `Link->Dir` and other variables *after* `Waitdraw()` in one frame, and then use these values to modify other pointer members so that they are drawn correctly at the next execution of `Waitdraw()`.


!!! important "Waitdraw() in FFC and item scripts"
	As of 2.53.2, calling `Waitdraw()` in an FFC script or an item script is not allowed or advised. It will throw an error in the compiler and may result in unexpected behavior.
	
---

### Waitframe()

void Waitframe()
:	* ZASM Instruction: `WAITFRAME`

Temporarily halts execution of the current script. This function returns at the beginning of the next frame of gameplay.

!!! note
	Calling Waitframe() in an item script is currently effectively identical to calling `Quit()`. This behaviour may change in future versions of ZC, and using Waitframe() in an item script is not advised. The same is true for global scripts in the `Init`, `onExit`, and `onContinue` slots.

	It is safe to call `Waitframe()` in the active global script. Unlike with `Waitdraw()`, it is also safe to call `Waitframe()` in FFC scripts.

	A `Waitframe()` is required in all infinite loops (like `while (true)`) so that ZC may pause to break in order to advance to the next frame, then resume the loop from the start. Without a `Waitframe()` instruction, any infinite loops will cause the game to hang.

<!-- **Example** -->
``` C
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
``` C
DoSomeStuff(); // This command will run.
Quit(); 
DoSomeMoreStuff(); // This command and any subsequent commands will not run.
```

---

## Tile Modifying Functions

### CopyTile()

void CopyTile(int srctile, int desttile)
:	* ZASM Instruction: `COPYTILERR d2,d3`, `COPYTILEVV`, `COPYTILERV`, `COPYTILEVR`

Copies the tile specified by scrtile onto the tile space specified by desttile. The valid tile value range is **0** to **65519**. This change is temporary within the quest file and will not be retained when saving the game.

!!! tip
	`CopyTile()` may be used to change Link's tile, by copying a tile onto whatever tile ZC is using as a source for `Link->Tile`. Thus, although you cannot write directly to `Link->Tile`, you can write to the actual tile that is being used for this Link attribute, and you can do this for any other game graphic that you need to change.

	When doing this, it is important to read `Link->Dir` or `Link->Flip` **after** `Waitdraw()`, then perform the `CopyTile()` operation immediately thereafter.

<!-- **Example** -->
``` C
CopyTile(312,11614);
// This will copy tile 314 to tilespace 11614. These tiles will then be identical.
```

---
	
### SwapTile()

void SwapTile(int firsttile, int secondtile)
:	* ZASM Instruction: `SWAPTILERR d2,d3`, `SWAPTILEVV`, `SWAPTILERV`, `SWAPTILEVR`

Swaps the two tiles specified by `firsttile` and `secondtile`. The valid tile value range is **0** to **65519**. This change is temporary within the quest file and will not be retained when saving the game.

<!-- **Example** -->  
``` C
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

You may trace `int` and `float` types with `Trace()`. To trace boolean values, see **[TraceB()](#traceb)** below. `int` values are not truncated when printed, and will always have three zeroes after the decimal point.

Values printed to allegro.log do not, by default, incorporate any whitespace or line breaks. You must manually add these. To add new lines, see **[TraceNL()](#tracenl)** below.

<!-- **Example** -->
``` C	
int xyz = 4;
Trace(xyz);
// Prints 4.000 to allegro.log.
```

---

### TraceB()

void TraceB(bool state)
:	* ZASM Instruction: `TRACE2R d3`, `TRACE2V`

Prints a boolean state to allegro.log (and the debug console). Similar to `Trace()`, above, except it outputs `true` or `false` as text.

<!-- **Example** -->
``` C	
bool test = true;
TraceB(test);
// Prints "true" to allegro.log.
```

---

### ClearTrace()

void ClearTrace()
:	* ZASM Instruction: `TRACE4`

Clears allegro.log of all current traces and messages from Zelda Classic/ZQuest. Works on a per-quest, per-session basis. Values recorded from previous sessions are not erased.

---

### TraceNL()

void TraceNL()
:	* ZASM Instruction: `TRACE5`

Traces a newline to allegro.log
This inserts a line break/carriage return (as if pressing return/enter) into allegro.log and is useful for providing formatting to debugging.

---

### TraceS()

void TraceS(int s[])
:	* ZASM Instruction: `TRACE6 d3`

Works as Trace() above, but prints a full string to allegro.log, using the array pointer `s` as its argument.

Maximum 512 characters. Functions from string.zh can be used to split larger strings.

<!-- **Example** -->
``` C	
int testString[] = "This is a string.";
TraceS(testString);
// Prints 'This is a string.' to allegro.log.
```

---

## Array Functions

### SizeOfArray()

int SizeOfArray(int array[])

:	* ZASM Instruction: `ARRAYSIZE d2`

Returns the index size of the array pointed by `array`. Works only on `int` and `float` type arrays. Boolean arrays are not supported. Useful in `for` loops. 

<!-- **Example** -->
``` C	
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

**NOTE**
:	The paramater `n` is an integer, and any floating point (ZScript float) value passed to it will be truncated (floored) to the nearest integer. `Rand(3.75)` is identical to `Rand(3)`.

<!-- **Example** -->
``` C	
// Roll a six-sided die
int DiceThrow;
DiceThrow = rand(1,6);
```

---

### Max()

float Max(float a, float b)
:	* ZASM Instruction: `MAXR<><>`, `MAXV<><>`

Returns the greater of `a` and `b`.

<!-- **Example** -->
``` C
int GetBigger;
GetBigger = max(5.1, 20.5); // Returns 20.5
```

---
	
### Min()

float Min(float a, float b)
:	* ZASM Instruction: `MINR<><>`, `MINV<><>`

Returns the lesser of `a` and `b`.

<!-- **Example** -->
``` C
int GetLesser;
GetLesser = min(5.1, 20.5); // Returns 5.1
```

---
	
### Pow()

int Pow(int base, int exp)
:	* ZASM Instruction: `POWERR<><>`, `POWERV<><>`

Returns `base ^ exp`. The return value is undefined for `base = exp = 0`. Note also negative values of `exp` may not be useful, as the return value is truncated to the nearest integer.

<!-- **Example** -->
!!! error "Todo"
	(TODO) !

---

### InvPow()

int InvPow(int base, int exp)
:	* ZASM Instruction: `IPOWERR<><>`, `IPOWERV<><>`

Returns `base ^ (1 / exp)`. The return value is undefined for `exp = 0`, or if `exp` is even and base is negative. Note also that negative values of `exp` may not be useful, as the return value is truncated to the nearest integer.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---
	
### Log10()

float Log10(float val)
:	* ZASM Instruction: `LOG10<>`

Returns the log of val to the base 10. Any value <= 0 will return 0.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Ln()

float Ln(float val)
:	* ZASM Instruction: `LOGE<>`

Returns the natural logarithm of val (to the base e). Any value <= 0 will return 0.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Factorial()

int Factorial(int val)
:	* ZASM Instruction: `FACTORIAL<>`

Returns val!. val < 0 returns 0.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Abs()

float Abs(float val)
:	* ZASM Instruction: `ABS<>`

Return the absolute value of the parameter, if possible. If the absolute value would overflow the parameter, the return value is undefined.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Sqrt()

float Sqrt(float val)
:	* ZASM Instruction: `SQROOTV<><>`, `SQROOTR<><>`

Computes the square root of the parameter. The return value is undefined for val < 0.

**NOTE**
:	Passing negative values to Sqrt() will return an error. See SafeSqrt() in std.zh

<!-- **Example** -->
``` C
int x = Sqrt(16); // x = 4
```

---
	
## Trigonometric Functions

### Sin()

float Sin(float deg)
:	* ZASM Instruction: `SINR<><> d2,d3`, `SINV<><>`

Returns the trigonometric sine of the parameter, which is interpreted as a degree value.

<!-- **Example** -->
``` C	
float x = Sin(32); // x = 0.5299
```

---

### Cos()

float Cos(float deg)
:	* ZASM Instruction: `COSR<><> d2,d3`, `COSV<><>`

Returns the trigonometric cosine of the parameter, which is interpreted as a degree value.

<!-- **Example** -->
``` C	
float x = Cos(40); // x = 0.7660
```

---

### Tan()

float Tan(float deg)
:	* ZASM Instruction: `TANR<><> d2,d3`, `TANV<><>`

Returns the trigonometric tangent of the parameter, which is interpreted as a degree value. The return value is undefined if `deg` is of the form `90 + 180n` for an integral value of `n`.

<!-- **Example** -->
``` C	
float x = Tan(100); // x = -5.6712
```

---
	
### RadianSin()

float RadianSin(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric sine of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### RadianCos()

float RadianCos(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric cosine of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### RadianTan()

float RadianTan(float rad)
:	* ZASM Instruction: ` `

Returns the trigonometric tangent of the parameter, which is interpreted as a radian value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---
	
### ArcTan()

float ArcTan(int x, int y)
:	* ZASM Instruction: `ARCTANR<>`

Returns the trigonometric arctangent of the coordinates, which is interpreted as a radian value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### ArcSin()

float ArcSin(float x)
:	* ZASM Instruction: `ARCSINR<><>`

Returns the trigonometric arcsine of `x`, which is interpreted as a radian value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---
	
### ArcCos()

float ArcCos(float x)
:	* ZASM Instruction: `ARCCOSR<><>`, `ARCCOSV<><>`

Returns the trigonometric arccosine of `x`, which is interpreted as a radian value.

<!-- **Example** -->

	(TODO) !