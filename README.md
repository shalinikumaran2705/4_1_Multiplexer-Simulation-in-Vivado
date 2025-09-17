# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
`timescale 1ns / 1ps
module mux4(I,s,Y);
input [3:0]I;
input [1:0]s;
output Y;
wire [4:1]w;
and (w[1],~s[1],~s[0],I[0]);
and (w[2],~s[1],s[0],I[1]);
and (w[3],s[1],~s[0],I[2]);
and (w[4],s[1],s[0],I[3]);
or (Y,w[1],w[2],w[3],w[4]);
endmodule
```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
module mux4_tb;
reg [3:0]I;
reg [1:0]s;
wire Y;
mux4 uut(I,s,Y);
initial 
begin
I=4'b0111;
s=2'b00;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b01;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b10;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b11;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
$finish;
end 
endmodule
```
## Simulated Output Gate Level Modelling
![WhatsApp Image 2025-09-17 at 13 44 23_83651aa6](https://github.com/user-attachments/assets/90f6735b-7954-42e1-a32d-52700b04ce61)

_______ Here Paste the Simulated output  ___________

---
### 4:1 MUX Data flow Modelling
```verilo
`timescale 1ns / 1ps
module MUX4_1(I,s,Y);
input [3:0]I;
input [1:0]s;
output Y;
wire [4:1]w;
assign w[1]=(~s[1])&&(~s[0])&&I[0];
assign w[2]=(~s[1])&&(s[0])&&I[1];
assign w[3]=(s[1])&&(~s[0])&&I[2];
assign w[4]=(s[1])&&(s[0])&&I[3];
assign Y=w[1]||w[2]||w[3]||w[4];
endmodule
```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
module MUX4_1_tb;
reg [3:0]I;
reg [1:0]s;
wire Y;
MUX4_1 uut(I,s,Y);
initial 
begin
I=4'b0111;
s=2'b00;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b01;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b10;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
s=2'b11;
#10;
$display("selection is %b %b, output : %b",s[0],s[1],Y);
$finish;
end 
endmodule
```
## Simulated Output Dataflow Modelling
![WhatsApp Image 2025-09-17 at 13 54 36_0fd813a8](https://github.com/user-attachments/assets/fcf27540-baad-4d4f-88f8-d62481bb7212)


_______ Here Paste the Simulated output  ___________

---
### 4:1 MUX Behavioral Implementation
```verilog
`timescale 1ns / 1ps
module MUX_4_1(I,s,Y);
input [3:0]I;
input [1:0]s;
output reg Y;
always @(I,s)
      begin
         case(s)
         2'b00:Y=I[0];
         2'b01:Y=I[1];
         2'b10:Y=I[2];
         2'b11:Y=I[3];
         endcase
      end   
endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
module MUX_4_1tb;
reg [3:0]I;
reg[1:0]s;
wire Y;
MUX_4_1 uut(I,s,Y);
initial
begin
I=4'b0111;
s=2'b00;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b01;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b10;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b11;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
$finish;
end
endmodule
```
## Simulated Output Behavioral Modelling
![WhatsApp Image 2025-09-17 at 13 57 37_2d0b3b91](https://github.com/user-attachments/assets/4841e4bd-66da-42b4-8254-d3f916ba0fb4)



_______ Here Paste the Simulated output  ___________


### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)
```verilog

`timescale 1ns / 1ps
module muxs4(Y, I0, I1, s);
  input I0, I1, s;
  output Y;
  wire w1, w2, w3;
  not (w1, s);
  and (w2, I0, w1);
  and (w3, I1, s);
  or  (Y, w2, w3);
endmodule
module mux4(Y, I, s);
  output Y;
  input [3:0] I;
  input [1:0] s;
  wire w1, w2;
  mux2to1 m1(w1, I[0], I[1], s[0]);
  mux2to1 m2(w2, I[2], I[3], s[0]);
  mux2to1 m3(Y, w1, w2, s[1]);
  endmodule
```
### Testbench Implementation
```verilog
module mux4_tb;
reg [3:0]I;
reg [1:0]s;
wire Y;
mux4 uut(Y,I,s);
initial
begin
I=4'b0111;
s=2'b00;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b01;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b10;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
s=2'b11;
#10;
$display("selection is %b %b ,output : %b",s[1],s[0],Y);
$finish;
end
endmodule
```
## Simulated Output Structural Modelling
![WhatsApp Image 2025-09-17 at 14 09 56_d26a3911](https://github.com/user-attachments/assets/adaaa76a-d62a-4266-a36e-1deb42992619)


_______ Here Paste the Simulated output  ___________

---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

