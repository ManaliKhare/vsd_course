# vsd_course Day 1

1. Invoke openlane:

Once the virtual machine is up, open a Terminal and go to the directory highlighted in red in below snapshot. Then type docker, it will open a bash shell, them type './flow.tcl -interactive'. Interactive mode is to execute rtl2gds flow step by step for better understanding. 

![image](https://github.com/user-attachments/assets/626e3420-b13c-488a-9209-054627eee2e5)

2. Inside the directory "~/Desktop/work/tools/openlane_working_dir" there is also the "pkds" directory. PDK is process design kit, which comes from the Foundry. It has the information on the libraries, tech files, various rules files to be used while designing in a particular technology.
   

![image](https://github.com/user-attachments/assets/fd2f917f-0618-46ad-86e4-bea6036dfe41)

In below snapshot, inside the Sky130A pdk variant (sky130 is the node 130nm), there is libs.tech directory which has all files specific to the tools to be used for the RTL2GDS flow and libs.ref which has all the process specific files like lib, lef, tech lef, spice, verilog etc.
![image](https://github.com/user-attachments/assets/0b7e46b3-9f4a-4cb3-b203-85c79d57e052)
![image](https://github.com/user-attachments/assets/9206b0ee-ffaa-42dc-8bb1-c126e1bfa95b)
Files inside lib directory: It has the libs for different PVT corners (process, voltage, temperature)
![image](https://github.com/user-attachments/assets/a7e74373-2ab5-47cc-8420-f223c96ede4b)

Files inside verilog directory: Verilog fiiles for all components like decap, fake diode, standard cells etc.
![image](https://github.com/user-attachments/assets/c343ddcb-462e-46e9-bca8-03bd7599aa43)

Files inside lef directory: Lef files for all cells like decap, fakediode, standard cells etc.
![image](https://github.com/user-attachments/assets/76edd5d8-9315-4ee3-81b8-ba83fcbd2403)

Files inside techlef directory: Tech lef file has information on the metak and via stack 
![image](https://github.com/user-attachments/assets/28071480-930f-4433-bb35-0cfd2bbc84ac)
![image](https://github.com/user-attachments/assets/d03da675-919d-45f2-824d-e1c850567fab)

Files inside the spice directory: Spice netlists for the cells.
![image](https://github.com/user-attachments/assets/7ce69cbb-9cd8-42e6-a2e4-d44eca54ace1)

3. Designs built in openlane: We would be using the design picorv32a.
![image](https://github.com/user-attachments/assets/bccb2293-36dd-40e8-9b6f-90f3b2afb4dc)

4. Contents inside picorv2 directory. src has the rtl netlist and the sdc. config.tcl file is to overwrite the default openlane settings.
![image](https://github.com/user-attachments/assets/f49454ba-da73-44c1-b10e-5297c61084e6)
   config.tcl file is to set the pointers to the input files and to set values for parameters like clock period.
   ![image](https://github.com/user-attachments/assets/cf9279bb-088c-417c-a8e4-f6399362d551)

   sky130A_sky130_fd_sc_hd_config.tcl file can overwrite the settings from config.tcl. sky130A_sky130_fd_sc_hd_config.tcl has highest priority.
![image](https://github.com/user-attachments/assets/8b9f9cfb-efb9-4938-935c-0d488e059bf7)

5. Steps to run the openlane flow:

   
![openlane_flow](https://github.com/user-attachments/assets/fb3cc285-2a34-473e-b346-79db54c2cf81)



a. package require openlane 0.9
![image](https://github.com/user-attachments/assets/5eadd84e-49cb-4919-96b8-b6fa269dd47e)

b. design setup step: prep -design <design_name> - This step merges the cell lef and tech lef, sets the PDK path, sources config.tcl file, creates a run directory with the present date.
![image](https://github.com/user-attachments/assets/c3954947-8216-45bf-9743-1ac4a6519667)

Inside the runs directory created after prep design, there is 
![image](https://github.com/user-attachments/assets/bdf62bda-ba84-4ef6-b754-446a20910bf4)

Everything except tmp directory would be initially empty. tmp directory stores the temporary files. it also has the merged.lef file.

![image](https://github.com/user-attachments/assets/ac9dcd6d-1b5b-45e2-8c8a-4130e2052113)

A config.tcl file is also created inside the runs/<date> directory which has info on the pdk paths and all other input file paths, and the final settings used in the run.
![image](https://github.com/user-attachments/assets/2b4a9af4-0c69-4ae3-b3bd-5066a0524de9)

c. run_synthesis:
This command runs the sysnthesis on the RTL netlist.

Inside the results/synthesis directory. There is the synthesised netlist.
![image](https://github.com/user-attachments/assets/4c62fd4a-7090-4e83-9661-54289c9388e1)

Calculate the flop ratio = Total no. of DFF/ Total no. of cells in design = 1613/14876 = 0.1084 = 10.84%

![image](https://github.com/user-attachments/assets/aac65c60-bc60-4004-ae8d-e2a2c9f1825b)

Inside the reports/synthesis directory. The last generated yosys report gives the synthesis stats.
![image](https://github.com/user-attachments/assets/8c01b1a4-fb81-4ea3-8343-a4d285d984ce)

# vsd_course Day 2

Utilization Factor = {Area of the netlist/Area of the chip}

run_floorplan:

Standard cell placement happens not in floorplan but during placement.

![image](https://github.com/user-attachments/assets/5f0d729b-1247-4eda-949e-c1e039d7dea9)

Dimensions of the chip = 660685/1000 x 671405/1000 = 660.685 um x 671.405 um

Area of the chip = 660.685 um x 671.405 um = 4,43,587.212425 um2 

![image](https://github.com/user-attachments/assets/4cd58187-0008-4b61-8b79-73626aeffed6)

Opening magic to view the floorplan:

![image](https://github.com/user-attachments/assets/e6d5fe69-1d3f-4a4d-9320-20c330175900)

![image](https://github.com/user-attachments/assets/cc5acf66-7d4b-4de5-a287-66c078d715a4)

Horizontal IO pins are at Metal 3:
![image](https://github.com/user-attachments/assets/6b485381-7862-455e-b6a2-51596cffda73)

Vertical IO pins are at Metal 2:
![image](https://github.com/user-attachments/assets/708df43d-f60e-4ecf-bacb-dcbae8b9c4ff)

Decaps and Tap cells placemnet:
![image](https://github.com/user-attachments/assets/5ca6f68b-1089-4529-921c-793dc8b3c1bb)

Standard cells placement:
![image](https://github.com/user-attachments/assets/fee4cfad-07df-4284-b8cc-298ddf9e36b8)

## Placement & Routing

1. Bind netlist with physical cells:
* In reality, each gate in netlist is represented as a rectangular box with specific width and height.
* Library consists of information related to the sizing of the cell, the delay, and the when conditions.
* Additoionally, Library also offers various flavors of the same cell i.e. cell with a bigger size, hence lesser delay, hence faster.

2. Placement of cells:
* Place the cells such that the input cells are closer to the input ports and output cells are closer to the output ports.
  
3. Optimize Placement:
* This is the stage where we estimate the wire length and capacitance and insert repeaters accordingly.
* Repeaters are buffers that recondition the original signal, and send it ahead to next stage. They are placed to account for the loss of signal due to long routes.
* This is called signal integrity.
* However, adding repeaters will cost more area.
  ![image](https://github.com/user-attachments/assets/f4f6ab36-4ebf-450e-8331-fc8a73ebc4b5)
* Once the placement is optimized after adding buffers, do a quick setup timing analysis considering ideal clock, to find if the placement of cells done is reasonable and meets the timing specs.

## Library characterization and Modeling

![image](https://github.com/user-attachments/assets/e9ca87a6-ef5d-454d-a934-91c0648abe95)

* Library files model the gates in such a fashion so that it would be understood by the EDA tool. It describes the functionality, timing characteristics of the gates.

## Congestion aware placement using RePLace
![image](https://github.com/user-attachments/assets/c26997fd-3d1d-4689-b052-a6de151d18ec)

* In placement, first step is global placement which focuses on reductin of wire length (HPWL)
* HPWL - Half Parameter Wire Length , OVFL - Overflow
* Placement ensures that standard cells are placed correctly in standard cell rows.
* PDN happens after CTS


## Cell design and characterization flows:

1. Inputs for cell design flow:
* Library files - Library has cells with diff functionality &  different sizes & different Threshold voltages.
* Inputs for cell design, eg Inverter - PDK (Process Design Kits) given by Foundry which has DRC & LVS rules (Tech files), SPICE models (), libs and user defined specs
![image](https://github.com/user-attachments/assets/1075cc17-bb41-4105-a492-b2c0656c7bd9)

* User defined specs:
   - Cell-height - Separation between the power and ground rail
   - Cell-width - Decided by the drive strength of the cell
   - Supply Voltage - Operating voltage of chip, according to the supply voltage library developer has to design a cell which will operate at given supply voltage, takinmg care of the noise margin levels
   - Metal layers
   - Pin locations
   - Drawn gate length
  
2. Design steps:
* Circuit design
   - Implement the function
   - Decide the sizing of the PMOS & NMOS, mainly to satisfy the equation Idp + Idn = 0 , Idp
     - Idp - Drain current of PMOS, Idn - Drain current of NMOS   
   - Output of this step is CDL file - Circuit Description Language
* Layout design - Euler's path -> Stick diagram -> Layout
   - ![image](https://github.com/user-attachments/assets/59173168-a6be-46bd-ac98-1416467dccc2)
   - ![image](https://github.com/user-attachments/assets/039c3535-cf45-46d1-9775-0de560696290)
   - Layout design - Magic open source layout design tool
   - Extract the RLC parasitics from the layout 

* Characterization -
   - ![image](https://github.com/user-attachments/assets/8c5a264e-8320-43a0-8af7-8be0f0506dc3)
   - ![image](https://github.com/user-attachments/assets/f5839002-a72d-4b09-a8e5-bdd13d51c444)
   - ![image](https://github.com/user-attachments/assets/54a349ce-eea9-4d6f-a986-e8f844a7f40c)

3. Output - CDL, GDSII, LEF, Extracted spice netlist (.cir), timing .libs, noise .libs, power .libs, function
  
## Timing Characterization
![image](https://github.com/user-attachments/assets/07a5f490-b027-4818-ba4f-9ead063437f4)

Propagation delay : out_rise_thr - in_rise_thr & out_fall_thr - in_fall_thr

![image](https://github.com/user-attachments/assets/ffda83d9-ed92-41cd-b39d-70cf1e09c1a1)
   - Choosing the right threshold points is important to avoid negative propagation delays.
   - Also, huge wire delays due to long routes can cause negative delays which needs to be rectified.
![image](https://github.com/user-attachments/assets/a1cbe3b4-a3d7-46d2-bb30-35f35bc70130)

# vsd_course Day 3

## Changing the variable on the fly and rerun:
Changing the IO pins placement mode from 1 to 2 and seeing the difference in the IO pins placement.
With mode 1, the pins are placed equidistant:
![image](https://github.com/user-attachments/assets/a77b9cc1-72e1-4d65-a1e6-21d6558b4371)

With mode 2 set on the fly, the IO pins placement changes



