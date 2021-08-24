# Link Functions and Variables

class Link
:	<!-- - -->

<!-- //Unimplemented? Invincibility: LINKINVINC<> -->

## Player XYZ Position Variables

### Link->X

int X
:	* ZASM Instruction: `LINKX`

The player's X position on the screen, in pixels. Float values passed to this will be truncated to ints.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Y

int Y
:	* ZASM Instruction: `LINKY`

The player's Y position on the screen, in pixels. Float values passed to this will be truncated to ints.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Z

int Z
:	* ZASM Instruction: `LINKZ`

The player's Z position on the screen, in pixels. Float values passed to this will be truncated to ints.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Link Status Variables

### Link->Invisible

bool Invisible
:	* ZASM Instruction: `LINKINVIS`

Whether the player is currently being draw to the screen. Set this to `true` to remove the player's visibility, `false` to make the player visible.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->CollDetection

bool CollDetection
:	* ZASM Instruction: `LINKINVINC`

If `true`, the player's collision detection with npcs and eweapons is currently turned on. If `false`, engine collision is disabled.

This variable works on a different system to clocks and the level 4 cheat, so it will not necessarily return true if they are set.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Jump

int Jump
:	* ZASM Instruction: `LINKJUMP`

The player's upward velocity, in pixels. If negative, the player will fall.

The downward acceleration of gravity (in Init Data) modifies this value every frame. <!-- Zoria wrote that this value is intended to be in pixels, but appears to be in tiles. This might be a bug that was fixed? -->

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->SwordJinx

int SwordJinx
:	* ZASM Instruction: `LINKSWORDJINX`

The time, in frames, until the player regains use of their sword. -1 signifies a permanent loss of the sword caused by a Red Bubble.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->ItemJinx

int ItemJinx
:	* ZASM Instruction: `LINKITEMJINX`

The time, in frames, until the player regains use of items. -1 signifies a permanent loss of their items caused by a Red Item Bubble.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Drunk

int Drunk
:	* ZASM Instruction: `LINKDRUNK`

The time, in frames, that the player will be "drunk". If positive, the player's controls are randomly interfered with, causing them to move erratically.

This value is decremented once per frame. As the value of Drunk approaches 0, the intensity of the effect decreases.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Dir

int Dir
:	* ZASM Instruction: `LINKDIR`

The direction the player is facing. Use the `DIR_` constants in **std.zh** to set or compare this variable.

NOTE
:	Even though the player can move diagonally if the quest allows it, their sprite doesn't ever use any of the diagonal directions, which are intended for enemies only.	
	Reading this value occurs after **[Waitdraw()](global.html#waitdraw)**.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->HitDir

int HitDir
:	* ZASM Instruction: `LINKHITDIR`

The direction the player should bounce in when they are hit. This is mostly useful for simulating getting hit by setting `Link->Action` to `LA_GOTHURTLAND`.

This value does nothing is `Link->Action` is not `LA_GOTHURTLAND` or `LA_GOTHURTWATER`. Forcing this value to -1 will prevent player knockback (i.e. from injuries or enemy interactions).

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->HP

int HP
:	* ZASM Instruction: `LINKHP`

The player's current hitpoints measured as 1/16th of a heart.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->MP

int MP
:	* ZASM Instruction: `LINKMP`

The player's current magic points measured as 1/32nd of a magic block.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->MaxHP

int MaxHP
:	* ZASM Instruction: `LINKMAXHP`

The player's current maximum HP measured as 1/16th of a heart.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->MaxMP

int MaxMP
:	* ZASM Instruction: `LINKMAXMP`

The player's current maximum MP measured as 1/32nd of a magic block.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Action

int Action
:	* ZASM Instruction: `LINKACTION<>`

The player's current action. Use the `LA_` constants in **std.zh** to set or compare this value.

This value is read-write, but some actions are undefined in this version of ZC. The following are known to work:

* (TODO) ! nothing listed?????? 

The effect of writing to this field is currently undefined.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->HeldItem

int HeldItem
:	* ZASM Instruction: `LINKHELD<>`

The item that the player will hold over his head if an item's Pickup flags are `IP_PICKUP` or if `Link->Action` == `LA_HOLD*`. Reading or setting this value is undefined if the player is not holding up an item.

Use the `I_` constants in **std.zh** to specify the item, or -1 to show no item.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->LadderX

int LadderX
:	* ZASM Instruction: `LINKLADDERX<>`

The X position of the player's stepladder, or 0 if no ladder is onscreen.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->LadderY

int LadderY
:	* ZASM Instruction: `LINKLADDERY<>`

The Y position of the player's stepladder, or 0 if no ladder is onscreen.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Controller/Input Booleans

### Input Functions

The following Input* boolean values return true if the player is pressing the corresponding button, analog stick, or key. Writing to this variable simulates the press or release of that referenced button, analog stick, or key.

bool InputStart
:	* ZASM Instruction: `INPUTSTART`

bool InputMap
:	* ZASM Instruction: `INPUTMAP`

bool InputUp
:	* ZASM Instruction: `INPUTUP`

bool InputDown
:	* ZASM Instruction: `INPUTDOWN`

bool InputLeft
:	* ZASM Instruction: `INPUTLEFT`

bool InputRight
:	* ZASM Instruction: `INPUTRIGHT`

bool InputA
:	* ZASM Instruction: `INPUTA`

bool InputB
:	* ZASM Instruction: `INPUTB`

bool InputL
:	* ZASM Instruction: `INPUTL`

bool InputR
:	* ZASM Instruction: `INPUTR`

bool InputEx1     
:	* ZASM Instruction: `INPUTEX1`

bool InputEx2     
:	* ZASM Instruction: `INPUTEX2`

bool InputEx3     
:	* ZASM Instruction: `INPUTEX3`

bool InputEx4     
:	* ZASM Instruction: `INPUTEX4`

bool InputAxisUp
:	* ZASM Instruction: `INPUTAXISUP`

bool InputAxisDown
:	* ZASM Instruction: `INPUTAXISDOWN`

bool InputAxisLeft
:	* ZASM Instruction: `INPUTAXISLEFT`

bool InputAxisRight
:	* ZASM Instruction: `INPUTAXISRIGHT`

---

### Press Functions

The following Press\* boolean values return true if the player activated the corresponding button, analog stick, or key **starting this frame**. Writing to this variable simulates the **first** frame of input of that referenced button, analog stick, or key.

bool PressStart
:	* ZASM Instruction: `INPUTPRESSSTART`

bool PressMap
:	* ZASM Instruction: `INPUTPRESSMAP`

bool PressUp
:	* ZASM Instruction: `INPUTPRESSUP`

bool PressDown
:	* ZASM Instruction: `INPUTPRESSDOWN`

bool PressLeft
:	* ZASM Instruction: `INPUTPRESSLEFT`

bool PressRight
:	* ZASM Instruction: `INPUTPRESSRIGHT`

bool PressA
:	* ZASM Instruction: `INPUTPRESSA`

bool PressB
:	* ZASM Instruction: `INPUTPRESSB`

bool PressL
:	* ZASM Instruction: `INPUTPRESSL`

bool PressR
:	* ZASM Instruction: `INPUTPRESSR`

bool PressEx1     
:	* ZASM Instruction: `INPUTPRESSEX1`

bool PressEx2     
:	* ZASM Instruction: `INPUTPRESSEX2`

bool PressEx3     
:	* ZASM Instruction: `INPUTPRESSEX3`

bool PressEx4     
:	* ZASM Instruction: `INPUTPRESSEX4`

bool PressAxisUp
:	* ZASM Instruction: `INPUTPRESSAXISUP`

bool PressAxisDown
:	* ZASM Instruction: `INPUTPRESSAXISDOWN`

bool PressAxisLeft
:	* ZASM Instruction: `INPUTPRESSAXISLEFT`

bool PressAxisRight
:	* ZASM Instruction: `INPUTPRESSAXISRIGHT`

---

### Link->InputMouseX

int InputMouseX
:	* ZASM Instruction: `INPUTMOUSEX`

The mouse's in-game X position. This value is undefined if the mouse pointer is outside the Zelda Classic window.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->InputMouseY

int InputMouseY
:	* ZASM Instruction: `INPUTMOUSEY`

The mouse's in-game Y position. This value is undefined if the mouse pointer is outside the Zelda Classic window.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

