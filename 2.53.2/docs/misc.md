# Miscellany

## ZASM Flags

ZASM uses a series of special flags to determine how it should follow logical instructions, including the following:

#### Script flags

* `TRUEFLAG`: A condition in the script is **true**
* `MOREFLAG`: Must be set manually with ZASM
* `FALSEFLAG`: Must be set manually with ZASM
* `LESSFLAG`: Must be set manually with ZASM

#### Instructions

These flags are used in evaluation instructions to determine if an instruction should run.

* `SETTRUE`: Set the Script Flag TRUEFLAG. SETTRUE Sets a true condition for the Assembler, if a COMPARERV and COMPARER validate. This is used when making statements in ZScript.
* `SETFALSE:` Set the Script Flag FALSEFLAG. ZScript does not use this. 
* `SETMORE`: Set the Script Flag MOREFLAG. ZScript does not use this. 
* `SETLESS`: Set the Script Flag LESSFLAG. ZScript does not use this. 

#### Evaluation Instructions

* `GOTOTRUE`: Executes the GOTO instruction only if the Script Flag TRUEFLAG is enabled.
* `GOTOFALSE`: Executes the GOTO instruction only if the Script Flag FALSEFLAG is enabled.
* `GOTOMORE`: Executes the GOTO instruction only if the Script Flag MOREFLAG is enabled.
* `GOTOLESS`: Executes the GOTO instruction only if the Script Flag LESSFLAG is enabled.

In contrast, `GOTO` and `GOTOR` ignore all flags and conditions.

ZScript always compiles down to `GOTO`, `GOTOR`, and `GOTOTRUE` instructions. The other FLAG-typed GOTO instruction types are valid only in ZASM, and serve no useful purpose to ZScript's compiler. `GOTOLESS`, `GOTOMORE`, and `GOTOFALSE` are effectively deprecated.

## Instruction Processing Order

1. Instructions in the **Global Init script** (if starting a new game).
2. Instructions in the **Global OnContinue script** (if resuming a game from the file menu).
3. Instructions in **FFC scripts.** \*
4. Instructions in the **Global Active script** prior to `Waitdraw()`.
5. Screen scrolling (2.50.2 or later).
6. Screen draws occur in the order they were enqueued above.
7. `Waitdraw()` returns in a **Global Active script**.
8. Engine writing to `Link->Dir` and `Link->Tile`.
9. Instructions from **Item Action scripts**.
10.     Instructions from **Item Pickup scripts**.
11.     Instructions in the **Global Active script** after `Waitdraw()`.
12.     Screen Scrolling (2.50.0 and 2.50.1)
13.     Instructions in the **Global OnExit script** (if the game is exiting).
14.     Return to (3).

\* *Instructions are handled on a per-ffc basis, in ID order; so a script on ffc ID 1 runs, then a script on ffc ID 2, up to ffc ID 32. If an ffc has no script, it is skipped. If "Run Script at Screen Init" is checked, instructions will process until Waitframe() before the screen is loaded.*

## Pointers

Global array pointers start at **4096** (when traced). These are added in escalating value, but in the reverse-order of declaration. e.g. The last declared array will be ID 4096.

## ZASM stuff that should probably go elsewhere

(TODO) !#! what is this.  where do i put this. i think that i am going to just split out all of the ZASM stuff into its own section

ZASM only operators:

SET ADDRESS ARG		SETA1<><>
			SETA2<><>
GET ADDRESS ARG		GETA1<><>
			GETA2<><>
			

Set Working FFC ID:     ZASM Instruction
        REFFFC
        