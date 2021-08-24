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

## Status Variables

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

!!! note
	Even though the player can move diagonally if the quest allows it, their sprite doesn't ever use any of the diagonal directions, which are intended for enemies only.
	
!!! note
	Reading this value occurs after **[Waitdraw()](global.html#waitdraw)**.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->HitDir

int HitDir
:	* ZASM Instruction: `LINKHITDIR`

The direction the player should bounce in when they are hit. This is mostly useful for simulating getting hit by setting `Link->Action` to `LA_GOTHURTLAND`.

This value does nothing if `Link->Action` is not `LA_GOTHURTLAND` or `LA_GOTHURTWATER`. Forcing this value to -1 will prevent player knockback (i.e. from injuries or enemy interactions).

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## HP/MP Variables

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

## Action Variables

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

## Input Variables

### Link->Input* Booleans

!!! hint
	The following Input\* boolean values return true if the player is pressing the corresponding button, analog stick, or key. Writing to this variable simulates the press or release of that referenced button, analog stick, or key.

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

### Link->Press* Booleans

!!! hint
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

### Link->InputMouseB

int InputMouseB
:	* ZASM Instruction: `INPUTMOUSEB`

Whether the left or right mouse buttons are pressed, as two flags OR'd (`|`) together;  
use the MB_ constants or the `Input*Click` functions in **std.zh** to check the button states.

!!! note
	`InputMouseB` is read-only; while setting it is not syntactically incorrect, it does nothing.

!!! hint
	If you are not comfortable with binary, you can use the `InputMouse*` functions in **std.zh**.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->InputMouseZ

int InputMouseZ
:	* ZASM Instruction: `INPUTMOUSEB` (TODO) ! the readme claims it's 'INPUTMOUSEB'. inspect this. i'm guessing it's 'INPUTMOUSEZ'

The current state of the mouse's scroll wheel; negative for scrolling down and positive for scrolling up. (TODO) ! this could use more explanation

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Inventory Variables

### Link->Item[]

bool Item[256]
:	* ZASM Instruction: `LINKITEMD`

True if the player's inventory contains the item whose ID is the index of the array access. Use the `I_` constants in **std.zh** as an index into this array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Equipment

int Equipment
:	* ZASM Instruction: `LINKEQUIP`

Contains the item IDs of the items currently equipped to the player's A and B buttons. The first 8 bits contain the A button item, and the second 8 bits contain the B button item.

!!! note
	The ability to write to this function was introduced in ZC version 2.53.0c. (TODO) ! Update nomenclature if necessary

!!! hint
	If you are not comfortable with performing binary operations, you can use the functions `GetEquipmentA()`, `GetEquipmentB()`, and `SetEquipment(int a, int b)` in **std.zh**.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !
	
---

## Graphical Variables

### Link->Tile

int Tile
:	* ZASM Instruction: `LINKTILE`

The current tile associated with the player. The effect of writing to this variable is undefined.

!!! caution
	Because the player's tile is not determined until they are drawn, this will actually represent the player's tile in the **previous** frame.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Flip

int Flip
:	* ZASM Instruction: `LINKFLIP`

The current tile flip state associated with the player. The effect of writing to this variable is undefined. (TODO) ! Actually... document the way tile flips work in practice. Is it DIR_?

!!! caution
	Because the player's tile is not determined until they are drawn, this will actually represent the player's tile flip in the **previous** frame.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

<!-- 

---

### Link->Extend

        ZASM Instruction:
          n/a

/**
* This value is NOT set by script. There is no instruction for it; however in the sprites editor
* (Menu: Quest->Graphics->Sprites->Link ) it is possibly to modify the Extend value of link. 
* To do this, click on his sprites for any given action, and preee the 'x' key.
* The options are 16x16, 16x32, and 32x32; which correspond to Extend values of ( ?, ?, and ? ) respectively. 
*/ 


---

## Hitbox Variables

### Link->HitHeight

int HitHeight
:	* ZASM Instruction: `LINKHYSZ`

The player's Hitbox height in pixels.

!!! note
	As of 2.53.1, this value is read-only; while setting it is not syntactically incorrect, it does nothing.


---

### Link->HitWidth

int HitHeight
:	* ZASM Instruction: `LINKHXSZ`

The player's Hitbox width in pixels.

!!! note
	As of 2.53.1, this value is read-only; while setting it is not syntactically incorrect, it does nothing.


---

### Link->TileHeight

int TileHeight
:	* ZASM Instruction: `LINKTXSZ`

The player's height in tiles.

!!! note
	As of 2.53.1, this value is read-only; while setting it is not syntactically incorrect, it does nothing.


---

### Link->TileWidth

int TileWidth
:	* ZASM Instruction: `LINKTYSZ`

The player's width in tiles.


!!! note
	As of 2.53.1, this value is read-only; while setting it is not syntactically incorrect, it does nothing.

int HitZHeight;       ZASM Instruction: 
          LINKHZSZ
        
/**
* The Z-axis height of Link's hitbox, or collision rectangle.
* The lower it is, the lower a flying or jumping enemy must fly in order to hit Link.
* The values of DrawZOffset and HitZHeight are linked. Setting one, also sets the other. 
* Writing to this is ignored unless Extend is set to values >=3.
* This is not usable, as Link->Extend cannot be set.
* While setting it is not syntactically incorrect, it does nothing.
* You can read a value that you assign to this (e.g. for custom collision functions).
* This value is not preserved through sessions: Loading a saved game will reset it to the default. 
*
*/ Example Use: !#!
  
/************************************************************************************************************/

--- -->

---

### Link->HitXOffset

int HitXOffset
:	* ZASM Instruction: `LINKHXOFS`

The X offset of the player's hitbox, or collision rectangle. Setting it to positive or negative values will move the player's hitbox left or right.

!!! note
	This value is not preserved through sessions: Loading a saved game will reset it to the default. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->HitYOffset

int HitYOffset
:	* ZASM Instruction: `LINKHYOFS`

The Y offset of the player's hitbox, or collision rectangle. Setting it to positive or negative values will move the player's hitbox up or down.

!!! note
	This value is not preserved through sessions: Loading a saved game will reset it to the default. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->DrawXOffset

int DrawXOffset
:	* ZASM Instruction: `LINKXOFS`

The X offset of the player's sprite. Setting it to positive or negative values will move the sprite's tiles left or right relative to its position.

!!! note
	This value is not preserved through sessions: Loading a saved game will reset it to the default. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->DrawYOffset

int DrawYOffset
:	* ZASM Instruction: `LINKYOFS`

The Y offset of the player's sprite. Setting it to positive or negative values will move the sprite's tiles up or down relative to its position.

!!! note
	This value is not preserved through sessions: Loading a saved game will reset it to the default. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->DrawZOffset

int DrawZOffset
:	* ZASM Instruction: `LINKZOFS`

The Z offset of the player's sprite.

!!! note
	This value is not preserved through sessions: Loading a saved game will reset it to the default. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Miscellaneous Link Functions and Variables

### Link->Misc[]

float Misc[]
:	* ZASM Instruction: `LINKMISC`, `LINKMISCD`

An array of 16 miscellaneous variables for you to use as you please.  
These variables are not saved when you save the game.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->Warp()

void Warp(int DMap, int screen)
:	* ZASM Instruction: `WARP`, `WARPR`

Warps the player to the given screen in the given DMap, just like if they'd triggered an 'Insta-Warp'-type warp. Uses Warp Return square A. (TODO) ! verify this?

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->PitWarp()

void PitWarp(int DMap, int screen)
:	* ZASM Instruction: `PITWARP`, `PITWARPR`

This is identical to Warp, but the player's X and Y positions are preserved when they enter the destination screen, rather than being set to the Warp Return square.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->SelectAWeapon()

void SelectAWeapon(int dir)
:	* ZASM Instruction: ` `

Sets the A button item to the next one in the given direction based on the indices set in the subscreen. This will skip over items if A and B would be set to the same item. (TODO) ! is the given direction a DIR_ constant?

If the quest rule "Can Select A-Button Weapon On Subscreen" is disabled, this function does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Link->SelectBWeapon()

void SelectBWeapon(int dir)
:	* ZASM Instruction: ` `

Sets the B button item to the next one in the given direction based on the indices set in the subscreen. This will skip over items if A and B would be set to the same item. (TODO) ! is the given direction a DIR_ constant?

<!-- **Example** -->
!!! error "TODO"
	(TODO) !