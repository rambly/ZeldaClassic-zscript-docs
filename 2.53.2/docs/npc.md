# NPC Functions and Variables

class npc
:	<!-- - -->

## Status Variables

### npc->IsValid()

bool IsValid()
:	* ZASM Instruction: `ISVALIDNPC`

Returns whether or not this NPC pointer is still valid. A pointer becomes invalid if the enemy dies or Link leaves the screen.

!!! note
	Trying to access any other variable of an invalid NPC pointer prints an error to allegro.log and does nothing.

---

### npc->GetName()

void GetName(int buffer[])
:	* ZASM Instruction: `NPCNAME`

Loads the NPC's name into `buffer`. To load an NPC from an ID rather than a pointer, use `GetNPCName()` from **std.zh**.

---

### npc->ID

int ID
:	* ZASM Instruction: `NPCID`

The NPC's enemy ID number.

`npc->ID` is read-only; while setting it is not syntactically incorrect, it does nothing.

---

### npc->Type

int Type
:	* ZASM Instruction: `NPCTYPE`

The NPC's Type. Use the `NPCT_` constants in **std.zh** to compare this value.

`npc->Type` is read-only; while setting it is not syntactically incorrect, it does nothing.

---

## NPC XYZ Position Variables

### npc->X

int X
:	* ZASM Instruction: `NPCX`

The NPC's current X coordinate, in pixels. Float values passed to this will be cast to int.

---

### npc->Y

int Y
:	* ZASM Instruction: `NPCY`

The NPC's current Y coordinate, in pixels. Float values passed to this will be cast to int.

---

### npc->Z

int Z
:	* ZASM Instruction: `NPCZ`

The NPC's current Z coordinate, in pixels. Float values passed to this will be cast to int.

---

### npc->Jump

int Jump
:	* ZASM Instruction: `NPCJUMP`

The NPC's upward velocity, in pixels. If negative, the NPC will fall.

The downward acceleration of Gravity (in Init Data) modifies this value every frame.

---

### npc->Dir

int Dir
:	* ZASM Instruction: `NPCDIR`

The direction that the weapon is facing. Used by certain weapon types to determine movement, shield deflection and such. (TODO) ! is this determined by `DIR_` constants?

---

## Movement and Behavior Variables

### npc->Rate

int Rate
:	* ZASM Instruction: `NPCRATE`

The rate at which the NPC changes direction. For a point of reference, the "Octorok (Magic)" enemy has a rate of 16.

The effect of writing to this field is currently undefined.

---

### npc->Haltrate

int Haltrate
:	* ZASM Instruction: `NPCHALTRATE`

The extent to which the NPC stands still while moving around the screen. As a point of reference, the Zols and Gels have a haltrate of 16.

The effect of writing to this field is currently undefined.

---

### npc->Homing

int Homing
:	* ZASM Instruction: `NPCHOMING`

How likely the NPC is to move towards Link.

The effect of writing to this field is currently undefined.

---

### npc->Hunger

int Hunger
:	* ZASM Instruction: `NPRCHUNGE`

How likely the NPC is to move towards bait.

The effect of writing to this field is currently undefined.

---

### npc->Step

int Step
:	* ZASM Instruction: `NPCSTEP`

The NPC's movement speed. A Step of 100 usually means that the enemy moves at approximately one pixel per animation frame. As a point of reference, the "Octorok (Magic)" enemy has a step of 200.
  
The effect of writing to this field is currently undefined.

---

### npc->CollDetection

bool CollDetection
:	* ZASM Instruction: `NPCCOLLDET`

Whether or not the NPC will interact with the player and lweapons.

---

### npc->ASpeed

int ASpeed
:	* ZASM Instruction: `NPCFRAMERATE`

The the NPC's animation frame rate, in screen frames.

The effect of writing to this field is currently undefined.

---

### npc->DrawStyle

int DrawStyle
:	* ZASM Instruction: `NPCDRAWTYPE`

The way the NPC is animated. Use the `DS_` constants in **std.zh** to set or compare this value.
  
The effect of writing to this field is currently undefined.

---

## NPC Interaction Variables and Functions

### npc->HP

int HP
:	* ZASM Instruction: `NPCHP`

The NPC's current hitpoints. A weapon with a Power of 1 removes 2 hitpoints.

---

### npc->Damage

int Damage
:	* ZASM Instruction: `NPCDP`

The amount of damage dealt to an unprotected Link when he touches this NPC, in quarter-hearts.

---

### npc->WeaponDamage

int WeaponDamage
:	* ZASM Instruction: `NPCWDP`

The amount of damage dealt to an unprotected Link by this NPC's weapon, in quarter-hearts.

---

### npc->Stun

int Stun
:	* ZASM Instruction: `NPCSTUN`

The time, in frames, that the NPC will be stunned. Some types of enemies cannot be stunned.

---

### npc->ItemSet

int ItemSet
:	* ZASM Instruction: `NPCITEMSET`

The items that the NPC might drop when killed. Use the `IS_` constants in **std.zh** to set or compare this value.

---

### npc->BreakShield()

void BreakShield()
:	* ZASM Instruction: `BREAKSHIELD`

Breaks the enemy's shield if it has one. This works even if the flag "Hammer Can Break Shield" is not checked.

---

## Graphics and SFX Variables

### npc->OriginalTile

int OriginalTile
:	* ZASM Instruction: `NPCOTILE`

The number of the starting tile used by this NPC.

---

### npc->Tile

int Tile
:	* ZASM Instruction: `NPCTILE`

The current tile associated with this NPC.

The effect of writing to this variable is undefined.

---

### npc->Weapon

int Weapon
:	* ZASM Instruction: `NPCWEAPON`

The weapon used by this enemy. Use the `WPN_` constants (**NOT** the `EW_` constants) in **std.zh** to set or compare this value.

---

### npc->CSet

int CSet
:	* ZASM Instruction: `NPCCSET`

The CSet used by this NPC.

---

### npc->BossPal

int BossPal
:	* ZASM Instruction: `NPCBOSSPAL`

The boss palette used by this NPC. This palette is only used if CSet is 14 (the reserved boss CSet).

Use the `BPAL_` constants in **std.zh** to set or compare this value.

---

### npc->SFX

int SFX
:	* ZASM Instruction: `NPCBGSFX`

The sound effects emitted by the enemy. Use the `SFX_` constants in **std.zh** to set or compare this value.

---

### npc->Extend

int Extend
:	* ZASM Instruction: `NPCEXTEND`

Whether to extend the sprite of the enemy.

---

## Size, Offset and Hitbox Variables

### npc->TileWidth

int TileWidth
:	* ZASM Instruction: `NPCTXSZ`

The number of tile columns composing the sprite.

Writing to this is ignored unless Extend is set to values `>=3`.

---

### npc->TileHeight

int TileHeight
:	* ZASM Instruction: `NPCTYSZ`

The number of tile rows composing the sprite.

Writing to this is ignored unless Extend is set to values `>=3`.

---

### npc->HitWidth

int HitWidth
:	* ZASM Instruction: `NPCHXSZ`

The width of the sprite's hitbox.

---

### npc->HitHeight

int HitHeight
:	* ZASM Instruction: `NPCHYSZ`

The height of the sprite's hitbox.

---

### npc->HitZHeight

int HitZHeight
:	* ZASM Instruction: `NPCHZSZ`

The Z-axis height of the sprite's hitbox, or collision rectangle. The greater it is, the higher Link must jump or fly over the sprite to avoid taking damage.

This is a pointer to the same value as `DrawZOffset`. In other words, setting this variable to a value will also set `DrawZOffset` to the same value.

---

### npc->HitXOffset

int HitXOffset
:	* ZASM Instruction: `NPCHXOFS`

The X offset of the sprite's hitbox, or collision rectangle. Setting it to positive or negative values will move the sprite's hitbox left or right.

---

### npc->HitYOffset

int HitYOffset
:	* ZASM Instruction: `NPCHYOFS`

The Y offset of the sprite's hitbox, or collision rectangle. Setting it to positive or negative values will move the sprite's hitbox up or down.

---

### npc->DrawXOffset

int DrawXOffset
:	* ZASM Instruction: `NPCXOFS`

The X offset of the sprite. Setting it to positive or negative values will move the sprite's tiles left or right relative to its position.

---

### npc->DrawYOffset

int DrawYOffset
:	* ZASM Instruction: `NPCYOFS`

The Y offset of the sprite. In non-sideview screens, this is usually -2. Setting it to positive or negative values will move the sprite's tiles up or down relative to its position.

---

### npc->DrawZOffset

int DrawZOffset
:	* ZASM Instruction: `NPCZOFS`

The Z offset of the sprite. This is ignored unless Extend is set to values `>=3`.

This is a pointer to the same value as `HitZHeight`. In other words, setting this variable to a value will also set `HitZHeight` to the same value.

---

## Miscellaneous Player Variables

### npc->Defense[]

int Defense[]
:	* ZASM Instruction: `NPCDEFENSED`

The npc's Defense values, as an array of 18 integers.

Use the `NPCD_` and `NPCDT_` constants in std.zh to set or compare these values.

---

### npc->Attributes[]

int Attributes[]
:	* ZASM Instruction: `NPCDD`

The npc's Miscellaneous Attributes, as an array of fifteen integers.

!!! note
	As of 2.53.0c, these are read/write. \[(TODO) ! Update nomenclature if necessary\] In older versions, this variable is read-only and sized to ten integers.

---

### npc->MiscFlags

int MiscFlags
:	* ZASM Instruction: `NPCMFLAGS`

The npc's Misc. Flags as 14 bits ORed together, starting with 'Damaged by Power 0 Weapons', and working down the flags in the order they are shown in the Enemy Editor.

If you are not comfortable with binary operations, you can use `GetNPCMiscFlag()` from **std.zh**.
 
`npc->MiscFlags` is read-only; while setting it is not syntactically incorrect, it does nothing.

---

### npc->Misc[]

float Misc[]
:	* ZASM Instruction: `NPCMISCD`

An array of 16 miscellaneous variables for you to use as you please.