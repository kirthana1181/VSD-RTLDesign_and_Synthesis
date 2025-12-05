# Logic Optimisation

Squeezing the Design to an optimised design for area and power savings
- Boolean-Logic Optimisation: using K-Map, QM Method
- Constant Propagation: a direct optimisation

## 1. Combinational Logic Optimisation

A compiler optimization technique that involves the reduction of variables with constants during synthesis.
- Reduces Gate count
- It improves timing paths and optimizes resources
- Reduces power as a result

## 2. Sequential Logic Optimisation

- Constant Propagation
- State Optimisation: basically optimization of unused states
- Retiming: partitioning the circuit to improve the performance by assigning time to redistribute delay
- Sequential Logic Cloning: is performed in a physical-aware synthesis. For example, a Flip-Flop is cloned in case there is a routing issue due to a greater distance between the two connections for a logic.

## LAB 1

Code

   ```verilog
module opt_check (input a , input b , output y);
    assign y = a?b:0;
    endmodule
```
The steps performed the as same as those performed on [DAY 1- for Yosys Synthesis](https://github.com/kirthana1181/VSD-RTLDesign_and_Synthesis/blob/main/Day%201/Introduction%20to%20iverilog%20and%20Yosys.md#yosys-synthesis-lab)

For optimisation purpose, the line of command inserted between `synth -top` and `abc -liberty <technology_lib_file_path>`

    opt_clean purge

### Output
<img width="1920" height="1013" alt="day3_lab2" src="https://github.com/user-attachments/assets/53950116-16b5-4f6a-a70a-3882173ac68e" />

## LAB 2

Code

   ```verilog
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```

### Output
<img width="1920" height="1020" alt="day3_lab1" src="https://github.com/user-attachments/assets/f306709e-d482-4b7a-98e3-0de9f254b2eb" />

## LAB 3
Code
```verilog
    module opt_check3 (input a , input b, input c , output y);
    assign y = a?(c?b:0):0;
    endmodule
```
### Output
<img width="959" height="504" alt="image" src="https://github.com/user-attachments/assets/89f12b3c-544c-4944-af93-dee5cf9f07e1" />

## LAB 4

```verilog
    module opt_check4 (input a , input b , input c , output y);
     assign y = a?(b?(a & c ):c):(!c);
     endmodule
```
### Output

<img width="959" height="506" alt="image" src="https://github.com/user-attachments/assets/0e2c6519-0b17-49df-bbcc-976912f74f65" />




