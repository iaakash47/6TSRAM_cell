# Design and Implementation of 6T SRAM Cell
* This project focuses on design of a design and Implementation of 6T SRAM Cellusing Google Skywater (sky130nm) Technology node with operating voltage of 1.8V .The project is build using Open Source Tools like Sky130PDK and eSim and Ngspice. Refer following website for more details 6T SRAM Shifter:https://en.wikipedia.org/wiki/Static_random-access_memory
 
# Table of Contents

1. [Introduction](#introduction)
2. [Installation of the tools](#installation-of-the-tools)
3. [Creation of project](#creation-of-project)
    * [eSim Window ](#esim-window)
    * [eSim Schematic Window](#esim-schematic-window)
4. [Reference Circuit](#reference-circuit)
5. [Reference Waveform](#reference-waveform)
6. [Methodology](#methodology) 
7. [Schematic](#schematic)
8. [Circuit Schematic](#circuit-schematic)
9. [Netlist](#netlist)
10. [Initial Transitent Analysis](#initial-transitent-analysis)
11. [Waveforms](#waveforms)
    * [Read operation Waveforms](#read-operation-waveforms)
    * [Write operation Waveforms](#write-operation-waveforms)
12. [References](#references)
13. [Contributor](#contributor)
14. [Acknowledgments](#acknowledgments)


## Introduction 
####  6T SRAM
* With the advent of portable devices, the demand for static random-access memory (SRAM)
is increasing with large use of SRAM in System on Chip and high-performance VLSI circuits. SRAM
optimization has become a focal point for research work, as 60% to 70% area of the chip is consumed
by the memories. The performance parameters optimization can lead to the overall optimization of the
performance of the chip. In this paper design and analysis of the 6T SRAM cell at different
technologies using PTM (Predictive Technology Model) model has done with the aim of reducing
power dissipation while maintaining stability. Then the performance of SRAM cell is compared on the
basis of power dissipation i.e. dynamic power dissipation and static power dissipation, delay, Power
Delay Product (PDP) and Static Noise Margin (SNM).SRAM cell read stability and write-stability are
major concerns in nanometer CMOS technologies, due to the progressive increase in intra-die
variability and Vdd scaling. Cell stability is also examined by the calculation of SNM with the help of
the butterfly curve method at different CMOS technologies. Effect of variation of channel length on
static power consumption, dynamic power consumption, delay, PDP and SNM is also measured. SNM
variation is also observed with the variation of the supply voltage.

## Installation of the Tools

- eSim : [Link](https://esim.fossee.in/downloads)
- Ngspice : [Link](https://sourceforge.net/projects/ngspice/files/)
 * Ngspice gets installed alongwith eSim. If any other version ids to be installed refer: http://ngspice.sourceforge.net/download.html
- Sky130 PDK : [Link](https://static.fossee.in/esim/installation-files/sky130_fd_pr.zip)
 
  * After Downloading eSim extract it choose the Directory to save the eSim Workspace


* Opensource Tools used

1. eSim: eSim (previously known as Oscad / FreeEDA) is a free/libre and open source EDA tool for circuit design, simulation, analysis and PCB design developed by FOSSEE, IIT Bombay. It is an integrated tool    built using free/libre and open source software such as KiCad, Ngspice and GHDL. eSim is released under GPL. eSim offers similar capabilities and ease of use as any equivalent proprietary software for schematic creation, simulation and PCB design, without having to pay a huge amount of money to procure licenses. Hence it can be an affordable alternative to educational institutions and SMEs. It can serve as an alternative to commercially available/licensed software tools like OrCAD, Xpedition and HSPICE. For more info refer: https://esim.fossee.in/home

2. Ngspice: Ngspice is the open source spice simulator for electric and electronic circuits. Ngspice offers a wealth of device models for active, passive, analog, and digital elements. Model parameters are provided by the semiconductor manufacturers. The user add her circuits as a netlist, and the output is one or more graphs of currents, voltages and other electrical quantities or is saved in a data file. For more info refer: http://ngspice.sourceforge.net/

3. Skywater Pdk: The SkyWater Open Source PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility. As of May 2020, this repository is targeting the SKY130 process node. If the SKY130 process node release is successful then in the future more advanced technology nodes may become available.
For more info refer: https://github.com/google/skywater-pdk, https://skywater-pdk.readthedocs.io/en/latest/


## Google SkyWater PDK

The SkyWater Open Source PDK is a collaboration between Google and SkyWater Technology Foundry to provide a fully open source Process Design Kit and related resources, which can be used to create manufacturable designs at SkyWater’s facility.

![skywater-pdk-logo](https://user-images.githubusercontent.com/80625515/152778227-8a0c133c-ec8e-4f1a-96bc-2739e4689419.png)

More details of SkyWater Open Source PDK can be found [here](https://github.com/google/skywater-pdk).

## Skywater Pdk Installation(Ubuntu)
Open the terminal and follow these steps:
```
git clone git://opencircuitdesign.com/open_pdks
cd open_pdks
./configure --enable-sky130-pdk
make
sudo make install
```

#### Cloning
* Clone this repository using the following commands:
```
$ sudo apt install -y git
$ git clone https://github.com/iaakash47/Barrel_shifter.git

``` 
 
Follow these steps for Sky130 download and implementaion :
1. Download sky130 from this link mentioned above and unzip it.
2. Save the .cir.out file in the sky_fd_pr folder as .cir file.
3. Open with notepad and add the path .lib "models/sky130.lib.spice" tt at the top.
4. Replace with CMOSP, mos_p with sky130_fd_pr_pfet_01v8 and CMOSN, mos_n with  sky130_fd_pr_nfet_01v8.
5. To replace inductor, capacitor, resistor do it this way, for Ex : L1 out gnd 1m by x1  out gnd mid 0 sky130_fd_pr__ind_03_90.

```
Note: For more details go to the cells folder in sky_fd_pr. 
Open the specific component folder which you want to use. 
Then open the test folder and check the SPICE file. 
The SPICE file is an example of implementation of that component. 
You will get to know how to use the component in your ckt.

```

 
 ## Creation of project 
 * Click on the New Project and save the file name without any space 
 * Project will be created 
 
 
 ## eSim Window 
 ![eSim](https://user-images.githubusercontent.com/88897605/152910524-9211a17b-02d8-45a5-a353-28dc422f83c6.png)
 
 
 
 ## eSim Schematic Window 
 ![eSimWindow](https://user-images.githubusercontent.com/88897605/152910659-23f4e30a-12d6-4d09-bb6f-732041acbe60.png)
 

To Run the ckt using ngspice:
1. Replace with sky130nm cells and save this .cir file.
2. Paste the .cir file in gedit document where the sky130_fd_pr folder is present  
3. To Run the ngspice waveform,save the .cir file and replace with filename.spice  
4. Open Terminal in the saved Directory 
5. And run the following command(ngspice filename.spice)
- For reference to download the tools and get an exposure to simulation using eSim, ngspice and Sky130, you may want to check the course : [Link](https://www.udemy.com/share/104Ie63@EAkZWPY9P8VxMdqx7DK4NzA2SwmLzfA1pfjL_MLTmkTV9O283uXSWpJkSSNIPjmKmA==/)

# Reference Circuit 
* Reference Circuit of 6T SRAM is as shown below 
![Conventional-6T-SRAM-Cell-7](https://user-images.githubusercontent.com/88897605/157731476-664195fe-7a1f-4974-9fd4-7c78c35efbe7.png)


# Reference Waveform
* Reference Waveform of 6T SRAM is as shown below
![Output-waveform-of-6T-SRAM-cell](https://user-images.githubusercontent.com/88897605/157731756-3f52729f-97a9-4553-bef2-acf776096d04.png)



## Methodology

# Prelayout Simulation in eSim and Ngspice
Refer following manual to know how to operate eSim:
https://static.fossee.in/esim/manuals/eSim_Manual_2020_August.pdf

# Schematic

## Schematic Window
- Construct the "6T SRAM" as shown in the figure below using eSim 
![6tsram_schematic](https://user-images.githubusercontent.com/88897605/157733150-5d6e94b3-8d32-4c59-9fc0-61170d2993cd.png)

# Circuit Schematic
* 6T SRAM
![6T_SRAM_DESGIN](https://user-images.githubusercontent.com/88897605/157733232-3ee21556-8575-4eb9-ba7c-69f8ab2a0194.png)


- Once every step is followed perfectly open the Netlist that is generated and make the necessary changes to add the Sky130 models
- The Netlist generated initially is as shown below and replace the components with skywater130nm cells

#### Editing the Netlist
```

a) To execute the .cir file, follow these steps:
Step 1: Open the .cir file (barrel_shifter.cir in my case) with notepad 
Step 2: Make sure the path .lib "sky130_fd_pr/models/sky130.lib.spice" tt at the top.
Step 3: Make sure that all mosfets are replace with sky130_fd_pr__nfet_01v8
Step 4: Delete any / added if any 
Step 5: Prefix x with all Transistors starting with M. Do this for all transistors 
e.g Before M1, after xM1
Step 6: Comment with * if any ports are added by defaults 
e.g *U1  /input_In0 PORT	
*U9  /Out_0 PORT	
Step 7: Next Start adding Inputs sources, supply voltage, etc (Vdd was considered as 1.8V)
Step 8: Add .tran statement with initial step time and final stop time 
eg. .tran 0.4ns 40ns 
Step8: Add .control command and run command to run the plot 
Step9: Add the voltage or current input or output quantities to be plotted 
eg. plot V(input_In0) 
plot V(Out_0) 
Step 10: Last step is to add .endc followed by .end command 

```
* Now Run the circuit with ngspice.

To Run the ckt using ngspice:
1. Replace with sky130nm cells and save this .cir file.
2. Paste the .cir file in gedit document where the sky130_fd_pr folder is present  
3. To Run the ngspice waveform,save the .cir file and replace with filename.spice  
4. Open Terminal in the saved Directory 
5. And run the following command(ngspice filename.spice)
- For reference to download the tools and get an exposure to simulation using eSim, ngspice and Sky130, you may want to check the course : [Link](https://www.udemy.com/share/104Ie63@EAkZWPY9P8VxMdqx7DK4NzA2SwmLzfA1pfjL_MLTmkTV9O283uXSWpJkSSNIPjmKmA==/)

# Netlist

# Netlist - Read Operation
 
```
* /home/user/eSim-Workspace/6Tsram/6Tsram.cir

* EESchema Netlist Version 1.1 (Spice format) creation date: thur Mar 10 16:56:06 2022

.lib "sky130_fd_pr/models/sky130.lib.spice" tt

* Sheet Name: /
xM1  Q Q1 Net-_M1-Pad3_ Net-_M1-Pad3_ sky130_fd_pr__pfet_01v8 w=0.84 l=0.21 
		
xM2  Q Q1 GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21		
xM3  Q1 Q Net-_M1-Pad3_ Net-_M1-Pad3_ sky130_fd_pr__pfet_01v8 w=0.84 l=0.21
		
xM4  Q1 Q GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21	
xM7  Net-_M1-Pad3_ Q vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.21
	
xM5  Q WL BL GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21
xM6  RBL Q1 GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21

V1 vdd gnd dc 1.8V

VWL WL gnd pulse 0 1.8 0 60ps 60ps 20ns 40ns
VQ Q gnd pulse 1.8 0 0 60ps 60ps 5ns 10ns
.tran 0.1n 100n 
.control
run
plot V(WL)+8 V(BL)+2 V(RBL) V(Q)+4 V(Q1)+6
.endc
.end


```

# Netlist - Write Operation

```

* /home/user/eSim-Workspace/6Tsram/6Tsram.cir

* EESchema Netlist Version 1.1 (Spice format) creation date: thur Mar 10 16:56:06 2022

.lib "sky130_fd_pr/models/sky130.lib.spice" tt

* Sheet Name: /
xM1  Q Q1 Net-_M1-Pad3_ Net-_M1-Pad3_ sky130_fd_pr__pfet_01v8 w=0.84 l=0.21 
		
xM2  Q Q1 GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21		
xM3  Q1 Q Net-_M1-Pad3_ Net-_M1-Pad3_ sky130_fd_pr__pfet_01v8 w=0.84 l=0.21
		
xM4  Q1 Q GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21	
xM7  Net-_M1-Pad3_ Q vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.21
	
xM5  Q WL BL GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21
xM6  RBL Q1 GND GND sky130_fd_pr__nfet_01v8 w=0.42 l=0.21

V1 vdd gnd dc 1.8V

VWL WL gnd pulse 0 1.8 0 60ps 60ps 20ns 40ns
VBL BL gnd pulse 0 1.8 0 60ps 60ps 5ns 10ns
VQ1 Q1 gnd pulse 1.8 0 0 60ps 60ps 5ns 10ns
VRBL RBL gnd pulse 1.8 0 0 60ps 60ps 5ns 10ns
.tran 0.1n 100n 
.control
run
plot V(WL)+8 V(BL)+6 V(RBL)+4 V(Q)+2 V(Q1)
.endc
.end

```

* Save the above ngspice subcircuit spice file in a folder where the sky_fd_pr_ folder is present

![sky130nm_window](https://user-images.githubusercontent.com/88897605/157734314-69052973-f39f-49b1-9717-0a1be9557213.png)


* Run the spice file with following Terminal Command as shown 

![read_wind](https://user-images.githubusercontent.com/88897605/157734543-ddeabb66-4489-40f5-a4ab-ee6aee72ae5b.png)

# Initial Transitent Analysis

## Initial Transitent Analysis - Read
![initial_read](https://user-images.githubusercontent.com/88897605/157734831-abe7c990-48de-479e-a913-77b5a4111fc9.png)


## Initial Transitent Analysis - Write
![initial_write](https://user-images.githubusercontent.com/88897605/157734846-837f4acf-43e5-431c-8665-9512af5cfde3.png)

# Waveforms 

* Read operation Waveforms 
* Write operation Waveforms 

# Read operation Waveforms
![6tsram_read](https://user-images.githubusercontent.com/88897605/157735054-b50c287e-4ed3-4d23-9053-40db90785f9b.png)


# Write operation Waveforms 
![6SRAM_write](https://user-images.githubusercontent.com/88897605/157735081-26f2fdeb-883c-4bc8-881d-364bf45b983d.png)


# References
- Design of Low Power 6T Sram with and without ROFs
- Analysis of 6T SRAM Cell in Different Technologies


# Contributor
Aakash.K</br>
Contact:iaakashkrish@gmail.com</br>

Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com

# Acknowledgments
Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com

Fossee IIT Bombay 

Sumantho Kar IIT Bombay Senior Project Co-ordinator











