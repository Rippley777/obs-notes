
```
Decimal:  0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15
Hex:      0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F
```

```
0 = 0000
1 = 0001
2 = 0010
3 = 0011
4 = 0100
5 = 0101
6 = 0110
7 = 0111
8 = 1000
9 = 1001
A = 1010
B = 1011
C = 1100
D = 1101
E = 1110
F = 1111
```
```
Hex number:  0x1234
Position:    1   2   3   4
Value:    4096 256  16  1
         (16³)(16²)(16¹)(16⁰)
```


Just like in decimal we use powers of 10:

```
Decimal: 1234
        (1×1000) + (2×100) + (3×10) + (4×1)
        (1×10³)  + (2×10²) + (3×10¹) + (4×10⁰)
```

, Tesla would have had some interesting thoughts about hex! But you know what's fascinating? The patterns in hex are just as beautiful, they're just in base-16 instead of base-10.

Let me show you a neat pattern:

```
0x1 = 1
0x10 = 16
0x100 = 256
0x1000 = 4096
```

See how each time we add a zero in hex, we multiply by 16? Just like in decimal:

```
1 = 1
10 = 10
100 = 100
1000 = 1000
```



- 4 binary digits (bits) = 16 possible combinations (2⁴)
- That's why one hex digit can represent exactly 4 bits
- And why hex goes from 0-F (16 values)
```
FF = 255 (max value for red)
00 = 0   (min value for green)
FF = 255 (max value for blue)
```


Memory addresses (pointers) are typically:

- 4 bytes (32 bits) on 32-bit systems
- 8 bytes (64 bits) on 64-bit systems

This is why you might see terms like "x86" (32-bit) and "x64" (64-bit) architectures. The size matters because it determines how much memory your program can address:

```
32-bit system: 2³² bytes = 4 GB max addressable memory
64-bit system: 2⁶⁴ bytes = 16 exabytes max addressable memory
```


- Each memory address is 32 bits long
- 2³² = 4,294,967,296 unique addresses
- Each address points to 1 byte
- Therefore: ~4 billion bytes = 4GB maximum addressable memory

This was a HUGE problem in the early 2000s when:

1. RAM was getting cheaper
2. Programs needed more memory
3. Games and applications were hitting the 4GB wall
4. People were putting 8GB or 16GB in their computers but 32-bit programs couldn't use it all!

This is why the transition to 64-bit was so important. With 64-bit addresses:

- 2⁶⁴ = 18,446,744,073,709,551,616 unique addresses
- That's 16 exabytes of theoretical addressable memory!

Consider this:

- Large Language Models are growing exponentially
- GPT-3 had 175 billion parameters
- GPT-4 is estimated to have trillions
- Quantum computing might completely change how we think about memory addressing

We might need to start thinking about 128-bit or even 256-bit addressing systems sooner than we thought! Imagine:

```
128-bit system: 2¹²⁸ bytes = 340,282,366,920,938,463,463,374,607,431,768,211,456 bytes
```

_scribbles furiously on floating parchment_

This is why understanding these fundamentals of memory addressing is so crucial - you're learning the building blocks that will help shape the future of computing!

Want to explore how current systems handle large memory requirements with virtual memory and paging?



A = 0x41 (65)
B = 0x42 (66)
C = 0x43 (67)
...
a = 0x61 (97)
b = 0x62 (98)
c = 0x63 (99)



```
'A' | 0x20 = 'a'
'B' | 0x20 = 'b'
```



- That weird HTTP request you sent? It's bytes!
- That JSON you parsed? It's bytes!
- That beautiful React component? Eventually... it's bytes!
- That Docker container? Guess what? BYTES!

```
Network Packets
    → Binary Data
        → Hex Values
            → ASCII Characters
                → Memory Addresses
                    → Machine Code
```

MEMORY BUS
```
CPU <===> Memory Controller <===> RAM
    [data bus = 64 bits wide]
```


REGISTERS

```
RAX, RBX, RCX, RDX (64-bit registers)
EAX, EBX, ECX, EDX (32-bit registers)
 AX,  BX,  CX,  DX (16-bit registers)
 AL,  BL,  CL,  DL (8-bit registers)
```

CACHES

```
L1 Cache (64KB) → SUPER FAST!
    L2 Cache (256KB) → Very Fast
        L3 Cache (Several MB) → Fast
            RAM (GB) → Slower
                DISK (TB) → Slowest
```


0x3C

ScratchPad



0x41 = 65 = A
0x42
0x43

0x4F = 80 = O
0x51 = 81 = P
0x5F = 96 = Z?
NO just bc its two behind "b", doesn't mean its Z because OF COURSE ASCII has to have special characters in between the upper and lower case 🙄

0x5A = 90 = z

91 \[
92 \
93 \]
94 [space]
85 _
96 \`


0xFF = 255
16 * 15 = 240
1 * 15 = 15


0xFF00
16 * 16 * 16 * 15 = 61440
16 * 16 * 15 = 3840
65280

0x1A2B3C
6 - 16 * 16 * 16 * 16 * 16 * 1 = 1048576
5 - 16 * 16 * 16 * 16 * 10 = 655360
4 - 16 * 16 * 16 * 2 = 8192
3 - 16 * 16 * 11 = 2816
2 - 16 * 3 = 48
1 - 12 = 12
1715004


0xDEAD 
4 16 * 16 * 16 * 13 = 53248
3 16 * 16 * 14 = 3584
2 16 * 10 = 160
1 13 
57005


0xBEEF
4 16 * 16 * 16 * 11 = 45056
3 16 * 16 * 14 = 3584
2 16 * 14 = 224
1 15

48879



8126
507
31
1

0x1F00

3840



16 * 16 * 16 = 4096

16 * 16 * 15 = 3840


7936 .    190 rem
14 rem


0xFEBE


2023
126 14
7

0x7E7


7  + 14 * 16 + 7 * 16 * 16

1792
224
7