# **OpenROAD installation guide**  
**OpenROAD** is an open-source, fully automated RTL-to-GDSII flow for digital integrated circuit (IC) design. It supports synthesis, floorplanning, placement, clock tree synthesis, routing, and final layout generation. The tool is built to enable rapid design iterations and experimentation, making it ideal for academic and industrial use.  

---

### **Steps to Install OpenROAD and Run GUI**  

#### **1. Clone the OpenROAD Repository**  
      git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
      cd OpenROAD-flow-script
#### **2. Run the Setup Script**  
       sudo ./setup.sh



#### **3. Build OpenROAD**  

      ./build_openroad.sh --local


#### **4. Verify Installation**  

       source ./env.sh
       yosys -help  
       openroad -help






#### **5. Run the OpenROAD Flow**  
       cd flow
       make


##### 3. Launch the graphical user interface (GUI) to visualize the final layout:  
      make gui_final


#### directory structure
