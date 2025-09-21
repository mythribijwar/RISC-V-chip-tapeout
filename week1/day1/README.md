1)WHAT IS A SIMULATOR, DESIGN, AND TESTBENCH?

 Simulator

 A simulator is a software tool used to simulate and verify the behavior of your digital circuit. It allows you to input test    signals into your design and check the outputs. This ensures that your circuit functions correctly without having to implement  it physically, saving both time and resources.

 Design

 The design refers to your Verilog (or other hardware description language) code that defines the intended logic and             functionality of the digital circuit you want to create.

 Testbench

 A testbench is a special environment or code written to apply different test inputs to the design and observe the outputs. It   helps in verifying if the design works as expected by comparing the generated outputs with the expected results.

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/194c2e54db9721c223e69d47952dabd7f608f9bd/week1/day1/pictures/testbench_pic.jpg)

2)IVERILOG

Iverilog is an open-source simulator for Verilog that compiles and simulates both design and testbench files. It generates a .vcd file for waveform visualization in GTKWave.
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/194c2e54db9721c223e69d47952dabd7f608f9bd/week1/day1/pictures/iverilog_based_simulationflow.jpg)

3)LAB:simulating MULTIPLEXER 2:1

 follow the below steps
 
 a)Clone the Workshop Repository
 
    git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
    cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
    
 b)Install Required Tools
 
    sudo apt install iverilog
    sudo apt install gtkwave
    
 c)Simulate the Design
 
   Compile the design and testbench

    iverilog good_mux.v tb_good_mux.v
   Run the simulation

    ./a.out
   View  waveform

    gtkwave tb_good_mux.vcd
    
   ![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/59762b3502b1246e29eebdc12ecb40e98543177a/week1/day1/pictures/tb_output.png)
   
4)VERILOG CODE

  command to be given to see the code(access your verilog_files)
  
     /home/mythri/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files# gvim tb_good_mux.v -o good_mux.v
     
   ![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/936638c86cd1a12cf1a3b646993b8d0c7b38c1ac/week1/day1/pictures/2_1%20mux%20code.png)
   ![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/936638c86cd1a12cf1a3b646993b8d0c7b38c1ac/week1/day1/pictures/2_1%20mux%20tb%20code.png)
   
5)INTRODUCTION TO YOSYS AND GATE LIBRARIES

  a)What is Yosys?

   -Yosys is a powerful open-source synthesis tool for digital hardware. It takes your Verilog code and converts it into a       gate- level netlist, which is a detailed hardware blueprint showing gates and their connections.

  ![image alt]( https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/d394bf9fb1d3f010ddffae0df3749d17d8c7abc1/week1/day1/pictures/yosys_setup.jpg)

  b)What is Synthesis (RTL to Gate-Level Translation)?

   -Synthesis is the process of converting a Register Transfer Level (RTL) design (written in Verilog or VHDL) into a gate-      level netlist.

   -The design is translated into logic gates (AND, OR, NAND, NOR, etc.).

   -The connections between these gates are established.

   -The output is typically a netlist file (.sa or similar) that describes the gates and their interconnections.

  c)What is a .lib file?

   -A .lib file is a library file that contains:

   -A collection of logical modules or gates (like NAND, NOR, OR, etc.).

   -Different “flavors” or variants of the same gate with different characteristics (speed, power, size).

  d)Why Different Flavors of Gates?

   -Combinational delay (t_combi) in the logic path affects the maximum operating speed of a digital circuit (e.g., clock        speed).

   -The clock period (t_clock) > (t_combi )for correct operation
   
   -Faster cells help reduce t_combi and increase speed, but are they always enough?

  e)Why Do We Need Slow Cells?

   -Slow cells are needed to avoid hold time violations (hold issues).

   -Example: If Flip-Flop A is fast and Flip-Flop B is too fast, B might capture the wrong data before A's output settles.

   -Mixing fast and slow cells helps balance timing and ensure reliable data transfer.

 f)Faster Cells vs Slower Cells

  -Faster cells have wider transistors that can source or sink more current, charging and discharging capacitive loads          quicker → lower delay but larger area and power consumption.

  -Slower cells use smaller transistors → higher delay but save area and power.
