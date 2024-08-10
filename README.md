## Marvin

Marvin is a hypothetical computer with sixteen 16-bit registers and 65,536 32-bit words of main memory (RAM). In addition to the sixteen registers, Marvin has a 16-bit program counter `pc` and a 32-bit instruction register `ir`. A Marvin program (ie, a `.marv` file) is assembled and loaded into memory starting at location 0. Marvin supports 32 instructions, each of which accepts between 0 and 3 arguments (aka inputs). See [Marvin Machine Specification](https://www.cs.umb.edu/~siyer/teaching/marvinspec.pdf) for the instruction set. 

The program `marvin.py` is an emulator for the Marvin machine. Here is the usage string for the emulator:
```
$ python3 marvin.py 

Usage: marvin.py [-v] <.marv file>

This program serves as an emulator for a register-based machine called Marvin (named after
the paranoid android character, Marvin, from The Hitchhiker's Guide to the Galaxy by 
Douglas Adams). The design of the machine was inspired by that of the Harvey Mudd 
Miniature Machine (HMMM) developed at Harvey Mudd College. The program accepts a .marv file 
as input, assembles and simulates the instructions within, and prints any output to stdout. 
Any input to the .marv program is via stdin. If the optional -v argument is specified, 
the emulator prints the assembled instructions to stdout before simulating them.

```

Here is a sample Marvin program called `Coundown.marv` that accepts $n$ (int) from standard input and writes to standard output a countdown from $n$ to 0.
```
# Accepts n (int) from standard input and writes a countdown from n to 0 to standard output.

0    read     r1          # read n
1    jltn     r1 r0 5     # if n < 0 jump to 5
2    write    r1          # write n
3    addn     r1 -1       # n = n - 1
4    jumpn    1           # jump to 2
5    halt                 # halt the machine
```

Here is the output from running `Countdown.marv` using `marvin.py`:
```
$ python3 marvin.py -v Countdown.marv
    0: 00000001 00000000 00000000 00000001                    0: read   r1  
    1: 00011000 00010000 00000000 00000101                    1: jltn   r1 r0 5
    2: 00000010 00000000 00000000 00000001                    2: write  r1  
    3: 00000111 00000001 10000000 00000001                    3: addn   r1 -1 
    4: 00001111 00000000 00000000 00000001                    4: jumpn  1  
    5: 00000000 00000000 00000000 00000000                    5: halt     

5
5
4
3
2
1
0
```

## Software Dependencies

* [Python](https://www.python.org/)
