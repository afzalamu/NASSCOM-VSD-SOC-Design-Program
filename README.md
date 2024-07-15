
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
  - [CELL DESIGN AND CHARCATERISATION FLOWS](#cell-design-and-characterisation-flows)
- [DAY2 LABS: FLOORPLANNING & PLACEMENT](#day2-labs-floorplanning--placement)
  - [STEPS TO RUN FLOORPLAN USING OPENLANE](#steps-to-run-floorplan-using-openlane)
  - [STEPS TO PERFORM PLACEMENT IN OPENLANE](#steps-to-perform-placement-in-openlane)

    







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

### CELL DESIGN AND CHARCATERISATION FLOWS

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
![2](https://github.com/user-attachments/assets/bf52d41f-7c70-4971-b0b1-8b73303bab02)

When the floorplaning is completed, To view the results go to the path as shown in image below  : 

![4 def file](https://github.com/user-attachments/assets/229f9afe-3a12-4afa-b5f3-a38f97544d65)

open the def file:

![5 def file reuslts](https://github.com/user-attachments/assets/484078cb-b5d8-4f09-895c-159fd63d4e5f)

These results are useful for various analysis, for example: we can see the die area :

![6 area](https://github.com/user-attachments/assets/14b5aac1-a100-434a-8499-ce6dd35d3716)

Now, to open this "def" file in magic , use the following command:
```
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

```

![7 opening in magic](https://github.com/user-attachments/assets/14b20546-e434-4bad-93d1-6be3ea5fee71)
Now, we can use 'Magic' tool to expllore the floorplan.

#### Design Alignment Instructions in MAGIC

| **Task**                       | **Steps**                                                                                                         |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **Centering the Design**       | 1. Press `S` to select the entire design.<br>2. Press `V` to align it vertically to the middle of the screen.       |
| **Zooming In on a Specific Area** | 1. Left-click and drag to highlight the desired region.<br>2. Right-click to open the context menu.<br>3. Press `Z` to zoom in on the selected area. |
| **Retrieving Cell Details**    | 1. Hover your cursor over the cell you want details for.<br>2. Press `S` to select the cell.<br>3. In the `tkcon` window, type the command `what` to display the cell's details. |

![8 what command](https://github.com/user-attachments/assets/5941e834-c4c9-48ee-9db3-a514dc51cb38)

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
![1 placement donw](https://github.com/user-attachments/assets/00b4b998-a96a-43ab-8018-a8ae6547f80f)

After the Placement is done. To view the results Go to the following loacation:
```
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-07_11-26/results/placement$
```
And then we can see 'picorv32a.placement.def' file. To open it using MAGIC use the follwoing command:
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def
```
![2 placement result magic](https://github.com/user-attachments/assets/c480ee72-2130-422a-8f1c-c4f403072830)
![image](https://github.com/user-attachments/assets/6ffd41e9-d805-4da9-aa15-8f641046d05e)


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

## HOW TO GIT CLONE THE "vsdstdcelldesign"?

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





  









