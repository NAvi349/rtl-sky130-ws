# Table of Contents
 * [Day 1](#day-1)
 * [Day 2](#day-2)
 * [Day 3](#day-3)
 * [Day 4](#day-4)
 * [Day 5](#day-5)

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

### Setup and hold time
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
* Include the library
* Include the verilog file
* Select top level module to Synthesize
* From the RTL Design(Verilog) generate synthesized netlist with the standard cell libraries
* View the logic
* Generate (Write) verilog file for the synthesized netlist

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
![image](https://user-images.githubusercontent.com/66086031/165503013-3b7eef02-4c3a-43ce-a34e-1818ec314085.png)
![image](https://user-images.githubusercontent.com/66086031/165503817-94a71298-05f2-40cf-8cbd-1e1e8b1eb69b.png)
![image](https://user-images.githubusercontent.com/66086031/165505251-ba96fa2f-72ca-4e5d-a772-0c67fe8eeac2.png)
![image](https://user-images.githubusercontent.com/66086031/165506961-c02ebcf8-a8d5-4bf4-a916-7bbf81bccc08.png)
![image](https://user-images.githubusercontent.com/66086031/165505986-34f1a631-1e4b-4529-b4a5-500c4eef4380.png)
![image](https://user-images.githubusercontent.com/66086031/165507626-7e254cc9-7c8b-48fb-b60e-ca9c87f9a3e4.png)
![image](https://user-images.githubusercontent.com/66086031/165508485-d74c18a2-9b0c-4bd7-b5d4-2e61f6ff9d0a.png)




# Day 2
# Day 3
# Day 4
# Day 5
