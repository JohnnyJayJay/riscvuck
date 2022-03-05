# riscvuck

riscvuck ("risk-fuck") is a brainfuck interpreter written in RISC-V assembly for 32-Bit Linux, mainly for educational purposes. It mostly follows the reference and guidelines provided by [brainfuck.org](http://brainfuck.org). However this implementation is technically not Turing-complete because the internal array size is static.

## How
Install a RISC-V 32 Bit assembler and linker. Assemble and link `bf.riscv`. On Arch-based distros, `./build` should work for this purpose.

The resulting program (let's call it `bf`) takes one argument: the source code file. You can run it on non-RISC-V architectures using `qemu`:

`qemu-riscv32 bf hello-world.b`

I/O is done through standard I/O. 

Possible exit codes and their meanings:
- `0`: success
- `1`: you didn't provide an input file
- `2`: couldn't open the file
- `3`: couldn't allocate memory to load the file or the brainfuck array
- `4`: you have a syntax error

## Some Details of the implementation

- Input files must be `2^31 - 1` bytes at max (if this bothers you: what's wrong with you?).
- There are exactly 2^16 cells available, execution begins at the leftmost cell.
- Each cell holds a 32-Bit signed integer, initially all 0.
- If you access an out of bounds cell, may god have mercy on your soul.
- Reading from stdin `,` when EOF has been reached continues execution as normal and leaves the current cell unchanged. 
- Syntax checking is done ahead of execution time.

## License
Licensed under the MIT License (https://mit-license.org).
