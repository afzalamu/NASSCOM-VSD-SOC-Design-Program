# NASSCOM-VSD-SOC-Design-Program

## DAY1 THEORY : Open-source EDA, OpenLANE and Sky130 PDK

### Insight into the QFN-48 Chip: Pads, Core, Die, and IP Components








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
  
### Design Preperation Step
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















