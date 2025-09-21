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
