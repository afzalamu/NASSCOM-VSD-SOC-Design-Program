
# NASSCOM-VSD-SOC-Design-Program

## Table of Contents
- [DAY1 THEORY: Open-source EDA, OpenLANE and Sky130 PDK](#day1-theory--open-source-eda-openlane-and-sky130-pdk)
  - [What is an RTL to GDSII flow?](#what-is-an-rtl-to-gdsii-flow)
  - [Insight into the QFN-48 Chip: Pads, Core, Die, and IP Components](#insight-into-the-qfn-48-chip-pads-core-die-and-ip-components)
  - [SOC DESIGN USING OPENLANE](#soc-design-using-openlane)
- [DAY1 LABS: GETTING FAMILIAR WITH OPEN SOURCE EDA TOOLS](#day1-labs--getting-familiar-with-open-source-eda-tools)
  - [Understanding OPENLANE Directory Structure](#understanding-openlane-directory-structure)
  - [Design Preparation Step](#design-preparation-step)
  - [Review files after design prep and run synthesis](#review-files-after-design-prep-and-run-synthesis)
  - [Characterization of Synthesized Results](#characterization-of-synthesized-results)
- [DAY2 THEORY: GOOD FLOORPLAN VS BAD FLOORPLAN & INTRODUCTION TO LIBRARY CELLS](#day2-theory-good-floorplan-vs-bad-floorplan--introduction-to-library-cells)
  - [CHIP FLOORPLANNING CONSIDERATIONS](#chip-floorplanning-considerations)
    - [UTILIZATION FACTOR AND ASPECT RATIO](#utilization-factor-and-aspect-ratio)
    - [CONCEPT OF PREPLACED CELLS](#concept-of-preplaced-cells)
    - [CONCEPT OF DECOUPLING CAPACITOR](#concept-of-decoupling-capacitor)



# NASSCOM-VSD-SOC-Design-Program

## DAY1 THEORY : Open-source EDA, OpenLANE and Sky130 PDK

### What is an RTL to GDSII flow?
![image](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/8781543a-f108-4821-a3e9-45f1d8d5dd93)
The RTL (Register Transfer Level) to GDSII (Graphic Data System II) flow is a comprehensive process in integrated circuit (IC) design that transforms a high-level hardware description into a physical layout ready for fabrication. It begins with RTL design, where the circuit's functionality is coded in hardware description languages like Verilog or VHDL. This RTL code is then synthesized into a gate-level netlist. Design for Test (DFT) features are incorporated to facilitate testing. The netlist undergoes floorplanning, placement, and routing to map the circuit onto the chip layout. Clock Tree Synthesis (CTS) ensures efficient clock distribution. After detailed placement and routing, signoff checks including Design Rule Checking (DRC), Layout Versus Schematic (LVS) checks, and Static Timing Analysis (STA) are performed. Finally, the design is exported as a GDSII file, which is used by semiconductor foundries to fabricate the physical ICs

### Insight into the QFN-48 Chip: Pads, Core, Die, and IP Components
The image below is an Arduino Microcontroller Board. Our focus is on the encircled area, which contains the 'Microprocessor.
We will be designing this microprocessor from the abstract level to the fabrication level using the RTL to GDS flow. 
![image](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/d4f23775-c0c2-4f05-a198-9235b756aafe)

***let us Understand about some IC Design Components and Terminologies***
![image](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/fd2d6097-a140-4f37-868c-bb49447cb385)

| **Component** | **Description** |
|---------------|-----------------|
| **Core** | The core is the section of the chip where the fundamental logic pf the design is placed.|
| **IO Pads** | IO pads serve as the communication channels between the core and the external environment.|
| **Die** | The die is the part of the chip that includes both the core and IO pads. It is the area that is implemented on silicon wafer|
| **IPs** | Foundry IPs require manual design or human intervention to create, such as components  ADC, DAC, PLLs and may more.|

### SOC DESIGN USING OPENLANE
Here is the OpenLANE Detailed ASIC Design Flow:
![image](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/8e45d006-cccb-429e-a3c1-35e275cf86e9)


## DAY1 LABS : GETTING FAMILIAR WITH OPEN SOURCE EDA TOOLS 

### Understanding OPENLANE Directory Structure 

Open the LINUX Terminal (By default we are in home directory)

![2](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/ab949a2a-b11f-4748-a835-4fb9b9666c21)


- Important LINUX Commands
  - cd : It is used to change the current working directory.
  - ls : It lists the contents of a directory.
  - ls -ltr : It lists the contents of a directory in long format, sorted by modification time in reverse order (oldest first).
  - ls --help: It displays a help message with a list of options and usage information for the "ls" command.
     Note : You can give any command name and then type "--help" to get info about that command.
  - clear: It clears the terminal screen.
 

Now, we go to the  work directory where all files related to the workshop are stored
```
cd Desktop
```
```
cd work/tools/
```
we wil be working with 'openlane_working_dir' --> 'openlane' so use : 

```
cd openlane_working_dir/
```
```
cd openlane/
```
![6](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/0d142dcd-3b98-4639-a480-99cb7a256544)


- Important Files and Directories
  ```
   pdks: It is known as Process Design Kit. For this workshop we are using an opensource pdk i.e 'skywater 130nm pdk'. OPENLANE is built around this 'skywater 130nm pdk'.
    - skywater-pdk : This has all the pdk related files such as timing libraries, Lef files etc.
    - open_pdks : It contains set of scripts & files that converts the foundary level pdks to be compatible with the open source EDA Tools.
    - sky130A : It is a pdk variant , already made compatible with the open source EDA tools.
          - libs.ref: It contains files specific to the technology such as design libraries, standard cells and many more.
          - libs.tech: It contains files specific to the Tools.
  ```
  
### Design Preparation Step

To enter into bash while being in the openalne dircetory use the command
```
docker
```
Now after this we use the script 'flow.tcl' and alongwith it use '-interactive' for the step by step openlane flow. here is the command:
```
./flow.tcl -interactive
```
![7](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/823cdab4-9c21-4edd-b7c2-1a546c4f36a9)
.
Now, OPENLANE is opened, and we input the required packages using the following command:
```
% package require openlane 0.9
```
Now, Ther are various pre-built designs in the 'designs' subdirectory.
So, here we are selecting the "picorv32a.v" design on which we will execute the RTL to GDS flow.
To carry out the synthesis (the project's initial stage) on this design, we first need to set it up using the command:
```
prep -design picorv32a
```
![8](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/8345b349-097c-45cb-9478-0394c1b89054)

After the preparation is complete, we can see a new directory with todays date is created within 'runs' folder in 'picorv32a' folder.

![9](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/cb3cefd1-145a-4a08-b203-4fbf564ce584)

### Review files after design prep and run synthesis
Now, when we open the newly created directory:
![10](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/b414945d-dc0d-47b2-8e64-5ffa6167f2c9)

At first, every directory will be empty since no operations have been performed on the design. However, there will be a directory named "tmp" that contains various types of files. One of these files is "merged.lef" which includes information about metal layer levels and cell levels.

![11](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/b0504629-bdac-4fe8-b056-068a8184404f)

use the follwoing command to open "merged.lef":
```
less merged.lef
```
- "config.tcl" File: This file shows which all default parameter is taken by the run.
- ![12](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/80333993-1e56-4c7c-9bf8-feeb4fd8b307)
  To open the file use the following command:
  ```
  less config.tcl
  ```
  ![13](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/fac38ff5-c389-4cfa-8e9f-bf5de455b0f0)


Now, coming back to the step where design preperation was completed successfully.
Now, To perform synthesis on the design use the following command :
```
% run_synthesis
```
![a](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/b67df7ad-3abc-46e7-9b84-c8f64b816aee)
It will take some time to get completed.

* Extras: Watch these videos
  * [Fossi Dial Up : Skywater 130nm PDK](https://www.youtube.com/live/EczW2IWdnOM?si=OPWnxYsm_Q6uZhyS)
  * [Fossi Dial Up : Openlane Digital ASIC flow](https://www.youtube.com/live/Vhyv0eq_mLU?si=uAuQ8_DU5NJ-uKy2)


### Characterization of Synthesized Results

Now, First objective after the synthesis is completed is to calculate the Flip Flop Ratio.

Now, if we see the synthesized results we find:
![15](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/1c9dba6c-7591-4c35-b2bc-0206190c2928)



```
Number of D Flipflops : 1613
Total number of Cells : 14876
```
Hence, flip flop ratio = (Number of D Flipflops)/(Total number of Cells)
Flipflop percentage = FF ratio * 100
```
FF Ratio : 0.1084
FF Percentage : 10.84 %
```

Also, Now if we go to:
```
/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-07_06-37/results/synthesis$
```
![16](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/5ab1a9f4-ca35-49cb-a4e8-58526278d6d6)

we have the synthesis results stored here now.


## DAY2 THEORY: GOOD FLOORPLAN VS BAD FLOORPLAN & INTRODUCTION TO LIBRARY CELLS

### CHIP FLOORPLANNING CONSIDERATIONS

#### UTILIZATION FACTOR AND ASPECT RATIO
  
  In order to calculate the utilization factor & aspect ratio, first we need to calculate the height and width of the core and die.
  ![image](https://github.com/user-attachments/assets/638b2fc2-54c8-43f4-afad-183281247e6b)
  The core area's dimensions will be determined by the design's netlist, which is based on the number of components necessary to implement
  the logic. Consequently, the die area's height and width will depend on the core area's dimensions.

  For example, lets consider a netlist that is having two logic gates and two flipflops.
  ![image](https://github.com/user-attachments/assets/d648385f-74aa-4103-b60b-e5a1ba0e98e6)

  Now, if we consider the elements each having area of 1 sq.unit. The netlist contains 4 elements and the minimum total area required for the
  core area will be 4 sq.units.
![image](https://github.com/user-attachments/assets/44685856-5790-4279-bdfd-45bb4370ee07)

* **Utilization Factor:** The Utilization Factor is defined as the ratio of the core area occupied by the netlist to the total core area. In an effective floorplan, the Utilization Factor should not be 1. If the Utilization Factor reaches 1, there will be no available space for adding any additional logic, making it a poor floorplan.
```
Utilization Factor = (Area occupied by netlist / Total core area)
```
* **Aspect Ratio:** The Aspect Ratio is defined as the ratio of the height of the core to its width. When the Aspect Ratio is 1, the core is considered to be square-shaped. If the Aspect Ratio is different from 1, the core will have a rectangular shape.
```
Aspect Ratio = (Height of the core / Width of the core)
```
![image](https://github.com/user-attachments/assets/e971d307-4928-4107-84b8-5f329fdfd8ed)
So, for the above case:
```
Utilisation Factor = (4 sq units)/(4sq units) = 1
Aspect Ratio = (2 units)/(2 units) = 1 i.e core has Square Shape
```
Now, if we take the another case given below:
![image](https://github.com/user-attachments/assets/4fd9844c-bf22-43e2-8a56-02797b381148)
```
Utilisation Factor = (4 sq units)/(8 sq units) = 0.5
Aspect Ratio = (2 units)/(4 units) = 0.5 i.e core has Rectangular Shape
```

#### CONCEPT OF PREPLACED CELLS
![image](https://github.com/user-attachments/assets/ac8dc27f-1213-4814-bfb5-76ebae9fbd3c)

The concept of preplaced cells begins with organizing a complex combinational logic circuit, which may contain thousands of gates, into predefined locations within the layout. This involves identifying and positioning critical components or blocks, such as memory modules, clock gating cells, comparators, and multiplexers. These preplaced cells are treated as distinct entities or "black boxes" to streamline integration and management. The arrangement of these preplaced cells and other IPs within the design layout is known as floorplanning. 
These IP`s / blocks have user defined locations and hence are  placed in chip before automated placement- and-routing and are called pre-placed cells.
Automated Plcement and routing tools places the remaining logical cells in the design onto the chip.

#### CONCEPT OF DECOUPLING CAPACITOR
![image](https://github.com/user-attachments/assets/8bfb1295-5fa8-4b59-a3e9-2ce191ffea69)
In circuits, certain high-power components may not receive adequate power from the source due to voltage drops in the connecting wires, causing their operation to fall outside their required voltage range for reliable switching. To address this issue, decoupling capacitors (De-cap cells) are strategically placed near these power-intensive components. These capacitors are connected to the power source and charge to a high level when no switching occurs. When switching activities commence, the decoupling capacitors quickly discharge to supply the necessary power directly to these components. Once switching ceases, the capacitors recharge, ensuring consistent and reliable power delivery to critical circuit components. This mechanism is essential in circuit design to maintain stable operation and prevent performance issues caused by fluctuating power supply conditions.

#### CONCEPT OF POWER PLANNING



## DAY2 LABS: FLOORPLANNING

To ensure a smooth floorplanning process, designers must pay attention to certain parameters, known as switches, which can significantly impact the floorplan when adjusted. For instance, the utilization factor and aspect ratio are among these critical switches. Designers need to verify that these parameters align with the project requirements before initiating the floorplanning stage. The image below illustrates various types of switches involved in the floorplanning phase.
![1](https://github.com/user-attachments/assets/91630f9e-fa8b-4e4a-afc2-0c3d66c39ffa)

* Now, after the synthesis is completed, To run the Floorplan Use the following command:
  ```
  run_floorplan
  ```
![2](https://github.com/user-attachments/assets/bf52d41f-7c70-4971-b0b1-8b73303bab02)
When the floorplaning is completed, To view the results go to the path as shown in image below  : 
![4 def file](https://github.com/user-attachments/assets/229f9afe-3a12-4afa-b5f3-a38f97544d65)
open the def file
![5 def file reuslts](https://github.com/user-attachments/assets/484078cb-b5d8-4f09-895c-159fd63d4e5f)
These results are useful for various analysis, for example: we can see the die area :
![6 area](https://github.com/user-attachments/assets/14b5aac1-a100-434a-8499-ce6dd35d3716)

Now, to open this "def" file in magic , use the following command:
```
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

```



  









