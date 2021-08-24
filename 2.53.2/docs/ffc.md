# FFC Functions and Variables

class ffc
:	* Set Working FFC ID ZASM Instruction: `REFFFC`

The following functions and variables are part of the `ffc` class. All variables are both readable from and writable to unless specified otherwise.

In the scope of an FFC script, these functions are accessible by using the `this` pointer,  
e.g. `this->TileWidth`.

These functions may also be used with a user-defined `ffc` pointer, like so:

	ffc MyFFC; // Initialize our FFC as a variable
	MyFFC = Screen->LoadFFC(10); // Load the 10th FFC on the current screen into the pointer
	
	// Now we can read or modify aspects of the FFC being pointed to.
	int FFCXPosition = MyFFC->X;
	MyFFC->TileWidth = 2;
	
### ffc->Data

int Data
:	* ZASM Instruction: `DATA<d3>`

Returns or sets the combo ID of the FFC being pointed to.

<!-- **Example** -->
``` C
	OldCombo = MyFFC->Data;
	MyFFC->Data = 27;
	// The FFC's combo will change to combo #27 on the combo page
	
```

---

### ffc->Script

int Script
:	* ZASM Instruction: `FFSCRIPT<d3>`

The number of the script assigned to the FFC. This will be automatically set to 0 when the FFC's script exits. A script cannot change the script of the FFC running it; in other words, you cannot write to `this->Script`. 

When an FFC's script is changed, its arguments, `Misc[]` data, and registers will all be set to 0, and it will start running from the beginning. Set **ffc->InitD[]** after setting the script before the script starts running to pass arguments to it.

Setting `->Data` to 0 DOES NOT clear `->Script`, and it is not treated as exiting. To do this, call **[Quit()](global.html#quit)**, or otherwise exit the scope of the `run()` function.

<!-- **Example** -->
``` C
	int OldScriptID = MyFFC->Script;
	MyFFC->Script = 6;
	/// Load and begin running the script in FFC Script slot 6.
	
```

---

### ffc->CSet

int CSet
:	* ZASM Instruction: `FCSET<d3>`

The CSet of the FFC.

<!-- **Example** -->
``` C
	int CurrentCSet = MyFFC->CSet;
	if (CurrentCSet != 4) {
		MyFFC->CSet = 4;
	}
	// Set the CSet of the FFC to 4.
	
```

---

### ffc->Delay

int Delay
:	* ZASM Instruction: `DELAY<d3>`

The FFC's animation delay in frames.

<!-- **Example** -->
``` C
	MyFFC->Delay = 40;
	// Wait 40 frames before animating
	
```

---

### ffc->X

int X
:	* ZASM Instruction: `FX<d3>`

The FFC's X position on the screen.

Values outside the screen boundaries *are* legal. 

<!-- **Example** -->
``` C
	OldXPosition = MyFFC->X;
	MyFFC->X = 113;
	
```

---

### ffc->Y

int Y
:	* ZASM Instruction: `FY<d3>`

The FFC's Y position on the screen.

Values outside the screen boundaries *are* legal. 

<!-- **Example** -->
``` C
	OldYPosition = MyFFC->Y;
	MyFFC->Y = 46;

```

---

### ffc->Vx

int Vx
:	* ZASM Instruction: `XD<d3>`

The FFC's velocity's X-component.

<!-- **Example** -->
``` C
	MyFFC->Vx = 20; // The FFC will move 20 pixels per second rightward.
	MyFFC->Vx = -12; // The FFC will move 12 pixels per second leftward.
	
```

---

### ffc->Vy

int Vy
:	* ZASM Instruction: `YD<d3>`

The FFC's velocity's Y-component.

<!-- **Example** -->
``` C
	MyFFC->Vy = 10; // The FFC will move 10 pixels per second downward.
	MyFFC->Vy = -17; // The FFC will move 17 pixels per second upward.
	
```

---

### ffc->Ax

int Ax
:	* ZASM Instruction: `XD2<d3>`

The FFC's acceleration's X-component.

<!-- **Example** -->
``` C
	MyFFC->Ax = 1.03; // Every frame, the velocity X-component will increase by 1.03.
	
```

---

### ffc->Ay

int Ay
:	* ZASM Instruction: `YD2<d3>`

The FFC's acceleration's Y-component.

<!-- **Example** -->
``` C
	MyFFC->Ay = -0.72; // Every frame, the velocity Y-component will decrease by 0.72.
	
```

---

### ffc->Flags[]

bool Flags[]
:	* ZASM Instruction: `FLAG<d3>`, `FFFLAGSD`

The FFC's set of flags as an array of 11 boolean values.

Use the `FFCF_` constants in **std.zh** as the index to access a particular flag.

<!-- **Example** -->
``` C
	MyFFC->Flags[FFCF_TRANS] = true; // Sets the "Translucent" flag of the FFC to true.
	bool IsChanger = MyFFC->Flags[FFCF_CHANGER]; // Reads the state of the "Is A Changer" flag.
	
```

---

### ffc->TileWidth

int TileWidth
:	* ZASM Instruction: `FFTWIDTH<d3>`, `WIDTH<>`

The number of tile columns composing the FFC, or its visible width. The maximum value is `4`.

<!-- **Example** -->
``` C
	MyFFC->TileWidth = 2; // Sets the tile columns for the FFC to 2.
	
```

---

### ffc->TileHeight

int TileHeight
:	* ZASM Instruction: `FFTHEIGHT<d3>`, `HEIGHT<>`

The number of tile rows composing the FFC, or its visible height. The maximum value is `4`.

<!-- **Example** -->
``` C
	MyFFC->TileHeight = 3; // Sets the tile columns for the FFC to 3.
	
```

---

### ffc->EffectWidth

int EffectWidth
:	* ZASM Instruction: `FFCWIDTH<d3>`

The width (in pixels) of the area of effect of the combo associated with the FFC. This will make combo types such as "Damage(X Heart)" affect larger or smaller areas. The maximum value is `64`.

<!-- **Example** -->
``` C
	MyFFC->EffectWidth = 32; // Sets the area of effect's width to 32 pixels.
	
```

---

### ffc->EffectHeight

int EffectHeight
:	* ZASM Instruction: `FFCHEIGHT<d3>`

The width (in pixels) of the area of effect of the combo associated with the FFC. This will make combo types such as "Damage(X Heart)" affect larger or smaller areas.  The maximum value is `64`.

<!-- **Example** -->
``` C
	MyFFC->EffectHeight = 20; // Sets the area of effect's width to 20 pixels.
	
```

---

### ffc->Link

int Link
:	* ZASM Instruction: `FFLINK<d3>`, `LINK<>`

The number of the FFC linked to by this FFC. Has nothing to do with the `Link` player class.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### ffc->InitD[]

float InitD[8]
:	* ZASM Instruction: `FFINITD<>`, `FFINITDD<>?`, `D<>`

The original values of the FFC's 8 D input values as they are stored in the .qst file, regardless of whether they have been modified by ZScript.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### ffc->Misc[]

float Misc[16]
:	* ZASM Instruction: `FFMISC`, `FFMISCD`

An array of 16 miscellaneous variables for you to use as you please. These variables are not saved with the FFC.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !
