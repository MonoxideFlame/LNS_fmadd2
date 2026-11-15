# Objective

The hope is to use PWL interpolation to obviate the need for a multiplier circuit in LNS arithmetic for 12 bit arithmetic, compared to fp12. The question is ultimately whether the extra lookup tables overshoot the area of a 12x12 multiplier and FP edge case handling.

EDA Playground link
https://edaplayground.com/x/kWXT


This unique method of doing PWL involves choosing the intervals as carefully as possible to make all the weights have a small hamming weight (2 bits high), so the computation becomes easier.

y = (x - a)*w + b;

a is carefully chosen so that w is a word with 2 high bits. So the multiplication becomes two shifts and an add. 

The relative errors stay within 2 percent for an addition. This is within a deviation of 1 LSB, so it is pretty good. 



# LNS Arithmetic Basics:


We represent a real number as a fixed point logarithm with 1 sign bit, 4 integer bits, and 7 fractional bits. This gives a precision to 0.5% roughly. 

Multiplication and division are lightning fast. Addition and subtraction require tables to convert the following values:


```
a + b  = a + log(1 + 2^(b - a))
a - b  = a + log(1 - 2^(b - a))
```


These tables are a problem. So the PWL trick was used to refactor them to shrink the size of the LUT. 

The synthesized netlist is roughly the same size as the FP12 one. This may be a replacement. 
