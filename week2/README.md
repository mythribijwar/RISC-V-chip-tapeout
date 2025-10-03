# 🧠 SFAL-VSD-SoC-Journey  
## Fundamentals of SoC Design  

---

### **Problem Statement**

This project focuses on designing a small, open-source **System on Chip (SoC)** named **BabySoC**.  
It is built around the **RVMYTH** processor core, which follows the **RISC-V** architecture.  

The SoC integrates:  
- A **Phase-Locked Loop (PLL)** for stable and precise clock signal generation.  
- A **10-bit Digital-to-Analog Converter (DAC)** that converts digital data into analog signals.  

This conversion allows BabySoC to send analog outputs (like **audio or video**) to devices such as **televisions** and **mobile phones**.  
Built using **Sky130 technology**, BabySoC provides a well-documented, educational platform to learn about digital–analog interfacing and SoC design.

---

## **1. What is a System on a Chip (SoC)?**

A **System on a Chip (SoC)** is essentially a **complete computer built into a single chip**.  
Instead of having separate components for each function, all are combined into one small, efficient unit.  

This makes SoCs ideal for **compact**, **power-efficient**, and **high-performance** devices such as smartphones, tablets, and smartwatches.

---

### **Main Components of an SoC**

- **CPU (Central Processing Unit):**  
  The main brain of the chip that performs all processing tasks.

- **Memory:**  
  - **RAM** stores temporary data.  
  - **ROM/Flash** stores permanent data.

- **Input/Output (I/O) Ports:**  
  Enable communication with other devices like cameras, USB drives, or headphones.

- **GPU (Graphics Processing Unit):**  
  Handles visual data — gaming, videos, and user interfaces.

- **DSP (Digital Signal Processor):**  
  Manages real-time processing of audio and video signals.

- **Power Management Unit:**  
  Distributes power efficiently to maximize battery life.

- **Extra Modules:**  
  Often includes Wi-Fi, Bluetooth, and security systems.

---

### **Benefits of SoCs**

✅ **Compact Design:** Combines all components into a single chip.  
✅ **Energy Efficient:** Uses less power due to shorter internal connections.  
✅ **Fast Performance:** Reduced data travel distance increases speed.  
✅ **Low Cost:** Manufacturing one chip is cheaper than multiple components.  
✅ **More Reliable:** Fewer physical parts mean fewer points of failure.

---

### **Applications of SoCs**

- **Smartphones and Tablets** – Core of all modern mobile devices.  
- **Smartwatches and Wearables** – Used for health tracking and notifications.  
- **IoT Devices** – Found in smart home products and automation systems.  
- **Cars, TVs, and Appliances** – Embedded inside infotainment systems and electronic controls.

---

### **Popular SoCs**

| Manufacturer | Example SoC | Used In |
|---------------|-------------|---------|
| Apple | A-Series | iPhones, iPads |
| Qualcomm | Snapdragon | Android smartphones |
| Samsung | Exynos | Samsung devices |
| NVIDIA | Tegra | Nintendo Switch |

---

### **Challenges in SoC Design**

- **Complex Architecture:** Designing and verifying multiple modules together is challenging.  
- **Thermal Issues:** High density of transistors can lead to heating problems.  
- **Less Flexibility:** SoCs are difficult to modify once manufactured.

---

## **2. Types of SoCs**

1. **Microcontroller-Based SoC:**  
   - Simple and power-efficient.  
   - Ideal for basic control tasks like in home appliances, automotive systems, and IoT devices.

2. **Microprocessor-Based SoC:**  
   - Can run full operating systems (like Android or Linux).  
   - Used in smartphones and tablets for multitasking and complex applications.

3. **Application-Specific SoC (ASIC):**  
   - Designed for a specific function, such as graphics processing or AI.  
   - Highly optimized for speed and efficiency.

#### soc designflow
![image alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/969ddc6c81c0d245dea89903bb52df5e4b3e9bca/week2/pictures/soc_design_flow.png)

---

## **3. Introduction to VSDBabySoC**

**VSDBabySoC** is a **compact and educational RISC-V-based SoC**.  
It was created to test multiple open-source IP cores and calibrate its analog modules.  

### **Main Components**

- **RVMYTH Processor:** Performs data processing and computation.  
- **8x Phase-Locked Loop (PLL):** Produces a stable clock signal.  
- **10-bit Digital-to-Analog Converter (DAC):** Converts digital data into analog signals for external devices.


---

### **How VSDBabySoC Works**

1. **Clock Initialization:**  
   The PLL generates a stable and synchronized clock signal, ensuring all components operate together without timing mismatches.

2. **Data Processing (RVMYTH):**  
   The processor updates its **r17 register** with data that will later be converted into analog signals.

3. **Analog Signal Output (DAC):**  
   The DAC takes the digital data from RVMYTH and converts it into analog signals stored in an `OUT` file.  
   These signals can be used to drive devices such as **TVs or mobile phones**, producing **audio or video**.

---

## **4. Components in Detail**

### **RVMYTH (RISC-V CPU)**
- Open-source and simple processor core based on the RISC-V architecture.  
- Ideal for educational purposes and experimentation in CPU design.

---

### **Phase-Locked Loop (PLL)**

A **PLL** is an electronic control system that keeps its output signal synchronized in frequency and phase with an input signal.  

**Main Parts:**
1. **Phase Detector:** Compares input and output signals.  
2. **Loop Filter:** Converts phase error into a control voltage.  
3. **Voltage-Controlled Oscillator (VCO):** Adjusts its frequency based on the control voltage.

#### blockdaigram
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/969ddc6c81c0d245dea89903bb52df5e4b3e9bca/week2/pictures/pll.png)

**Purpose:**  
Maintains frequency stability and ensures synchronized operation within the SoC.

**Why On-Chip PLLs Are Better:**
- Lower signal delay and jitter.  
- Multiple frequency generation for different components.  
- More accurate and temperature-stable than off-chip crystals.

---

### **Digital-to-Analog Converter (DAC)**

A **DAC** transforms digital binary values (0s and 1s) into continuous analog signals such as voltage or current.

**Types of DACs:**
- **Weighted Resistor DAC:** Uses resistors of different values for each bit.  
  ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/969ddc6c81c0d245dea89903bb52df5e4b3e9bca/week2/pictures/weighted%20resistor%20DAC.jpg)
- **R-2R Ladder DAC:** Uses a repeating resistor network (R and 2R) for easier design.
  ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/969ddc6c81c0d245dea89903bb52df5e4b3e9bca/week2/pictures/r2r%20ladder%20dac.png)

**In BabySoC:**  
- Uses a **10-bit DAC**, which means it converts 10-bit digital data into one precise analog output.  
- Enables BabySoC to connect with real-world devices like **speakers, displays, and sensors**.

---

## **5. Conclusion**

**VSDBabySoC** shows how digital and analog components can work together inside a single chip.  
By combining a **RISC-V processor**, **PLL**, and **DAC**, it demonstrates the full process of:

1. Digital data processing  
2. Clock synchronization  
3. Analog signal generation  

This project provides a clear and practical foundation for learning about **embedded systems**, **SoC architecture**, and **digital-to-analog interfacing** — essential concepts in modern chip design.

---

## VSDBabySoC Project

### Overview

**VSDBabySoC** is a small-scale System-on-Chip (SoC) design that combines three main hardware blocks — a **RISC-V processor (rvmyth)**, a **Phase-Locked Loop (PLL)**, and a **Digital-to-Analog Converter (DAC)**.  
The project showcases how these IP cores can be integrated into a single system and verified through **pre-synthesis** and **post-synthesis simulations**.

---

### Project Structure

- **src/include/** → Contains Verilog header (`.vh`) files defining macros, constants, and parameters used in the design.  
- **src/module/** → Includes Verilog source code for each module that makes up the SoC.  
- **output/** → Stores simulation results, compiled files, and waveform outputs.

---

### Requirements

Make sure the following tools are installed before running the simulations:

- **Icarus Verilog** – to compile and simulate the Verilog design  
- **GTKWave** – to visualize the waveform outputs (`.vcd` files)

> ⚙️ This project is intended to be executed in a Unix-like environment such as **Linux** or **macOS**.

### 1. Setup 
Clone or set up the directory structure as follows:

```bash
        VSDBabySoC/
├── src/
│   ├── include/
│   │   ├── sandpiper.vh
│   │   └── other header files...
│   ├── module/
│   │   ├── vsdbabysoc.v      # Top-level module integrating all components
│   │   ├── rvmyth.v          # RISC-V core module
│   │   ├── avsdpll.v         # PLL module
│   │   ├── avsddac.v         # DAC module
│   │   └── testbench.v       # Testbench for simulation
└── output/
└── compiled_tlv/         # Holds compiled intermediate files if needed

```
### 2. Module Descriptions

#### 2.1 Top-Level SoC: `vsdbabysoc.v`

The `vsdbabysoc` module serves as the top-level design integrating the RISC-V core (`rvmyth`), PLL (`avsdpll`), and DAC (`avsddac`).

[VSDBabySoC](https://github.com/manili/VSDBabySoC.git)

**Inputs:**
- `reset` – resets the processor  
- `VCO_IN`, `ENb_CP`, `ENb_VCO`, `REF` – PLL control signals  
- `VREFH` – DAC reference voltage  

**Outputs:**
- `OUT` – analog output from the DAC  

**Connections:**
- `RV_TO_DAC` – 10-bit bus connecting RISC-V output to DAC input  
- `CLK` – clock signal generated by the PLL  

---

#### 2.2 RISC-V Core: `rvmyth.v`

The `rvmyth` module implements a simple RISC-V processor that outputs a 10-bit digital signal to the DAC.
  [rvmyth](https://github.com/kunalg123/rvmyth/)

**Inputs:**
- `CLK` – clock signal from the PLL  
- `reset` – initializes or resets the processor  

**Output:**
- `OUT` – 10-bit digital signal to be converted by the DAC  

---

#### 2.3 PLL Module: `avsdpll.v`

The `avsdpll` module generates a stable clock to synchronize the RISC-V core and other modules.

[avsdpll](https://github.com/lakshmi-sathi/avsdpll_1v8.git)

**Inputs:**
- `VCO_IN`, `ENb_CP`, `ENb_VCO`, `REF` – PLL control and reference signals  

**Output:**
- `CLK` – stable clock signal  

---

#### 2.4 DAC Module: `avsddac.v`

The `avsddac` module converts the 10-bit digital signal from the processor into an analog output.
 [avsddac](https://github.com/vsdip/rvmyth_avsddac_interface.git)

**Inputs:**
- `D` – 10-bit digital input from the processor  
- `VREFH` – DAC reference voltage  

**Output:**
- `OUT` – analog output signal  

---
### 3. Testbench

The `testbench.v` module verifies the functionality of the `vsdbabysoc` design. It provides:

- Clock generation  
- Reset initialization  
- Waveform dumping for simulation  

**Waveform files generated:**
- `pre_synth_sim.vcd` – pre-synthesis simulation  
- `post_synth_sim.vcd` – post-synthesis simulation  

---

### 4. Simulation Steps:

Run the following commands:

1.install the required packages 
```bash
 # Install tools
sudo apt update
sudo apt install python3-venv python3-pip

# Create virtual env
python3 -m venv sp_env
source sp_env/bin/activate

# Install SandPiper-SaaS
pip install pyyaml click sandpiper-saas

# Convert TLV → Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```
2.gitclone VSDBabySoc design files and testbenches

3. cd /home/mythri/VSDBabySoc
#### Pre-Synthesis Simulation
```bash
mkdir -p output/pre_synth_sim

iverilog -o output/pre_synth_sim/pre_synth_sim.out \
  -DPRE_SYNTH_SIM \
  -I src/include -I src/module \
  src/module/testbench.v

cd output/pre_synth_sim
./pre_synth_sim.out
```
explanation:
-DPRE_SYNTH_SIM defines a macro for conditional compilation in the testbench.

The resulting pre_synth_sim.vcd file can be visualized using GTKWave.



viewing waveforms

```bash
  gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/969ddc6c81c0d245dea89903bb52df5e4b3e9bca/week2/pictures/presynth.png)

In this picture we see the following signals:

CLK: This is the input CLK  of the RVMYTH core. This signal comes from the PLL, originally.

reset: This is the input reset signal of the RVMYTH core. This signal comes from an external source, originally.

OUT: This is the output OUT signal of the VSDBabySoC module. This signal comes from the DAC (due to simulation restrictions it behaves like a digital signal which is incorrect), originally.

RV_TO_DAC[9:0]: This is the 10-bit output [9:0] OUT port of the RVMYTH core. This port comes from the RVMYTH register #17, originally.

OUT: This is a real datatype net which can simulate analog values. It is the output net real OUT signal of the DAC module. This signal comes from the DAC, originally.

#### Post-Synthesis Simulation
Run the following commands:
Copy code
```Bash
iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM \
-I src/include -I src/module \
src/module/testbench.v output/synthesized/vsdbabysoc.synth.v
cd output/post_synth_sim
./post_synth_sim.out
```

This verifies the SoC behavior after synthesis.

### 5. Summary
vsdbabysoc.v – Integrates the RISC-V core, PLL, and DAC

rvmyth.v – Produces a 10-bit digital output signal

avsdpll.v – Generates a stable clock signal

avsddac.v – Converts digital data to analog output

testbench.v – Validates functionality through pre- and post-synthesis simulations
