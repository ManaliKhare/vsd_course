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


## Spice deck creation for CMOS inverter
![image](https://github.com/user-attachments/assets/f1f95501-d4b5-4452-a8e6-06d480eea577)

![image](https://github.com/user-attachments/assets/0e9f85d7-a357-411b-ba1d-a3cd47992f5f)
![image](https://github.com/user-attachments/assets/d172445a-18bc-4a5d-848d-25e794e6ba07)
.mod is the model file for NMOS &PMOS which has all the parameters for the mos devices.

![image](https://github.com/user-attachments/assets/38095a67-570f-4de2-b0c8-4046a58df8b5)


![image](https://github.com/user-attachments/assets/5459785d-d158-4602-8735-92f5d9ee9453)
- CMOS inverter is a robust device. Inverter characteristics are maintained across all devic sizes.
- Switching threshold- Point where Vin = Vout
- Switching throshold is computed by drawing a 45degree line on the dc transfer characteristics and finding the intersection point.
![image](https://github.com/user-attachments/assets/c4ce3875-4af7-4412-bd59-128e4ed3edb6)
![image](https://github.com/user-attachments/assets/922b689d-f4c1-4318-9f80-f275f172d4cf)
- The rise and fall delay of cmos inv can be calculated by doing a transient analysis and using a pulse signal at the input Vin.
- Plot Vout & Vin overlapping and find the time diff when 50% Vout - 50% Vin
- When Wp/Lp = Wn/Ln = 1.5, Vm = 0.99V and Rise delay = 148ps and Fall delay = 71ps.
![image](https://github.com/user-attachments/assets/7bb94da7-e630-43ec-ac7b-8ec24ab8eae2)

- Clone the setup from github
  ![image](https://github.com/user-attachments/assets/260713b4-b548-453b-afd7-ab49acfc4c35)
  ![image](https://github.com/user-attachments/assets/ba8d204b-f216-45d9-a132-da11ae95e025)
     - copy the sky130A.tech file to the cloned directory
       ![image](https://github.com/user-attachments/assets/5a11d6fe-7c31-47c1-a44e-83c291d79fa5)
     - Open magic tool to check CMOS inv layout ![image](https://github.com/user-attachments/assets/697c8580-ecdd-4ad4-a393-6c614e1742bb)
     - CMOS inv layout looks like below, named as sky130_inv
       ![image](https://github.com/user-attachments/assets/e2f12492-f61b-4805-a802-9dc6d39fdb31)

- CMOS Fabrication Process : 16 Mask CMOS process
   1. Selecting a substrate: P type substrate with a doping level less than the well doping. Doping is 10^15cm-3, orientation 100
   2. Creating the active regions for transistors:
        - Isolation is required for the pockets
        - Deposit 40nm Silicon dioxide SiO2 & 80nm od Silicon Nitrie Si3N4 & 1um of photoresist. Masks allow some regions of photoresist to be exposed to UV light which are later washed off to get desired patterns.
          ![image](https://github.com/user-attachments/assets/4bb796d3-d9c3-417a-b07d-f61230b7bd16)
        - Later the remainig photoresist is removed chemically and the Si wafer is put in oxidation furnace for SiO2 desposition in the gaps which will later act as isolation between two MOS devices (Field oxide). The process is called LOCOS - Local Oxidation of Silicon
          
          ![image](https://github.com/user-attachments/assets/0953a52a-f294-47b6-8f9b-30e9682f01e6)
        - The Si3N4 is removed in hot phosphoric acid.
          ![image](https://github.com/user-attachments/assets/8fb5ede9-a4a9-4ed7-938b-c0b53426c39f)

   3. N-well & P-well fabrication:
        - We will protect one active area with a photoresist and mask2 and expose the other active area.
        - Create P-well using Boron ion implantation (high energy impantation 200keV)
          ![image](https://github.com/user-attachments/assets/1c995b7e-2cec-44b9-84ac-fc06f4e685f9)
        - Next we will use Mask3 to protect the first active and expose 2nd active to form N-well. Ion implantation of Phosphorous done for N-well.
        - Next put the substrate in a drive-in furnace at 1100 Degree for ~6hrs, to diffuse Boron and Phosphorous ions deeper in the p-substrate to form twin wells.
          ![image](https://github.com/user-attachments/assets/c3694001-e18c-4d90-ad24-ba9871516c5e)

   4. Formation of Gate terminal:
        - Doping concentration and Oxide capacitance directly impacts the threshold voltage Vt. Vt is applied at Gate terminal
          ![image](https://github.com/user-attachments/assets/93f7bf26-21aa-4bd2-a9f7-2e935fb2decc)
         - To maintain the doping concentration a low energy Boron is implanted in pwell and Arsenic in nwell Using Mask4 & Mask5 respectively.
           ![image](https://github.com/user-attachments/assets/5e28e9cd-1ffc-4e82-a602-69d283c384f9)
           ![image](https://github.com/user-attachments/assets/463b7915-90f3-4072-9ced-9e054b02876f)

         - The damaged SiO2 is then stripped off using dilute hydrofluoric acid (HF) solution and a new high quality oxide is regrown of same thickness ~10nm (as per Vt required)
         - For gate, deposit ~400nm thick poly-silicon layer on Oxide and dope with Arsenic for low sheet resistance
           ![image](https://github.com/user-attachments/assets/12c7c2f5-a6b4-4be3-9b37-74c09ca7218f)

         - Using Mask6, form the gates for nmos & pmos.
           ![image](https://github.com/user-attachments/assets/cd6d1152-babb-4454-b5b0-b5f4eace6c93)
           ![image](https://github.com/user-attachments/assets/236587d8-647e-46cc-a22d-91ae582e59b6)
   5. Lightly doped drain
        - P+, P-, N doping for PMOS in nwell & N+, N-, P doping profile in pwell for NMOS is needed
        - Lightly doped drain is to control hot electron effect and short channel effect
        - Mask7 protects Nwell and dopes the Pwell with N- for LDD NMOS, Mask8 protects Pwell and dopes the Nwell with P- for PMOS
          ![image](https://github.com/user-attachments/assets/7f9d30f6-27ac-4dcc-b745-9aed19d413e0)
          ![image](https://github.com/user-attachments/assets/da82409c-a7c0-4acc-bd31-f5db354dea93)
        - Spacers are deposited for protecting the lightly doped regions near the gate.
          ![image](https://github.com/user-attachments/assets/5a2c4d4f-08ea-4fca-a1df-8bebe8a74c75)

   6. Source Drain formation
         - Thin layer of screen oxide is added to avoid channeling during s/d implants.
         - Mask9 protects Nwell and does Arsenic N+ in Pwell for Nmos formation. Spacers help to keep the previous lightly doped N- intact thus enabling N+,N-,P doping profile.
         - Mask9 protects Pwell and does Boron P+ in Nwell for Pmos formation. Spacers help to keep the previous lightly doped P- intact thus enabling P+,P-,N doping profile.
         - Expose to high tempearture furnace for high temp annealing.
     
   7. Contacts and interconnect formation
        - Etch the screening oxide using HF, to expose source drain for forming contacts.
        - Now deposit Titanium on wafer through sputtering. Ti metal is hit with Argon gases which causes Ti will get sputtered/emitted out and get deposited into the substrate.
         - Ti is deposited uniformly everywhere. Now the wafer is heated at about 650 to 700 degrees C in N2 ambient for 60 seconds. TiSi2 is a low resistant material that can be used for connectivity. Also TiN is formed due to the ambient N present, which is used for local connections. It has higher resistivity can be used for nmos & pmos drain connections.
         - Mask11 is used now to etch out the unwanted TiN using RCA cleaning. RCA solution is H2O:NH4OH:H2O2 = 5:1:1
          ![image](https://github.com/user-attachments/assets/61668ca7-1ecc-40a4-ab96-f15287c6c18f)
   8. Higher level metal formation
        - Deposit thick SiO2 of 1um doped with B or P, then do CMP (chemical mechanical polishing) to planarize surface
        - Drilling contact holes using lithography obviously, using Mask12 and deposit TiN- TiN acts as a very good adhesion layer for SiO2 and barrier layer between bottom and top interconnects.
        - Next is blanket deposition of tungsten and then CMP to planarise it.
        - After that is blanket deposition of Aluminium and using Mask13 enable Aluminium connectivity to above metal stack.
        - Use Mask 14 to drill contact holes, repeat previous steps like TiN depostion, Tungsten and Al.
          ![image](https://github.com/user-attachments/assets/a5d24069-b629-4486-93bc-b1582d028206)

        - As we go from bottom to top, thickness of interconnect increases.
        - For last metal contact formation, Si3N4 dielectric is used instead of SiO2 as Si3N4 is stronger.
     
## Sky130 basic layers layout
- CMOS inverter layour in Magic.
- Layers panel on the right side shows all the layers.
- When the Polysilicon crosses the ndiffusion, it forms an NMOS. When Polysilicon crosses the pdiffusion, it forms a PMOS.
![image](https://github.com/user-attachments/assets/188e8562-b855-479c-9783-ad1f63d68933)
![image](https://github.com/user-attachments/assets/9804a6f5-4cb6-4dee-a454-bd91b239e4fe)
- Dimensions of the bbox for inverter. select the inv and write 'box' in tkcon window.
  ![image](https://github.com/user-attachments/assets/5783bed6-a309-4446-ad38-a95099ff4bf0)

- LEF file has the bbox info and the pins info for the cell. It does not hold any connectivity info. Hence the IP vendors provide only the LEF file for IP to protect it's logical connectivity.
  ![image](https://github.com/user-attachments/assets/cc3736d5-5729-4282-9771-b3b38b2c8726)
  ![image](https://github.com/user-attachments/assets/0a3991e8-9512-4057-ac87-08fa88369065)
nsubstrate -> nsub contcat-> loacali -> licon -> metal1
- Magic is an interactive DRC tool
- For logical functionof the design, extract the design into a spice netlist. The Magic command is 'extract all'
![image](https://github.com/user-attachments/assets/ddf5337f-96c3-498e-a665-7aacab380fc3)
- sky130_inv.ext file
  ![image](https://github.com/user-attachments/assets/904ec7e1-49ae-4f76-9b70-e751739f7bec)

- Using below command convert .ext file to spice netlist
  
![image](https://github.com/user-attachments/assets/8ea12f33-7a92-4e52-98c3-ef1585f5bbe2)

- Spice netlist looks like below
  
![image](https://github.com/user-attachments/assets/791ac0ee-0440-450b-9aa1-91a507be6f46)

- Modified spice deck to include proper nmos pmos model names, Va, VDD, VSS sources.
![image](https://github.com/user-attachments/assets/fde6fd9f-5d2a-4ba1-9cf7-a1b09d917682)


- Next, is to run the spice deck with ngspice 
![image](https://github.com/user-attachments/assets/f5075d80-c25b-4fa5-a242-cc54d29e9b50)

- Plotting the o/p Y and i/p A vs time for the 
![image](https://github.com/user-attachments/assets/e1295651-c623-4cf8-8aa2-f7b3a56630de)

- There are some spikes seen in the A & Y waveforms. Changing the Cload to 2fF (cap load between Y and VGND) to see the impact on spikes.
![image](https://github.com/user-attachments/assets/7f08c72a-4bd9-4adb-ba35-7793f74012ac)

- Rise transition - Time taken for o/p to rise from 20% to 80% of max power supply, 20% of 3.3 = 0.66V, 80% of 3.3 = 2.64V
     - Rise transition time = 2.23975ns - 2.17993ns = 0.5982ns = 59.82ps
![image](https://github.com/user-attachments/assets/f5014b97-502b-471a-ad5f-2018ce216744)

- Fall transition - Time taken for o/p to fall from 80% to 20% of max power supply
   - Fall transition time = 4.09326ns - 4.05052ns = 0.04274ns = 42.74ps
 ![image](https://github.com/user-attachments/assets/461d7818-f5c5-45e0-a787-20c0e6135502)
  
- Cell rise delay (propagation delay when o/p rises)
     - 2.20721ns - 2.14988ns = 0.05733ns = 57.33ps
 
![image](https://github.com/user-attachments/assets/777b42ef-5afa-4ece-9576-dc0dc0188435)

- Cell fall delay (propagation delay when o/p falls)
     - 4.07534ns - 4.05ns = 0.02534ns = 25.34ps
       
  ![image](https://github.com/user-attachments/assets/132562b2-b17e-434c-bc0d-4d1b7e9aaef1)

## SKY_L3 - Lab introduction to Magic tool options and DRC rules

1. Learning MAGIC layout tool
![image](https://github.com/user-attachments/assets/7e60a50a-0df5-4370-82bd-06efd6ca18f3)

2. CIF – Caltech Intermediate Format an old format similar to GDS
3. SKY130 - open source PDK available online to learn fabrication process
   
![image](https://github.com/user-attachments/assets/43520d4d-429f-4fb1-8af5-3875bc6828d0)

## SKY_L4 - Lab introduction to Sky130 pdk's and steps to download labs
1. Download drc tests

![image](https://github.com/user-attachments/assets/4db21417-28fe-4d07-8570-f276ba2bac5c)
   
![image](https://github.com/user-attachments/assets/46f0abee-e611-47ed-8d52-a290f070c6cc)

2. Magicrc file:

![image](https://github.com/user-attachments/assets/bdbea17a-d6fc-4a4a-85e5-9a0b0df849f4)

3. open magic using command "magic -d XR"

![image](https://github.com/user-attachments/assets/6ab8fe8e-d8ad-46ea-8648-f744242849b4)

## SKY_L5 - Lab introduction to Magic and steps to load Sky130 tech-rules

1. Opening met3 layout in magic. Either use command "magic -d XR met3.mag" or open magic and load file met3.mag from "File -> Open" icon

![image](https://github.com/user-attachments/assets/1f787d06-7aa3-4046-9ef6-a479cd2d73f0)

2. Clicking on Drc -> DRC Update, found 10 DRC violations.
 
![image](https://github.com/user-attachments/assets/0dfb5d03-6fcf-480d-b8af-f39a0a5a4d62)

3. Selecting a part of layout by left click and right click and hen press : drc why. It gives the reason for DRC violation and rule no.

![image](https://github.com/user-attachments/assets/392eb19f-29a1-448e-939e-f36513963a4c)

 4. cif see VIA2
 5. feed clear
 6. snap int

## SKY_L6 - Lab exercise to fix poly.9 error in Sky130 tech-file 
1. load poly or File -> Open -> poly.mag

![image](https://github.com/user-attachments/assets/4e2c6207-5158-4091-a430-9f1c851bb14a)

 2. Let's focus on the incorrect poly.9 . poly.9 rule says spacing between npolyres and poly should be minimum 0.48um.

![image](https://github.com/user-attachments/assets/26ffa67c-a5eb-4f77-bbfb-2a40e5db304a)

 3. As seen, the distance between npolyres and poly layer is 0.21um which is less than 0.48 um and it should be flagged as DRC violaition. However, it is not shown as DRC violation. Reason being the sky130A.tech file does not have this spacing rule included.

![image](https://github.com/user-attachments/assets/713292ac-b02b-44aa-bd2f-c7bd874a29e6)

 4. Updating poly.9 rule in sky130A.tech. Adding allpolynonres as it's an alias for *poly

![image](https://github.com/user-attachments/assets/e7d6df13-adfa-479c-9dee-8e9a54dbe5ee)
![image](https://github.com/user-attachments/assets/735d2ef9-b912-4ff6-8c4d-b4b8db846055)

 5. Using command "tech load sky130A.tech" load the updated tech file to see if now the DRC violations are flagged.

 6. After "drc check" command, DRC violation are seen in layout now, which were missing earlier.
 ![image](https://github.com/user-attachments/assets/3f48f5b8-035c-4506-8099-53a205a7a91e)

## SKY_L7 - Lab exercise to implement poly resistor spacing to diff and tap

1. Copy the three resistors (npolyres, ppolyres, xpolyres) by creating a bbox by left click and right click and pressing the key 'a' . Paste it by moving the cursor and pressing key 'c'

![image](https://github.com/user-attachments/assets/b534dad3-7e2a-47cd-a0b9-821321f0f9e1)

2. Now add the ndiffusion and pdiffusion layers above and below the resistors as shown by creating a bbox and selecting the layer from layers panel and pressing key 'p'. The DRC violations increase to 49 from 35.

![image](https://github.com/user-attachments/assets/0b60c9ab-eb20-4de0-8524-c95620faadec)

3. Adding nwell below.

![image](https://github.com/user-attachments/assets/cdd9ffbc-7a54-499d-83e0-5e1cc6dc3ab4)

4. modified the tech file to include the drc rule for npolyres and ntap & diffusion. Now DRC errors increased to 51.

5. Use drc why command to know the reason for drc violation

![image](https://github.com/user-attachments/assets/c1a3a3db-d1fd-40d6-a431-db5cea7eebd3)


## SKY_L8 - Lab challenge exercise to describe DRC error as geometrical construct

1. Load nwell.mag layout and zoom to nwell.6

![image](https://github.com/user-attachments/assets/c05299bc-6024-49ee-b58d-51831789e0cd)

2. type "cif ostyle drc" in tkcon

3.

 ![image](https://github.com/user-attachments/assets/6bca2816-f2e5-4bb4-afaf-a1e18f72731c)

## SKY_L9 - Lab challenge to find missing or incorrect rules and fix them

1. Here, the nwell is not tapped. but no DRC violaion is seen.

![image](https://github.com/user-attachments/assets/778a3b5a-e06c-4a3b-836b-2cbc8b49e7f5)

2. modifying the rules in tech file.

3. After modifying the tech rules and changing the drc style to drc full, the nwell drc violatin is flagged. As seen below, nwell is untapped and is highlighted for drc.

![image](https://github.com/user-attachments/assets/d14fc6c1-b95f-41d7-93f9-1253f31ca01a)

4. Addinn a new nwell with a substrate contact in it shows no drc violation.

![image](https://github.com/user-attachments/assets/c8f2c1b4-5fa0-4220-91cd-5dd996c4598b)


# Day 4

## SKY130_D4_SK1 - Timing modelling using delay tables / SKY_L1 - Lab steps to convert grid info to track info

1. There are 4 drc violation in the inverter layout.

![image](https://github.com/user-attachments/assets/90c51d34-3d1d-4e90-ad35-e7e590f86de9)

2. During PnR, we only need the Power/Gnd metal, the input/outout opins, the PR boundry. Logic connectivity info is not required. Here, LEF file is important.
3. Rules: The input and output ports need to be on the intersection of the vertical & horizontal tracks. The width of the standard cell should be in the odd multiples of the track horizontal pitch & height should be odd multiple of the vertical pitch.
4. tracks.info file inside the sky130A pdk's , libs.tech, has the info about the metal layer offset and horizontal & vertical pitch. the routes can be placed only along the tracks.

![image](https://github.com/user-attachments/assets/9d61d0ef-c069-4bfc-b555-49cd7faa5f5b)

5. Ports A & Y are of locali layer
6. Changing the grid size as per li1 values in tracks.info file, Ports A, Y are indeed on the intersection of li1 horizontal & vertical tracks.

![image](https://github.com/user-attachments/assets/25107624-f114-43e7-8b6d-e0df41b61bf1)

## SKY_L2 - Lab steps to convert magic layout to std cell LEF

1. Width of std cell is odd multiple of x-pitch. Here we see, width is covering 3 boxes, so width is 3*x-pitch

![image](https://github.com/user-attachments/assets/5da17cf7-3956-4feb-a7b2-55b31a53429f)

2. Height of std cell is 7 boxes, meaning 7*ypitch    

![image](https://github.com/user-attachments/assets/28c7c142-4e1c-4eca-9c46-102e6ef5a37d)

3. Defining ports for the input output pins and pwr/gnd pins for lef. A & Y ports are attached to layer locali, whereas pwr/gnd ports are attached to layer metal1.

![image](https://github.com/user-attachments/assets/ac4f0d30-cb30-42bf-a0ba-a2f0926fc28c)
![image](https://github.com/user-attachments/assets/1487aa01-88f3-4c3a-944a-a23192f2d1b7)

 Got to Edit -> Text. there we can define the text label, enable it as port, select the metal attached to the label and decide the order.

![image](https://github.com/user-attachments/assets/8f8050cb-e173-4124-b649-472cf589b878)

4. Next is to define purpose of the port, port class can be input, output, inout & port use can be signal, power, ground. Once port is efined, we can extract the lef from magic.

![image](https://github.com/user-attachments/assets/af521460-aa3d-4608-bf94-1f08c467f5ee)

5. There are DRC violations present currently. the width of transisor is less than 0.42um causing DRC violation. Fixing the DRC is important. DRC is fixed by widening the pdiffusion and ndiffusion widths to 0.42um from 0.35um.

![image](https://github.com/user-attachments/assets/d3c52c4d-baf5-4092-8f10-83e2308b0609)

The DRC reduced to 1 after widening the pdiff and ndiff widths.

![image](https://github.com/user-attachments/assets/2c6a52b5-47b5-491b-a4c6-69884a49c687)
