# NASSCOM-VSD-SOC-Design-Program
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
we wil be working with 'openlane_working_dir' so use : 

```
cd openlane_working_dir/
```
![5](https://github.com/afzalamu/NASSCOM-VSD-SOC-Design-Program/assets/124300839/cce17ef1-19d8-4129-98ec-b658086c92f7)

- Important Files and Directories
  ```
   pdks: It is known as Process Design Kit. For this workshop we are using an opensource pdk i.e 'skywater 130nm pdk'. OPENLANE is built around this 'skywater 130nm pdk'.
    - skywater-pdk : This has all the pdk related files such as timing libraries, Lef files etc.
    - open_pdks : It contains set of scripts & files that converts the foundary level pdks to be compatible with the open source EDA Tools.
    - sky130A : It is a pdk variant , already made compatible with the open source EDA tools.
          - libs.ref: It contains files specific to the technology such as design libraries, standard cells and many more.
          - libs.tech: It contains files specific to the Tools.
  ```


    













