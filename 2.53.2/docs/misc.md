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

1. Instructions in **global script Init** (if starting a new game)

2. Instructions in **global script OnContinue** (if resuming a game)

3. Instructions from **FFCs that run on screen initialization**, with the exception of drawing instructions.\*

4. Instructions **immediately inside the `run()` function of a global active script**, if the game has just loaded.

5. Instructions **in the global active script's infinite loop** (i.e. within `while (true)`) prior to `Waitdraw()`.

6. Instructions from an FFC script positioned after (an illegal) `Waitdraw()` instruction in that script from the previous frame. \*\*

7. Screen bitmap drawing.

8. Enqueued script drawing from the global active script (and from FFCs on the previous frame).

9. **Drawing instructions in the global active script** prior to `Waitdraw()`.

10. **Instructions in an FFC script**, with the exception of drawing instructions.

11. Screen scrolling (in 2.50.2 and later)

12. **`Waitdraw()`** in a global active script.

13. Engine writing to `Link->Dir` and `Link->Tile`.

14. FFCs **enqueue draws** for the next frame.

15. Instructions from **item action scripts**.

16. Instructions from **item collect scripts**.

17. Instructions in the **global active script** that are called **after** `Waitdraw()`

18. **Screen scrolling** (before 2.50.2)

19. Instructions in an **OnExit script** (if the game is exiting)

20. Return to **step 3**.

\* *Instructions are handled on a per-FFC basis, in order of ID. That is, a script on FFC ID 1 runs, then a script on FFC ID 2, and so on. If an FFC has no script, it is skipped.*

\*\* *Requires being on at least the second frame of a game session.*

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
        