# Data Types

- Defines a set of possible values (the domain) and the pre-defined operations
- Defines how to interpret bit strings of various lengths

## Primitive

- *Integer*- almost always an exact reflection of hardware
    - python has unlimited precision ints (other languages limit based on number of bits)
- *Floats*- model real numbers (but only as approximations)
    - IEEE Floating Point Standard 754
    - float- usually 32 bits
    - double- double the precision so often 64 bits
- *Complex*- two floats (1 real, 1 complex)
- *Decimal*- attempts were made to store a fixed number of decimal digits in coded form (Binary Coded Decimal) where each digit is encoded separately but was overall a failure 
    - Pros: increased accuracy since each digit is represented by 4 bits
    - Cons: limited range, wastes memory, not all CPUs have direct hardware support
    - Used by business applications for representing money (e.g. C# has a double and decimal type which has more precision)
- *Boolean*- implemented as a byte due to byte-addressable memory (can't address single bits)
    - Pros: readability in logic expressions (as opposed to interpreting numeric expressions)
- Character- 
    - ASCII is a 7-bit character set which is limited and inadequate in the modern age
    - UNICODE 
        - initially fixed 16-bit representation 
        - includes the base multilingual plane for non-roman characters
        - backwards compatible with ASCII
        - still inadequate
    - UTF-8 
        - variable length for bit representation 
        - most widely used