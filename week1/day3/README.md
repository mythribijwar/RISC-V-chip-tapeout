

# Combinational and Sequential Optimization

## Combinational logic optimization

Combinational logic optimization focuses on minimizing the complexity of the logic circuit in terms of area, power, and delay while maintaining the same functionality. Optimization techniques are applied to reduce the number of gates, minimize gate delays, and lower the overall power consumption of the design.

   ### 1)Constant Propagation (Direct Optimization):

Constant propagation is a form of optimization where constant values are substituted directly into Boolean expressions. This simplifies the design by eliminating variables that have a fixed value.

  ###  2)Boolean Logic Optimization:

#### Karnaugh Maps (K-map): 
K-maps are used to simplify Boolean expressions by visualizing them in a two-dimensional grid and grouping together terms that can be simplified.

#### Quine–McCluskey Algorithm:
This is a tabular method for minimization of Boolean expressions. It is particularly useful for Boolean functions with many variables.

 ## Sequential Logic Optimization

Sequential logic optimization deals with optimizing circuits where outputs depend on both the current inputs and previous states, i.e., circuits with memory elements like flip-flops or registers.

### a) Basic Sequential Logic Optimization

#### Sequential Constant Propagation: 
Just like in combinational logic, constant propagation can be applied in sequential logic to propagate constant values through registers or flip-flops, simplifying the design.

### b) Advanced Sequential Logic Optimization

#### State Optimization: 
This involves optimizing the finite state machine (FSM) by reducing the number of states while maintaining equivalent behavior.

#### State Minimization: 
Techniques like partition refinement or state merging are used to combine equivalent states into a single state, reducing the total number of states in an FSM.


#### Retiming: 
This technique involves shifting registers in a sequential circuit to optimize performance, such as improving the circuit's clock speed or reducing the area.


#### Sequential Logic Cloning (Floorplan-Aware Synthesis):
Cloning is the replication of a sequential element (e.g., a register or flip-flop) to balance the timing across different parts of the circuit.

### Lab 1

Below is the Verilog code for Lab 1:

```verilog
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```

**Explanation:**
- `assign y = a ? b : 0;` means:
  - If `a` is true, `y` is assigned the value of `b`.
  - If `a` is false, `y` is 0.

Follow the steps from [Day 1 Synthesis Lab](https://github.com/Ahtesham18112011/RTL_workshop/tree/main/Day_1#6-synthesis-lab-with-yosys) and add the following between `abc -liberty` and `synth -top`:
```shell
opt_clean -purge
```

![Lab 1 Output](https://github.com/user-attachments/assets/4d224d8d-f6f5-4a37-9732-ab570b64e31e)

---

### Lab 2

Verilog code:

```verilog
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```

**Code Analysis:**
- Acts as a multiplexer:
  - `y = 1` if `a` is true.
  - `y = b` if `a` is false.

![Lab 3 Output](https://github.com/user-attachments/assets/157b16d3-cecd-441a-aacf-bae296910886)


---

### Lab 3

Verilog code:

```verilog
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```

**Functionality:**  
2-to-1 multiplexer; `y = a ? 1 : b` (outputs `1` when `a` is true, otherwise `b`).

![Lab 3 Output](https://github.com/user-attachments/assets/157b16d3-cecd-441a-aacf-bae296910886)

---

### Lab 4

Verilog code:

```verilog
module opt_check4 (input a , input b , input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
 endmodule
```

**Functionality:**
- Three inputs (`a`, `b`, `c`), output `y`.
- Nested ternary logic:
  - If `a = 1`, `y = c`.
  - If `a = 0`, `y = !c`.
- Logic simplifies to:  
  `y = a ? c : !c`

![Lab 4 Output](https://github.com/user-attachments/assets/08d1e447-78c6-47c4-8c99-239645b38617)

---

### Lab 5

Verilog code:

```verilog
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```

**Functionality:**
- D flip-flop with:
  - Asynchronous reset to 0
  - Loads constant `1` when not in reset

![Lab 5 Output](https://github.com/user-attachments/assets/a42fac06-a092-4efc-be39-33b263caaaa1)

---

### Lab 6

Verilog code:

```verilog
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```

**Functionality:**
- D flip-flop always sets output `q` to `1` (regardless of reset or clock).

![Lab 6 Output](https://github.com/user-attachments/assets/ae45f7db-0a7f-4256-b43b-01cc4a1588f7)

---



