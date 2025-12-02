# Introduction to iVerilog and Gtkwave

Initially, we install iverilog and gtkwave using the commands :

    sudo apt install iverilog
    sudo apt install gtkwave
The compilation and simulation are performed using the commands:

    iverilog tb_good_mux.v good_mux.v
    ./a.out

Executing _a.out_ file basically dumps the .vcd file 

<img width="959" height="452" alt="day1_terminal1" src="https://github.com/user-attachments/assets/7c9743b0-8ac8-43e4-9970-6cd61b4b77bb" />

The iverilog design code and testbench for good_mux is retreived in vim editor using command

    gvim tb_good_mux.v -o good_mux.v 

<img width="383" height="481" alt="day1_design_and_tb" src="https://github.com/user-attachments/assets/6ec5e8f6-6444-4aa1-ac64-919268f5e1d3" />

Following the developement and compilation of the design spec, gtkwave is used to view the design testbench with the command as

    gtkwave tb_good_mux.vcd

The resulting image is obtained
<img width="958" height="425" alt="day1_gtk1" src="https://github.com/user-attachments/assets/54f2d9dc-19db-4959-9b04-65b92b08ca3c" />

# Logic Synthesis in Yosys with sky130 PDKs

**RTL Design**

The behavioural description of the required design specification.

**What happens during synthesis?**

- The design is translated from RTL to gates.
- Logic is mapped to technology cells provided in the .lib file.
- Connections between gates are created.
- The output of synthesis is a gate-level netlist

  **We need slower cells** for hold time constraints. To avoid hold issues:

We intentionally use slow cells to increase delay. Thus, a .lib contains both fast and slow versions of the same basic gates.

**Faster Cells**

- Required to achieve high performance.
- Use wider transistors:
  - Lower delay
  - Higher area and power
    
**Slower Cells**

- Help satisfy hold constraints.
- Use narrow transistors:
  - Higher delay
  - Lower area and power

| Topic                | Key Idea                                           |
| -------------------- | -------------------------------------------------- |
| Synthesis            | RTL → Gate-level logic using cell library          |
| Fast cells           | Reduce TCOMBI to meet max clock speed              |
| Slow cells           | Avoid hold violations                              |
| Cell characteristics | Wider = fast but costly; Narrow = slow but compact |


# Yosys Synthesis Lab

The following image summarizes the yosys set-up:
  <img width="1920" height="1080" alt="yosys_setup" src="https://github.com/user-attachments/assets/1fb1ded2-6d2c-45d0-837a-c0803e94e4f8" />

To invoke yosys

    yosys
    
To read the library the command used after invoking yosys is (as shown in the figure below)

    read_liberty -lib #relative path to the library#
    
<img width="831" height="462" alt="image" src="https://github.com/user-attachments/assets/1ad15274-678d-4855-86ec-1933abcd329d" />

To read the Verilog file in yosys

    read_verilog good_mux.v

<img width="602" height="481" alt="image" src="https://github.com/user-attachments/assets/71552b57-f9c5-4382-a3f2-1ced6dc8aee3" />

In case the design is spanning more than 1 file, all the files need to be read in this manner.

# Synthesis

To perform synthesis of the top module, the command given in yosys is

    synth -top good_mux 

<img width="623" height="461" alt="image" src="https://github.com/user-attachments/assets/f34b1ee2-6f24-4a26-8909-11089df2f3c4" />


To generate the netlist for the above top module(good_mux), the command is

    abc -liberty #library path#

The _abc_ command converts rtl file into digital logic design.
<img width="959" height="488" alt="image" src="https://github.com/user-attachments/assets/dfce0c06-b7fe-4fb9-b733-546f31db75b9" />

We use the _show_ command to display a graphical version or an image of the realized design as shown below

<img width="959" height="500" alt="image" src="https://github.com/user-attachments/assets/0fcdd70d-177c-420a-9a7c-85e6b6a36b3c" />


# Writing Netlist

To add a netlist to the existing verilog design file, we create a netlist file named: _good_mux_netlist.v_ as

        write_verilog good_mux_netlist.v
The corresponding netlist file is opened in the Vim editor with command in yosys:

        !gvim good_mux_netlist.v
We remove the unnecessary information and retain the refined code using the within the write command with resulting image shown below

        write_verilog -noattr good_mux_netlist.v

<img width="907" height="502" alt="image" src="https://github.com/user-attachments/assets/1d5bbaa5-d8ef-494a-8426-1e4365f557ec" />
