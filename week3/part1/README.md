# GLS OF BABYSOC
## POST-SYNTHESIS SIMULATION

### Purpose of GLS:
Gate-Level Simulation is used to verify the functionality of a design after the synthesis process. Unlike behavioral or RTL (Register Transfer Level) simulations, which are performed at a higher level of abstraction, GLS works on the netlist generated post-synthesis. This netlist includes the actual gates and connections used to implement the design.

### Key Aspects of GLS for BabySoC:
1. **Verification with Timing Information:**
   - GLS is performed using Standard Delay Format (SDF) files to ensure timing correctness.
   - This checks if the SoC behaves as expected under real-world timing constraints.

2. **Design Validation Post-Synthesis:**
   - Confirms that the design's logical behavior remains correct after mapping it to the gate-level representation.
   - Ensures that the design is free from issues like metastability or glitches.

3. **Simulation Tools:**
   - Tools like Icarus Verilog or a similar simulator can be used for compiling and running the gate-level netlist.
   - Waveforms are typically analyzed using GTKWave.

4. **Importance for BabySoC:**
   - BabySoC consists of multiple modules like the RISC-V processor, PLL, and DAC. GLS ensures that these modules interact correctly and meet the timing requirements in the synthesized design.


Here is the step-by-step execution plan for running the  commands manually:

---

### Step 0: 
```bash
mkdir -p output/post_synth_sim
```

### **Step 1: Load the Top-Level Design and Supporting Modules**
```bash
yosys
```

Inside the Yosys shell, run:
```yosys
read_verilog /home/mythri/VLSI/VSDBabySoC/src/module/vsdbabysoc.v
read_verilog -I /home/mythri/VLSI/VSDBabySoC/src/include /home/mythri/VLSI/VSDBabySoC/src/module/rvmyth.v
read_verilog -I /home/mythri/VLSI/VSDBabySoC/src/include /home/mythri/VLSI/VSDBabySoC/src/module/clk_gate.v
```


---

### **Step 2: Load the Liberty Files for Synthesis**
Inside the same Yosys shell, run:
```yosys
read_liberty -lib /home/mythri/VLSI/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -lib /home/mythri/VLSI/VSDBabySoC/src/lib/avsddac.lib
read_liberty -lib /home/mythri/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```


---

### **Step 3: Run Synthesis Targeting `vsdbabysoc`**
```yosys
synth -top vsdbabysoc
```


---

### **Step 4: Map D Flip-Flops to Standard Cells**
```yosys
dfflibmap -liberty /home/mythri/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```


---

### **Step 5: Perform Optimization and Technology Mapping**
```yosys


opt
abc -liberty /home/mythri/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}
```
---

### **Step 6: Perform Final Clean-Up and Renaming**
```yosys
flatten
setundef -zero
clean -purge
rename -enumerate
```


---

### **Step 7: Check Statistics**
```yosys
stat
```


---

### **Step 8: Write the Synthesized Netlist**
```yosys
write_verilog -noattr /home/mythri/VLSI/VSDBabySoC/output/post_synth_sim/vsdbabysoc.synth.v

```


---

## POST_SYNTHESIS SIMULATION AND WAVEFORMS
---

### **Step 1: Compile the Testbench**
Run the following `iverilog` command to compile the testbench:
```bash
iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM \
-I src/include -I src/module \
src/module/testbench.v output/post_synth_sim/vsdbabysoc.synth.v
cd output/post_synth_sim
./post_synth_sim.out
```
---
### **Step 2: Navigate to the Post-Synthesis Simulation Output Directory**
```bash
cd output/post_synth_sim/
```
---
### **Step 3: Run the Simulation**

```bash
./post_synth_sim.out
```
---
### **Step 4: View the Waveforms in GTKWave**

```bash
gtkwave post_synth_sim.vcd
```
---




