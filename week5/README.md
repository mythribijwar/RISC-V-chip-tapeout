# **OpenROAD installation guide**  
**OpenROAD** is an open-source, fully automated RTL-to-GDSII flow for digital integrated circuit (IC) design. It supports synthesis, floorplanning, placement, clock tree synthesis, routing, and final layout generation. The tool is built to enable rapid design iterations and experimentation, making it ideal for academic and industrial use.  

---
## reference 
 https://cadhut.com/2022/08/07/how-to-install-openroad-and-other-vlsi-tools-under-ubuntu-22-04-or-linux-mint-21/#:~:text=If%20you%27re%20not%20using,install%20it%2C%20as%20shown%20below

### **Steps to Install OpenROAD and Run GUI**  

#### **1. Clone the OpenROAD Repository**  
      git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
      cd OpenROAD-flow-scripts
#### **2. Run the Setup Script**  
       sudo ./setup.sh

![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/b136105299dbd45b3738a1ad28a27730885d4dba/week5/pic/Screenshot%202025-10-25%20231050.png)
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/b136105299dbd45b3738a1ad28a27730885d4dba/week5/pic/image.png)

#### **3. Build OpenROAD**  

      ./build_openroad.sh --local

 error occured 
 ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/1b49e1256fa58670a536353bf839b3ba3ad62c24/week5/pic/Screenshot%202025-10-26%20003140.png)
 

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
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/1b49e1256fa58670a536353bf839b3ba3ad62c24/week5/pic/Screenshot%202025-10-26%20004410.png)
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/1b49e1256fa58670a536353bf839b3ba3ad62c24/week5/pic/Screenshot%202025-10-26%20004334.png)
