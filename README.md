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
    - [CONCEPT OF POWER PLANNING](#concept-of-power-planning)
  - [LIBRARY BINDING AND PLACEMENTS](#library-binding-and-placements)
    - [Netlist binding and initial place design](#netlist-binding-and-initial-place-design)
    - [Optimize placement using estimated wire-length and capacitance](#optimize-placement-using-estimated-wire-length-and-capacitance)
  - [CELL DESIGN AND CHARACTERISATION FLOWS](#cell-design-and-characterisation-flows)
  - [GENERAL TIMING CHARACTERISATION PARAMETERS](#general-timing-characterisation-parameters)
- [DAY2 LABS: FLOORPLANNING & PLACEMENT](#day2-labs-floorplanning--placement)
  - [STEPS TO RUN FLOORPLAN USING OPENLANE](#steps-to-run-floorplan-using-openlane)
  - [STEPS TO PERFORM PLACEMENT IN OPENLANE](#steps-to-perform-placement-in-openlane)
    
- [DAY3 THEORY : DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION](#day3-theory--design-library-cell-using-magic-layout-and-ngspice-characterization)
  - [SPICE DECK CREATION FOR CMOS INVERTER](#spice-deck-creation-for-cmos-inverter)
  - [INCEPTION OF LAYOUT & CMOS FABRICATION PROCESS](#inception-of-layout--cmos-fabrication-process)
    - [CREATE ACTIVE REGIONS](#create-active-regions)
    - [FORMATION OF WELLS](#formation-of-wells)
    - [FORMATION OF GATE TERMINALS](#formation-of-gate-terminals)
    - [LIGHTLY DOPED DRAIN (LDD) FORMATION](#lightly-doped-drain-ldd-formation)
    - [SOURCE DRAIN FORMATION](#source-drain-formation)
    - [LOCAL INTERCONNECT FORMATION](#local-interconnect-formation)
    - [HIGHER LEVEL METAL FORMATION](#higher-level-metal-formation) 
- [DAY3 LABS :](#day3-labs-)
  - [HOW TO MAKE CHANGES WHILE BEING IN THEN FLOW?](#how-to-make-changes-while-being-in-then-flow)
  - [HOW TO GIT CLONE THE "vsdstdcelldesign"](#how-to-git-clone-the-vsdstdcelldesign)
  - [INTRODUCTION TO SKY130 BASIC LAYERS LAYOUT AND LEF USING INVERTER](#introduction-to-sky130-basic-layers-layout-and-lef-using-inverter)
  - [TO CREATE STANDARD CELL LAYOUT IN MAGIC](#to-create-standard-cell-layout-in-magic)
  - [TO EXTRACT THE NETLIST IN MAGIC](#to-extract-the-netlist-in-magic)
  - [SKY130 TECH FILE LABS](#sky130-tech-file-labs)
    - [CREATE SPICEDECK USING SKY130 TECH](#create-spicedeck-using-sky130-tech)
    - [CHARACTERIZE INVERTER USING SKY130 TECH FILES](#characterize-inverter-using-sky130-tech-files)
  - [Introduction to Magic Tools and DRC Rules](#introduction-to-magic-tools-and-drc-rules)
  - [Introduction to SKY130 PDK](#introduction-to-sky130-pdk)
  - [Introduction to Magic & Steps to Load SKY130 Tech Rules](#introduction-to-magic--steps-to-load-sky130-tech-rules)
  - [Lab Exercise to Fix Poly-9 Error in SKY130 Tech File](#lab-exercise-to-fix-poly-9-error-in-sky130-tech-file)
  - [Lab Challenge Exercise to Describe DRC Error as Geometrical Construct](#lab-challenge-exercise-to-describe-drc-error-as-geometrical-construct)
  - [Lab Challenge to Find Missing or Incorrect Rules and Fix Them](#lab-challenge-to-find-missing-or-incorrect-rules-and-fix-them)

- [DAY4: THEORETICAL CONCEPTS](#day4-theoretical-concepts)
  - [Introduction to delay tables](#introduction-to-delay-tables)
  - [Introduction to CTS](#introduction-to-cts)
  - [TIMING ANALYSIS](#timing-analysis)
- [DAY4 LABS: PRE-LAYOUT TIMING ANALYSIS & IMPORTANCE OF GOOD CLOCK TREE](#day4-labs-pre-layout-timing-analysis--importance-of-good-clock-tree)
  - [Timing Modelling Using Delay Tables](#timing-modelling-using-delay-tables)
    - [Converting the Grid Info to Track Info](#converting-the-grid-info-to-track-info)
    - [Converting Magic Layout to Standard Cell LEF](#converting-magic-layout-to-standard-cell-lef)
    - [Introduction to Timing Libs and Steps to Include New Cell in Synthesis](#introduction-to-timing-libs-and-steps-to-include-new-cell-in-synthesis)
    - [Steps to configure synthesis settings to fix slack and include vsdinv](#steps-to-configure-synthesis-settings-to-fix-slack-and-include-vsdinv)
  - [Timing analysis with ideal clocks using openSTA](#timing-analysis-with-ideal-clocks-using-opensta)
    - [Configure OpenSTA for post-synth timing analysis](#configure-opensta-for-post-synth-timing-analysis)
    - [Steps to run CTS using TritonCTS](#steps-to-run-cts-using-tritoncts)
  - [Timing analysis with real clocks using openSTA](#timing-analysis-with-real-clocks-using-opensta)
    - [Steps to execute OpenSTA with right timing libraries and CTS assignment](#steps-to-execute-opensta-with-right-timing-libraries-and-cts-assignment)
    - [Now if we want to include buf_1 again?](#now-if-we-want-to-include-buf_1-again)

- [References](#references)



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

![Screenshot (733)](https://github.com/user-attachments/assets/a1163602-9883-4dc0-a351-b5700c124a41)

### Review files after design prep and run synthesis
Now, when we open the newly created directory:
![Screenshot (734)](https://github.com/user-attachments/assets/2edcd507-a905-435f-a82e-b67901f5bbce)

At first, every directory will be empty since no operations have been performed on the design. However, there will be a directory named "tmp" that contains various types of files. One of these files is "merged.lef" which includes information about metal layer levels and cell levels.
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
  
Now, coming back to the step where design preperation was completed successfully.
Now, To perform synthesis on the design use the following command :
```
% run_synthesis
```
![Screenshot (735)](https://github.com/user-attachments/assets/255117ca-b01e-44c1-b994-a2bfbe04f459)

It will take some time to get completed.

* Extras: Watch these videos
  * [Fossi Dial Up : Skywater 130nm PDK](https://www.youtube.com/live/EczW2IWdnOM?si=OPWnxYsm_Q6uZhyS)
  * [Fossi Dial Up : Openlane Digital ASIC flow](https://www.youtube.com/live/Vhyv0eq_mLU?si=uAuQ8_DU5NJ-uKy2)


### Characterization of Synthesized Results

Now, First objective after the synthesis is completed is to calculate the Flip Flop Ratio.

Now, if we see the synthesized results we find:
![Screenshot (736)](https://github.com/user-attachments/assets/b128b579-a3aa-4657-ba2a-df35a97d8a3e)
![Screenshot (737)](https://github.com/user-attachments/assets/3e943a0e-6bb9-409e-82ac-33849826b85b)

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
![Screenshot (738)](https://github.com/user-attachments/assets/07d02e35-78d8-4ffc-b73c-e28d159a973c)

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
In the previous section, we discussed using decoupling capacitors (De-cap cells) to manage power distribution for various blocks. However, De-cap cells come with limitations, such as leakage power and increased chip area. To mitigate these issues, we use a technique called power planning. In areas of the chip with significant switching activity, two phenomena can occur: voltage drop and ground bounce.
![image](https://github.com/user-attachments/assets/77cef52e-a458-4a2f-bb3d-6e53b75bf932)
**Voltage Drop**
Voltage drop happens when a group of cells switch from 0 to 1 simultaneously, causing a high demand for power. If the power is supplied from a single source, there may be insufficient power, leading to a drop in input voltage at that location. This issue becomes problematic when the voltage level falls below the noise margin.

**Ground Bounce**
Ground bounce occurs when a group of cells switch from 1 to 0 simultaneously, dumping power to the ground pin at the same time. This causes the ground voltage to rise briefly instead of remaining at 0, leading to a phenomenon known as ground bounce. The issue arises when the voltage level exceeds the noise margin.

**Power Planning Technique**
![image](https://github.com/user-attachments/assets/b4859dea-2da9-4f12-b459-389bbdae8fa1)
To prevent these issues, a technique called power planning is used. This involves creating two separate power meshes: one for Vdd (positive voltage) and another for ground. These meshes are typically implemented using the top two metal layers to minimize voltage drops. They are spread across the design and connected to multiple Vdd and ground sources. With this approach, when a cell requires power to switch from 0 to 1, it draws from the nearest Vdd layer. Conversely, when a cell needs to drain power, it discharges to the nearest ground layer. This ensures stable and efficient power distribution throughout the chip.

### LIBRARY BINDING AND PLACEMENTS

#### Netlist binding and initial place design
In a netlist, each component has a distinct shape— for example, an AND gate has one shape while an OR gate has another. However, in a library, all components are represented by a uniform square or rectangular shape. A library contains a variety of elements that are ready to use, each with specified properties such as area and delay. Additionally, there are different versions of the same component, each with varying properties.
![image](https://github.com/user-attachments/assets/fb46bf68-612c-4df5-9014-1b74aca1375e)
In the image above, we have three different sets of the same elements. The larger elements are faster but take up more space, while the smaller elements occupy less area but operate more slowly compared to the larger ones.

#### Optimize placement using estimated wire-length and capacitance
In the placement stage, it is crucial to take into account the estimated wire length when positioning cells. Wire length estimation involves calculating the distances from the input sources of cells to the output sinks they drive.

In the example above, the tool positions the blocks based on these estimated wire lengths, as illustrated in the figure below.
![image](https://github.com/user-attachments/assets/997a2b24-fdf1-4284-bb8d-d709ef55bc4d)

### CELL DESIGN AND CHARACTERISATION FLOWS

![image](https://github.com/user-attachments/assets/3b5e890e-49ba-4d19-9dd4-0062b387a8dc)
![image](https://github.com/user-attachments/assets/630a5549-1c14-4bae-9ab3-cdb37c0fefc2)
* **Standard Cells:** These are basic logic gates (like NAND, NOR, XOR, etc.) or more complex functional blocks (like flip-flops or adders) designed to be reusable across different IC designs. They are characterized by their functionality, area, power consumption, and timing characteristics.

* **Library:** In the context of IC design, a library (or cell library) consists of a collection of standard cells. Each cell in the library is optimized for specific parameters such as speed (delay), power consumption, area (size), and drive strength.

- A typical Cell Design Flow Involves the follwoing steps as shown below:
![image](https://github.com/user-attachments/assets/bdbaf1c3-b853-4c3b-886f-80e98d7e5a15)

### GENERAL TIMING CHARACTERISATION PARAMETERS
![image](https://github.com/user-attachments/assets/c46b462b-8dd0-4c54-8816-449a96f27909)
* Propogation Dealy:
 ![image](https://github.com/user-attachments/assets/8f5398c5-5f93-4e10-b2a1-dd6380cef7d8)
Let us take example wavefrom and calculate the Propogation Delay:
![image](https://github.com/user-attachments/assets/f491ea30-cfae-4170-81ae-357e6cba8cf9)
But Here a problem can occur if the thresholds move and results may vary:
![image](https://github.com/user-attachments/assets/c9a117f1-c5d0-4d83-95fb-ccc5e8095b08)
So choosing a threshold point carefully is very important.

* Transition Time
![image](https://github.com/user-attachments/assets/79f62b1b-b71e-4b8a-a4fa-f340f177e028)
![image](https://github.com/user-attachments/assets/c2a1337b-9628-4d4a-befc-5045f957c884)




## DAY2 LABS: FLOORPLANNING & PLACEMENT

### STEPS TO RUN FLOORPLAN USING OPENLANE

To ensure a smooth floorplanning process, designers must pay attention to certain parameters, known as switches, which can significantly impact the floorplan when adjusted. For instance, the utilization factor and aspect ratio are among these critical switches. Designers need to verify that these parameters align with the project requirements before initiating the floorplanning stage. The image below illustrates various types of switches involved in the floorplanning phase.
![1](https://github.com/user-attachments/assets/91630f9e-fa8b-4e4a-afc2-0c3d66c39ffa)

* Now, after the synthesis is completed, To run the Floorplan Use the following command:
  ```
  run_floorplan
  ```
![image](https://github.com/user-attachments/assets/3be9d1c4-9b6b-4e36-a06f-7c0da99d763b)

When the floorplaning is completed, To view the results go to the path as shown in image below  : 

![image](https://github.com/user-attachments/assets/5e0deaff-3d8d-4778-b6d2-2ecc0b8fee5a)

open the def file:

![image](https://github.com/user-attachments/assets/aeca9fd4-bb1f-4278-954d-13f046f9b876)

These results are useful for various analysis, for example: we can see the die area :

![6 area](https://github.com/user-attachments/assets/14b5aac1-a100-434a-8499-ce6dd35d3716)

Now, to open this "def" file in magic , use the following command:
```
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

```

![image](https://github.com/user-attachments/assets/4dde39bc-f9e1-4278-860c-1523e0f5c372)

Now, we can use 'Magic' tool to expllore the floorplan.

#### Design Alignment Instructions in MAGIC

| **Task**                       | **Steps**                                                                                                         |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **Centering the Design**       | 1. Press `S` to select the entire design.<br>2. Press `V` to align it vertically to the middle of the screen.       |
| **Zooming In on a Specific Area** | 1. Left-click and drag to highlight the desired region.<br>2. Right-click to open the context menu.<br>3. Press `Z` to zoom in on the selected area. |
| **Retrieving Cell Details**    | 1. Hover your cursor over the cell you want details for.<br>2. Press `S` to select the cell.<br>3. In the `tkcon` window, type the command `what` to display the cell's details. |

![image](https://github.com/user-attachments/assets/33129dcd-b761-4e9d-9845-a7a3b6dd99cf)

### STEPS TO PERFORM PLACEMENT IN OPENLANE
After successfully completing floorplanning, the design process moves on to the placement stage, which comprises two main phases:

**Global Placement:**
During this phase, the tool determines the approximate locations for all the standard cells in the design.
**Detailed Placement:**
In this phase, the tool finalizes the exact positions for all the standard cells and ensures the placement is legal. Legalization involves verifying that no standard cells overlap and that they are all correctly positioned within the designated site rows.
To initiate the placement process, use the following command:
```
run_placement
```
![image](https://github.com/user-attachments/assets/08891124-a8e5-4149-9d11-25a493c09cda)

After the Placement is done. To view the results Go to the following loacation:
```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/20-07_16-44/results/placement
```
And then we can see 'picorv32a.placement.def' file. To open it using MAGIC use the follwoing command:
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def
```
![image](https://github.com/user-attachments/assets/4c6fe222-33ca-4368-95ca-a04da25b2a6e)

![image](https://github.com/user-attachments/assets/cb1d52a8-fb7f-4a6d-abe6-37a4bdc02efd)

# DAY3 THEORY : DESIGN LIBRARY CELL USING MAGIC LAYOUT AND NGSPICE CHARACTERIZATION

## SPICE DECK CREATION FOR CMOS INVERTER
Spice deck basically Netlist having the connectivity information, Input to be provided, Output Tap points and much more.
Proceeding with an example:
![image](https://github.com/user-attachments/assets/396e8d43-5143-4a83-9726-01a51f62549a)
- Nodes are required to define the netlist.
  ```
  MOSFET (ORDER FOR NETLIST) : Drain Gate Substrate Source
  Syntax for MOSFET In a Netlist:
  e.g : M1 out in vdd vdd pmos W = 0.375u L = 0.25u
  ```
![image](https://github.com/user-attachments/assets/d8cdeaa8-c462-4a10-bd0f-b58e6c91b8b7)
![image](https://github.com/user-attachments/assets/937ef7be-d437-4920-9dc1-8d3c1c3dc748)
CMOS circuit is a very Robust device, seee the below image:
![image](https://github.com/user-attachments/assets/1b541867-0ca3-4832-9e7f-d5c7c6051ae7)

## Inverter Characteristics

### Static Characteristics

| Characteristic         | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **Switching Threshold (Vth)** | The voltage level at which the inverter switches from a high state (logic 1) to a low state (logic 0). |
| **Input Low Voltage (Vil)**   | The highest input voltage that is recognized as logic 0.              |
| **Input High Voltage (Vih)**  | The lowest input voltage that is recognized as logic 1.               |
| **Output Low Voltage (Vol)**  | The output voltage level when the inverter transitions from high to low. |
| **Output High Voltage (Voh)** | The output voltage level when the inverter transitions from low to high. |
| **Noise Margins**             | The voltage ranges that define the low noise margin (between Vil and Vol) and the high noise margin (between Vih and Voh). |

### Dynamic Characteristics

| Characteristic           | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| **Propagation Delays**   | The time delay for the output to respond to a change in the input signal.   |
| **Rise Time (tr)**       | The duration for the output to shift from Vol to Voh.                       |
| **Fall Time (tf)**       | The duration for the output to shift from Voh to Vol.                       |


## INCEPTION OF LAYOUT & CMOS FABRICATION PROCESS

### CREATE ACTIVE REGIONS
![Presentation1](https://github.com/user-attachments/assets/cbd805ea-ad86-4ad9-a830-ed658ef98a2c)

### FORMATION OF WELLS
![Presentation2](https://github.com/user-attachments/assets/0b159169-a4e3-4960-943b-2cb35f890c18)

### FORMATION OF GATE TERMINALS
![Presentation3](https://github.com/user-attachments/assets/532497dc-b850-43d6-8710-06b6245c2a90)

### LIGHTLY DOPED DRAIN (LDD) FORMATION
![Presentation5](https://github.com/user-attachments/assets/400d590f-aa0d-4444-8af6-53b5069c4b2d)

### SOURCE DRAIN FORMATION
![Presentation6](https://github.com/user-attachments/assets/c50c5c3a-47b1-4e0b-966d-265c94a9bade)

### LOCAL INTERCONNECT FORMATION
![Presentation7](https://github.com/user-attachments/assets/3519dd28-d7b1-4521-9018-aa994e89b8ae)

### HIGHER LEVEL METAL FORMATION
![Presentation8](https://github.com/user-attachments/assets/45c62a3a-96ef-454a-97b3-a1a61bec9723)




## DAY3 LABS :

## HOW TO MAKE CHANGES WHILE BEING IN THEN FLOW?

* **Example** : TO CHANEG THE IO PLACER SETTINGS
First let us verify the current configuration of the Pins, Go to following directory as shown in image below:
  ![image](https://github.com/user-attachments/assets/96bbae31-1f95-471b-a0b8-c5611d2318e5)
Then use the command to open the 'def' file in magic:
```
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def
```
![image](https://github.com/user-attachments/assets/b17d3703-53b6-452e-b068-79aeceb42e56)
As we can seee Pins are randomly equidistant :
Now, if want it to change to some other IO strategy, as there are four strategy supported by IO placer(Open source EDA tool)
To do this, first go the following directory and open 'floorplan.tcl' file:
```
:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ 
```
![image](https://github.com/user-attachments/assets/a4070962-cbbc-4104-a8d8-bc13a8cdd0f1)
And from here we can see the switching variable :
```
set ::env(FP_IO_MODE) 1; # 0 matching mode - 1 random equidistant mode
```
It is set as 1 and hence pins are randomly equidistant.
Now, go the follwoing tab as shown below and put the following command and change the IO placer settings:
```
set ::env(FP_IO_MODE) 2
run_floorplan
```
![image](https://github.com/user-attachments/assets/0f8ffc5e-09b5-40a5-9a45-71bc7b0a5a33)
Hence, we run the floorplan again
Now, we can check the chaneg in the IO placer strategy:
We can see that def file has been updated from the time stamps and date:
![image](https://github.com/user-attachments/assets/e768c8d7-7e8b-4a7c-b736-76df39912450)
Now, let us open it in magic using the earlier used command:
![image](https://github.com/user-attachments/assets/79bbe21a-4550-455d-a667-c220b006a8a0)
And from the above image we can see teh configuration has been changed.

## HOW TO GIT CLONE THE "vsdstdcelldesign"

- Go to Openlane directory and use the following command:
  ```
  git clone <url of the github repo you want to clone>
  ```
  For example here:
  ```
  git clone https://github.com/nickson-jose/vsdstdcelldesign.git
  ```
  ![image](https://github.com/user-attachments/assets/08dee3c2-f175-4d83-8636-d437d7f91c03)
  From the above image we can see it is cloned successfully.
  Now, we will open the 'mag' file and in order to do that we require 'tech'file taht is present in the following directory:
  ```
  vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic$ 
  ```
  so first we copy that file here, by using the following command:
  ```
  cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
  ```
  ![image](https://github.com/user-attachments/assets/79665b35-d92d-4af0-9833-383a78950814)
  It is copied successfully.
  Now, open the mag file magic:
  ```
  magic -T sky130A.tech sky130_inv.mag &
  ```
  ![image](https://github.com/user-attachments/assets/ab5881d8-6103-4301-80a9-be5374fd1880)



## INTRODUCTION TO SKY130 BASIC LAYERS LAYOUT AND LEF USING INVERTER
When polysilicon crosses the ndiffusion region it is termed as 'NMOS' and when it crosses the pdiffusion region it is termed as 'PMOS', same is verified in image below:
![image](https://github.com/user-attachments/assets/664e26ff-25c9-4ca1-a2ae-26ee5ef13b0f)
![image](https://github.com/user-attachments/assets/26cf1727-4940-40ba-a479-d0b0c8093d97)

## TO CREATE STANDARD CELL LAYOUT IN MAGIC
follow this Repository: [Click here](https://github.com/nickson-jose/vsdstdcelldesign)

## TO EXTRACT THE NETLIST IN MAGIC
In the tckon window, use the following command:
```
% extract all
% ext2spice cthresh 0 rthresh 0
```
![image](https://github.com/user-attachments/assets/1bac51de-c6ff-4774-a5c5-edfc6041732e)
![image](https://github.com/user-attachments/assets/3f29aa49-2686-4578-9bdd-c132a1c57769)
Now, lets open the created spice file:
![image](https://github.com/user-attachments/assets/9b9c5726-9aa9-40f4-a690-0aa3ecba8d50)

This contains the spice deck.

## SKY130 TECH FILE LABS

### CREATE SPICEDECK USING SKY130 TECH
Make the follwoing cahnges in the 'sky130_inv.spice' file:
![image](https://github.com/user-attachments/assets/2010623a-5770-46d2-a0fa-4d1bf54eeb45)

Now to run the simulation in ngspice, use the follwoing command while being in the 'vsdstdcelldesign' directory:
```
ngspice sky130_inv.spice
```
![image](https://github.com/user-attachments/assets/db7f79e8-4f05-4cde-96b5-5bfe5f781018)

Now, to open the plot use ```plot y vs time a ``` in ngspice terminal
![image](https://github.com/user-attachments/assets/9c6e061b-92f7-4fa1-87e2-61b57de96d5a)

### CHARACTERIZE INVERTER USING SKY130 TECH FILES
To characterize the inverter, we analyzed the ngspice plot and determined the following parameters:

* **Rise Time:** The time for the output waveform to transition from 20% to 80% of its maximum value.
  
  From plot points: (x0 = 2.18197e-09, y0 = 0.660482) to (x0 = 2.24571e-09, y0 = 2.64019).
  Calculated Rise Time = 0.0637 ns
  
* **Fall Time:** The time for the output waveform to transition from 80% to 20% of its maximum value.

  From plot points: (x0 = 4.0526e-09, y0 = 2.63973) to (x0 = 4.09512e-09, y0 = 0.659245).
  Calculated Fall Time = 0.0425 ns
  
* **Propagation Delay(Cell Rise Delay)** The time for the output to transition 50% in response to a 50% change at the input.

  From plot points: Input(x0 = 2.15018e-09, y0 = 1.65018) to Output(x0 = 2.21088e-09, y0 = 1.65).
  Calculated Propagation Delay = 0.060 ns
  
* **Cell Fall Delay:** The delay for the output to transition 50% due to a 50% change at the input.

  From plot points: (x0 = 4.04991e-09, y0 = 1.65) to (x0 = 4.07745e-09, y0 = 1.65).
  Calculated Cell Fall Delay = 0.0275 ns
  
With these parameters successfully characterized, the next step is to create a LEF file.

## INTRODUCTION TO MAGIC TOOLS AND DRC RULES
[Follow this Webpage](http://opencircuitdesign.com/magic/)

## INTRODUCTION TO SKY130 PDK
[Follow this Webpage for Documentation](https://skywater-pdk.readthedocs.io/en/main/)
Now us the follwoing command to download the Lab files while being in the home directory :
```
sudo wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

```
![image](https://github.com/user-attachments/assets/a6439cb4-6ff2-440b-a2dd-297d84cd5cf7)

Now you have downloaded the zip file. To extract the labs from the zip file use the command
```
sudo tar xfz drc_tests.tgz
```
![image](https://github.com/user-attachments/assets/f61a4bf3-ea18-45de-857a-329014cdd1b0)

In the downloaded files , **.magicrc** file serves as the start-up script for MAGIC.

## INTRODUCTION TO MAGIC & STEPS TO LOAD SKY130 TECH RULES
"Run the command `magic -d XR` to open the Magic tool."
![image](https://github.com/user-attachments/assets/4f33e4e4-4192-46d2-8ca8-c9ec5efd2a67)
Let us start by opening met3.mag file in magic
![image](https://github.com/user-attachments/assets/d2cc0e9d-8371-43f5-8f58-215e6a61f6b5)

---

| **Step**                              | **Instructions**                                                                                                                                   |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| **Select an Area and Fill with Metal 3** | 1. Open the Magic GUI.<br>2. Select the desired area on your layout.<br>3. Navigate to the metal 3 layer.<br>4. Press `P` to fill the selected region with metal 3. |
| **Create the VIA2 Mask**              | 1. Open the tkcon terminal within Magic.<br>2. Type the command: `cif see VIA2`.<br>3. The metal 3-filled area will now be associated with the VIA2 mask.              |

---
![image](https://github.com/user-attachments/assets/3c179c55-a2e4-43be-b3ff-538665db0c37)
![image](https://github.com/user-attachments/assets/2010323b-ae16-4559-b46b-6842f061006b)
```
use 'feed clear' to go back to previous view
```

## Lab exercise to fix Poly-9 error in Sky130 tech file
Load 'poly.mag' file in magic 
![image](https://github.com/user-attachments/assets/8f7cb9f4-cf9c-46a3-93b7-5e6a2c51e33a)
Verify the spacing between the poly resistor and the poly in the layout and compare it with the specified value on the Skywater website. The image below highlights the spacing error between them. Let's proceed to correct it.
![image](https://github.com/user-attachments/assets/38d76300-fc04-4200-9846-cc6e748029e3)
![image](https://github.com/user-attachments/assets/39de23bd-709f-4854-8d50-f13da2c2fef0)

Open the Sky130a.tech file located in the drc_tests directory. Search for the poly.9 keyword and apply the changes shown in the images below. Save the file after making the modifications.

![image](https://github.com/user-attachments/assets/50c09602-f045-4642-adfe-75be38fdfa53)
![image](https://github.com/user-attachments/assets/771de5e8-f60c-4f98-bc7d-0abf237b0288)

Reload the tech file using the command tech load sky130A.tech, and recheck the design rule checks (DRC) by executing drc check in the tkcon terminal.
![image](https://github.com/user-attachments/assets/5f15aa07-f354-4b2f-8537-d6dc72b17b2a)

## Lab challenge exercise to describe DRC error as geometrical construct
Now load nwell.mag file into the magic and check for violations.
![image](https://github.com/user-attachments/assets/30cf2eb7-48a7-48da-8008-ea491ee7e95d)
In the above layout we have some violations, Open tech file and make changes as shown:
![image](https://github.com/user-attachments/assets/c3bf0b0f-89c9-4806-add7-d02db84c42b8)
![image](https://github.com/user-attachments/assets/7cb3538a-a06d-4517-b79a-224ba266f611)


## Lab challenge to find missing or Incorrect rules and fix them
After updating the tech file, use the following commands:
```
tech load sky130A.tech
drc check
drc style drc(full)
```
![image](https://github.com/user-attachments/assets/4bfb7e93-8fa6-4969-915d-956d09f2b472)
Now, we can see as we apply the contact the errors are removed.

# DAY4 : THEORETICAL CONCEPTS

## Introduction to delay tables
![image](https://github.com/user-attachments/assets/0b14100e-35e3-43fd-bde8-63f42c77cd70)
![image](https://github.com/user-attachments/assets/a96e61d8-e7bf-4944-839f-53991fd756e7)
At every level , each node  is driving the same load, hence there is no skew, if there would be a case with different loads then there will be skew.

## Introduction to CTS
![image](https://github.com/user-attachments/assets/bdcf4277-83ff-4631-b4b8-c4b4be887026)
![image](https://github.com/user-attachments/assets/540dd2bb-2d28-44ab-8462-28e82b7f2aac)
![image](https://github.com/user-attachments/assets/7fd8c791-57e4-4b05-ba5a-c17da5d3dde6)
![image](https://github.com/user-attachments/assets/4f8e59b2-40bd-47e0-9140-35769fb80035)

# TIMING ANALYSIS
* Setup Timing Analysis
![image](https://github.com/user-attachments/assets/3e2b6ea2-2788-4f50-be12-24bf49ba8f03)
* Hold Timing Analysis
![image](https://github.com/user-attachments/assets/cd7e38c5-d9e1-4662-82e6-dd381f68ab5e)

![image](https://github.com/user-attachments/assets/97ef2e04-a6e1-4b3f-a149-1a89900b20ed)

# DAY4 LABS: PRE-LAYOUT TIMING ANALYSIS & IMPORTANCE OF GOOD CLOCK TREE

## TIMING MODELLING USING DELAY TABLES

### Converting the Grid Info to Track Info
**Purpose:**

In physical design, it is essential to convert grid information, such as rows and columns, into track information. Tracks are predefined horizontal and vertical paths on each metal layer.

**Considerations:**

When designing standard cells, consider the following:

Case 1: Input and output ports should align with the intersections of vertical and horizontal tracks.
Case 2: The standard cell's width should be an odd multiple of the horizontal track pitch, and its height should be an odd multiple of the vertical track pitch.

**LEF File Extraction:**

To continue, we need the LEF (Library Exchange Format) file for the Inverter cell. Extract this file from the current Inverter cell to provide essential information for the place-and-route (PNR) process.

**Understanding Tracks:**

Open the tracks.info file to learn more about the horizontal and vertical tracks available on each metal layer. This file specifies pitch, spacing, and other relevant details necessary for efficient routing.

* Command to open the custom Inverter Layout in Magic, first go to the 'vsdstdcelldesign' dircetory and then use:
  ```
  magic -T sky130A.tech sky130_inv.mag &
  ```
  ![image](https://github.com/user-attachments/assets/da714e9e-32db-4001-b5de-58e0ee56e7c1)

* Open the tracks.info file to know more about tracks:
  ```
  # Fisrt go to the following directory :
  /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd

  # open the tracks.info file
  less tracks.info
  ```
  ![image](https://github.com/user-attachments/assets/9a8380e7-de59-4682-a84a-fdbf095cb305)

- To set grids as tracks of locali layer, use the follwoing command:
  ```
  grid 0.46um 0.34um 0.23um 0.17um
  ```
  ![image](https://github.com/user-attachments/assets/583c0ebe-5852-41c9-af4a-5aab981d9ea3)
  
  Now, we can see in the below image , that the Case 1 consideration is met i.e. Input and output ports are aligned with the intersections of vertical and horizontal tracks.
  ![image](https://github.com/user-attachments/assets/80f04067-318a-49c6-97a3-33b1ffac7f28)
  Now, we can see in the below image , that the Case 2 consideration are also met as 3 boxes are covered between the boundariesi.e. The standard cell's width should be an odd multiple of the horizontal track pitch, and its height     should be an odd multiple of the vertica track pitch.
  ![image](https://github.com/user-attachments/assets/61fbdc5c-3b97-48c5-947b-0a355681f015)
  ![image](https://github.com/user-attachments/assets/26b1a068-37fe-4408-b627-97f1b99079c9)

  - How to convert labels to ports *[No need to do it here as it is already done]*:
    ![image](https://github.com/user-attachments/assets/65cb992f-3965-4eba-ba36-09414af9b3a2)
    
  ## Converting magic layout to standard cell LEF
   *Follow this Github Repository For more deatils: * [Click here](https://github.com/nickson-jose/vsdstdcelldesign)
  Now, setting up the ports type:
  ![image](https://github.com/user-attachments/assets/bd4878b6-e001-43e4-86a3-e4a66d2f10d9)
  ![image](https://github.com/user-attachments/assets/0e5e2138-11ce-47d7-9d47-251a01f74cc6)
  ![image](https://github.com/user-attachments/assets/007c1a62-367f-4a23-9ff2-0cc0d506400f)
  ![image](https://github.com/user-attachments/assets/68d743d9-0a1e-4308-b457-f6ad79705bc0)

  Now we need to extract the LEF file. First save .mag file by using the command ``save sky130_vsdinv.mag``` in the tkcon terminal.
  ![image](https://github.com/user-attachments/assets/6edb6cf6-a688-4910-b2a2-875637e06c78)
  
  Now, use the follwoing command to open the saved mag file:
  ```
  magic -T sky130A.tch sky130_vsdinv.mag &
  ```
  ![image](https://github.com/user-attachments/assets/e5e5b29c-306e-4613-942a-465ed92fa7d5)

  Now, us the follwoing command in tckon window:
  ```
  # To extract the Lef file use the command:
  lef write
  ```
  ![image](https://github.com/user-attachments/assets/e12a0f56-8e47-4717-97af-32c8ff91b845)
  Now, open the file ``` less sky130_vsdinv.lef```
  ![image](https://github.com/user-attachments/assets/6fb07bff-948c-4797-91b2-f3ad2be1dae3)

  ## Introduction to timing libs and steps to include new cell in synthesis
  Now, first copy the files in src directory, us ethe following command:
  ```
  cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
  ```
  ![image](https://github.com/user-attachments/assets/e1c17c20-4059-4caf-862c-2c635f90a980)
  Now, basic idea is to include our custom cell in picorv32a openlane design flow
  Also, copy the follwoing files shown in image below in src directory, us the following command:
  ![image](https://github.com/user-attachments/assets/fdafbd6b-2200-454e-b74f-5617857b0dba)
  ```
  cp sky130_fd_sc_hd__* /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
  ```
  ![image](https://github.com/user-attachments/assets/61f4e306-528c-4cfa-8e5a-957be5a9cdeb)
  Now, we need to modify the config.tcl file:
  Go to picorv32a dircetory and open the file using vim
  ```
  vim config.tcl
  ```
  make the following modifications:
  ![image](https://github.com/user-attachments/assets/697bcfe9-219e-4d84-9e8e-386b7d4f6531)
  Now, invoke the docker:
  ![image](https://github.com/user-attachments/assets/6945cc20-7fbb-4ace-9a92-e6bf4e198151)
  Now, do the regular steps as shown:
  ```
  ./flow.tcl -interactive
  package require openlane 0.9

  #to continue the work in already made directory in runs folder
  prep -design picorv32a -tag 12-07_11-26 -overwrite
  ```
  This will continue our work in '12-07_11-26' and '-overwrite' will continue the work with the chanegs we made and overwrite them.
  ![image](https://github.com/user-attachments/assets/61bc6b5a-89c2-48cd-b62f-f0a1b8878646)
   Now run synthesis ```run_synthesis```
  ![image](https://github.com/user-attachments/assets/0e16b94c-c4a5-4a31-8a36-7afea30c59c9)
  ![image](https://github.com/user-attachments/assets/6f62332d-2cbb-41f3-8295-f0241cec8f51)
  From the figure above, it is evident that the synthesis was successful, with a total of 1554 instances of our vsdinverter. Therefore, this stage has been completed successfully.
  From the above figure we can see the worst slack is -23.89 and total negative slack is -711.59.

  ## Steps to configure synthesis settings to fix slack and include vsdinv
  Chip area for module '\picorv32a': 147712.918400
  See the Readme File in configuration directory:
  ![image](https://github.com/user-attachments/assets/f6c21b7f-79ff-4620-965b-03a56a6e57d9)

  - Commands to view and change parameters to improve timing and run synthesis:

| Step | Command | Description |
|------|---------|-------------|
| 1 | `prep -design picorv32a -tag 24-03_10-03 -overwrite` | Prepare the design for updating variables |
| 2 | `set lefs [glob $::env(DESIGN_DIR)/src/*.lef]` | Include newly added LEF files in the OpenLane flow |
| 3 | `add_lefs -src $lefs` | Merge the LEF files |
| 4 | `echo $::env(SYNTH_STRATEGY)` | Display the current value of the `SYNTH_STRATEGY` variable |
| 5 | `set ::env(SYNTH_STRATEGY) "DELAY 3"` | Set a new value for the `SYNTH_STRATEGY` variable |
| 6 | `echo $::env(SYNTH_BUFFERING)` | Check if `SYNTH_BUFFERING` is enabled by displaying its current value |
| 7 | `echo $::env(SYNTH_SIZING)` | Display the current value of the `SYNTH_SIZING` variable |
| 8 | `set ::env(SYNTH_SIZING) 1` | Set a new value for the `SYNTH_SIZING` variable |
| 9 | `echo $::env(SYNTH_DRIVING_CELL)` | Check the current value of `SYNTH_DRIVING_CELL` to ensure it's the correct cell |
| 10 | `run_synthesis` | Run the synthesis process after the design is prepared |

![image](https://github.com/user-attachments/assets/bdad3276-f68e-4e2f-8ecc-7e005d80fd94)

![image](https://github.com/user-attachments/assets/cc2b649c-dc83-4cbb-8bb6-00f9e4349733)

Now, tns and wns is zero and  Chip area for module '\picorv32a': 181730.544000 is increased now.
Now ```run_floorplan```
![image](https://github.com/user-attachments/assets/674001ab-313e-4dcf-aa12-12587ad8481d)
As we can see from the above image, it is failed.
So, run these:


```h```````````````````````````````````````````````````````````````````````````````````````````````````````````h ```
As we have completed the synthesis stage now we complete the floorplan using the following command:
```
init_floorplan
place_io
tap_decap_or
```
![image](https://github.com/user-attachments/assets/061403dc-8294-4d9a-b237-3a2b13e786ff)

Now, as floorplan stage is completed , we run placement
```
run_placement
```
![image](https://github.com/user-attachments/assets/04af4d5f-aa8a-41f8-a2e7-8ccadb86fc33)

Now, lets check whether the cell that we have created has been included in the design or not.
Go to the follwoing directory :
```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/20-07_16-44/results/placement
```
use :
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/user-attachments/assets/d27072a6-f7a9-4955-9129-320b2617cb37)

we cans ee that the cell is successfully placed in the deisgn.
now let us check its alignment is correct or not use command 'expand' in 'tckon' window.
![image](https://github.com/user-attachments/assets/e5cef10f-e4d4-407f-846c-56a756aff777)


# Timing analysis with ideal clocks using openSTA

## Configure OpenSTA for post-synth timing analysis

Next stage is to perform STA on the design:
First create 'pre_sta.conf' file in the openlane directory as shiown below:
![image](https://github.com/user-attachments/assets/45121ad5-0b64-4764-8005-9112283da803)
```
set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um
read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pins}
report_tns
report_wns
```

and then create 'my_base.sdc' file in the /picorv32a/src directory as shown below:
![image](https://github.com/user-attachments/assets/e8cd06f5-7f1d-4c4c-a8fe-c5fda8ba82bb)
```


set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 24.73
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.653
set ::env(IO_PCT) 0.2
set ::env(SYNTH_MAX_FANOUT) 6

create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)

set input_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]

puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"

set_max_fanout $::env(SYNTH_MAX_FANOUT) [current_design]

set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]

set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]

set all_inputs_wo_clk_rst $all_inputs_wo_clk

set_input_delay $input_delay_value -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst

set_output_delay $output_delay_value -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]

set cap_load [expr $::env(SYNTH_CAP_LOAD) /1000.0]

puts "\[INFO\]: Setting load to: $cap_load"

set_load $cap_load [all_outputs]
```
Now use the command:
```
sta pre_sta.conf
```

![image](https://github.com/user-attachments/assets/28a4d931-3fd1-4c07-b877-93bd64aa1f2b)
As we can see that Slack is equal to of that we got in synthesis stage. So STA is succesful.

## Steps to run CTS using TritonCTS

To update the previous design with the improved version, use the command:

```
write_verilog //path of the previous design//
#In our case:
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/20-07_16-44/results/synthesis/picorv32a.synthesis.v
```
![image](https://github.com/user-attachments/assets/5e371a72-da7d-478b-aecb-9fa09d20abd9)


This will replace the old design with the optimized one. Once the update is complete, proceed with the Floorplan stage using the same commands as before.
```
init_floorplan
place_io
tap_decap_or
```
Upon successful completion of the Floorplan, proceed to the placement step by running the command:

```
run_placement
```
as we can see from the below images file has been overwritten
![image](https://github.com/user-attachments/assets/82baef26-bec0-4c9e-883d-4e1c68daca02)

![image](https://github.com/user-attachments/assets/78046951-c53b-41f5-abe0-8f4377a0ec98)
Now after the placement has  been completed, we go for CTS:
```
run_cts
```
![image](https://github.com/user-attachments/assets/1d44dafc-0475-471d-89d8-74c2369b85a9)

In cts stage buffers get added , modifying the netlist. After completion of the cts we can observe that in the synthesis results directory a new .cts file is added. The newly added CTS file contains both the previous netlist and also the clock buffers that were added during the cts stage.

![image](https://github.com/user-attachments/assets/a0f8d5fc-1839-4c91-8d20-b3c57f6ceb94)

## Timing analysis with real clocks using openSTA
use the below given command to enter into openRoad:
```
openroad
```
In openroad, We will first create the database (creted from lef and def files) and in the timing analysis this db is used.
Run the follwoing commands:
```
read_lef /openLANE_flow/designs/picorv32a/runs/20-07_16-44/tmp/merged.lef
```
![image](https://github.com/user-attachments/assets/f85780c0-983e-4e48-ae1a-f58dbad24d4c)

```
read_def /openLANE_flow/designs/picorv32a/runs/20-07_16-44/results/cts/picorv32a.cts.def
```
![image](https://github.com/user-attachments/assets/79a0fcc2-fe4b-45ee-bcbc-ef3eec3ab225)

```
write_db pico_cts.db
```
![image](https://github.com/user-attachments/assets/0fff2ce8-fefd-4d84-a5cd-3da7ff1ccce1)

```
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/20-07_16-44/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4

```
![image](https://github.com/user-attachments/assets/2f16e2db-a617-42a3-9b32-3759a1b8147b)

## Steps to execute OpenSTA with right timing libraries and CTS assignment
First use ```exit`` to exit from openroad, now you will come to openlane:
Now follow these steps:
To check the current value of CTS_CLK_BUFFER_LIST
```
echo $::env(CTS_CLK_BUFFER_LIST)
```
![image](https://github.com/user-attachments/assets/e906776e-e6cc-413e-8864-92429d5fed0b)

To remove sky130_fd_sc_hd__clkbuf_1 from the list
```
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
```
![image](https://github.com/user-attachments/assets/81c0a668-a981-4410-ac1f-246ec76e5beb)

Now, To check we run the cts agian ```run_cts```

Now, it will failed or in hung state then kill this task

To check the current value of CURRENT_DEF
```
echo $::env(CURRENT_DEF)
```
![image](https://github.com/user-attachments/assets/0784969d-fa4d-45f4-a4c0-74c831acd760)
To set def as placement def
```
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/12-07_11-26/results/placement/picorv32a.placement.def
```
![image](https://github.com/user-attachments/assets/0755db98-c683-4a91-b6c6-e2bd568e4198)
To check the current value of CTS_CLK_BUFFER_LIST
```
echo $::env(CTS_CLK_BUFFER_LIST)
```
![image](https://github.com/user-attachments/assets/eb9794bb-04cb-41ee-94b0-5bd307f300f2)

Now run_cts again.


Now, We need to follow the similar steps that we have followed earlier in the openroad.
go to openroad again and then:
```
read_lef /openLANE_flow/designs/picorv32a/runs/12-07_11-26/tmp/merged.lef

read_def /openLANE_flow/designs/picorv32a/runs/12-07_11-26/results/cts/picorv32a.cts.def

write_db pico_cts1.db

read_db pico_cts1.db

read_verilog /openLANE_flow/designs/picorv32a/runs/12-07_11-26/results/synthesis/picorv32a.synthesis_cts.v

read_liberty $::env(LIB_SYNTH_COMPLETE)

link_design picorv32a

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

set_propagated_clock [all_clocks]

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```
![image](https://github.com/user-attachments/assets/42248361-de62-4345-bff0-40266cf3d969)
The setup slack has improved if we use clock_buf_2 now. But there is a tradeoff with the area.
```
report_clock_skew -hold
```
![image](https://github.com/user-attachments/assets/275bd6dd-6fb6-4707-8562-379cfa95cd8d)

```
report_clock_skew -setup
```
![image](https://github.com/user-attachments/assets/49b918e1-5edd-46f9-a0cd-360061537577)

### Now if we want to include buf_1 again?
Exit the openroad first.
To check the current value of CTS_CLK_BUFFER_LIST
```
echo $::env(CTS_CLK_BUFFER_LIST)
```
![image](https://github.com/user-attachments/assets/096e422b-2580-4af0-8a46-24b0a75774ce)

To insert sky130_fd_sc_hd__clkbuf_1 from the list
```
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]
```
![image](https://github.com/user-attachments/assets/f30b8304-952c-4aa1-9643-82d66f76eea5)

# DAY 5: Final steps for RTL2GDS using tritonRoute and openSTA
* **Note:**  How to know which stage was done previously in the flow?
* We can see it by seeing the def, current def got updated to cts in the previous stage when cts was completed.
  use the folllwoing command to check it:
  ```
  echo $::env(CURRENT_DEF)
  ```
  ![image](https://github.com/user-attachments/assets/66f1dcd0-0f34-4102-b75e-76f363537d58)

## Introduction to Routing Algorithm
* Maze Routing
  ![image](https://github.com/user-attachments/assets/cea1a2e7-9d15-4b59-89c1-c280f8829384)
  ![image](https://github.com/user-attachments/assets/06521a9e-571f-4864-b1f0-f1561c328b79)

  Routing grid is build with standard dimensions
  ![image](https://github.com/user-attachments/assets/a30e4231-6ca6-4160-9f6c-8584faa4a665)
  Algorithm utilises this routing grod to find the best route between the source and the target.
  ![image](https://github.com/user-attachments/assets/276fd90f-51a3-4003-94ea-ddc7709eebff)
  ![image](https://github.com/user-attachments/assets/76dcfad2-9ae2-4e62-8a6e-2618504b3e06)
  ![image](https://github.com/user-attachments/assets/2c7ed45a-974d-4ea0-877f-8d28d8e1f85c)
  There are various routes possible, but routes with less band s are preferred (preferable single band).
  There are other algorithms too in its replacement as it is more time consuming.
  ![image](https://github.com/user-attachments/assets/6b6218c9-35b9-4eff-8d1d-384e8d9ead4c)
* While doing routing , DRC Rules need to be followed.
  
## Steps to build power distribution network
As the CST stage is compelted, now we need to lay down the Power Distribution Network.

Use the folloeing command ```gen_pdn```.

![image](https://github.com/user-attachments/assets/cf7290b2-fde5-4928-a2af-2846f2b15482)

Now, from the above image we can see PDN is successfully generated.

![image](https://github.com/user-attachments/assets/35d5c295-1885-435d-8559-478c2c02e295)

Now, can see that the pitch of the standard cell rails is 2.720, which we have expected.

## Steps from power straps to std cell power
![image](https://github.com/user-attachments/assets/611e293f-2b07-42c9-bf36-3cfabe9e284b)

In the figure above, we can see how power is distributed to the standard cells.
Surrounding the design are I/O pads, with the red and blue blocks representing power pads. The red pads supply power, while the blue ones provide the ground connection.
These pads connect to power and ground rings that encircle the design, supplying power to straps.
The vertical lines seen for the rings are known as power straps.
Connections from the power straps and rings extend to the power rails, with standard cells positioned between these rails. The height of the standard cells must be multiples of the rail pitch to ensure proper power and ground supply.

![image](https://github.com/user-attachments/assets/bb732958-682a-407b-8f90-35083ee6082b)
Now, we can see def has been modifoed from cts to pdn.


## Basics of global and detail routing and configure TritonRoute

Now the last stage in the design is Routing , us ethe following command: 
```
run_routing
```

### Routing using TritonRoute
![image](https://github.com/user-attachments/assets/bdf1ee06-3092-4f06-970d-632618d4438c)

# References

This project has utilized resources and materials from the following sources:

- [VSD Standard Cell Design](https://github.com/nickson-jose/vsdstdcelldesign)
- [Google Skywater PDK](https://github.com/google/skywater-pdk)
- Materials provided in the NASSCOM VSD SoC Design Program
