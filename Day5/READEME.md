# If-Else and Case Constructs

 _If_ is used to create priority logic. Case statement is used to categorise logic
 
## Caveats with If-Statements
- The caution required with 'if-else' is called as "**Inferred Latches**", which means an incomplete if statement i.e the current point latches onto the previous value
- This occurs because of the absence of _else_ statement.
- This depends on the use-case
- In a combinational circuit, this error must not occur.

## Caveats with Case-Statements
1. Incomplete case also lead to "**Inferred Latches**", which means an incomplete  statement i.e the current point latches onto the other cases. A solution is to code an _endcase_.
2. Partial assignments in cases, i.e not assigning all the outputs in each case, which leads to latching. To avoid this condition, state all outputs in every case.
3. There must not be overlapping case-statement. The output depends on the simulator and synthesizer

A Key Comparison between If-else and Case, a condition can repeat in If-else but not in case, and results in huge error in the circuit.

## LAB 1: An incomplete if statement

Code:
```verilog
module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
    if(i0)
        y <= i1;
end
endmodule
```
#### On Simulation:

<img width="959" height="340" alt="image" src="https://github.com/user-attachments/assets/abf967ab-0f64-43d9-982b-f11555211f88" />

#### Resulting Synthesis:
<img width="930" height="412" alt="image" src="https://github.com/user-attachments/assets/47317435-e8c2-4adb-bfe5-a54859fd9296" />

## LAB 2: An incomplete if statement without _else_

Code:
```verilog
module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
    if(i0)
        y <= i1;
    else if (i2)
        y <= i3;

end#
```
#### On Simulation:

<img width="959" height="398" alt="image" src="https://github.com/user-attachments/assets/a672c1b4-a42d-4033-94d6-0bea014152d9" />

#### Resulting Synthesis:
<img width="956" height="302" alt="image" src="https://github.com/user-attachments/assets/ad12cf03-a060-43c0-9e4e-c5182d703f58" />

## LAB 3: Incomplete Case statement
```verilog
  module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
    always @ (*)
    begin
        case(sel)
            2'b00 : y = i0;
            2'b01 : y = i1;
        endcase
    end
 endmodule
```

Partial Case:

```verilog
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
    case(sel)
        2'b00 : begin
            y = i0;
            x = i2;
            end
        2'b01 : y = i1;
        default : begin
                   x = i1;
               y = i2;
              end
    endcase
end
endmodule  
```

Complete Case:

```verilog 
module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
    case(sel)
        2'b00 : y = i0;
        2'b01 : y = i1;
        default : y = i2;
    endcase
end
endmodule
```

#### On Simulation of Incomplete Case
<img width="953" height="386" alt="image" src="https://github.com/user-attachments/assets/c9d7230f-cac3-438f-baa7-728fa726a56d" />

#### On Simulation of Complete Case
<img width="959" height="329" alt="image" src="https://github.com/user-attachments/assets/59a2c8ba-9684-4ad6-ab77-d4ce07e9a1f6" />

#### Resulting Synthesis:

##### For an Incomplete Case
<img width="959" height="259" alt="image" src="https://github.com/user-attachments/assets/ab8d598f-fec7-44e3-8123-50d7e6dba05a" />

##### For a Partial Case
<img width="959" height="335" alt="image" src="https://github.com/user-attachments/assets/4462a117-6aee-4f7f-b641-4d318b9ef2dd" />

##### For a Complete Case
<img width="957" height="239" alt="image" src="https://github.com/user-attachments/assets/d2c594b8-7ce7-4dea-8b7c-f361efd6ebe4" />

# Loop Constructs: For Loop and Generate For Loop

For Loop:
- used under always block
- used for evaluating expressions(repeatedly) and not for instantiating hardware

Generate For Loop:
- never used within an always block(specially 'generate' based blocks)
- used for instantiating a Hardware

Example Code: 
1. for a 256 to 1 Mux

```verilog
   module mux256to1(input [255:0]d,input [7:0] sel, output reg y);
     always @(*) begin
      for (integer i = 0; i < $bits(d); i = i+1) begin
        if(i == sel)
          y = d[i];
      end
     end
   endmodule
```
2. for a 1-to-8 Demux
   
```verilog
   module demux1to256(input y,input [7:0] sel, output reg [255:0]d);
     always @(*) begin
      for (integer i = 0; i < $bits(d); i = i+1) begin
        if(i == sel)
          d[i] = y;
        else if ( i != sel )
          d[i] = 1'b0;
      end
     end
   endmodule
```
## LAB 4: Mux generator using For Loop
Code:

```verilog
module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
wire [3:0] i_int;
assign i_int = {i3,i2,i1,i0};
integer k;
always @ (*)
begin
for(k = 0; k < 4; k=k+1) begin
    if(k == sel)
        y = i_int[k];
end
end
endmodule
```
#### Simulation

<img width="959" height="392" alt="image" src="https://github.com/user-attachments/assets/af2a694e-1e07-4378-8652-c1971ce2561e" />

## LAB 5: Demux generator using For Loop

Code:

```verilog
module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
for(k = 0; k < 8; k++) begin
    if(k == sel)
        y_int[k] = i;
end
end
endmodule
```
#### Simulation
<img width="1913" height="838" alt="image" src="https://github.com/user-attachments/assets/718e6d8b-8a14-4f60-bbd2-23dc73cfa6ba" />

#### Synthesis Result
<img width="436" height="412" alt="image" src="https://github.com/user-attachments/assets/f2f9d856-7347-48b9-afab-f958d39ae41c" />

## LAB 7: Ripple-Carry Adder using Generate Block

Code:

Top Module:

```verilog
module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
wire [7:0] int_sum;
wire [7:0]int_co;

genvar i;
generate
    for (i = 1 ; i < 8; i=i+1) begin
        fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
    end

endgenerate
fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule

```
Full Adder Module:

```verilog
module fa (input a , input b , input c, output co , output sum);
    assign {co,sum}  = a + b + c ;
endmodule
```

### Command to compile the top module:

    iverilog fa.v rca.v tb_rca.v

### Simulation

<img width="959" height="299" alt="image" src="https://github.com/user-attachments/assets/693790b5-5aee-4983-b9bb-708c467b97e7" />

### Synthesis Result

<img width="473" height="404" alt="image" src="https://github.com/user-attachments/assets/71e213a6-7aa1-4e01-a103-a006c835ef01" />

# Summary

- Writing complete if-else and case statements in order to avoid unintended latch inference.
- For loops and generate blocks help create reusable code that synthesizes well for different scales
- Assign values to all output signals irrespective of path the code takes in combinational logic blocks.
- Best way is to: Practice with hands-on labs using real Verilog code and check synthesis reports.

