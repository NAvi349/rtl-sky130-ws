# Table of Contents

- [Day 1](#day-1)
  * [iverilog](#iverilog)
  * [Yosys](#yosys)
    + [Logic Synthesis](#logic-synthesis)
    + [Setup and Hold time](#setup-and-hold-time)
    + [Fast cells vs Slow cells](#fast-cells-vs-slow-cells)
    + [Yosys](#yosys-1)
- [Day 2](#day-2)
  * [dot Lib file](#dot-lib-file)
  * [Hierarchial vs Flat Synthesis](#hierarchial-vs-flat-synthesis)
    + [Hierarchial Synthesis](#hierarchial-synthesis)
    + [**Why NAND gate is used for OR/NOR gate implementation?**](#why-nand-gate-is-used-for-ornor-gate-implementation)
    + [Flat Synthesis](#flat-synthesis)
    + [Sub-module level synthesis](#sub-module-level-synthesis)
  * [Flip Flops and Flop coding styles](#flip-flops-and-flop-coding-styles)
    + [Glitches and Hazards](#glitches-and-hazards)
    + [Asynchronous Vs Synchronous](#asynchronous-vs-synchronous)
    + [DFF with Asynchronous Reset](#dff-with-asynchronous-reset)
    + [DFF with Asynchronous Set](#dff-with-asynchronous-set)
    + [DFF with Synchronous Reset](#dff-with-synchronous-reset)
  * [Optimizations](#optimizations)
- [Day 3](#day-3)
  * [Intro to Optimizations](#intro-to-optimizations)
  * [Combinational Logic Optimizations lab](#combinational-logic-optimizations-lab)
    + [Example 1](#example-1)
    + [Example 2](#example-2)
    + [Example 3](#example-3)
    + [Example 4](#example-4)
    + [Example 5](#example-5)
    + [Example 6](#example-6)
  * [Sequential Optimizations](#sequential-optimizations)
    + [Example 1](#example-1-1)
    + [Example 2](#example-2-1)
    + [Example 3](#example-3-1)
    + [Example 4](#example-4-1)
    + [Example 5](#example-5-1)
  * [Unused outputs optimizations](#unused-outputs-optimizations)
    + [Example 1](#example-1-2)
    + [Example 2](#example-2-2)
- [Day 4](#day-4)
  * [Gate Level Simulation (GLS)](#gate-level-simulation-gls)
  * [Synthesis Simulation Mismatch](#synthesis-simulation-mismatch)
  * [Ternary operator Mux](#ternary-operator-mux)
  * [Bad MUX](#bad-mux)
  * [Blocking Statement Synthesis Simulation Mismatch](#blocking-statement-synthesis-simulation-mismatch)
- [Day 5](#day-5)
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [References](#references)


# Day 1
## iverilog
```
mkdir rtlws
cd ./rtlws
ls
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop
cd ./https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop
cd ./verilog_files
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```
![image](https://user-images.githubusercontent.com/66086031/165417764-c1872ac3-7fa2-4d1e-ac86-1f00ebe2b23d.png)
![image](https://user-images.githubusercontent.com/66086031/165417808-4277ae59-869d-4bfc-afad-448949b707d1.png)
![image](https://user-images.githubusercontent.com/66086031/165417995-089755e8-546b-477b-bbcb-506572ff6a28.png)
![image](https://user-images.githubusercontent.com/66086031/165419193-cde4de4c-3e65-4f57-be18-92b260c43303.png)
![image](https://user-images.githubusercontent.com/66086031/165419867-1570fad8-5931-4101-a43f-8a62b0a14d48.png)
![image](https://user-images.githubusercontent.com/66086031/165419920-0d55d648-ba66-405f-b6e4-fcddf89c179c.png)
![image](https://user-images.githubusercontent.com/66086031/165420217-efe5c5ec-7f77-4333-ac59-01766f1f71e4.png)
![image](https://user-images.githubusercontent.com/66086031/165420579-2c0c7b6e-54de-4b08-8855-5103f11a869b.png)
![image](https://user-images.githubusercontent.com/66086031/165420634-55d8522f-9404-4dc0-bf6a-9daa2a8ceef0.png)

## Yosys
It is a synthesizer which converts RTL design to a synthesized netlist
![image](https://user-images.githubusercontent.com/66086031/165420828-fa4e2152-76d4-4449-a350-98f6fc32ec3f.png)
netlist is the representation of the design in the form standard cells
![image](https://user-images.githubusercontent.com/66086031/165420934-cb78ab56-534e-4309-b96c-6d2048d850d9.png)
Same testbench can be used for RTL Design and Synthesized netlist simulation

### Logic Synthesis
RTL Definition:
![image](https://user-images.githubusercontent.com/66086031/165421301-73bd1fe9-4ce3-4519-bf49-ca6b699e2053.png)
.lib - library collection of all the standard cells, different versions of the same gate is present

### Setup and Hold time

#### Setup Time (Max Delay) Constraints

![image](https://user-images.githubusercontent.com/66086031/166118620-dd932eef-2e14-4689-a24d-d1e1e2098bcb.png)

* We need fast cells to satisfy Max Delay constraints.

#### Hold Time (Min. Delay Constraints

![image size="50%"](https://user-images.githubusercontent.com/66086031/166118808-82e6ff9a-34c3-4cbc-b40a-23cc1f2faa43.png)

* We need slow cells to satisfy hold time constraints

### Fast cells vs Slow cells
(Replace this image with text)
![image](https://user-images.githubusercontent.com/66086031/165422097-0aa73586-985a-4e18-8b3d-14c0edc69679.png)

![image](https://user-images.githubusercontent.com/66086031/165422232-94ce499f-ff06-4971-be92-f4d972400545.png)

### Yosys


**Steps:**
i. Include(read) the library and the verilog file

![image](https://user-images.githubusercontent.com/66086031/165503013-3b7eef02-4c3a-43ce-a34e-1818ec314085.png)

ii. Select top level module to Synthesize

![image](https://user-images.githubusercontent.com/66086031/165505251-ba96fa2f-72ca-4e5d-a772-0c67fe8eeac2.png)

iii. From the RTL Design(Verilog) generate gate-level netlist. 
iv. Then, map the synthesized netlist with the standard cell libraries **(Technology Mapping)**

![image](https://user-images.githubusercontent.com/66086031/165506961-c02ebcf8-a8d5-4bf4-a916-7bbf81bccc08.png)

iv. View the logic

![image](https://user-images.githubusercontent.com/66086031/165505986-34f1a631-1e4b-4529-b4a5-500c4eef4380.png)

v.  Generate (Write) verilog file for the synthesized(mapped) netlist

![image](https://user-images.githubusercontent.com/66086031/165508485-d74c18a2-9b0c-4bd7-b5d4-2e61f6ff9d0a.png)

**Code:**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr good_mux_netlist.v 
!gvim good_mux_netlist.v
```



![image](https://user-images.githubusercontent.com/66086031/165507626-7e254cc9-7c8b-48fb-b60e-ca9c87f9a3e4.png)


# Day 2
## dot Lib file
```
gvim ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
![image](https://user-images.githubusercontent.com/66086031/165761546-d37de039-34c9-49dc-993e-628933e782bc.png)

* tt - typical process
* 25C - optimal working temperature in 25 degrees
* 1v8 - voltage
* dot Lib contains standard cell features and specification
* Also specifies the leakage power and also the timing information for different input combinations 
* **insert image of leakage power formula**

## Hierarchial vs Flat Synthesis
![image](https://user-images.githubusercontent.com/66086031/165768331-d2313630-10c8-4308-9543-9f72863aca2f.png)

### Hierarchial Synthesis
```
cd ./verilog_files
yosys
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
write_verilog multiple_modules_hier.v
!gvim multiple_modules_hier.v
```
![image](https://user-images.githubusercontent.com/66086031/165770272-ac8ae53a-7146-4d8c-a458-9123832d3666.png)
![image](https://user-images.githubusercontent.com/66086031/165771177-5ac41a3a-e34e-4af6-aa23-8ee368407219.png)
![image](https://user-images.githubusercontent.com/66086031/165775940-6526ed05-9ecb-4665-9c27-757cdcec53b3.png)

* The hierarchy of the design is preserved.
* The structure of the submodules in the original design are preserved in the final synthesized (verilog) file.

### Why NAND gate is used for OR/NOR gate implementation?

* The logical effort of a NAND gate is less than that of an equivalent NOR gate.
* ![image](https://user-images.githubusercontent.com/66086031/166118137-1b1d4cb7-25b2-4ced-ad08-ec6fd74f879b.png)
* Logical effort - amount of current to drive a logic gate


### Flat Synthesis

```
flatten
write_verilog -noattr multiple_modules_flat.v
!gvim multiples_modules_flat.v
```
* Hierarchies are removed.
* No submodules are present in the (synthesized) verilog description
![image](https://user-images.githubusercontent.com/66086031/165787631-693182aa-a0d9-48bc-a7f3-9aec425389b1.png)
![image](https://user-images.githubusercontent.com/66086031/165785815-459eef54-a2ba-4506-8186-255477f0ed90.png)

### Sub-module level synthesis
```
yosys
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top submodule1
show
```
* This is useful when when we have multiples instances of same. So we can synthesize one module and replicate others.
* Also, the tool may not do a good job in synthesizing a a massive design. So, we synthesize the submodules and combine them.

![image](https://user-images.githubusercontent.com/66086031/165789685-a551ebad-2afb-478d-b982-163ba4547898.png)

## Flip Flops and Flop coding styles
### Glitches and Hazards

* In a combinational circuit, different paths have different delays, due to which the output might be unstable before settling to a stable value (Glitch).
* Flip Flops can be inserted to minimize the glitches.

**Put one image for the hazard from harris and harris book handdrawn**
* **Static-0 Hazard:**
* **Static-1 Hazard:**
* **Dynamic Hazard:**

### Asynchronous Vs Synchronous

| Asynchronous | Synchronous |
| ------------ | ----------- |
| Priority is given to the async reset(set) | Priority is given to the clock |
| baz          | bim         |

**Replace image with own drawing**

![image](https://user-images.githubusercontent.com/66086031/165873629-020cb422-d905-4caf-8878-652cdc6bb115.png)

### DFF with Asynchronous Reset
**Verilog Code:**
```verilog
module dff_asyncres ( input clk,  input async_reset, input d, output reg q );
 always @ (posedge clk, posedge async_reset) begin
  if(async_reset)
   q <= 1'b0;
  else	
   q <= d;
 end
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/165937101-359927cf-e79c-432d-aa13-e76acd7742f9.png)

**Yosys Synthesis:**
```console
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show dff_asyncres

```

![image](https://user-images.githubusercontent.com/66086031/165941329-30ad83ac-fbe2-4b36-895c-5d4de2cf1550.png)

### DFF with Asynchronous Set

```verilog
module dff_async_set ( input clk,  input async_set, input d, output reg q );
 always @ (posedge clk, posedge async_set) begin
  if(async_set)
   q <= 1'b1;
  else	
   q <= d;
 end
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/165937941-562a8b02-1ee9-4ef5-90a1-e373bafd3fa2.png)

**Yosys Synthesis:**

```console
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show dff_async_set
```

![image](https://user-images.githubusercontent.com/66086031/165942525-281ca909-e018-444e-a597-023448d3ae5c.png)


### DFF with Synchronous Reset

```verilog
module dff_syncres ( input clk, input sync_reset, input d , output reg q );
 always @ (posedge clk ) begin
  if (sync_reset)
   q <= 1'b0;
  else	
   q <= d;
 end
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/165939938-af5f9e21-61c0-403b-a229-eb9772331d99.png)

**Yosys Synthesis**
```console
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog dff_syncres.v 
synth -top dff_syncres
dfflibmap -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```

![image](https://user-images.githubusercontent.com/66086031/165944337-dca1351c-850d-41c2-b714-f027aeea2b68.png)

## Optimizations
* The tool just infers shifting operation for multiplication by powers of 2.

```verilog
module mul2 (input [2:0] a, output [3:0] y);
 assign y = a * 2;
endmodule
```
![image](https://user-images.githubusercontent.com/66086031/165946960-82b10e28-8e1e-4411-8bb3-19376c843c61.png)

**Synthesized netlist Verilog code:**

```verilog
module mul2(a, y);
  input [2:0] a;
  output [3:0] y;
  assign y = { a, 1'b0 };
endmodule
```

* Similiarly for multiplication with 9(8 + 1), first left shifting is done for 3 bit positions and then the signal replaces the last three bits.
```verilog
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule

```
![image](https://user-images.githubusercontent.com/66086031/165948933-db9247cb-5d33-478b-9a92-09e2af87e845.png)

**Synthesized netlist Verilog code:**

```verilog
module mult8(a, y);
  input [2:0] a;
  output [5:0] y;
  assign y = { a, a };
endmodule
```

# Day 3
## Intro to Optimizations
Reducing the area and power
Constant Propagation
![image](https://user-images.githubusercontent.com/66086031/166089587-b7eb8d66-f6a0-42ca-92ee-6ac02d1af519.png)

Boolean Logic Optimization
 ![image](https://user-images.githubusercontent.com/66086031/166089574-b6617577-bee6-4fc7-be40-ce1cdf1d5fbf.png)

Sequential Constant Propagation
![image](https://user-images.githubusercontent.com/66086031/166089739-576dc81a-f464-4043-baf2-84472c2f700c.png)

State Optimization

Retiming
![image](https://user-images.githubusercontent.com/66086031/166090131-2ffa70ae-44db-402b-8d85-f4d94e48e268.png)

Cloning
![image](https://user-images.githubusercontent.com/66086031/166090136-50984c27-a025-4c5d-86f8-ff257e159dcc.png)

## Combinational Logic Optimizations lab
(Include image of simplification for the examples with names)
### Example 1

**RTL Code:**
```verilog
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```

```console
// this command removes the extra unneccessary logic
opt_clean -purge
```

![image](https://user-images.githubusercontent.com/66086031/166091182-ad629375-512a-443a-9fc5-41f8a38a1117.png)

**Verilog code synthesized Netlist**
```verilog
module opt_check(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  input b;
  output y;
  sky130_fd_sc_hd__and2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule
```

### Example 2

**RTL Verilog Code:**

```verilog
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule

```

```console
opt_clean -purge
```

![image](https://user-images.githubusercontent.com/66086031/166091362-e1f91683-a013-4f9d-a80f-c998c08ee87b.png)

**Verilog code for synthesized netlist**
```verilog
module opt_check2(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  input b;
  output y;
  sky130_fd_sc_hd__lpflow_inputiso1p_1 _3_ (
    .A(_0_),
    .SLEEP(_1_),
    .X(_2_)
  );
  assign _0_ = a;
  assign _1_ = b;
  assign y = _2_;
endmodule
```

### Example 3

```verilog
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/166091838-e1bb9d99-714f-4ef7-9182-39208e8d0501.png)

**Verilog code for the synthesized netlist**

```verilog
module opt_check3(a, b, c, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire _4_;
  input a;
  input b;
  input c;
  output y;
  sky130_fd_sc_hd__and3_1 _5_ (
    .A(_2_),
    .B(_3_),
    .C(_1_),
    .X(_4_)
  );
  assign _2_ = b;
  assign _3_ = c;
  assign _1_ = a;
  assign y = _4_;
endmodule
```

### Example 4

**Verilog code for RTL Design**

```verilog
module opt_check4 (input a, input b, input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/166092081-26e0d98b-1476-4511-bd09-68b89a0b21fe.png)

**Verilog code for synthesized netlist**

```verilog
module opt_check4 (a, b, c, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  input b;
  input c;
  output y;
  sky130_fd_sc_hd__xnor2_1 _3_ (
    .A(_0_),
    .B(_1_),
    .Y(_2_)
  );
  assign _0_ = a;
  assign _1_ = c;
  assign y = _2_;
endmodule
```

### Example 5

**Verilog Code for RTL Design**

```verilog
module sub_module1(input a , input b , output y);
 	assign y = a & b;
endmodule

module sub_module2(input a , input b , output y);
 	assign y = a^b;
endmodule

module multiple_module_opt(input a , input b , input c , input d , output y);
	wire n1,n2,n3;

	sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
	sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
	sub_module2 U3 (.a(b), .b(d) , .y(n3));

	assign y = c | (b & n1); 


endmodule
```

![image](https://user-images.githubusercontent.com/66086031/166092733-f3a0c293-6ce9-482d-9886-70e241016616.png)

```verilog
module multiple_module_opt(a, b, c, d, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire _4_;
  wire \U1.y ;
  input a;
  input b;
  input c;
  input d;
  output y;
  sky130_fd_sc_hd__a21o_1 _5_ (
    .A1(_2_),
    .A2(_1_),
    .B1(_3_),
    .X(_4_)
  );
  assign _2_ = b;
  assign _3_ = c;
  assign y = _4_;
  assign _1_ = a;
endmodule
```
### Example 6
```verilog

module sub_module(input a , input b , output y);
 assign y = a & b;
endmodule

module multiple_module_opt2(input a , input b , input c , input d , output y);
	wire n1,n2,n3;

	sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
	sub_module U2 (.a(b), .b(c) , .y(n2));
	sub_module U3 (.a(n2), .b(d) , .y(n3));
	sub_module U4 (.a(n3), .b(n1) , .y(y));

endmodule
```
![image](https://user-images.githubusercontent.com/66086031/166093141-55ec45de-f76f-4bed-a899-62bc5917ae31.png)


```verilog
module multiple_module_opt2(a, b, c, d, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire _4_;
  wire \U1.y ;
  wire \U2.y ;
  wire \U3.y ;
  input a;
  input b;
  input c;
  input d;
  output y;
  assign _4_ = 1'h0;
  assign _0_ = a;
  assign _2_ = c;
  assign _1_ = b;
  assign _3_ = d;
  assign y = _4_;
endmodule
```

## Sequential Optimizations

### Example 1

**RTL Verilog Code:**

```verilog
module dff_const1(input clk, input reset, output reg q);
	always @(posedge clk, posedge reset)	begin
		if(reset)
			q <= 1'b0;
		else
			q <= 1'b1;
	end

endmodule
```

![image](https://user-images.githubusercontent.com/66086031/166094824-13d6af6a-28c0-4f13-8cfe-54226d99583f.png)
![image](https://user-images.githubusercontent.com/66086031/166095172-6e6df88a-9306-40f4-866d-82ff14f10ea9.png)

**Verilog Code for synthesized netlist:**
```verilog
module dff_const1(clk, reset, q);
	wire _0_;
	wire _1_;
	wire _2_;
	input clk;
	output q;
	input reset;
	sky130_fd_sc_hd__clkinv_1 _3_ (
		.A(_1_),
		.Y(_0_)
	);
	sky130_fd_sc_hd__dfrtp_1 _4_ (
		.CLK(clk),
		.D(1'h1),
		.Q(q),
		.RESET_B(_2_)
	);
	assign _1_ = reset;
	assign _2_ = _0_;
endmodule
```

### Example 2

**Verilog code for RTL**
```verilog
module dff_const2(input clk, input reset, output reg q);
	always @(posedge clk, posedge reset) begin
		if(reset)
			q <= 1'b1;
		else
			q <= 1'b1;
	end
endmodule
```

![image](https://user-images.githubusercontent.com/66086031/166095328-27ad919a-d8f6-45d8-8460-e090e0d6e6ef.png)
![image](https://user-images.githubusercontent.com/66086031/166096248-62b53982-2470-4a65-afb6-84336c2c7a1a.png)

**Verilog code for synthesized netlist**
```verilog
module dff_const2(clk, reset, q);
	input clk;
	output q;
	input reset;
	assign q = 1'h1;
endmodule
```

### Example 3


```verilog
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
	begin
		if(reset) begin
			q <= 1'b1;
			q1 <= 1'b0;
		end
		else begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```

In this the value of q1 is not immediately reflected at the clock edge of the second flip flop because of Tcq delay.

![image](https://user-images.githubusercontent.com/66086031/166096980-79675150-d065-4969-a7e9-89a7c4f79b16.png)
![image](https://user-images.githubusercontent.com/66086031/166096597-fffa84ae-110a-4071-9cb1-16c7d1df9357.png)
![image](https://user-images.githubusercontent.com/66086031/166096788-4cbaaa60-7cf3-493a-9d0d-95a1c8268f85.png)


```verilog
module dff_const3(clk, reset, q);
	  wire _0_;
	  wire _1_;
	  wire _2_;
	  wire _3_;
	  wire _4_;
	  input clk;
	  output q;
	  wire q1;
	  input reset;
	  sky130_fd_sc_hd__clkinv_1 _5_ (
		    .A(_2_),
		    .Y(_0_)
	  );
	  sky130_fd_sc_hd__clkinv_1 _6_ (
		    .A(_2_),
		    .Y(_1_)
	  );
	  sky130_fd_sc_hd__dfstp_2 _7_ (
		    .CLK(clk),
		    .D(q1),
		    .Q(q),
		    .SET_B(_3_)
	  );
	  sky130_fd_sc_hd__dfrtp_1 _8_ (
		    .CLK(clk),
		    .D(1'h1),
		    .Q(q1),
		    .RESET_B(_4_)
	  );
	  assign _2_ = reset;
	  assign _3_ = _0_;
	  assign _4_ = _1_;
endmodule
```
### Example 4

**Verilog code for the RTL Design**

```verilog
module dff_const4(input clk, input reset, output reg q);
	reg q1;

	always @(posedge clk, posedge reset) begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b1;
		end
		else
		begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
	
endmodule
```

In this the Flip flops are initialized to logic HIGH after the reset. The input to the first flip flop is also logic HIGH. So the output of the second Flip flop is a constant logic HIGH.

![image](https://user-images.githubusercontent.com/66086031/166097167-351a6da8-14fc-495e-ade2-7b00bbd366f4.png)
![image](https://user-images.githubusercontent.com/66086031/166097310-36660e64-c32c-4ee1-8dda-acb53c310538.png)

**Verilog code for the synthesized netlist**
```verilog

module dff_const4(clk, reset, q);
	input clk;
	output q;
	wire q1;
	input reset;
	assign q = 1'h1;
	assign q1 = 1'h1;
endmodule
```
### Example 5

**Verilog code for the RTL Design**

```verilog
module dff_const5(input clk, input reset, output reg q);
reg q1;

	always @(posedge clk, posedge reset) begin
		if(reset) begin
			q <= 1'b0;
			q1 <= 1'b0;
		end
		
		else begin
			q1 <= 1'b1;
			q <= q1;
		end
	end

endmodule
```

Both the FFs are initialized to zero by the reset. Input given to the first FF is reflected one cycle later in the second FF due to Tcq.

![image](https://user-images.githubusercontent.com/66086031/166098848-17f92c87-f3e5-4054-9615-1f47afb08745.png)
![image](https://user-images.githubusercontent.com/66086031/166099090-a7a6d011-d51e-4ffd-a816-926e3c8477e3.png)


**Verilog code for the synthesized netlist**
```verilog
module dff_const5(clk, reset, q);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire _4_;
  input clk;
  output q;
  wire q1;
  input reset;
  sky130_fd_sc_hd__clkinv_1 _5_ (
    .A(_2_),
    .Y(_0_)
  );
  sky130_fd_sc_hd__clkinv_1 _6_ (
    .A(_2_),
    .Y(_1_)
  );
  sky130_fd_sc_hd__dfrtp_1 _7_ (
    .CLK(clk),
    .D(q1),
    .Q(q),
    .RESET_B(_3_)
  );
  sky130_fd_sc_hd__dfrtp_1 _8_ (
    .CLK(clk),
    .D(1'h1),
    .Q(q1),
    .RESET_B(_4_)
  );
  assign _2_ = reset;
  assign _3_ = _0_;
  assign _4_ = _1_;
endmodule
```

## Unused outputs optimizations

### Example 1

```verilog
module counter_opt (input clk , input reset , output q);
	reg [2:0] count;
	assign q = count[0];

	always @(posedge clk ,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end
endmodule
```

In this the output q is needs only the value of count[0], so count[1], count[2] are not present in the synthesized netlist.

![image](https://user-images.githubusercontent.com/66086031/166100142-616c814e-2bb8-42b7-bb95-51d09cae00b6.png)

```verilog
module counter_opt(clk, reset, q);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire [2:0] _4_;
  wire _5_;
  input clk;
  wire [2:0] count;
  output q;
  input reset;
  sky130_fd_sc_hd__clkinv_1 _6_ (
    .A(_3_),
    .Y(_1_)
  );
  sky130_fd_sc_hd__clkinv_1 _7_ (
    .A(_2_),
    .Y(_0_)
  );
  reg \count_reg[0] ;
  always @(posedge clk, negedge _5_)
    if (!_5_) \count_reg[0]  <= 1'h0;
    else \count_reg[0]  <= _4_[0];
  assign count[0] = \count_reg[0] ;
  assign _4_[2:1] = count[2:1];
  assign q = count[0];
  assign _3_ = reset;
  assign _5_ = _1_;
  assign _2_ = count[0];
  assign _4_[0] = _0_;
endmodule
```

### Example 2

**Verilog code for the RTL Design**
```verilog
module counter_opt (input clk , input reset , output q);
	reg [2:0] count;
	assign q = (count[2:0] == 3'b100);

	always @(posedge clk ,posedge reset)
	begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
	end

endmodule
```

In this q needs all the three bits of count. So, three Flip Flops are present in the synthesized netlist.

![image](https://user-images.githubusercontent.com/66086031/166100435-7ccb3b8e-8f5b-42b4-9277-c1e032603c08.png)

**Verilog code for the synthesized netlist**

```verilog
module counter_opt(clk, reset, q);
  wire _00_;
  wire _01_;
  wire [2:0] _02_;
  wire [2:0] _03_;
  wire _04_;
  wire _05_;
  wire _06_;
  input clk;
  wire [2:0] count;
  output q;
  input reset;
  assign _02_[0] = ~count[0];
  assign _01_ = count[1] | count[0];
  assign q = count[2] & ~(_01_);
  assign _03_[1] = count[1] ^ count[0];
  assign _00_ = count[1] & count[0];
  assign _03_[2] = _00_ ^ count[2];
  assign _04_ = ~reset;
  assign _05_ = ~reset;
  assign _06_ = ~reset;
  sky130_fd_sc_hd__dfrtp_1 _16_ (
    .CLK(clk),
    .D(_03_[1]),
    .Q(count[1]),
    .RESET_B(_04_)
  );
  sky130_fd_sc_hd__dfrtp_1 _17_ (
    .CLK(clk),
    .D(_03_[2]),
    .Q(count[2]),
    .RESET_B(_05_)
  );
  sky130_fd_sc_hd__dfrtp_1 _18_ (
    .CLK(clk),
    .D(_02_[0]),
    .Q(count[0]),
    .RESET_B(_06_)
  );
  assign _03_[0] = _02_[0];
  assign _02_[2:1] = count[2:1];
endmodule
```

# Day 4
## Gate Level Simulation (GLS)

* The verilog code of the synthesized netlist is verified using a testbench in iVerilog.
* It is done to ensure the logical correctness after synthesis.
* When doing GLS, the Gate level verilog models from the standard cell library must be included.

## Synthesis Simulation Mismatch

* **Missing Sensitivity List:** 
	- ![image](https://user-images.githubusercontent.com/66086031/166102383-d28c0bb9-7d41-41d9-94cd-ab8b670d69d0.png)

Take some points below from the vlsi modelling
* **Blocking and Non Blocking Statements:**
	- ![image](https://user-images.githubusercontent.com/66086031/166102446-90ac6130-4838-4eef-83d6-5a8290302a58.png)
	- ![image](https://user-images.githubusercontent.com/66086031/166102493-bbdcc49a-0443-4d25-8e45-b03d7bb2318e.png)
	- ![image](https://user-images.githubusercontent.com/66086031/166102624-05f9ca04-dd92-4524-8540-4fe2f5ac78b6.png)

## Ternary operator Mux

**Verilog code for RTL Design:**

```verilog
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule
```
**RTL Simultation:**
![image](https://user-images.githubusercontent.com/66086031/166103163-cdc46474-f07f-4e81-81a3-345e359f6b30.png)

**Synthesized Netlist**
![image](https://user-images.githubusercontent.com/66086031/166103308-cf7c11ef-61c3-4935-9211-7c48184e480a.png)

**Verilog code for the synthesized netlist**
```verilog
module ternary_operator_mux(i0, i1, sel, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input i0;
  input i1;
  input sel;
  output y;
  sky130_fd_sc_hd__mux2_1 _4_ (
    .A0(_0_),
    .A1(_1_),
    .S(_2_),
    .X(_3_)
  );
  assign _0_ = i0;
  assign _1_ = i1;
  assign _2_ = sel;
  assign y = _3_;
endmodule
```
**GLS Commands:**

```console
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd

```

**GLS:**
![image](https://user-images.githubusercontent.com/66086031/166103505-eb0e52e9-91f2-46ad-afe5-498f5bf6224c.png)

## Bad MUX

* In this, only the sel is included in the sensitivity list. So the output is evaluated only when the sel changes.
* Even if the input changes, it will not be reflected in the output if sel does not change.

**Verilog code for the RTL Design**

```verilog
module bad_mux (input i0 , input i1 , input sel , output reg y);
	always @ (sel)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
endmodule
```
**RTL Simulation**

![image](https://user-images.githubusercontent.com/66086031/166113794-93c5c1b2-d6b2-47de-805f-cb3d160daf37.png)

**Synthesized Netlist**

![image](https://user-images.githubusercontent.com/66086031/166113976-35430366-ed83-430e-84b1-31447fad66a9.png)

**GLS for Bad MUX:**

![image](https://user-images.githubusercontent.com/66086031/166114069-5cf66491-573c-4def-a26a-a26abad8e769.png)

**Verilog code for the synthesized netlist**

```verilog
module bad_mux(i0, i1, sel, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input i0;
  input i1;
  input sel;
  output y;
  sky130_fd_sc_hd__mux2_1 _4_ (
    .A0(_0_),
    .A1(_1_),
    .S(_2_),
    .X(_3_)
  );
  assign _0_ = i0;
  assign _1_ = i1;
  assign _2_ = sel;
  assign y = _3_;
endmodule
```

## Blocking Statement Synthesis Simulation Mismatch

```verilog
module blocking_caveat (input a , input b , input  c, output reg d); 
	reg x;
	always @ (*)
	begin
		d = x & c;
		x = a | b;
	end
endmodule
```

**RTL Simulation** </br>

![image](https://user-images.githubusercontent.com/66086031/166115117-76cdcd48-23a0-4568-ae3e-4c870cc77d9d.png)

**No Flip Flops are inferred during synthesis** </br>

![image](https://user-images.githubusercontent.com/66086031/166115171-b2f5f131-0013-443b-9b02-38ad51445ee4.png)

**Synthesized Netlist** </br>

![image](https://user-images.githubusercontent.com/66086031/166115229-79581cc1-341a-410a-92ef-b0d1d1de02ca.png)

**Verilog code for the synthesized netlist**

```verilog
module blocking_caveat(a, b, c, d);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  wire _4_;
  input a;
  input b;
  input c;
  output d;
  sky130_fd_sc_hd__o21a_1 _5_ (
    .A1(_2_),
    .A2(_1_),
    .B1(_3_),
    .X(_4_)
  );
  assign _2_ = b;
  assign _1_ = a;
  assign _3_ = c;
  assign d = _4_;
endmodule
```

**GLS**

![image](https://user-images.githubusercontent.com/66086031/166115338-79631d5d-5ea1-4ddf-85f9-29abf976b0d7.png)


# Day 5

# Author
Navinkumar Kanagalingam, III Year, B. Tech ECE, Puducherry Technological University
(As of April 2022)

# Acknowledgements
* Kunal Ghosh
* VSD Team
 
# References

