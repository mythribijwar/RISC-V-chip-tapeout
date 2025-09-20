System and Virtual Machine Configuration
I configured a Virtual Machine (VM) with the following specifications:


 Operating SystemM :	Ubuntu 20.04+
 
  RAM :	6GB
  
  Storage :	50GB HDD
  
  vCPUs :	4

TOOLS INSTALLATION AND VERIFICATION

1.Yosys – RTL Synthesis Tool

Purpose: Converts RTL code into gate-level representations.

Installation steps

                               
    $ git clone https://github.com/YosysHQ/yosys.git
    $ cd yosys 
    $ sudo apt install make # (If make is not installed please install it) 
    $ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
    $ make 
    $ sudo make install
    
Installation Verification 

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/817fafa14027075e23581ce5d335aa7e5145b07b/week0/verification%20pic/yosys.png)

2.Iverilog – Verilog Simulator

Purpose: Compiles and simulates Verilog designs for functional verification.

Installation steps

    $ sudo apt-get install iverilog

Installation Verification 

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/817fafa14027075e23581ce5d335aa7e5145b07b/week0/verification%20pic/iverilog.png)

3.GTKWave – Waveform Viewer

Purpose: Analyzes and visualizes simulation waveforms for debugging.

Installation steps

    $ sudo apt update
    $ sudo apt install gtkwave

Installation Verification 

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/817fafa14027075e23581ce5d335aa7e5145b07b/week0/verification%20pic/gtkwave.png)

4.Ngspice – Circuit Simulator

Purpose: Performs analog and mixed-signal circuit simulation.

Installation steps

    $ sudo apt update
    $ sudo apt install ngspice

Installation Verification 

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/817fafa14027075e23581ce5d335aa7e5145b07b/week0/verification%20pic/ngspice.png)

5.Magic VLSI – Layout Tool

Magic VLSI is an open-source VLSI layout tool widely used for IC design, DRC, and visualization.

Installation steps

Follow the steps to install Magic on an Ubuntu system:

    # Install required dependencies
    sudo apt-get install m4
    sudo apt-get install tcsh
    sudo apt-get install csh
    sudo apt-get install libx11-dev
    sudo apt-get install tcl-dev tk-dev
    sudo apt-get install libcairo2-dev
    sudo apt-get install mesa-common-dev libglu1-mesa-dev
    sudo apt-get install libncurses-dev

    # Clone Magic repository
    git clone https://github.com/RTimothyEdwards/magic
    cd magic

    # Configure build
    ./configure

    # Build Magic
    make

    # Install system-wide
    sudo make install
    
Installation Verification 

![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/817fafa14027075e23581ce5d335aa7e5145b07b/week0/verification%20pic/magicvlsi.png)
