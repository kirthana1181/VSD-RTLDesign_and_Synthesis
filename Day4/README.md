# Gate-Level Simulation (GLS) & Synthesis Simulation Mismatches (SSM)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/102e75bb-cb7a-49d9-a1bc-18803bc41928" />

Running the testbench with the netlist as DUT(Design Under Test)

**Why GLS?**
- To verify the logical correctness of the synthesis
- Ensuring the timing of the design is met
The GLS is run using delay annotation

There are kinds of gate-level models:
1. Timing-aware
2. Functional

## Synthesis and Simulation Mismatch

This occurs because of:
1. Missing sensitivity list
2. Blocking vs Nonblocking Assignments
3. Non-Standard Verilog Coding


#### 1. Missing Sensitivity List
- Does not allow the sequential logic to be evaluated as per functionality resulting into an erroneous logic circuit
- This is because the synthesiser focuses on the body within the _always_ block, i.e the functional body

#### 2. Blocking vs Nonblocking Assignments

Caveats with Blocking assignments:

1. Order of assignment of signals down the program
2. The updating signal must be assigned as per its own dependency on the other declared signals and vice-versa
This leads to a functional error despite producing a clean synthesis.

## LAB 1
Code:

```verilog
    module ternary_operator_mux (input i0 , input i1 , input sel , output y);
    assign y = sel?i1:i0;
    endmodule
```
To run the GLS, after compiling the code, we use the command as follows:

    iverilog <pah to primitives.v> <path to sky130_fd_sc_hd.v> ternary_operator_mux_net.v tb_ternary_operator_mux.v


### GLS of ternary_operator_mux

#### Before Synthesis
<img width="959" height="457" alt="image" src="https://github.com/user-attachments/assets/84993584-0a12-4296-a5f9-ac764684d583" />

#### After Synthesis
<img width="959" height="494" alt="image" src="https://github.com/user-attachments/assets/9307c04f-6a8e-4070-8613-aa7d30e471a9" />

### Resulting Netlist
<img width="959" height="479" alt="image" src="https://github.com/user-attachments/assets/58377eb3-55fd-4acb-94cd-1e841f5e2d78" />

## LAB 2
Code:
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
Corrected code-version
```verilog
always @ (*) begin
  if (sel)
    y = i1;
  else
    y = i0;
end
```
### GLS of bad_mux

#### Before Synthesis

<img width="956" height="392" alt="image" src="https://github.com/user-attachments/assets/aa2ded12-c144-4b24-bb02-9aaacd8757fc" />

#### After Synthesis
<img width="956" height="365" alt="image" src="https://github.com/user-attachments/assets/98e243df-d624-44f3-b1d5-c400b4e49430" />

The difference is due to SSM, in the first [image](<img width="956" height="392" alt="image" src="https://github.com/user-attachments/assets/aa2ded12-c144-4b24-bb02-9aaacd8757fc" />) due to the absence of signals 'i1' i.e missing sensitivity list.

## LAB 3 
Code:
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
corrected order:
```verilog
always @ (*) begin
  x = a | b;
  d = x & c;
end
```
### GLS of blocking_caveat

#### Before synthesis
<img width="958" height="365" alt="image" src="https://github.com/user-attachments/assets/585a995c-a28b-4856-aa3f-9cf924acbb05" />

#### After synthesis
<img width="959" height="325" alt="image" src="https://github.com/user-attachments/assets/894ff4ec-3348-4c85-a6e8-f79e60136588" />

### Resulting Netlist
<img width="959" height="465" alt="image" src="https://github.com/user-attachments/assets/0e4d5191-e81b-4189-8011-4417db64eded" />

The difference is due to SSM, in the first [image](<img width="958" height="365" alt="image" src="https://github.com/user-attachments/assets/585a995c-a28b-4856-aa3f-9cf924acbb05" />) due to the unwanted use of blocking statement.

# Summary

Always write synthesizable, unambiguous RTL and follow good coding practices to minimise mismatches, in order to avoid Synthesis Simulation Mismatch. Specially make sure of the correct usage of blocking and nonblocking statements, and entries in the sensitivity list.
