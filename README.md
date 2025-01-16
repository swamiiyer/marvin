## Marvin

Marvin is a hypothetical computer with sixteen 16-bit registers and 65,536 32-bit words of main memory (RAM). In 
addition to the sixteen registers, Marvin has a 16-bit program counter `pc` and a 32-bit instruction register `ir`. A 
Marvin program (ie, a `.marv` file) is assembled and loaded into memory starting at location 0. Marvin supports 32 
instructions, each of which accepts between 0 and 3 arguments (aka inputs). See 
[Marvin Machine Specification](https://www.cs.umb.edu/~siyer/teaching/marvinspec.pdf) for more details about the 
machine, including its instruction set. 

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

Here is a sample Marvin program called `Coundown.marv` that accepts `n` (int) from standard input and writes to 
standard output a countdown from `n` to 0.
```
# Accepts n (int) from standard input and writes a countdown from n to 0 to standard output.

0    read     r0          # read n
1    set0     r1          # zero = 0
2    jltn     r0 r1 6     # if n < zero jump to 6
3    write    r0          # write n
4    addn     r0 -1       # n = n - 1
5    jumpn    2           # jump to 2
6    halt                 # halt the machine
```

Here is the output from running `Countdown.marv` using `marvin.py`:
```
$ python3 marvin.py -v Countdown.marv
    0: 00000001 00000000 00000000 00000000                    0: read   r0  
    1: 00000100 00000000 00000000 00000001                    1: set0   r1  
    2: 00011000 00000001 00000000 00000110                    2: jltn   r0 r1 6
    3: 00000010 00000000 00000000 00000000                    3: write  r0  
    4: 00000111 00000000 10000000 00000001                    4: addn   r0 -1 
    5: 00001111 00000000 00000000 00000010                    5: jumpn  2  
    6: 00000000 00000000 00000000 00000000                    6: halt     

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
