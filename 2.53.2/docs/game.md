# Game Functions and Variables

class Game
:	<!-- - -->
	
## Current Location Functions	

### Game->GetCurScreen()

int GetCurScreen()
:	* ZASM Instruction: `CURSCR`

Retrieves the number of the current screen within the current map.

<!-- **Example** -->
``` C
// Assuming we're on the very bottom-right screen of a map (0x7F)

Game->GetCurScreen()
// This will be 127, which is the decimal representation of hex 0x7F

```

---

### Game->GetCurDMapScreen()

int GetCurDMapScreen()
:	* ZASM Instruction: `CURDSCR`

Retrieves the number of the current screen within the current DMap.

<!-- **Example** -->
``` C
// Assuming we're on the entrance screen of 1st.qst level 2 (0x7D)

Game->GetCurScreen()
// This will be 125 (0x7D), which is the "absolute" position on the map

Game->GetCurDMapScreen()
// This will be 115 (0x73), which is the position of the screen on the DMap
// (after the DMap offset is applied)

```

---

### Game->GetCurLevel()

int GetCurLevel()
:	* ZASM Instruction: `CURLEVEL`

Retrieves the number of the dungeon level of the current DMap. Multiple DMaps can have the same dungeon level - this signifies that they share a map, compass, level keys and such.

<!-- **Example** -->
``` C
Game->GetCurLevel()
// will be the current DMap's level

```

---
	
### Game->GetCurMap()

int GetCurMap()
:	* ZASM Instruction: `CURMAAP`

Retrieves the number of the current map.

<!-- **Example** -->
``` C
Game->GetCurMap()
// will be the current number of the map Link is on

```

---

### Game->GetCurDMap()

int GetCurDMap()
:	* ZASM Instruction: `CURDMAP`

Returns the number of the current DMap.

<!-- **Example** -->
``` C
Game->GetCurDMap()
// will be the current loaded DMap's number
	
```

---

## DMap Info Functions

### Game->DMapFlags[]

int DMapFlags[]
:	* ZASM Instruction: `DMAPFLAGSD`

An array of 512 integers containing each DMap's flags ORed (`|`) together.

Use the `DMF_` constants or the '`DMapFlag()`' functions from **std.zh** if you are not comfortable with binary.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DMapLevel[]

int DMapLevel[]
:	* ZASM Instruction: `DMAPLEVELD`

An array of 512 integers containing each DMap's level.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DMapCompass[]

int DMapCompass[]
:	* ZASM Instruction: `DMAPCOMPASSD`

An array of 512 integers containing each DMap's compass screen.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DMapContinue[]

int DMapContinue[]
:	* ZASM Instruction: `DMAPCONTINUED`

An array of 512 integers containing each DMap's continue screen.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DMapMIDI[]

int DMapMIDI[]
:	* ZASM Instruction: `DMAPMIDID`

An array of 512 integers containing each DMap's MIDI. Positive numbers are for custom MIDIs, and negative values are used for the built-in game MIDIs. Because of the way DMap MIDIs are handled internally, however, built-in MIDIs besides the overworld, dungeon, and level 9 songs won't match up with `Game->PlayMIDI()` and `Game->GetMIDI()`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetDMapName()

int GetDMapName(int dmap, int buffer[])
:	* ZASM Instruction: `GETDMAPNAME`

Finds DMap `dmap` and loads its internal ZQuest name as a string into `buffer`.

See **std_constants.zh** for the appropriate buffer size.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetDMapTitle()

int GetDMapTitle(int dmap, int buffer[])
:	* ZASM Instruction: `GETDMAPTITLE`

Finds DMap `dmap` and loads its title as a string into `buffer`.

See **std_constants.zh** for the appropriate buffer size.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetDMapIntro()

int GetDMapIntro(int dmap, int buffer[])
:	* ZASM Instruction: `GETDMAPINTRO`

Finds DMap `dmap` and loads its intro text as a string into `buffer`.

See **std_constants.zh** for the appropriate buffer size.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DMapOffset[]

int DMapOffset[]
:	* ZASM Instruction: `DMAPOFFSET`

An array of 512 integers containing the X offset of each DMap.

!!! note
	`Game->DMapOffset` is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Playthrough Info Functions

### Game->NumDeaths

int NumDeaths;
:	* ZASM Instruction: `GAMEDEATHS`

Returns or sets the number of times Link has perished during this quest.

<!-- **Example** -->
``` C
x = Game->NumDeaths(); // will be the current death counter
Game->NumDeaths()--; // will decrement the death counter by one
	
```

---

### Game->Cheat

int Cheat;
:	* ZASM Instruction: `CHEAT`

Returns or sets the current cheat level of the quest player. Valid values are 0, 1, 2, 3, and 4.

<!-- **Example** -->
``` C
x = Game->Cheat; // will be the current cheat level
Game->Cheat = 4; // force the cheat level to be 4
Game->Cheat = 0; // and turn cheats off
	
```

---

### Game->Time()

int Time;
:	* ZASM Instruction: `GAMETIME`

Returns the time elapsed in this quest, in 60ths of a second. (i.e. in frames). 

The return value is undefined if TimeValid is false (see below).

<!-- **Example** -->
``` C
// Assuming we've been playing for an hour, 20 minutes, and 10 seconds...
x = Game->Time; // will be 288600
	
```

---

### Game->TimeValid()

int TimeValid;
:	* ZASM Instruction: `GAMETIMEVALID`

True if the elapsed quest time can be determined for the current quest.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->HasPlayed()

bool HasPlayed;
:	* ZASM Instruction: `GAMEHASPLAYED`

This value is `true` if the current quest session was loaded from a saved game, `false` if the quest was started fresh.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->Standalone()

bool Standalone;
:	* ZASM Instruction: `GAMESTANDALONE`

This value is `true` if the game is running in standalone mode, `false` if not. Standalone mode is set by command line parameters when launching ZC.

`Game->Standalone` is read-only; while setting it is not syntactically incorrect, it does nothing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Game State Variables

### Game->GuyCount[]

int GuyCount[]
:	* ZASM Instruction: `GAMEGUYCOUNT`

The number of NPCs (enemies and guys) on screen `i` of this map, where `i` is the index used to access this array. This array is exclusively used to determine which enemies had previously been killed, and thus won't return, when you re-enter a screen.

!!! note
	This is only a *count* of the enemies that remain on a screen; not their IDs.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->ContinueDMap

int ContinueDMap
:	* ZASM Instruction: `GAMECONTDMAP`

Returns or sets the DMap where Link will be respawned after quitting and reloading the game.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->ContinueScreen

int ContinueScreen
:	* ZASM Instruction: `GAMECONTSCR`

Returns or sets the map screen where Link will be respawned after quitting and reloading the game.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->LastEntranceDMap

int LastEntranceDMap
:	* ZASM Instruction: `GAMEENTRDMAP`

Returns or sets the DMap where Link will be respawned after dying and continuing.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Counter Arrays

### Game->Counter[]

int Counter[]
:	* ZASM Instruction: `GAMECOUNTERD`

Returns or sets the current value of the counter specified by the index of the array. Use the `CR_` constants in std.zh as the index of this array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->MCounter[]

int MCounter[]
:	* ZASM Instruction: `GAMEMCOUNTERD`

Returns or sets the current maximum value of the counter specified by the index of the array. Use the `CR_` constants in std.zh as the index of this array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->DCounter[]

int DCounter[]
:	* ZASM Instruction: `GAMEDCOUNTERD`

Returns or sets the current value of the game drain counter specified by the index of the array. Use the `CR_` constants in std.zh as the index of this array.

Note that if the player hasn't acquired the "1/2 Magic Upgrade" yet, then setting the `CR_MAGIC` drain counter to a negative value will drain the magic counter by 2 per frame rather than 1.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->Generic[]

int Generic[]
:	* ZASM Instruction: `GAMEGENERICD`

An array of miscellaneous game values, such as number of heart containers and magic drain rate. Use the `GEN_` constants in std.zh as the index of this array.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->LItems[]

byte LItems[]
:	* ZASM Instruction: `GAMELITEMSD`

The exploration items (map, compass, boss key etc.) of dungeon level `i` currently under the possession of the player, where `i` is the index used to access this array. Each element of this array consists of flags OR'd (`|`) together; use the `LI_` constants in std.zh to set or compare these values.

The valid range of values for this variable is 0 to 255.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->LKeys[]

byte LKeys[]
:	* ZASM Instruction: `GAMELKEYSD`

The number of level-specific keys of level `i` currently under the possession of the player, where `i` is the index used to access this array.

The valid range of values for this variable is 0 to 255.

<!-- **Example** -->
``` C
Game->LKeys[3] += 4; // Gives the player four keys to Level 3.
	
```

---

## Screen Flag & State Functions

### Game->GetScreenFlags()

int GetScreenFlags(int map, int screen, int flagset)
:	* ZASM Instruction: `GETSCREENFLAGS`

Returns the screen flags from screen `screen` on map `map`, interpreted in the same way as `Screen->Flags`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetScreenEFlags()

int GetScreenEFlags(int map, int screen, int flagset)
:	* ZASM Instruction: `GETSCREENEFLAGS`

Returns the enemy flags from screen `screen` on map `map`, interpreted in the same way as `Screen->EFlags`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetScreenState()

bool GetScreenState(int map, int screen, int flagset)
:	* ZASM Instruction: `SCREENSTATEDD`

As with `Screen->State`, but retrieves the miscellaneous flags of *any* screen, not just the current one. This function is undefined if `map` is less than 1 or greater than the maximum map number of your quest, or if `screen` is greater than 127 (i.e. `0x7F`).

Use the `ST_` constants in std.zh for the flag parameter.

!!! note
	Screen numbers in ZQuest are usually displayed in hexadecimal. [Per ZScript's syntax](syntax.html#numbers), you can use hexadecimal values prefixed with `0x` as the argument to `screen`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetScreenState()

void SetScreenState(int map, int screen, int flagset)
:	* ZASM Instruction: `SCREENSTATEDD`

As with `Screen->State`, but sets the miscellaneous flags of *any* screen, not just the current one. This function is undefined if `map` is less than 1 or greater than the maximum map number of your quest, or if `screen` is greater than 127 (i.e. `0x7F`).

Use the `ST_` constants in std.zh for the flag parameter.

!!! note
	Screen numbers in ZQuest are usually displayed in hexadecimal. [Per ZScript's syntax](syntax.html#numbers), you can use hexadecimal values prefixed with `0x` as the argument to `screen`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetScreenD()

float GetScreenD(int screen, int reg)
:	* ZASM Instruction: `SDDD`

Retrieves the value of `Screen->D[reg]` on the given `screen` of the current DMap.

!!! note
	This is **not** the same as FFC D0-D7 -- see `Screen->D[]` for more information on the screen-specific D registers.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetScreenD()

void SetScreenD(int screen, int reg, float value)
:	* ZASM Instruction: `SDDD`

Sets the value of `Screen->D[reg]` on the given `screen` of the current DMap to `value`.

!!! note
	This is **not** the same as FFC D0-D7 -- see `Screen->D[]` for more information on the screen-specific D registers.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetDMapScreenD()

void GetDMapScreenD(int dmap, int screen, int reg)
:	* ZASM Instruction: `SDDDD`

Retrieves the value of `Screen->D[reg]` on the given `screen` of the given `dmap`.

!!! note
	This is **not** the same as FFC D0-D7 -- see `Screen->D[]` for more information on the screen-specific D registers.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetDMapScreenD()

void SetDMapScreenD(int dmap, int screen, int reg, float value)
:	* ZASM Instruction: `SDDDD`

Sets the value of `Screen->D[reg]` on the given `screen` of the given `dmap` to `value`.

!!! note
	This is **not** the same as FFC D0-D7 -- see `Screen->D[]` for more information on the screen-specific D registers.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Audio Functions

### Game->PlaySound()

void PlaySound(int soundid)
:	* ZASM Instruction: `PLAYSOUNDR`, `PLAYSOUNDV`

Plays one of the quest's sound effects. Use the `SFX_` constants in std.zh as values of `soundid`, or refer to ZQuest's menus (**Quest->Audio->SFX Data**).

<!-- **Example** -->
``` C
Game->PlaySound(SFX_DODONGO); // Play a Dodongo roar!
Game->PlaySound(8); // This is the same thing
	
```

---

### Game->PlayMIDI()

void PlayMIDI(int MIDIid)
:	* ZASM Instruction: `PLAYMIDIR`, `PLAYMIDIV`

Changes the current screen MIDI to `MIDIid`. Will revert to the DMap (or screen) MIDI upon leaving the screen.

<!-- **Example** -->
``` C
Game->PlayMIDI(3); // Play the custom MIDI in MIDI slot 3 for the remainder of the screen
	
```

---

### Game->GetMIDI()

int GetMIDI()
:	* ZASM Instruction: `GETMIDI`

Returns the current screen MIDI that is playing. Positive numbers are for custom MIDIs, and negative values are used for the built-in game MIDIs.

<!-- **Example** -->
``` C
// If we're listening to the original Zelda overworld music...
x = Game->GetMIDI(); // Will be -1
	
```

---

### Game->PlayEnhancedMusic()

bool PlayEnhancedMusic(int filename[], int track)
:	* ZASM Instruction: `PLAYENHMUMSIC`

Play the specified enhanced music if it's available. If the music cannot be played, the current music will continue. The music will revert to normal upon leaving the screen.

Returns `true` if the music file was loaded successfully. The filename cannot be more than 255 characters. If the music format does not support multiple tracks, the track argument will be ignored.

<!-- **Example** -->
``` C
// Make a string with the filename of the music to play.
int myCoolMusicFile[] = "swankytunes.nsf"; 

// You can use the return value to simultaneously attempt to run the command
// and go to a fallback if it didn't run successfully, like so
if (!Game->PlayEnhancedMusic(myCoolMusicFile, 3))
	Game->PlayMIDI(7)

// Will play track 3 of the specified NSF file.
// If this were an mp3 or another trackless format
// the value 1 would be ignored (but would still need to be specified!)
// If swankytunes.nsf can't be loaded for some reason, we'll play a MIDI instead.

```

---

### Game->GetDMapMusicFilename()

void GetDMapMusicFilename(int dmap, int buf[])
:	* ZASM Instruction: `GETMUSICFILE`

Load the filename of the given DMap's enhanced music into the string specified by `buf`.

`buf` should be at least 256 characters (i.e. 256 array elements) in size.

<!-- **Example** -->
``` C
int Filename[256];
Game->GetDMapMusicFilename(7, Filename)
TraceS(Filename); // could be "swankytunes.nsf"
	
```

---

### Game->GetDMapMusicTrack()

int GetDMapMusicTrack(int dmap)
:	* ZASM Instruction: `GETMUSICTRACK`

Returns the given DMap's enhanced music track. This is valid but meaningless if the music format doesn't support multiple tracks.

<!-- **Example** -->
``` C
x = Game->GetDMapMusicTrack(7)
// Will be the track number of the enhanced music associated with DMap 7
// We can use this in tandem with Game->GetDMapMusicFilename(), like above.
	
```

---

### Game->SetDMapEnhancedMusic()

void SetDMapEnhancedMusic(int dmap, int filename[], int track)
:	* ZASM Instruction: `SETDMAPENHMUSIC`

Sets the specified DMap's enhanced music to the given filename and track number. If the music format does not support multiple tracks, the track argument will be ignored. The filename must not be more than 255 characters.

<!-- **Example** -->
``` C
int MySong[255] = "CheesyPopSong.mp3"; // We need to set the string first...
Game->SetDMapEnhancedMusic(8, MySong, 1)

// CheesyPopSong.mp3 will now try to play whenever DMap 8 is accessed.
// The last value will be ignored, but must still be specified to compile,
// so put whatever integer you want there

```

---

## Combo Functions

### Game->GetComboData()

int GetComboData(int map, int screen, int position)
:	* ZASM Instruction: `COMBODDM`

Grabs a particular placed combo's combo reference from anywhere in the game world, based on map (**NOT** DMap), screen number, and position.

Don't forget that the screen index should be in hexadecimal, and that maps are counted from 1 upwards.

`position` is considered an index, treated the same way as in `Screen->ComboD[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboData()

void SetComboData(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBODDM`

Sets a particular placed combo's combo reference from anywhere in the game world, based on map (**NOT** DMap), screen number, and position.

Don't forget that the screen index should be in hexadecimal, and that maps are counted from 1 upwards.

`position` is considered an index, treated the same way as in `Screen->ComboD[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetComboCSet()

void GetComboCSet(int map, int screen, int position)
:	* ZASM Instruction: `COMBOCDM`

Sets a particular placed combo's CSet from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboC[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboCSet()

void SetComboCSet(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBOCDM`

Sets a particular placed combo's CSet from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboC[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetComboFlag()

void GetComboFlag(int map, int screen, int position)
:	* ZASM Instruction: `COMBOFDM`

Sets a particular placed combo's *placed* flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboF[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboFlag()

void SetComboFlag(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBOFDM`

Sets a particular placed combo's *placed* flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboF[]`, with a legal range of 0 to 175.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetComboType()

void GetComboType(int map, int screen, int position)
:	* ZASM Instruction: `COMBOTDM`

Sets a particular placed combo's type from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboT[]`, with a legal range of 0 to 175.

Note that you are grabbing an actual combo attribute as referenced by the combo on screen you're referring to.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboType()

void SetComboType(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBOTDM`

Sets a particular placed combo's type from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboT[]`, with a legal range of 0 to 175.

!!! caution
	This command sets an actual combo attribute as referenced by the combo on screen you're referring to, which means that setting this attribute will affect **ALL** references to this combo throughout the quest.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetComboInherentFlag()

void GetComboInherentFlag(int map, int screen, int position)
:	* ZASM Instruction: `COMBOIDM`

Sets a particular placed combo's *inherent* flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboI[]`, with a legal range of 0 to 175.

Note that you are grabbing an actual combo attribute as referenced by the combo on screen you're referring to.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboInherentFlag()

void SetComboInherentFlag(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBOIDM`

Sets a particular placed combo's *inherent* flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboI[]`, with a legal range of 0 to 175.

!!! caution
	This command sets an actual combo attribute as referenced by the combo on screen you're referring to, which means that setting this attribute will affect **ALL** references to this combo throughout the quest.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetComboSolid()

void GetComboSolid(int map, int screen, int position)
:	* ZASM Instruction: `COMBOSDM`

Sets a particular placed combo's solidity flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboI[]`, with a legal range of 0 to 175.

Note that you are grabbing an actual combo attribute as referenced by the combo on screen you're referring to.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->SetComboSolid()

void SetComboSolid(int map, int screen, int position, int value)
:	* ZASM Instruction: `COMBOSDM`

Sets a particular placed combo's solidity flag from anywhere in the game world, based on map (**NOT** DMap), screen number, and position. `position` is considered an index, treated the same way as in `Screen->ComboI[]`, with a legal range of 0 to 175.

!!! caution
	This command sets an actual combo attribute as referenced by the combo on screen you're referring to, which means that setting this attribute will affect **ALL** references to this combo throughout the quest.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->ComboTile()

int ComboTile(int combo)
:	* ZASM Instruction: `COMBOTILE`

Returns the tile used by combo `combo`.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

## Miscellaneous Game Functions

### Game->GetSaveName()

int GetSaveName(int buffer[])
:	* ZASM Instruction: `GETSAVENAME`

Loads the current save file's name into `buffer`. `buffer` should be at least 9 characters long.

<!-- **Example** -->
``` C
	int GameName[9];
	Game->GetSaveName(GameName)
	// GameName is now whatever the player set their save game name to

```

---

### Game->SetSaveName()

void SetSaveName(int name[])
:	* ZASM Instruction: `SETSAVENAME`

Sets the current save file's name to `name`. `name` should be no more than 9 characters long.

<!-- **Example** -->
``` C
int GameName[9] = "THIEF";
Game->SetSaveName(GameName)
// The player's save game name is now set to "THIEF",
// and will display as such on the file select screen if saved.

```

---

### Game->End()

void End()
:	* ZASM Instruction: `GAMEEND`

**IMMEDIATELY** ends the current game and returns to the file select screen.

Any progress made by the player that was not saved will be lost.

<!-- **Example** -->
``` C
Game->End()
// Return to the file select screen immediately after this point.
// Any subsequent code will not run.
// Any progress made since the last save is lost.
	
```

---

### Game->Save()

void Save()
:	* ZASM Instruction: `GAMESAVE`

Saves the current game. This does not display the save screen; rather, it silently writes all progress to ZELDA.SAV effective immediately.

<!-- **Example** -->
``` C
Game->Save()
// All progress made up to this point is saved! Now isn't that nice?
	
```

---

### Game->ShowSaveScreen()

bool ShowSaveScreen()
:	* ZASM Instruction: `SAVESCREEN`

Displays the save screen. Returns `true` if the user chose to save, `false` otherwise.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->ShowSaveQuitScreen()

void ShowSaveScreen()
:	* ZASM Instruction: `SAVEQUITSCREEN`

Displays the save and quit screen. No return values.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->GetMessage()

void GetMessage(int string, int buffer[])
:	* ZASM Instruction: `GETMESSAGE`

Loads the contents of ZQuest string `string` into `buffer`.  
Use the standalone `GetMessage()` function from std.zh or use string.zh to remove trailing whitespace while loading.

<!-- **Example** -->
``` C
int message[]
Game->GetMessage(1,message)
// message[] could become "IT'S DANGEROUS TO GO      ALONE! TAKE THIS."
// Note that any whitespace *between* characters will be preserved,
// even with the std.zh GetMessage().
	
```

---

### Game->GetFFCScript()

void GetFFCScript(int name[])
:	* ZASM Instruction: `GETFFCSCRIPT`

Returns the number of the script matching `name` or -1 if there is no such script.

<!-- **Example** -->
``` C
int realscript[] = "MyFunkyNPCScript";
int fakescript[] = "ThisScriptDoesNotExist";

int ScriptID;
ScriptID = Game->GetFFCScript(realscript)
// If "MyFunkyNPCScript" is compiled and loaded into an FFC script slot,
// this will be a non-negative number.

// You can use this to test if a script exists.
if (Game->GetFFCScript(realscript) > -1) { // This will evaluate to true
if (Game->GetFFCScript(fakescript) > -1) { // And this, probably, to false
	
```

---

### Game->ClickToFreezeEnabled

bool ClickToFreezeEnabled;
:	* ZASM Instruction: `GAMECLICKFREEZE`

If this is false, the "Click to Freeze" setting will not function, ensuring that the script can use the mouse freely. This overrides the setting rather than changing it, so remembering and restoring the initial value is unnecessary.

<!-- **Example** -->
!!! error "TODO"
	(TODO) !

---

### Game->Version

int Version;
:	* ZASM Instruction: `ZELDAVERSION`

Returns the version of Zelda Classic being used to run the quest.

!!! note
	This command was implemented in Zelda Classic 2.53.1&mdash;it only exists in that version and later versions. It will return `0` in earlier versions.

<!-- **Example** -->

	(TODO) !