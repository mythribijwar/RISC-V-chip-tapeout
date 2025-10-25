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

![WhatsApp Image 2024-12-17 at 8 48 25 AM](https://github.com/user-attachments/assets/3c6f631c-8ce1-460e-8200-ca2f9c339af3)

#### **4. Verify Installation**  

       source ./env.sh
       yosys -help  
       openroad -help






#### **5. Run the OpenROAD Flow**  
       cd flow
       make

![WhatsApp Image 2024-12-17 at 8 48 24 AM](https://github.com/user-attachments/assets/9554cf56-e6bf-44f1-8096-80c0b4c48777)

##### 3. Launch the graphical user interface (GUI) to visualize the final layout:  
      make gui_final


#### directory structure
