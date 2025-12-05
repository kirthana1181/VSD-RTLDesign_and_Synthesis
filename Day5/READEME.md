<img width="959" height="335" alt="image" src="https://github.com/user-attachments/assets/036696d0-1088-4862-b8b7-ff61a9784f3f" /># If-Else and Case Constructs

 _If_ is used to create priority logic. Case statement is used to categorise logic
 
## Caveats with If-Statements
- The caution required with 'if-else' is called as "**Inferred Latches**", which means an incomplete if statement i.e the current point latches onto the previous value
- This occurs because of the absence of _else_ statement.
- This depends on the use-case
- In a combinational circuit, this error must not occur.

## Caveats with Case-Statements
1. Incomplete case also lead to "**Inferred Latches**", which means an incomplete  statement i.e the current point latches onto the other cases. A solution is to code an _endcase_.
2. Partial assignments in cases, i.e not assigning all the outputs in each case, which leads to latching. To avoid this condition, state all outputs in every case.
3. There must not be overlapping case-statement.

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
#### On GLS:

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
#### On GLS:

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

#### On GLS of Incomplete Case
<img width="953" height="386" alt="image" src="https://github.com/user-attachments/assets/c9d7230f-cac3-438f-baa7-728fa726a56d" />

#### On GLS of Complete Case
<img width="959" height="329" alt="image" src="https://github.com/user-attachments/assets/59a2c8ba-9684-4ad6-ab77-d4ce07e9a1f6" />

#### Resulting Synthesis:

##### For an Incomplete Case
<img width="959" height="259" alt="image" src="https://github.com/user-attachments/assets/ab8d598f-fec7-44e3-8123-50d7e6dba05a" />

##### For a Partial Case
<img width="959" height="335" alt="image" src="https://github.com/user-attachments/assets/4462a117-6aee-4f7f-b641-4d318b9ef2dd" />

##### For a Complete Case
<img width="957" height="239" alt="image" src="https://github.com/user-attachments/assets/d2c594b8-7ce7-4dea-8b7c-f361efd6ebe4" />


