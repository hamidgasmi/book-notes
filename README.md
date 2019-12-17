# Books' Notes
## 1. Write Great Code, Volume 1
by Randall Hyde, 2004

<details>
<summary>1. What You Need to Know to Write Great Code</summary>
</details>
<details>
<summary>2. Numeric Presentation</summary>

- Radix: Base 
- Binary representation in programming languages: 
    - MASM t assembler adds a suffix: 
        - 1001b = 1001B = 10 base 10 
        - 1001 = One hundredand one base (radix) 10 
- Hexadecimal representation: 
    - How to make the difference between the numbers DEAD, BEEF, FEED, DEAF from standard program identifiers
    - C, C++, C#, Java add a prefix: 0xDEAD 
    - MASM adds a sufix h or H and should beggin with a digit (0-9): 
        - 0A001h, 234H
        - Something obiguous like "dead" would be written "0deadh" 
- Numeric String Presentation: 
    - Reading/writing a number from/to a user’s consol involve a string to number conversion (cin >> i in C++) 
    - A conversion from/to a string to/from a number is low 
    - It requires multiple steps
    - E.g., Conversation of a string to an unsigned integer: 
        - (1) Initialize an integer variable to 0 
        - (2) If there are no digits in the string, then the algorithm is complete and the variable holds the numeric value 
        - (3) Fetch the next digit (going from left to right) from the string 
        - (4) Multiply the variable by then and then add the digit fetched in step (3) 
        - Go to step (2) 
    - Converting an integer to a string takes even more effort 
        - It involves divisions by 10 
        - Division is very slow 
    - Great programmer will be careful the use of numeric/string conversions
        - Only use them when necessary 
- Internal numeric Representation: 
    - Make sure that your program use data objects that the machine can represent efficiently 
    - A Bit: 
    - A Nibble:
        - 4 bits  
        - Most computer systems don’t provide efficient access to nibbles in memory 
    - A byte: 
        - 8 bits 
        - The smallest addressable Data item on many CPUs 
        - The CPU can efficiently retrieve data on a 8-bit boundary from memory 
        - It’s the smallest unit of a storage on most machines 
        - Many languages use bytes to represent objects that require fewer than 8 bits such as Boolean 
        - To describe bits within a bytes, a bit number is used: 
        - Bit 0: LO, the Low Order bit or Least Significant bit 
        - Bit 1: 
        - ...
        - Bit 7: HO, Highest Order or Most Significant bit 
    - A word: 
        - It has a different meaning depending on the CPU 
        - On some CPU, it’s a 16-bit Object 
        - On other CPU, it’s a 32-bit or 64-bit Object 
        - In the 80x86 terminology, it’s 16-bits quantity 
        - Bit number 0… 15, LO, HO 
    - A double word: 
        - It's also called: dword 
        - In the 80x86 terminology, it’s a 32-bit Object 
        - CPU handles efficiently objects up to a certain size (typically 32 or 64 bits) 
        - This doesn’t mean that we can’t work with larger objects 
        - It simply becomes less efficient to do so 
        - This is why you typically won’t see programme handling numeric objects much higher than about 128 or 256 bits
    - A Quad word: 64 bits 
    - A Long word: 128 bits (a convention in the book only) 
    - A tbyte: 
        - An 80-bit type that is on Intel 80x86 platforms 
        - The 80x86 CPU family uses tbyte variables to hold extended precision floating-point values and certain binary-coded decimal (BCD) values
- Signed and Unsigned Numbers: 
    - The two’s complement numbering system: 
        - It uses the HO bit as a sign bit 
        - With n digits, we can represent -2^[n -1] to +2^[n-1] - 1 
        - E.g., with a 16-bit number 0x8000 (1000_0000_0000_0000b): it's the smalled 16-bit negative number
    - Negation Algorithm: 
        - Invert all the bits in the number 
        - Add +1 and Ignore any overflow 
        - E.g. 1, 0x0005 (+5) => (Inversion) 0xFFFA =>(+1) 0xFFFB (-5) 
        - E.g. 2, 0xFFFB (-5) => 0x0004 => 0x0005 (+5) 
        - E.g. 3, 0x8000 (smallest negative number) => 0x7FFF => 0x8000 (-32,768) => smallest negative number in n-bit doesn't have a positive representation (see n-bit representation limit above) 
- Some useful Properties of Binary Numbers: 
    - If LO bit = 1 in a binary (integer) => odd 
    - If LO bit = 0 in a binary (integer) => even 
    - If the LO n bit of a binary number all contain 0 => the number is evenly divisible by 2^n 
    - If a binary value contains a 1 in bit position n and 0s everywhere else => it’s equal to 2^n 
    - If a binary value contains all 1s from Bit 0 to bit n - 1 and 0 elsewhere => it’s equal to 2^n - 1 

</details>

