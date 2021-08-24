# Screen Functions and Variables

class Screen
:	<!-- - -->

## Screen Data Functions

### Screen->D[]

float D[]
:	* ZASM Instruction: `SD`, `SDD`

Each screen has 8 general purpose registers for use by script programmers. These values are recorded in the save file when the player saves their game. Do with these as you will.

Note that these registers are tied to screen/DMap combinations. Encountering the same screen in a different DMap will result in a different `D[]` array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Flags[]

int Flags[]
:	* ZASM Instruction: `SCREENFLAGSD`, `SCREENFLAGS`

An array of ten integers containing the states of the flags in the 10 categories on the Screen Data tabs 1 and 2. Each flag is ORed into the `Flags[x]` value, starting with the top flag as the smallest bit.

Use the `SF_` constants in std.zh as the array access for this value, and the `GetScreenFlags()` function if you are not comfortable with binary.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->EFlags[]

int EFlags[]
:	* ZASM Instruction: `SCREENEFLAGSD`, `SCREENEFLAGS`

An array of 3 integers containing the states of the flags in the E.Flags tab of the Screen Data dialog. Each flag is ORed into the `EFlags[x]` value, starting with the top flag as the smallest bit.

Use the `SEF_` constants in std.zh as the array access for this value, and the `GetScreenEFlags()` function if you are not comfortable with binary.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Screen Combo Functions

### Screen->ComboD[]

int ComboD[]
:	* ZASM Instruction: `CD###`, `COMBOD`, `COMBODD`, `COMBODDM`, `COMBOSD`

The combo ID of the `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ComboC[]

int ComboC[]
:	* ZASM Instruction: `CC###`, `COMBOC`, `COMBOCD`, `COMBOCDM`

The CSet of the tile used by the `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ComboF[]

int ComboF[]
:	* ZASM Instruction: `CF###`, `COMBOF`, `COMBOFD`, `COMBOFDM`

The placed flag of `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high.

Use the `CF_` constants in std.zh to set or compare these values.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ComboI[]

int ComboI[]
:	* ZASM Instruction: `CI###`, `COMBOID`, `COMBOIDM`

The inherent flag of `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high.

Use the `CF_` constants in std.zh to set or compare these values.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ComboT[]

int ComboT[]
:	* ZASM Instruction: `CT###`, `COMBOTD`, `COMBOTDM`

The combo type of `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high.

Use the `CT_` constants in std.zh to set or compare these values.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ComboS[]

int ComboS[]
:	* ZASM Instruction: `CS###`, `COMBOSD`, `COMBOSDM`

The walkability mask of `i`th combo on the screen, where `i` is the index used to access this array. Combos are counted left to right, top to bottom. Screen dimensions are 16 combos wide by 11 combos high.

This array contains binary values. The least signficant bit is true if the top-left of the combo is solid, the second-least signficant bit is true if the bottom-left of the combo is is solid, the third-least significant bit is true if the top-right of the combo is solid, and the fourth-least significant bit is true if the bottom-right of the combo is solid.

To help visualize, if we take a binary number `0000` and represent the 4 digits as `1234`, then each digit represents the following corners of a combo:

	4 2
	3 1

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->MovingBlockX

int MovingBlockX
:	* ZASM Instruction: `PUSHBLOCKX`

The X position of the current moving block. If there is no moving block on the screen, it will be -1.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->MovingBlockY

int MovingBlockY
:	* ZASM Instruction: `PUSHBLOCKY`

The Y position of the current moving block. If there is no moving block on the screen, it will be -1.

This is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->MovingBlockCombo

int MovingBlockCombo
:	* ZASM Instruction: `PUSHBLOCKCOMBO`

The combo of the current moving block. If there is no moving block on the screen, the value is undefined.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->MovingBlockCSet

int MovingBlockCSet
:	* ZASM Instruction: `PUSHBLOCKCSET`

The CSet used by the current moving block. If there is no moving block on the screen, the value is undefined.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Screen State Functions
	
### Screen->UnderCombo

int UnderCombo
:	* ZASM Instruction: `UNDERCOMBO`

The current screen's under combo.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->UnderCSet

int UnderCSet
:	* ZASM Instruction: `UNDERCSET`

The current screen's under CSet.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->State[]

int State[]
:	* ZASM Instruction: `SCREENSTATED`

An array of miscellaneous status data associated with the current screen.
Screen states involve such things as permanent screen secrets, the status of lock blocks and treasure chest combos, and whether items have been collected.
These values are recorded in the save file when the player saves their game. Use the `ST_` constants in std.zh as indices into this array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Door[]

int Door[]
:	* ZASM Instruction: `SCRDOORD`, `SCRDOOR`

The door type for each of the four doors on a screen. Doors are counted using the first four `DIR_` constants in std.zh. Use the `D_` constants in std.zh to compare these values.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->RoomType

int RoomType
:	* ZASM Instruction: `ROOMTYPE`

The room type of the current screen (Special Item, Bomb Upgrade, et al.)

Use the `RT_` constants in std.zh to compare this value.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->RoomData

int RoomData
:	* ZASM Instruction: `ROOMDATA`

This is the data associated with the room type above. What it means depends on the room type. For Special Item, it will be the item ID, for a Shop, it will be the Shop Number, etc. Basically, this is what's in the "Catch-all" menu item underneath Room Type.

If the room type has no data (eg, Ganon's room), this will be undefined.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->TriggerSecrets()

void TriggerSecrets()
:	* ZASM Instruction: ` `

Triggers screen secrets temporarily. Set `Screen->State[ST_SECRET]` to `true` beforehand or afterward if you would like them to remain permanent.

<!-- **Example** -->

---

### Screen->Lit

bool Lit
:	* ZASM Instruction: `LIT`

Whether or not the screen is lit. Setting this variable will change the lighting setting of the screen until you change screens.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Wavy

int Wavy
:	* ZASM Instruction: `WAVY`

The time, in frames, that the 'wave' screen effect will be in effect. This value is decremented once per frame. As the value of Wavy approaches 0, the intensity of the waves decreases.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Quake

int Quake
:	* ZASM Instruction: `QUAKE`

The time, in frames, that the screen will shake. This value is decremented once per frame. As the value of Quake approaches 0, the intensity of the screen shaking decreases.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !
	
## Warp Data Functions

---

### Screen->SetSideWarp()

void SetSideWarp(int warp, int screen, int dmap, int type)
:	* ZASM Instruction: `SETSIDEWARP`

Sets the current screen's side warp 'warp' to the destination screen, DMap and type. If any of the parameters screen, dmap or type are equal to -1, they will remain unchanged. If `warp` is not between 0 and 3, the function does nothing.

The side warp directions match the `DIR_` contants in std.zh.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->SetTileWarp()

void SetTileWarp(int warp, int screen, int dmap, int type)
:	* ZASM Instruction: `SETTILEWARP`

Sets the current screen's tile warp `warp` to the destination screen, DMap and type. If any of the parameters `screen`, `dmap` or `type` are equal to -1, they will remain unchanged. If `warp` is not between 0 and 3, the function does nothing.

Warp tiles A, B, C, and D are 0, 1, 2, and 3 respectively.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetSideWarpDMap()

int GetSideWarpDMap(int warp)
:	* ZASM Instruction: `GETSIDEWARPDMAP`

Returns the destination DMap of the given side warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

The side warp directions match the `DIR_` contants in std.zh.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetSideWarpScreen()

int GetSideWarpScreen(int warp)
:	* ZASM Instruction: `GETSIDEWARPSCR`

Returns the destination screen of the given side warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

The side warp directions match the `DIR_` contants in std.zh.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetSideWarpType()

int GetSideWarpType(int warp)
:	* ZASM Instruction: `GETSIDEWARPTYPE`

Returns the warp type of the given side warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

The side warp directions match the `DIR_` contants in std.zh.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetTileWarpDMap()

int GetTileWarpDMap(int warp)
:	* ZASM Instruction: `GETTILEWARPDMAP`

Returns the destination DMap of the given tile warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

Warp tiles A, B, C, and D are 0, 1, 2, and 3 respectively.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetTileWarpScreen()

int GetTileWarpScreen(int warp)
:	* ZASM Instruction: `GETTILEWARPDSCR`

Returns the destination screen of the given tile warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

Warp tiles A, B, C, and D are 0, 1, 2, and 3 respectively.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetTileWarpType()

int GetTileWarpType(int warp)
:	* ZASM Instruction: `GETTILEWARPTYPE`

Returns the warp type of the given tile warp on the current screen. Returns -1 if `warp` is not between 0 and 3.

Warp tiles A, B, C, and D are 0, 1, 2, and 3 respectively.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Layer Data Functions

### Screen->LayerMap()

int LayerMap(int n)
:	* ZASM Instruction: `LAYERMAP`

Returns the map of the screen currently being used as the `n`th layer. Values of `n` less than 1 or greater than 6, or layers that are not set up, returns -1.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LayerScreen()

int LayerScreen(int n)
:	* ZASM Instruction: `LAYERSCREEN`

Returns the number of the screen currently being used as the `n`th layer. Values of `n` less than 1 or greater than 6, or layers that are not set up, returns -1.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Object Functions
	
### Screen->NumItems()

int NumItems()
:	* ZASM Instruction: `ITEMCOUNT`

Returns the number of items currently present on the screen. Screen items, shop items, and items dropped by enemies are counted; Link's weapons, such as lit bombs, or enemy weapons are not counted.

Note that this value is only correct up until the next call to `Waitframe()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LoadItem()

item LoadItem(int num)
:	* ZASM Instruction: `LOADITEMR`, `LOADITEMV`

Returns a pointer to the `num`th item on the current screen. The return value is undefined unless `1 <= num <= NumItems()`.

Attempting to return an invalid item pointer will print an error to allegro.log. 

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->CreateItem()

item CreateItem(int id)
:	* ZASM Instruction: `CREATEITEMV`, `CREATEITEMR`

(TODO) !

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LoadFFC()

item LoadFFC(int num)
:	* ZASM Instruction: `GETFFCSCRIPT`

Returns a pointer to the `num`th FFC on the current screen. The return value is undefined unless `1 <= num <= ffcs`, where `ffcs` is the number of FFCs active on the screen.

Note that FFCs don't need to be created, per se. All 32 FFCs on a screen technically always exist, albeit with "blank" initial values if they aren't otherwise set. To "create" an FFC, all you have to do is load a slot and fill out the parameters you want.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->NumNPCs()

int NumNPCs()
:	* ZASM Instruction: `NPCCOUNT`

Returns the number of NPCs (enemies and guys) on the screen. Note that this value is only correct up until the next call to `Waitframe()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LoadNPC()

npc LoadNPC(int num)
:	* ZASM Instruction: `LOADNPCR`, `LOADNPCV`

Returns a pointer to the `num`th NPC on the current screen. The return value is undefined unless `1 <= num <= NumNPCs()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->CreateNPC()

npc CreateNPC(int id)
:	* ZASM Instruction: `CREATENPCR`, `CREATENPCV`

Creates an npc of the given type at `(0,0)`. Use the `NPC_` constants in std.zh to pass into this method. The return value is a pointer to the new NPC.

The maximum number of NPCs on any given screen is 255. ZC will report an error to allegro.log if you try to create NPCs after reaching that maximum.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->NumLWeapons()

int NumLWeapons()
:	* ZASM Instruction: `LWPNCOUNT`

Returns the number of Link weapon projectiles currently present on the screen. This includes things like Link's arrows, bombs, magic, etc. Note that this value is only correct up until the next call of `Waitframe()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LoadLWeapon()

lweapon LoadLWeapon(int num)
:	* ZASM Instruction: `LOADLWEAPONR`, `LOADLWEAPONV`

Returns a pointer to the `num`th lweapon on the current screen. The return value is undefined unless `1 <= num <= NumLWeapons()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->CreateLWeapon()

lweapon CreateLWeapon(int num)
:	* ZASM Instruction: `CREATELWEAPONR`, `CREATELWEAPONV`

Creates an lweapon of the given type at `(0,0)`. Use the `LW_` constants in std.zh to pass into this method. The return value is a pointer to the new lweapon.

The maximum number of lweapons on any given screen is 255. ZC will **NOT** report an error to allegro.log if you try to create lweapons after reaching that maximum. The maximum instances for lweapons and eweapons are independent.

This cap is for *all* lweapons of any type. Mixing types will not increase this cap.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->NumEWeapons()

int NumEWeapons()
:	* ZASM Instruction: `EWPNCOUNT`

Returns the number of Enemy weapon projectiles currently present on the screen. This includes things like Enemy arrows, bombs, magic, etc. Note that this value is only correct up until the next call of `Waitframe()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->LoadEWeapon()

lweapon LoadEWeapon(int num)
:	* ZASM Instruction: `LOADEWEAPONR`, `LOADEWEAPONV`

Returns a pointer to the `num`th eweapon on the current screen. The return value is undefined unless `1 <= num <= NumEWeapons()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->CreateEWeapon()

eweapon CreateEWeapon(int num)
:	* ZASM Instruction: `CREATEEWEAPONR`, `CREATEEWEAPONV`

Creates an eweapon of the given type at `(0,0)`. Use the `EW_` constants in std.zh to pass into this method. The return value is a pointer to the new eweapon.

The maximum number of eweapons on any given screen is 255. ZC will **NOT** report an error to allegro.log if you try to create eweapons after reaching that maximum. The maximum instances for eweapons, and eweapons are independent.

This cap is for *all* eweapons of any type. Mixing types will not increase this cap.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !
	
## Misc. Screen Functions

---

### Screen->IsSolid()

bool IsSolid(int x, int y)
:	* ZASM Instruction: `ISSOLID`

Returns true if the screen position `(x, y)` is solid&mdash;that is, if it is within the solid portion of a combo on layers 0, 1 or 2. If either `x` or `y` exceed the screen's bounds, then it will return false.

It will also return false if the only applicable solid combo is a solid water combo that has recently been 'dried' by the whistle.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->ClearSprites()

void ClearSprites(int spritelist)
:	* ZASM Instruction: `CLEARSPRITESR`, `CLEARSPRITESV`

Clears all of a certain kind of sprite from the screen. Use the `SL_` constants in std.zh to pass into this method.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Message()

void Message(int string)
:	* ZASM Instruction: `MSGSTRR`, `MSGSTRV`

Prints the message `string` with given ID onto the screen. If `string` is 0, the currently displayed message is removed. This method's behavior is undefined if `string` is less than 0 or greater than the total number of messages in the quest.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## 2D Shape Drawing Commands

These commands use the Allegro 4 drawing primitives to render drawn effects directly to a screen.

There are several render targets available&mdash;by default, they draw to `RT_SCREEN`, which is the actual screen within the Zelda Classic window. `RT_BITMAP0` through `RT_BITMAP6` are offscreen bitmaps. These bitmaps do not have specific designated purposes and may be used as you see fit, then re-rendered back to `RT_SCREEN`.

All render targets have eight layers, 0 through 7. If the quest rule "Subscreen Appears Above Sprites" is set, passing the layer argument as 7 will allow drawing on top of the subscreen.

Within the context of the offscreen bitmaps, colour 0 is a translucent colour. If you draw a rectangle then draw a rectangle of colour 0 through that rectangle, it will erase that part of the rectangle. Any transparent area that extends through all layers will be drawn as transparent when rendered back to `RT_SCREEN` if `bool mask` is set to `true`. Drawing colour 0 directly to a screen layer is undefined behaviour.

The maximum number of script drawing instructions per frame is 1000.

**NOTE**
:	For all drawing commands, `color` accesses the entire 256-element palette: for instance, passing in a colour of 17 would use colour 1 of CSet 1. Since all CSets consist of 16 colours, you can simplify this a bit by passing a hexadecimal value as the argument, e.g., `0x11` for CSet 1, colour 1.

	`opacity` controls how transparent the rectangle will be. Values other than `OP_OPAQUE` and `OP_TRANS` are currently undefined. Any integer passed to `opacity` less than the value of `OP_OPAQUE` will render as `OP_TRANS`.

### Screen->Rectangle()

void Rectangle(int layer, int x, int y, int x2, int y2, int color, float scale, int rx, int ry, int rangle, bool fill, int opacity)
:	* ZASM Instruction: `RECTR`, `RECT`

Draws a rectangle on the specified layer of the current screen, using `(x,y)` as the top-left corner and `(x2,y2)` as the bottom-right corner. Then scales the rectangle uniformly about its center by the given factor. Lastly, a rotation, centered about the point `(rx, ry)`, is performed counterclockwise using an angle of `rangle` degrees.

A filled rectangle is drawn if `fill` is true; otherwise, this method draws a wireframe.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Circle()

void Circle(int layer, int x, int y, int radius, int color, float scale, int rx, int ry, int rangle, bool fill, int opacity)
:	* ZASM Instruction: `CIRCLE`, `CIRCLER`

Draws a circle on the specified layer of the current screen with center `(x,y)` and radius `scale*radius`. Then performs a rotation counterclockwise, centered about the point `(rx, ry)`, using an angle of `rangle` degrees.

A filled rectangle is drawn if `fill` is true; otherwise, this method draws a wireframe.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Arc()

void Arc(int layer, int x, int y, int radius, int startangle, int endangle, int color, float scale, int rx, int ry, int rangle, bool closed, bool fill, int opacity)
:	* ZASM Instruction: `ARC`, `ARCR`

Draws an arc of a circle on the specified layer of the current screen. The circle in question has center `(x,y)` and radius `scale*radius`.

The arc beings at `startangle` degrees counterclockwise from standard position, and ends at endangle degress counterclockwise from standard position. The behavior of this function is undefined unless `0 <= endangle-startangle < 360`. The arc is then rotated about the point `(rx, ry)` using an angle of `rangle` radians.

If `closed` is true, a line is drawn from the center of the circle to each endpoint of the arc, forming a sector of the circle. If `fill` is also true, a filled sector is drawn instead.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Ellipse()

void Ellipse(int layer, int x, int y, int xradius, int yradius, int color, float scale, int rx, int ry, int rangle, bool fill, int opacity)
:	* ZASM Instruction: `ELLIPSE2`, `ELLIPSER`

Draws an ellipse on the specified layer of the current screen with center `(x,y)`, x-axis radius `xradius`, and y-axis radius `yradius`. Then performs a rotation counterclockwise, centered about the point `(rx, ry)`, using an angle of rangle degrees.

A filled ellipse is drawn if `fill` is true; otherwise, this method draws a wireframe.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Spline()

void Spline(int layer, int x1, int y1, int x2, int y2, int x3, int y3, int x4, int y4, int color, int opacity)
:	* ZASM Instruction: `SPLINER`, `SPLINE`

Draws a cardinal spline on the specified layer of the current screen between `(x1,y1)` and `(x4,y4)`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Line()

void Line(int layer, int x, int y, int x2, int y2, int color, float scale, int rx, int ry, int rangle, int opacity)
:	* ZASM Instruction: `LINE`, `LINER`

Draws a line on the specified layer of the current screen between `(x,y)` and `(x2,y2)`.
Then scales the line uniformly by a factor of `scale` about the line's midpoint.
Finally, performs a rotation counterclockwise, centered about the point `(rx, ry)`, using an angle of rangle degrees.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->PutPixel()

void PutPixel(int layer, int x, int y, int color, int rx, int ry, int rangle, int opacity)
:	* ZASM Instruction: `PUTPIXEL`, `PUTPIXELR`

Draws a raw pixel on the specified layer of the current screen at `(x,y)`. Then performs a rotation counterclockwise, centered about the point `(rx, ry)`, using an angle of `rangle` degrees.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawTile()

void DrawTile(int layer, int x, int y, int tile, int blockw, int blockh, int cset, int xscale, int yscale, int rx, int ry, int rangle, int flip, bool transparency, int opacity)
:	* ZASM Instruction: `DRAWTILE`, `DRAWTILER`

Draws a block of tiles on the specified layer of the current screen, starting at `(x,y)`, using the specified cset.

Starting with the specified tile, this method copies a block of size `blockh x blockw` from the tile sheet to the screen. This method's behavior is undefined unless `1 <= blockh, blockw <= 20`.

Scale specifies the actual size in pixels! So scale 1 would mean it is only one pixel in size. To use the default sizes of `block w,h` you must set `xscale` and `yscale` to -1. These values are not independent of one another, so you cannot set `xscale` and leave `yscale` at -1.

`rx` and `ry` work just like the other primitives. `rangle` performs a rotation clockwise using an angle of `rangle` degrees.

`flip` specifies how the tiles should be flipped when drawn:

* 0: No flip
* 1: Horizontal flip
* 2: Vertical flip
* 3: Both (180 degree rotation)

If transparency is true, the tiles' transparent regions will be respected.  `opacity` controls the translucency of the solid portions of the tile.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->FastTile()

void FastTile(int layer, int x, int y, int tile, int cset, int opacity)
:	* ZASM Instruction: `FASTTILER`

Optimized and simpler version of `DrawTile()`. Draws a single tile on the current screen much in the same way as **[DrawTile()](#screen-drawtile)**. See **[DrawTile()](#screen-drawtile)**, just above, for an explanation on what these arguments do.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawCombo()

void DrawCombo(int layer, int x, int y, int combo, int w, int h, int cset, int xscale, int yscale, int rx, int ry, int rangle, int flip, bool transparency, int opacity)
:	* ZASM Instruction: `DRAWCOMBO`, `DRAWCOMBOR`

Draws a combo on the specified layer of the current screen, starting at `(x,y)`, using the specified cset.

Starting with the specified tile referenced by the combo, this method copies a block of size `blockh x blockw` from the tile sheet to the screen. This method's behavior is undefined unless `1 <= blockh, blockw <= 20`.

Scale specifies the actual size in pixels! So scale 1 would mean it is only one pixel in size. To use the default sizes of `block w,h` you must set `xscale` and `yscale` to -1. These values are not independant of one another, so you cannot set `xscale` and leave `yscale` at -1.

`rx` and `ry` work just like the other primitives. `rangle` performs a rotation clockwise using an angle of `rangle` degrees.

`flip` specifies how the tiles should be flipped when drawn:

* 0: No flip
* 1: Horizontal flip
* 2: Vertical flip
* 3: Both (180 degree rotation)

If transparency is true, the tiles' transparent regions will be respected.  `opacity` controls the translucency of the solid portions of the tile.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->FastCombo()

void FastCombo(int layer, int x, int y, int combo, int cset, int opacity)
:	* ZASM Instruction: `FASTCOMBOR`

Optimized and simpler version of `DrawCombo()`. Draws a single combo on the current screen much in the same way as `DrawCombo()`. See `DrawCombo()`, just above, for an explanation on what these arguments do.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawCharacter()

void DrawCharacter(int layer, int x, int y, int font, int color, int background_color, 	int width, int height, int glyph, int opacity)
:	* ZASM Instruction: `DRAWCHARR`

Draws a single ASCII character `glyph` on the specified layer of the current screen, using the specified font index (see std.zh for a `FONT_*` list to pass to this method), starting at` (x,y)`, using the specified `color` as the foreground color and `background_color` as the background color. Use `-1` for a transparent background.

The arguments `width` and `height` may be used to draw the glyph of any arbitrary size begining at 1 pixel up to 512 pixels large. (more than four times the size of the screen). Passing 0 or negative values to this will use the font's default width and height.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawInteger()

void DrawInteger(int layer, int x, int y, int font, int color, int background_color, int width, int height, int number, int number_decimal_places, int opacity)
:	* ZASM Instruction: `DRAWINTR`

Draws a ZScript `int` or `float` on the specified layer of the current screen, using the specified font index (see std.zh for a `FONT_*` list to pass to this method), starting at `(x,y)`, using the specified color as the foreground color and `background_color` as the background color. Use `-1` for a transparent background.

The arguments `width` and `height` may be used to draw the number of any arbitrary size begining at 1 pixel up to 512 pixels large. (more than four times the size of the screen). Passing 0 or negative values to this will use the font's default width and height.

The number can be rendered as type `int` or `float` by setting the argument `number_decimal_places`, which is only valid if set to 0 or `<=` 4.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawString()

void DrawInteger(int layer, int x, int y, int font, int color, int background_color, int format, int ptr[], int opacity)
:	* ZASM Instruction: `DRAWSTRINGR`

Prints a NULL terminated string up to 256 characters from an int array containing ASCII data (`*ptr`) on the specified layer of the current screen, using the specified `font` index (see std.zh for a `FONT_*` list to pass to this method),
using the specified color as the foreground color and `background_color` as the background color. Use `-1` for a transparent background.

The array pointer should be passed as the argument for `*ptr`, ie.

	int string[] = "Example String"; 
	Screen->DrawString(l,x,y,f,c,b_c,fo,o,string)
	
`int format` tells the engine how to format the string. (see std.zh for `TF_*` list to pass to this method)

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Pseudo-3D Drawing Commands

When allocating a texture, the size `(h,w)` must be between 1 and 16 and it must be a power of two. 

Thus, legal sizes are `1`, `2`, `4`, `8`, and `16`. This applies to all 3D drawing functions. 
  
To draw one of the rendering shapes with a solid colour, set the args as follows:

* **CSet:** colour to draw
* **Texture:** `-1`
* **Render Mode:** `PT_FLAT`

### Screen->Quad()

void Quad(int layer, int x1, int y1, int x2, int y2, int x3, int y3, int x4, int y4, int w, int h, int cset, int flip, int texture, int render_mode)
:	* ZASM Instruction: `QUADR`

Draws a quad on the specified layer with the corners x1,y1 through x4,y4. Corners are drawn in a counterclockwise order starting from x1,y1. (So, if you draw a "square" for example starting from the bottom-right corner instead of the usual top-left, the the image will be textured onto the quad so it appears upside-down.)

From there a single or block of tiles or combos is then texture mapped onto the quad using the arguments `w`, `h`, `cset`, `flip`, and `render_mode`. A positive value in texture will draw the image from the tilesheet pages, whereas a negative value will be drawn from the combo page. 0 will draw combo number 0.

`flip` specifies how the tiles/combos should be flipped when drawn:

  * 0: No flip
  * 1: Horizontal flip
  * 2: Vertical flip
  * 3: Both (180 degree rotation)

See std.zh for a list of all available `render_mode` arguments.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Triangle()

void Triangle(int layer, int x1, int y1, int x2, int y2, int x3, int y3, int w, int h, int cset, int flip, int texture, int render_mode)
:	* ZASM Instruction: `TRIANGLER`

Draws a triangle on the specified layer with the corners x1,y1 through x4,y4. Corners are drawn in a counterclockwise order starting from x1,y1.

From there a single or block of tiles or combos is then texture mapped onto the triangle using the arguments `w`, `h`, `cset`, `flip`, and `render_mode`. A positive value in texture will draw the image from the tilesheet pages, whereas a negative value will be drawn from the combo page. 0 will draw combo number 0.

`flip` specifies how the tiles/combos should be flipped when drawn:

  * 0: No flip
  * 1: Horizontal flip
  * 2: Vertical flip
  * 3: Both (180 degree rotation)

See std.zh for a list of all available `render_mode` arguments.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Triangle3D()

void Triangle3D(int layer, int pos[9], int uv[6], int csets[3], int size[2], int flip, int tile, int polytype)
:	* ZASM Instruction: `TRIANGLE3DR`

Draws a 3D triangle on the specified layer with the corners `x1,y1` through `x3,y3`.  Corners are drawn in a counterclockwise order starting from `x1,y1`. From there a single or block of tiles or combos is then texture mapped onto the triangle using the arguments `w`, `h`, `cset`, `flip`, and `render_mode`.

The `h` and `w` args are used to set the tile block size for the texture. A positive value in texture will draw the image from the tilesheet pages, whereas a negative value will be drawn from the combo page. 0 will draw combo number 0.  Both `w` and `h` are undefined unless `1 <= blockh, blockw <= 16`, and it is a power of two. ie: `1`, `2` are acceptable, but `2`, `15` are not.

Arguments take the form of array pointers: Thus, you must declare arrays with the values that you wish to use and pass their pointers to each of the following:

 * `[9]pos` - `x`, `y`, `z` positions of the 3 corners.
 * `[6]uv` - `x`, `y` texture coordinates of the given texture.
 * `[3]csets` - of the corners to interpolate between.
 * `[2]size` - `w`, `h`, of the texture. `w` and `h` must be in values of 1, 2, 4, 8, or 16. 

`flip` specifies how the tiles/combos should be flipped when drawn:

  * 0: No flip
  * 1: Horizontal flip
  * 2: Vertical flip
  * 3: Both (180 degree rotation)

See std.zh for a list of all available `render_mode` arguments.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->Quad3D()

void Quad3D(int layer, int pos[], int uv[], int cset[], int size[], int flip, int texture, int render_mode)
:	* ZASM Instruction: `QUAD3DR`

Draws a Quad on the specified layer similar to Quad.

Arguments take the form of array pointers: Thus, you must declare arrays with the values that you wish to use and pass their pointers to each of the following:

 * `[9]pos` - `x`, `y`, `z` positions of the 3 corners.
 * `[6]uv` - `x`, `y` texture coordinates of the given texture.
 * `[3]csets` - of the corners to interpolate between.
 * `[2]size` - `w`, `h`, of the texture. `w` and `h` must be in values of 1, 2, 4, 8, or 16. 

See std.zh for a list of all available `render_mode` arguments.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Bitmap, Screen, and Layer Drawing Commands

### Screen->SetRenderTarget()

void SetRenderTarget(int bitmap_id)
:	* ZASM Instruction: `SETRENDERTARGET`

Sets the target bitmap for all succesive drawing commands. These can be directly to the screen or any one of the available off-screen bitmaps, which are generally categorized as `-1` (screen) or `0 - bitmapNumber` (off-screen).
 
See std.zh for a complete list of valid render targets (`RT_*`).

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->GetRenderTarget()

void GetRenderTarget(int bitmap_id)
:	* ZASM Instruction: `GETRENDERTARGET`

Returns the ID of the current screen render target.

See std.zh for a complete list of valid render targets (`RT_*`).

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawBitmap()

void DrawBitmap(int layer, int bitmap_id, int source_x, int source_y, int source_w, int source_h, int dest_x, int dest_y, int dest_w, int dest_h, float rotation, bool mask)
:	* ZASM Instruction: `BITMAPR`

Copies a section of the offscreen bitmap `bitmap_id` onto an area of the screen (or another bitmap) at the given layer using a set of rectangular coordinates. `source_x`, `source_y`, `source_w`, and `source_h` define the position and size of the rectangle in the bitmap, and `dest_x`, `dest_y`, `dest_w`, `dest_h` define the position and size of the rectangle to draw to.  If the coordinates don't match, the bitmap will be scaled automatically.

The valid range of coordinates on a bitmap are 0 to 511 on either axis (bitmaps are 512x512 pixels in size).

If `rotation` is a non-zero number, it will rotate the bitmap by that number of degrees.

If `mask` is set to true, translucent areas of the bitmap will be cropped out when it's drawn to the destination.

**NOTE**
:	Script drawing functions are enqueued and executed in a frame-by-frame basis based on the order of which layer they need to be drawn to. Drawing to or from seperate render tagets or bitmaps is no exception!

<!-- **Example** -->
``` C
Screen->Bitmap(6, RT_BITMAP1, 0, 0, 16, 16, 79, 57, 32, 32, 0, true)

// Takes a 16x16 section of the 2nd bitmap at coordinates 0,0
// and draws it at coordinates 79,57 on layer 6 of the screen.
// This particular command's destination rectangle is 32x32,
// so the image will be scaled up 2x.
	
```

---

### Screen->DrawLayer()

void DrawLayer(int layer, int source_map, int source_screen, int source_layer, int x, int y, float rotation, int opacity)
:	* ZASM Instruction: `DRAWLAYERR`

Draws an entire Layer from source_screen on source_map on the specified layer of the current screen at `(x,y)`. If rotation is not zero, the entire layer will rotate about its center.

`opacity` controls how translucent the solid portions of the tiles will be, either `OP_OPAQUE` or `OP_TRANS`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Screen->DrawScreen()

void DrawScreen(int layer, int map, int screen, int x, int y, float rotation)
:	* ZASM Instruction: `DRAWSCREENR`

Draws an entire screen from `screen` on `map` on the specified layer of the current screen at `(x,y)`. If rotation is non-zero, the entire layer will rotate about its center.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !