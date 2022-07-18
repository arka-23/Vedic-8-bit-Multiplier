# Vedic-8-bit-Multiplier
This repository contains the proposed design and simulated results for a 8 bit Vedic Multiplier circuit using the Vedic Mathematics (Urdhva Tiryagbhyam sutra)



# Table of Contents
   * [Abstract](#abstract)
  * [Circuit Design Details](#circuit-design-details) 
 * [Verilog Implementation](#verilog-implementation) 
 * [References](#references)


## Abstract

Design provided for an 8 bit Vedic Multiplier circuit using the Vedic Mathematics (Urdhva Tiryagbhyam sutra) for generating the partial products. The partial product addition in Vedic multiplier is realized using carry-skip technique.
An 8-bit multiplier is realized using four 4-bit multiplier and three ripple carry adders. 

## Circuit Design Details

The Vedic logic used is the “Urdhva Triyakbhyam Sutra”. Urdhva – Triyakbhyam is the general formula applicable to
all cases of multiplication of a large number by another large number. It means vertically and crosswise.  


The method is explained for two, 2 bit numbers A
and B where A = a1a0 and B = b1b0 as shown in Fig. 2.
Firstly, the least significant bits are multiplied which gives the
least significant bit of the final product (vertical). Then, the
LSB of the multiplicand is multiplied with the next higher bit
of the multiplier and added with, the product of LSB of
multiplier and next higher bit of the multiplicand (crosswise).
The sum gives second bit of the final product and the carry is
added with the partial product obtained by multiplying the
most significant bits to give the sum and carry. The sum is the
third corresponding bit and carry becomes the fourth bit
Of the final product.

The 2X2 Vedic multiplier module is implemented using four 2 - input AND gates & two half-adders which is displayed in the block diagram in Fig. 2. 

The 4x4 bit Vedic multiplier module is implemented using
four 2x2 bit Vedic multiplier modules as discussed in Fig. 3.


Thus, following similar steps and using the fundamental of Vedic multiplication, taking four
bits at a time and using 4 bit multiplier blocks we
can perform the multiplication. The outputs of 4x4 bit
multipliers are added accordingly to obtain the final product.
Here total four 4-bit multipliers and three 8 bit Ripple-Carry Adders are required as shown in Fig. 4.


## Reference Circuit Diagrams and Outputs

<p align="center">
  
  ![image](https://user-images.githubusercontent.com/70422874/179449293-c597eaa3-295f-47bf-bb82-f91903bd59a9.png)
  
  Fig. 1: Working of Bits
</p>

![image](https://user-images.githubusercontent.com/70422874/179449346-d5fa9e54-748b-4af9-83ff-96e0afd6cb02.png)

  Fig. 2: Vedic 2x2 Multiplier Hardware Design


![image](https://user-images.githubusercontent.com/70422874/179449367-07397b01-1d4c-488e-a663-33d7343f3bfa.png)

  Fig. 3: Vedic 4x4 Multiplier Block Diagram


![image](https://user-images.githubusercontent.com/70422874/179449398-edd972cc-3428-401b-976b-578f1cd215d0.png)

  Fig. 4: 8-Bit Vedic Multiplier Block Diagram


## Verilog Implementation

Verilog Code:

   ![image](https://user-images.githubusercontent.com/70422874/179450188-8f98e279-e12c-4afe-8475-7ebdf930d477.png)
   
   ![image](https://user-images.githubusercontent.com/70422874/179450290-9a6069ef-77e5-4e3a-9226-dfc06a7b550b.png)

   ![image](https://user-images.githubusercontent.com/70422874/179450351-b52df147-76f0-4f8c-9f61-fc297425b449.png)
   
   ![image](https://user-images.githubusercontent.com/70422874/179450416-b11e5694-9f6e-46e1-844c-2455da1c81da.png)

Verilog Testbench:

![image](https://user-images.githubusercontent.com/70422874/179450487-9c652875-6d90-498c-987b-cbc2fcb44779.png)

Outputs:

![image](https://user-images.githubusercontent.com/70422874/179450541-db95545a-b0b6-43b9-8d99-318a31a5433b.png)


## References
 - Douglas A. Pucknell, Kamran Eshraghian, “ Basic VLSI Design”, PHI, Third Edition.
 - Neil Weste, Harris \& Banerjee, CMOS VLSI   Design: A Circuits and Systems Perspective,   Edition, Pearson Education, Boston.
 - http://vlsinano.blogspot.com/2018/03/vedic-multiplier-verilog-code-and.html


