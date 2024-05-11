

SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

DATE:

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:

Xilinx 14.7
Spartan6 FPGA

PROCEDURE:
```
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.
```

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

VERILOG CODE:
```
module srflipflop(clk,res,s,r,q);
input clk,res,s,r;
output reg q;
always@(posedge clk)
begin
if(res)
q<=1'b0;
else begin
case({s,r})
2'b00:q<=q;
2'b01:q<=1'b0;
2'b10:q<=1'b1;
2'b11:q<=1'bx;
default:q<=1'bx;
endcase
end
end
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/926b0c0f-91db-45d5-b4cb-4695cdded668)





JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

VERILOG CODE:

```
module jk(clk,res,j,k,q);
input clk,res,j,k;
output reg q;
always@(posedge clk)
begin
if(res)
q<=1'b0;
else begin
case({j,k})
2'b00:q<=q;
2'b01:q<=1'b0;
2'b10:q<=1'b1;
2'b11:q<=~q;
default:q<=~q;
endcase
end
end
endmodule
```
OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/6942baf8-ba7b-4cc5-9362-d1b20388e75e)



T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

VERILOG CODE:
```
module tflipflop(clk,res,q,t);
input clk,res,t;
output reg q;
always@(posedge clk)
begin
if(res)
q<=1'b0;
else
begin
if(res)
q<=0;
else if(t)
q<=~q;
else
q<=q;
end
end
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/3d9e81c1-9ace-4162-a187-1896a94a9b07)



D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

VERILOG CODE:
```
module dflipflop(c,r,d,q);
input c,r,d;
output reg q;
always @(posedge c)
begin
if(r)
q<= 1'b0 ;
else
q<=d;
end
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/f96c726b-515a-48c7-97a4-2a8b38495801)




COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

4-BIT UPCOUNTER

VERILOG CODE:
```
module upcounter(clk,rest,count);
input clk,rest;
output [3:0]count;
reg[3:0]count;
always@(posedge clk)
begin
if(rest)
count<=4'b0;
else
count<=count+1;
end
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/51ca4f89-ae21-4f30-8d5a-4a519b42a305)

4-BIT DOWN COUNTER

VERILOG CODE:
```
module downcounter(clk,rest,count);
input clk,rest;
output [3:0]count;
reg[3:0]count;
always@(posedge clk)
begin
if(rest)
count<=4'b0;
else
count<=count-1;
end
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/40525e6a-dd68-431d-8dcc-f0a7c3b06ef0)

MOD10 COUNTER:

VERILOG CODE:
```
module mod10(clk,res,count);
input clk,res;
output [3:0]count;
reg [3:0]count;
always@(posedge clk)
begin
if(res|count==4'd9)
count<=4'b0;
else
count<=count+1;
end 
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/63618a5b-1489-4b11-836e-29c944871834)

RIPPLE CARRY COUNTER:

VERILOG CODE:
```
module jkff(j,k,clock,reset,q,qb);
input j,k,clock,reset;
output reg q,qb;
always@(negedge clock)
begin
case({reset,j,k})
3'b100 :q=q;
3'b101 :q=0;
3'b110 :q=1;
3'b111 :q=~q;
default :q=0;
endcase
qb<=~q;
end
endmodule
module ripple_count(j,k,clock,reset,q,qb);
input j,k,clock,reset;
output wire [3:0]q,qb;
jkff JK1(j,k,clock,reset,q[0],qb[0]);
jkff JK2(j,k,q[0],reset,q[1],qb[1]);
jkff JK3(j,k,q[1],reset,q[2],qb[2]);
jkff JK4(j,k,q[2],reset,q[3],qb[3]);
endmodule
```

OUTPUT:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/159146834/ebb377e9-44f1-4b1b-b2bd-2699b92e2992)





RESULT

Thus ,the given JK flipflop, SR flipflop, T flipflop, D flipflop ,counter are simulated and synthesis are executed successfully



