Day 2: Timing Libraries, Synthesis Techniques, and Optimized Flip-Flop Coding

Welcome to the second day of the RTL Workshop! Today’s focus includes three key areas:

Gaining insight into the .lib timing library (sky130_fd_sc_hd__tt_025C_1v80.lib) commonly used in open-source process design kits (PDKs).

Examining the differences between hierarchical and flat synthesis approaches.

Learning best practices for writing efficient and clean flip-flop code in RTL design.

Timing Libraries

SKY130 PDK Overview
The SKY130 PDK is an open-source Process Design Kit based on SkyWater Technology’s 130nm CMOS process. It includes essential models and libraries that support integrated circuit design, covering timing, power characteristics, and process variation data.

Decoding tt_025C_1v80 in the SKY130 PDK

tt: Stands for the typical process corner, representing standard manufacturing conditions.

025C: Indicates the operating temperature of 25°C, which affects device performance.

1v80: Specifies the core voltage at 1.8V.

ierarchical vs. Flattened Synthesis

Hierarchical Synthesis

Definition: Preserves the module hierarchy as defined in the RTL code, synthesizing each module separately.

How it Works: Tools like Yosys analyze and synthesize each module independently using commands such as hierarchy to maintain the design structure.

Advantages:

Faster synthesis for large designs due to modular processing.

Easier debugging and analysis because module boundaries remain intact.

Supports a modular workflow, facilitating integration with other design tools.

Disadvantages:

Limited cross-module optimization opportunities.

Additional configuration may be needed for comprehensive reporting.

Flattened Synthesis

Definition: Combines all modules into a single flat netlist, removing the hierarchy.

How it Works: Using commands like flatten in Yosys, the hierarchy is collapsed, allowing optimizations across the entire design.

Advantages:

Enables aggressive optimizations that span multiple modules.

Produces a unified netlist, which can simplify some downstream tasks.

Disadvantages:

Longer synthesis time, especially for large designs.

Loss of hierarchy complicates debugging and analysis.

Potentially higher memory usage and increased netlist complexity.
