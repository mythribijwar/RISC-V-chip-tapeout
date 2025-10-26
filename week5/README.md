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

 #### to correct error
  use  below command to setup everything to remove error
  
             sudo ./etc/DependencyInstaller.sh -all
   repeat step 3
        
  

#### **4. Verify Installation**  

       source ./env.sh
       yosys -help  
       openroad -help
 ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/6e4eb95acd77c56e580ce0772384057134320c4a/week5/pic/Screenshot%202025-10-26%20095908.png)





#### **5. Run the OpenROAD Flow**  
       cd flow
       make


   ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/6e4eb95acd77c56e580ce0772384057134320c4a/week5/pic/Screenshot%202025-10-26%20100232.png)

#### **6.Launch the graphical user interface (GUI) to visualize the final layout:**  
      make gui_final
      
   ![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/30a109862756a7cc5704f02770ad841b6eb05f96/week5/pic/Screenshot%202025-10-26%20100441.png)


### directory structure
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/1b49e1256fa58670a536353bf839b3ba3ad62c24/week5/pic/Screenshot%202025-10-26%20004410.png)
![img alt](https://github.com/mythribijwar/RISC-V-chip-tapeout/blob/1b49e1256fa58670a536353bf839b3ba3ad62c24/week5/pic/Screenshot%202025-10-26%20004334.png)
