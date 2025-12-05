# RTL Design Using Verilog with SKY130 Technology
## Workshop Overview

This repository documents learnings and lab work from the “RTL Design using Verilog with Sky130 Technology” workshop offered by VLSI System Design (VSD), focused on building an end‑to‑end open‑source RTL design and synthesis flow using the SkyWater SKY130 process node. The program emphasizes writing clean, synthesis‑friendly Verilog, validating designs through simulation, and mapping them to standard cells using open‑source tools.

The workshop provides comprehensive hands-on training in RTL design, simulation, synthesis, and implementation using the open-source SKY130 PDK.

## Workshop Contents

### 📁 Day 1: Introduction to Verilog RTL Design and Synthesis
- Introduction to open-source simulator iVerilog
- Introduction to GTKWave
- Introduction to Yosys and Logic Synthesis
- Labs on Verilog RTL design and synthesis

**Lab Work:** [Day 1 Labs](https://github.com/kirthana1181/VSD-RTLDesign_and_Synthesis/tree/main/Day%201)

---

### 📁 Day 2: Timing Libs, Hierarchical vs Flat Synthesis and Efficient Flop Coding Styles
- Introduction to timing libraries (.lib)
- Hierarchical vs Flat synthesis
- Various flop coding styles and optimization
- Labs on timing libs, synthesis, and flop implementations

**Lab Work:** [Day 2 Labs](https://github.com/kirthana1181/VSD-RTLDesign_and_Synthesis/tree/main/Day2)

---

### 📁 Day 3: Combinational and Sequential Optimizations
- Introduction to logic optimizations
- Combinational logic optimizations
- Sequential logic optimizations
- Labs on combinational and sequential optimizations

**Lab Work:** [Day 3 Labs](https://github.com/kirthana1181/VSD-RTLDesign_and_Synthesis/tree/main/Day3)

---

### 📁 Day 4: GLS, Blocking vs Non-blocking and Synthesis-Simulation Mismatch
- Gate Level Simulation (GLS)
- Synthesis-Simulation mismatch
- Blocking vs Non-blocking statements
- Labs on GLS and synthesis-simulation mismatch

**Lab Work:** [Day 4 Labs](https://github.com/kirthana1181/VSD-RTLDesign_and_Synthesis/tree/main/Day4)

---

### 📁 Day 5: Design for Testability (DFT) and Introduction to Logic Synthesis
- If, case, for loop and for generate
- Optimization techniques
- Labs on if, case statements, and looping constructs

**Lab Work:** [Day 5 Labs](./day5/)

---

## Tools Used

- **iVerilog**: Open-source Verilog simulator
- **GTKWave**: Waveform viewer for debugging
- **Yosys**: Open-source synthesis tool
- **SKY130 PDK**: Open-source 130nm process design kit by SkyWater Technology

## Repository Structure

```
.
├── README.md
├── day1/
│   ├── READEME.md
├── day2/
│   ├── READEME.md
│   └── screenshots/
├── day3/
│   ├── labs/
│   ├── notes.md
│   └── screenshots/
├── day4/
│   ├── READEME.md
│   └── screenshots/
└── day5/
    ├── labs/
    ├── READEME.md
    └── screenshots/
```

## Key Learnings

- ✅ Understanding RTL design flow
- ✅ Verilog coding styles and best practices
- ✅ Synthesis using Yosys with SKY130 PDK
- ✅ Timing analysis and optimization techniques
- ✅ Gate Level Simulation and verification
- ✅ Identifying and resolving synthesis-simulation mismatches

## Author

**KIRTHANA**
- GitHub: [Kirthana P Rao](https://github.com/kirthana1181)

## Acknowledgments

Special thanks to **VSD (VLSI System Design)** for organizing this comprehensive workshop and providing excellent training materials and support.

## References

- [SkyWater SKY130 PDK Documentation](https://skywater-pdk.readthedocs.io/)
- [Yosys Documentation](https://yosyshq.net/yosys/)
- [iVerilog Documentation](http://iverilog.icarus.com/)

## License

This repository is for educational purposes. Please refer to individual tool licenses for usage terms.

---

⭐ If you found this repository helpful, please consider giving it a star!
