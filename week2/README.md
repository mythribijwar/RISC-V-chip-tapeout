# 🧠 SFAL-VSD-SoC-Journey  
## 11. Fundamentals of SoC Design  

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
- **R-2R Ladder DAC:** Uses a repeating resistor network (R and 2R) for easier design.

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