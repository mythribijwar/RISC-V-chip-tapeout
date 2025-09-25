# Day 2: Timing Libraries, Synthesis Techniques, and Optimized Flip-Flop Coding

Welcome to the second day of the RTL Workshop! Today’s focus includes three key areas:

Gaining insight into the .lib timing library (sky130_fd_sc_hd__tt_025C_1v80.lib) commonly used in open-source process design kits (PDKs).

Examining the differences between hierarchical and flat synthesis approaches.

Learning best practices for writing efficient and clean flip-flop code in RTL design.

## Timing Libraries

### SKY130 PDK Overview
The SKY130 PDK is an open-source Process Design Kit based on SkyWater Technology’s 130nm CMOS process. It includes essential models and libraries that support integrated circuit design, covering timing, power characteristics, and process variation data.

#### Decoding tt_025C_1v80 in the SKY130 PDK

tt: Stands for the typical process corner, representing standard manufacturing conditions.

025C: Indicates the operating temperature of 25°C, which affects device performance.

1v80: Specifies the core voltage at 1.8V.

### Opening and Exploring the .lib File
To open the sky130_fd_sc_hd__tt_025C_1v80.lib file:

Install a text editor:

    sudo apt install gedit
Open the file:

    gedit sky130_fd_sc_hd__tt_025C_1v80.lib


![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/variations.png)

## Hierarchical vs. Flattened Synthesis

### Hierarchical Synthesis

Definition: Preserves the module hierarchy as defined in the RTL code, synthesizing each module separately.

How it Works: Tools like Yosys analyze and synthesize each module independently using commands such as hierarchy to maintain the design structure.

#### Advantages:

Faster synthesis for large designs due to modular processing.

Easier debugging and analysis because module boundaries remain intact.

Supports a modular workflow, facilitating integration with other design tools.

#### Disadvantages:

Limited cross-module optimization opportunities.

Additional configuration may be needed for comprehensive reporting.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/multiple_modules.png)

### Flattened Synthesis

Definition: Combines all modules into a single flat netlist, removing the hierarchy.

How it Works: Using commands like flatten in Yosys, the hierarchy is collapsed, allowing optimizations across the entire design.

#### Advantages:

Enables aggressive optimizations that span multiple modules.

Produces a unified netlist, which can simplify some downstream tasks.

#### Disadvantages:

Longer synthesis time, especially for large designs.

Loss of hierarchy complicates debugging and analysis.

Potentially higher memory usage and increased netlist complexity.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/multiple_modules_flat.png)

#### simulation and systhesis steps are given at last
## Flip-Flop Coding Styles

Flip-flops are fundamental sequential elements in digital design, used to store binary data. Below are efficient coding styles for different reset/set behaviors.

### Asynchronous Reset D Flip-Flop

```verilog
module dff_asyncres (input clk, input async_reset, input d, output reg q);
  always @ (posedge clk, posedge async_reset)
    if (async_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```
- **Asynchronous reset**: Overrides clock, setting q to 0 immediately.
- **Edge-triggered**: Captures d on rising clock edge if reset is low.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_asyncres_gtk.png)
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_asyncres.png)
### Asynchronous Set D Flip-Flop

```verilog
module dff_async_set (input clk, input async_set, input d, output reg q);
  always @ (posedge clk, posedge async_set)
    if (async_set)
      q <= 1'b1;
    else
      q <= d;
endmodule
```
- **Asynchronous set**: Overrides clock, setting q to 1 immediately.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_async_set_gtk.png)
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_async_set.png)
### Synchronous Reset D Flip-Flop

```verilog
module dff_syncres (input clk, input async_reset, input sync_reset, input d, output reg q);
  always @ (posedge clk)
    if (sync_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```
- **Synchronous reset**: Takes effect only on the clock edge.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_asyncres_syncres_gtk.png)
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/7b4979b6b545b3831da384dc8f6f7161db587ddf/week1/day2/pictures/dff_syncres.png)
---

## Simulation and Synthesis Workflow

### Icarus Verilog Simulation

1. **Compile:**
   ```shell
   iverilog dff_asyncres.v tb_dff_asyncres.v
   ```
2. **Run:**
   ```shell
   ./a.out
   ```
3. **View Waveform:**
   ```shell
   gtkwave tb_dff_asyncres.vcd
   ```



### Synthesis with Yosys

1. Start Yosys:
   ```shell
   yosys
   ```
2. Read Liberty library:
   ```shell
   read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
3. Read Verilog code:
   ```shell
   read_verilog /path/to/dff_asyncres.v
   ```
4. Synthesize:
   ```shell
   synth -top dff_asyncres
   ```
5. Map flip-flops:
   ```shell
   dfflibmap -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
6. Technology mapping:
   ```shell
   abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   
   ``` 
7. for flattend synthesis :
   ```shell
   flatten
   ```
8. write verilog code
   ```shell
   write_verilog -noattr filename_flat.v
   ```
9. opens file after flattening
   ```shell
   !gvim filename_flat.v
   ```
10. Visualize the gate-level netlist:
   ```shell
   show
   ```
user hier in 8,9 instead of flat for hierachial sysnthesis




