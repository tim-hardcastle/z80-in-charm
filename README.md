# Z80-in-charm

A toy Z80 interpreter. "Interpreter" because the assembly doesn't get converted into bytecode and put into memory somewhere, it's just run against the emulated machine state.

And "toy" because it implements only the more popular subset of the language, as follows.

## Z80 specification

Operations : ld, push, pop, add, adc, sub, sbc, cmp, neg, nop, inc, dec, jp

Registers : af, bc, de, hl

Flags : zero, negative, carry

Numbers are given as two- or four-digit lower-case hexadecimal preceeded by a #, e.g. #e6, #50f4.

As usual in Z80 assembler, parentheses around a number indicate that it is an address.

Labels are any string preceded by @.

Example code to compute as much of the Fibonacci sequence as will fit in eight bits:

```
ld a, #01
ld (#0001), a
ld (#0002), a
ld c, a
ld e, a
ld l, #02
@loop
ld a, c
add a, e
ld c, e
ld e, a
inc hl
ld (hl), a
ld a, l
cp #0d
jp nz, @loop
```

## The Charm frontend

Commands are:

`ex <string>` : applies the given line to the machine state, eg ex "ld a, #05"

`load <filename>` : loads a z80 file

`reset` : resets the memory, stack, registers, etc.
  
`run` : runs the loaded file

`step` : takes one step through the instructions in the loaded file

`show` : shows the machine state
