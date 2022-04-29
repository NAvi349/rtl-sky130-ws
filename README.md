# Table of Contents
 * [Day 1](#day-1)
 * * [iVerilog Introduction](#iverilog)
 * * [Yosys Introduction](#Yosys)
 * * [Logic Synthesis](#Logic-Synthesis)
 * * [Setup and Hold Time](#Setup-and-Hold-time)
 * * [Fast cells and Slow cells](#Fast-cells-vs-Slow-cells)
 * [Day 2](#day-2)
 * * [dot Lib file]
 * * [Hierarchial Vs Flat Synthesis]
 * * [Flip Flops and Flop coding styles]
 * * [Optimizations]
 * [Day 3](#day-3)
 * [Day 4](#day-4)
 * [Day 5](#day-5)
 * [Author](#author)
 * [Acknowledgements](#acknowledgements)
 * [References](#references)

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
(put picture of setup time FF from that VLSI subsytem course)
We need fast cells to satisfy setup time constraints
(put picture of hold time FF from that VLSI subsytem course)
We need slow cells to satisfy hold time constraints

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

### **Why NAND gate is used for OR/NOR gate implementation?**

* The logical effort of a NAND gate is less than that of an equivalent NOR gate.
* **insert image of logical effort of NOR NAND **

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
# Day 4
# Day 5

# Author
Navinkumar Kanagalingam, III Year, B. Tech ECE, Puducherry Technological University
(As of April 2022)

# Acknowledgements
* Kunal Ghosh
* VSD Team
 
# References

