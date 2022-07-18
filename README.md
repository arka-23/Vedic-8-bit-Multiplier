# Vedic-8-bit-Multiplier
This repository contains the proposed design and simulated results for a 8 bit Vedic Multiplier circuit using the Vedic Mathematics (Urdhva Tiryagbhyam sutra)



# Table of Contents
   * [Abstract](#abstract)
  * [Circuit Design Details](#circuit-design-details) 
 - [Verilog Implementation](#verilog-implementation) 
 - [References](#references)


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

![image](https://user-images.githubusercontent.com/70422874/179449293-c597eaa3-295f-47bf-bb82-f91903bd59a9.png)
<p align="center">
  Fig. 1: Working of Bits
</p>

![image](https://user-images.githubusercontent.com/70422874/179449346-d5fa9e54-748b-4af9-83ff-96e0afd6cb02.png)
<p align="center">
  Fig. 2: Vedic 2x2 Multiplier Hardware Design
</p>

![image](https://user-images.githubusercontent.com/70422874/179449367-07397b01-1d4c-488e-a663-33d7343f3bfa.png)
<p align="center">
  Fig. 3: Vedic 4x4 Multiplier Block Diagram
</p>

![image](https://user-images.githubusercontent.com/70422874/179449398-edd972cc-3428-401b-976b-578f1cd215d0.png)
<p align="center">
  Fig. 4: 8-Bit Vedic Multiplier Block Diagram
</p>

##Verilog Implementation

Verilog Code:

module vedic8x8(a, b, result);

    input  [7:0] a,b;
    output [15:0] result;
    wire [15:0] result;

wire [7:0] temp1;
wire [7:0] temp2;
wire [7:0] temp3;
wire [9:0] temp4;
wire [9:0] temp5;
wire [7:0] temp6;
wire [7:0] temp7;

vedic4x4 M1(a[3:0], b[3:0], temp1);
assign result[3:0] = temp1[3:0];

vedic4x4 M2(a[7:4], b[3:0], temp2);
vedic4x4 M3(a[3:0], b[7:4], temp3);

adder10 A1({2'b00, temp2}, {2'b00,temp3}, temp4);
adder10 A2(temp4, {6'b000000, temp1[7:4]}, temp5);
assign result[7:4] = temp5[3:0];

vedic4x4 M4(a[7:4], b[7:4], temp6);
adder8 A3(temp6, {2'b00,temp5[9:4]}, temp7);

assign result[15:8] = temp7;

endmodule

module vedic4x4(a, b, result);

    input  [3:0] a,b;
    output [7:0] result;
    wire [7:0] result;

wire [3:0] temp1;
wire [3:0] temp2;
wire [3:0] temp3;
wire [5:0] temp4;
wire [5:0] temp5;
wire [3:0] temp6;
wire [3:0] temp7;
wire [5:0] w1;

vedic_2x2 V1(a[1:0], b[1:0], temp1);
assign result[1:0] = temp1[1:0];

vedic_2x2 V2(a[3:2], b[1:0], temp2);
vedic_2x2 V3(a[1:0], b[3:2], temp3);

assign w1 = {4'b0000, temp1[3:2]};

adder6 A1({2'b00, temp3}, {2'b00, temp2}, temp4);
adder6 A2(temp4, w1, temp5);

assign result[3:2] = temp5[1:0];

vedic_2x2 V4(a[3:2], b[3:2], temp6);

adder4 A3(temp6, temp5[5:2], temp7);
assign result[7:4] = temp7;


endmodule

module vedic_2x2 (a, b, result);
    input [1:0] a,b;
    output [3:0] result;

    wire [3:0] w;
    
    
    assign result[0]= a[0]&b[0];
    assign w[0]     = a[1]&b[0];
    assign w[1]     = a[0]&b[1];
    assign w[2]     = a[1]&b[1];

    halfAdder H0(w[0], w[1], result[1], w[3]);
    halfAdder H1(w[2], w[3], result[2], result[3]);    
    
endmodule

module halfAdder(a,b,sum,carry);
    input a,b;
    output sum, carry;

assign sum   = a ^ b;
assign carry = a & b;

endmodule

module adder4(a,b,sum);

input [3:0] a,b;
output [3:0] sum;
wire [3:0] sum;

assign sum = a + b;

endmodule

module adder6(a,b,sum);

input [5:0] a,b;
output [5:0] sum;
wire [5:0] sum;

assign sum = a + b;

endmodule

module adder8(a,b,sum);

input [7:0] a,b;
output [7:0] sum;
wire [7:0] sum;

assign sum = a + b;

endmodule

module adder10(a,b,sum);

input [9:0] a,b;
output [9:0] sum;
wire [9:0] sum;

assign sum = a + b;

endmodule
