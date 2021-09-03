# Antman

## Fundamentals

You need to know about C types difference their size bitwise operators and more:

### Types Signed and Unsigned and their sizes

```c
char // is (1 byte|8 bits)
short int // is (2 bytes|16bits) or (4 bytes|32bits)
int // is (4 bytes|32bits)
long // is (4 or 8 bytes|32 or 64bits) between the implementations
long long // Is (8|64bits) bytes if the machine is a 32bits otherwise it will be a 32bit
```

But to be sure about the number of bytes we use we use `stdint` so we can use directly:
```c
int8_t
int16_t
int32_t
int64_t
```

Why should I use unsigned when working with bitwise ?

It is easier to work with otherwise you would aknowledge that for example on a `char` aka `int8_t` you can go from -126 to 127 and that the ascii table goes from 0 to 127 and the other characters are below 0
So that would mean that to go to the 128 character you would go to -128 why -128 ?
It is because -1 is represented as:

8bits for a char:
--------------------------------
|---------------|--------------|
| Integer Value | Binary Value |
|---------------|---------------
| 0             | 0b00000000   |
|---------------|---------------
| 127           | 0b01111111   |
|---------------|---------------
| 128           | 0b10000000   |
|---------------|---------------
| -128          | 0b10000000   |
|---------------|---------------
| -127          | 0b10000001   |
|---------------|---------------
| -1            | 0b11111111   |
|---------------|--------------|
--------------------------------

To represent a binary number in negative:
Formula: `(-(maximum_value_of_the_bitset + 1) + sum_of_the_last_7_bits)`
Examples:
```
-128 = (-128 + 0b00000000) = (-128 + 0)
-127 = (-128 + 0b00000001) = (-128 + 1)
-1   = (-128 + 0b11111111) = (-128 + 127)
-40  = (-128 + 0b01011000) = (-128 + 88)
```

So unsigned number are easier to work with because the bit of sign is ignored and is used to compute the number
The char that was -128 to 127 is now an unsigned char going from 0 to 255

So to go from 127 to -128 you do not need to go to negative that would be error prone

Even tough on a char 127 + 1 = -128 it is much prefered and less error prone to do 127 + 1 = 128

Also think to use :
```c
uint8_t == unsigned char
uint16_t
uint32_t
uint64_t
```

Also consider that when you use an int is equivalent to `char [4]` because `sizeof(char) == 1` and `sizeof(int) == 4` so `char[4] == sizeof(char) * 4 == 4`

### Bitwise Operators

Basic operators:
```
108 = 0b01101100
82  = 0b01010010

108 & 82 = 64

  01101100
& 01010010
----------
  01000000


Xor operator
108 ^ 82 = 62
  01101100
^ 01010010
----------
  00111110

Or operator
108 | 82 = 126
  01101100
| 01010010
----------
  01111110
```

Special operators:
```
<< Operator

0b1 << 1 = 0b10
0b1 << 2 = 0b100
0b1 << 3 = 0b1000

0b001101 << 1 = 0b011010
0b001101 << 2 = 0b110100
0b001101 << 3 = 0b1101000

>> Operator
0b100 >> 1 = 0b10
0b100 >> 2 = 0b1
0b100 >> 3 = 0b0

0b001101 >> 1 = 0b00110
0b001101 >> 2 = 0b00011
0b001101 >> 3 = 0b00001
```

## Algorithms

Here are some algorithms you can use to do the project:
    - bzip2
    - Finite state Entropy
    - Huffman Coding (Is inneficient alone but can be paired to a lot of other algorithms to make powerful things)
    - LZ77 and LZ78 (Uses Huffman coding and passes +50% of the tests when it is well implemented)
    - ZSTD
