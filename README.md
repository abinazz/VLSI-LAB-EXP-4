# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

# APPARATUS REQUIRED:
Vivado 2023.1.
**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  

# PROCEDURE:

Open Vivado: Launch Xilinx Vivado software on your computer.

Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# PROGRAM:
# SR FLIP FLOP
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
OUTPUT WAVEFORM
 ![ABI-SR](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/1174e6bf-2596-4519-8cc7-00e7d40a0d19)
 # JK FLIP FLOP
 ```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```
# OUTPUT
![ABI-JK](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/b5fd1eef-dcba-44b7-b452-77bd4e368909)
# T FLIP FLOP
```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```
# OUTPUT
![ABI- T FLIP](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/486104d1-3630-4d8d-b7e5-738fb2ea01e7)
# D FLIP FLOP
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
# OUTPUT
![ABI-D FLIP](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/5d12e7c2-6859-42c4-93f8-fcbb7bb333fa)
# COUNTER
# UPDOWN COUNTER
```
module updowncounter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if (updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
# OUTPUT
![ABI-UP COUN](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/067189c4-816a-4c17-8548-31cb9eaf7132)
# MOD10 COUNTER
```
module mod10counter(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
# OUTPUT
![ABI-DOWN](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/ca862d6f-ae18-4f98-a827-0d9d2bc954ee)
# RIPPLE COUNTER
```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```
# OUTPUT
![ABI-RIPPLE](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/165630162/9e49cbd9-9f7a-495f-b566-34489381f8eb)


# RESULT
Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1 is simulated and synthesised.

