# SIMPL-F compiler
Racket Assembler/Compiler that compiles a artificial functional language into artificial machine code

The program converts a program written in SIMPL-F into PRIMPL, which can then be run using (load-primp) and (run-primp) provided by PRIMPL.rkt 

## Table of Contents
* [Languages & Syntax] (#languages--syntax)
* [Technologies] (#technologies)
* [Setup] (#setup)

## Languages & Syntax
Languages:
 * PRIMPL (Primitive IMperative Language): Machine code
 * A-PRIMPL (Assembly PRIMPL)
 * SIMPL (Simple IMperative Language): High level imperative language
 * SIMPL-F (SIMPL with Functions)

Steps:
  - SIMPL-F => SIMPL
  - SIMPL => A-PRIMPL (compiler)
  - A-PRIMPL => PRIMPL (assembler)

Syntax:
```
   _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
  |                            PRIMPL                            |
  |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
  | PC: Program Counter. Holds loc of next instruct.             |
  | opnd: Operand. e.g. 2 is a val, (2) is a loc.                |
  |                                                              |
  | (add dst opnd1 opnd2)                   dst <= opnd1 + opnd2 |
  | (sub dst opnd1 opnd2)                   dst <= opnd1 - opnd2 |
  | (mul dst opnd1 opnd2)                   dst <= opnd1 * opnd2 |
  | (div dst opnd1 opnd2)                   dst <= opnd1 / opnd2 |
  | (mod dst opnd1 opnd2)                   dst <= opnd1 % opnd2 |
  | (equal dst opnd1 opnd2)                 dst <= opnd1 = opnd2 |
  | (not-equal dst opnd1 opnd2)             dst <= opnd1 ≠ opnd2 |
  | (gt dst opnd1 opnd2)                    dst <= opnd1 > opnd2 |
  | (ge dst opnd1 opnd2)                    dst <= opnd1 ≥ opnd2 |
  | (lt dst opnd1 opnd2)                    dst <= opnd1 < opnd2 |
  | (le dst opnd1 opnd2)                    dst <= opnd1 ≤ opnd2 |
  | (land dst opnd1 opnd2)                  dst <= opnd1 & opnd2 |
  | (lor dst opnd1 opnd2)                   dst <= opnd1 | opnd2 |
  | (lnot dst opnd)                         dst <= !opnd         |
  | (move dst opnd)                         dst <= opnd          |
  | (jump loc)                              PC <= loc            |
  | (jsr dst loc)                           dst <= PC; PC <= loc |
  | (branch opnd loc)                       PC <= loc if opnd    |
  | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|
```
```
   _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
  |                           A-PRIMPL                           |
  |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
  | Base syntax is the same as PRIMPL, with additional           |
  | pseudo-instructions as follows:                              |
  |                                                              |
  | (lit num)                 insert num at current pos          |
  | (const sym num)           const: sym = num                   |
  | (label NAME)              allows direct jump to NAME         |
  | (data NAME x1 x2 ..)      seq of vals starting at loc NAME   |
  | (data NAME (n val))       seq of n vals starting at loc NAME |
  | (halt)                    halts program                      |
  | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|
```
```
   _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
  |                             SIMPL                            |
  |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
  | A SIMPL program is a sequence of var statements, initialized |
  | to ints, followed by instructions                            |
  |                                                              |
  | e.g. (vars [(x 0) (y 1) (z 2)]                               |
  |              (print x))                                      |
  |                                                              |
  | 
  | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|
```
