# Introduction to Timing Libraries

Using the gvim command, we open the path of our sky130 library to decode the importance of PVT: Process, Voltage, (and) Temperature
These 3 parameters determine how an IC operates.
Thus, the libraries are characterized by these 3 variable parameters.

## The meaning of tt_025C_1v80

- **tt** indicates typical operating condition
- **025C** indicates a temperature of 25 degrees Celsius
- **1v80** indicates a voltage of 1.8V

  <img width="788" height="482" alt="image" src="https://github.com/user-attachments/assets/f8994876-b89d-432a-ab53-c0fe32c1b5a0" />

Given the number of digital logic variables (5), there are (here)32 leakage power combinations.
The power information has been mentioned first, followed by timing information (_timing()_).

# Hierarchical vs. Flat Synthesis

In our example, we produce the flattened design synthesis and the hierarchical design synthesis as shown

The flattened synthesis is synthesized from hierarchical synthesis, after synthesising the top module, by using this command

    write_verilog multiple_modules_hier.v
    flatten

<img width="1920" height="1080" alt="day2_flatten" src="https://github.com/user-attachments/assets/9de99cca-91dd-4aba-af55-545e9a41e045" />

<img width="1920" height="1080" alt="day2_flattenSynth" src="https://github.com/user-attachments/assets/d4482abe-01ca-4c76-898b-2b6a66c97b7b" />

<img width="1920" height="1080" alt="day2_after-flatten" src="https://github.com/user-attachments/assets/c9dc8cfa-2159-45c4-a574-c56127a04b9e" />

where _multiple_modules_hier.v_ represents the hierarchical _multiple_modules_ file

## Sub-module Level Synthesis
<img width="1920" height="1080" alt="day2_aftersub1-synth" src="https://github.com/user-attachments/assets/19bff67e-b96f-4af1-9b62-54bff79c317a" />

Synthesis of the sub-module is performed first by reading the library and top module, followed by sub-module synthesis, as shown

    synth -top <sub-module name>
    
<img width="1920" height="1080" alt="day2_aftersub1-synth" src="https://github.com/user-attachments/assets/446dd6d5-318e-4bdb-bc65-f89008c7c5ea" />

- We synthesise sub-modules because
  1. If multiple instances of the same module are preferred (or)
  2. The Divide and Conquer Approach is to be applied, in case the design is massive.

**After Synthesis**

<img width="1920" height="1080" alt="day2_showsub1" src="https://github.com/user-attachments/assets/9646ffce-c0ef-4469-8861-f2b8f1f1183f" />

# Flop Coding style

- Propagation delay (pd): the amount of time taken for the output to be visible after the input data is fed.
- Glitch: An unintended change in output data that follows _pd_.
- This style is prominently used because, in a FF, the output data is governed by the presence of a clock pulse, and thus shields the output from **_glitch_**
- If a FF is not initialized, then it produces a garbage value. For this purpose, there are 2 kinds of buttons: RESET and SET, which initialize all the input and output values.

# Summary
- There is always a typical variation parameter value for each IC, denoted as **_tt<temp-value>C_voltage**
- This is because a Stacked CMOS generates higher logical effort, as compared to a simpler or Flat CMOS
- Higher logical effort causes an increase in area and limits design while leading to a tradeoff with performance.
- 
