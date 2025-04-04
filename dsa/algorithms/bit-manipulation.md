# Bit Manipulation

---

Bit masking

Get

set

clear

toggle

---

# Binary numbers

Binary numbers are base-2

![101101 = 45](Untitled%206.png)

101101 = 45

---

# Addition

![0110 + 0010 = 1000 or 6 + 2 = 8](Untitled%207.png)

0110 + 0010 = 1000 or 6 + 2 = 8

Add from right to left ,

If is 1+1 = 2 , becomes 0 and add 1 to next column (left) 

---

# Subtraction

![0110 - 0011 = 0011 or 6 - 3 = 3](Untitled%208.png)

0110 - 0011 = 0011 or 6 - 3 = 3

Subtract from right to left

If it is 0 - 1 , borrow from left 

![Untitled](Untitled%209.png)

---

# Multiplication

![0011*0101 = 1111 or 3*5 = 15](Untitled%2010.png)

0011*0101 = 1111 or 3*5 = 15

0011 is the multiplicand 

0101 is the multiplier

1. Multiply from right to left the multiplier digit to the mulitplicand digits 
2. Make sure that each multiplied result is in it corresponding places 
3. Sum the multiplied results 

---

# Division

???????

---

# AND

Bitwise AND Operator 

&

Returns 1 if both the bits are 1 else 0.

![Untitled](Untitled%2011.png)

---

# OR

Bitwise OR Operator 

|

Returns 1 if either the bits are 1 else 0.

![Untitled](Untitled%2012.png)

---

# NOT

Bitwise OR Operator 

~

Inverse the bits

![Untitled](Untitled%2013.png)

---

# XOR

Bitwise OR Operator 

^

Returns 1 if only one of the bits is 1

![Untitled](Untitled%2014.png)

---

# Left Shift

Bitwise left shift operator

<<

Shift bits to left and fills right with 0

![Untitled](Untitled%2015.png)

Shifting a single bit to the left by one place doubles its value

![Untitled](Untitled%2016.png)

![Untitled](Untitled%2017.png)

---

# Right Shift

Bitwise left shift operator

>>

Shift bits to right and delete those values that fall off

![Untitled](Untitled%2018.png)

Shifting a single bit to the right by one place halfs its value 

![Untitled](Untitled%2019.png)

![Untitled](Untitled%2020.png)

---

# Signed vs Unsigned numbers

## Signed ( either positive or negative )

- Left most bit is the sign bit
    - 0 means positive
    - 1 means negative

## Unsigned ( only positive )

---

# 2’s complement

> Why?
 Because using **Sign-Magnitude method** is only good for representing positive and negative numbers , and but does not work well in computating them(addition, subtraction)
> 

![Untitled](Untitled%2021.png)

1. Write out the positive of number
2. Invert the bits , add 1 
3. Add sign bit to front

![Untitled](Untitled%2022.png)

---

# Negative number