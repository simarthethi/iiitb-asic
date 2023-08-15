# iiitb-asic
This github repository contains the progress made in asic 

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

## Day 0

<details>
 <summary> summary </summary>
  installed and launched the required tools
</details>

<details>
 <summary> Yosys </summary>


 I installed Yosys using the following commands:
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys-master 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install
```
afterinst:

![Screenshot from 2023-08-01 11-24-29](https://github.com/simarthethi/iiitb-asic/assets/140998783/a785f703-c42b-49cf-9224-73cb47949e5a)
</details>

<details>
 <summary> iverilog </summary>


 Installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
below is thescreenshot showing iverilog successfully installed
![Screenshot from 2023-08-01 11-25-21](https://github.com/simarthethi/iiitb-asic/assets/140998783/8e2c2866-d51e-4bef-942a-849306bfbce7)
</details>

<details>
 <summary> gtkwave </summary>


 Installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
Screenshot of gtkwave successfully installed
![Screenshot from 2023-08-01 11-26-05](https://github.com/simarthethi/iiitb-asic/assets/140998783/6aedab78-71dd-4088-b589-54aaeae00841)
</details>

<details>
 <summary> OpenSTA </summary>


 Installed and built OpenSTA (including the needed packages) using the following commands:
 ```bash
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
screenshot of OpenSTA successfully launched
![Screenshot from 2023-08-01 11-27-24](https://github.com/simarthethi/iiitb-asic/assets/140998783/122a3c8b-8843-422d-a3f3-ccf9c6abc4de)
</details>

<details>
 <summary> ngspice </summary>


 I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:
 ```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
screenshot of ngspice successfully launched

![Screenshot from 2023-08-01 11-29-03](https://github.com/simarthethi/iiitb-asic/assets/140998783/a3cca15a-d8ee-4299-9ea8-8443c02836a4)
</details>

<details>
 <summary> magic </summary>


 Installed magic using the following commands:
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```
screenshot of magic successfully launched
![Screenshot from 2023-08-01 11-28-15](https://github.com/simarthethi/iiitb-asic/assets/140998783/4db4a9e7-6c8e-4e74-a672-0bebaa594885)

![Screenshot from 2023-08-01 11-28-30](https://github.com/simarthethi/iiitb-asic/assets/140998783/9056e4bf-3fd2-4a07-8573-fd258089822e)
</details>


## Day 1

<details>
<summary> Summary </summary>
This section shows how I simulated and synthesized a 2x1 mux using iverilog and yosys respectively. iverilog generates from the RTL design and its testbench a value changing dump file (vcd). gtkwave is the tool used to plot the simulation results of the design. Yosys is a tool which synthesizes RTL designs into a netlist. It is also used to test the synthesized netlist when we provide it with a testbench.

</details>
<details>

<summary> Introduction to RTK design and Synthesis </summary>
**Simulator** : The RTL design is checked for adherence to the spec by simulating the design.
Simulator is the tool used for simulating the design.
** RTL Design **: the RTL Design is the actual verilog code or set of codes which has the intended functionality to meet with the required specifications.
**Testbench**: Testbench is the setup to apply stimulus to the design to check its functionality.

The simulator looks for changes on the input signls. Upon chnages to he input the output is evaluated 

![vsd day_1 simulator](https://github.com/simarthethi/iiitb-asic/assets/140998783/2dcfe72c-25b7-4b2f-8382-0553551bf6b5)

Here **iverilog** is used an open source simulator 
The output of the simulator is a VCD file(Value Change Dump file) which is viewed using **GTKWave** to visualize the waveform

Simulation flow of verilog-
![Screenshot from 2023-08-15 22-45-36](https://github.com/simarthethi/iiitb-asic/assets/140998783/6f142380-b18b-4186-bde1-ccc82de6db1f)
</details>
<details>
<summary> Introduction to Lab </summary>
Under this we will go through how to setup the directory and lab for the course and how to access various files and execute.

**Lab Setup**
The first step under the lab setup is to form a seperate directory for VLSI and gotclone the couse files from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```bash
$ cd vsd
$ cd VLSI
$ cd git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```
Upon the cloning, a new folder with the name sky130RTLDesignAndSynthesisWorkshop is made. 
Under this folder, there will be several folders, such as lib which contains the standard set 
library for sky130 which will be used for the synthesis, verilog_files which contains all the 
source files and testbenches for the experiments to be done.

**Working with iverilog and gtkwave**
Under this, we go over how load files on iverilog and visualise using gtkwave. The terminal is 
opened and the directory is set to the verilog_files, where various source files and their 
respective testbenches are stored. Under this example we will execute the mux using good_mux.v 
and check the functionality using gtkwave to visualise the dumpfile generated. Both the source 
file and testbench are loaded to iverilog.
```bash
$vsd
$ cd VLSI
$ cd sky130RTLDesignAndSynthesisWorkshop
$ cd verilog_files/
$ ls
$ iverilog good_mux.v tb_good_mux.v
$ ./a.out
$ gtkwave tb_good_mux.vcd
```
![vsd day1](https://github.com/simarthethi/iiitb-asic/assets/140998783/ba50c87d-b69c-4cb3-bbf9-e18f3cba145d)
![vsd_day1 libraries](https://github.com/simarthethi/iiitb-asic/assets/140998783/4cf0d6d0-0d06-4f7e-9bdf-a2829e3744ac)
**Waveform on GTKWave**
![vsd day_1 gtk wave](https://github.com/simarthethi/iiitb-asic/assets/140998783/e1c842e3-05f4-4f0f-96cd-e09957e7e9f7)
the waveformon gtkwave is used to check the variations in the output with input.

**MUX code**
To read the code one can use the gvim command and access both the source and testbench
```bash
$ gvim tb_good_mux.v -o good_mux.v
```
**the Source and testbench code**
![Screenshot from 2023-08-13 00-01-25](https://github.com/simarthethi/iiitb-asic/assets/140998783/c50eb689-e502-46ba-b54b-5cc653bea8a0)
</details>
<details>
<summary> introduction to Yosys and Logic synthesis </summary>

The RTL design is the behavioural model of the said specification written in an HDL language. For 
mapping this code to a hardware circuit comes the synthesis. The RTL code is translated to gate 
level using the front end libraries that are .lib files, through synthesis the netlist file is 
derived.

The front end library is also called .lib, which can be explained as a collection for modules for 
the logic gates for the mapping. It contains various types of the same logic gate, such as 2 and 
3 input and gates, and modules for the same gate with different execution speed, which can de 
decided upon the usecase and required specification. The speed of the gates depends the load, 
which for digital circuits are capacitors, thus charging and discharging of capacitors determine 
the speed of the gate, thus the system. For faster speed, we need transistor with more current 
sourcing capacity. Thus the need for wider transistors. But wider transistors enables faster 
processes with the trade off of power and area. Narrow transistors comsumes lesser area and 
power, but comes with bigger delays. Thus the choice of the gate models is made accordingly. The 
time delat should small enough to cover the propogation delay and setup times and at the same
time large enough that it doesn't cause a hold crisis, that is its bigger than the hold time of 
the next gate in process.

One has to guide the synthesizer for the required execution time, ie, the use of faster and slower transistor models while mapping. This is known as constraints.

The synthesizer used under this coursework is Yosys.

Yosys setup flow- 
![Screenshot from 2023-08-15 23-19-06](https://github.com/simarthethi/iiitb-asic/assets/140998783/2c4c6c27-5d4d-4b11-9437-c8543339f9cf)
The design block has the function read_design and .lib has a read_liberty function which reads the design file and .lib 
respectively. The netlist block has the fucntion read_netlist which upon execution generates the netlist file for the 
given design. It is to note design file and netlist file are two different representations for the same given 
specification.

Synthesis verification flow
![Screenshot from 2023-08-15 23-20-39](https://github.com/simarthethi/iiitb-asic/assets/140998783/8371c5eb-7090-4c3a-9e46-d718ae9e3a80)
To verify the synthesis output, we use the iverilog simulator which is given the netlist and testbench as inputs, attain a vcd file, which is visualised using gtkwave. The output on the gtkwave with the netlist file should be the same as in the case of RTL simulation. Since the primary inputs and outputs in case of RTL designs and netlist design remains the same, the same testbench can be used to verify the design.
</details>
<details>
<summary> Lab using and Sky130 PDKs </summary>
Under this section, we go through how to invoke the synthesizer yosys and synthesize the design. For the demonstration, we have taken the synthesis of mux, the good_mux.v file, which we have previously simulated before.

- Step one is to go to the directory for the verilog files and invoke yosys synthesizer.
``` bash
$ cd Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/
$ yosys
```
![Screenshot from 2023-08-15 23-37-45](https://github.com/simarthethi/iiitb-asic/assets/140998783/49e9b91d-13bb-48d7-a31d-151c25a602a6)


- Now we read the .lib using read_liberty and the path is set to the .lib files.
- The behavourial model of mux is read using read_verilog followed by determining the module name to be synthesized.
- The netlist is generated by abc -liberty followed by the path to .lib which specifies what gates are to be linked. Thus the RTL file is converted to netlist.
- The logic being realised can be view using show.
```bash
 read_liberty -lib ~/Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog good_mux.v
 synth -top good_mux
 abc -liberty ~/Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/sky130_fd_sc_hd__tt_025C_1v80.lib
 show
```
![vsd day_1 path to lib](https://github.com/simarthethi/iiitb-asic/assets/140998783/34bae7d2-d759-4270-935e-007539eb13a3)
![Screenshot from 2023-08-13 20-55-19](https://github.com/simarthethi/iiitb-asic/assets/140998783/68eb5bab-cc9b-402d-995e-b80974ed5adc)
![vsd day_1 graphical version of logic](https://github.com/simarthethi/iiitb-asic/assets/140998783/98548ea5-3b96-4576-8a48-e091f3980849)

- The netlist file is wriiten using write_verilog followed by the name for the file.
- Gvim edittor is used view the netlist file.
```bash
read_verilog -noattr good_mux_netlist.v
!gvim good_mux_netlist.v
```
![vsd day_1 netlist diagram](https://github.com/simarthethi/iiitb-asic/assets/140998783/b9617e24-c0f7-47ec-9324-36637d712d64)
</details>

## Day 2
<details>
 <summary> Summary </summary>
 I first synthesized a multiple module (made of two submodules) at the multiple module level 
 (both in hierarchical and flattened forms) then at the submodule level. Synthesis at the 
 submodule level is important for two reasons: 1-) when we have multiple instances of same module 
 (we synthesize once and replicate this netlist multiple times and stitch together the replicas 
 to get the multiple module netlist, and 2-) when we want to divide and conquer (in massive 
 designs) so that the tool can generate a portion by portion of the overall netlist and then we 
 can stitch together the netlist portions to get the multiple module netlist. After that, I 
 sumulated the different flop designs using iverilog and gtkwave, then synthesized the designs. 
 Finally, I synthesized 2 designs that were special; their synthesis used optimizations.
</details>
<details>
 <summary> Introduction to .lib </summary>
Under this section, we get a better insight regarding .lib. We have the general overview that it 
stores the models of all the standards cells, various variations and flavours as per the need of 
specification provided. Getting an insight into the .lib file, we start with the file name -

sky130_fd_sc_hd__tt_025C_1v80  
The name sky130 represemts that the library is based on 130nm technology. Under the nomenclature, we define PVT - process, voltage and temperature. Process refers to the variations due to the fabrication, ie. there will variations in the silicon fabricated even by the same machine. There is variation due to the voltage and temperature as well. Silicon is very sensitive to temperature. All these 3 determines how the silicon is going to perform. We aim to design such that silicon works in all the conditions, across various variations. These three are indicated under the name, tt stands for typical process, 25c indicates the temperature - 25C and 1v80 indicates the voltage of 1.80volts. It is to be noted, all the models under the said library are designed for the given PVT parameters.

We open the .lib file using gvim to go through various other informations it provides.
![vsd day_2 walkthrough of lib sky130](https://github.com/simarthethi/iiitb-asic/assets/140998783/983dccad-65ff-4217-b270-0dcd770c8ac3)

- It defines the technology begin used "CMOS" and the delay model as "table_lookup"
- It defines the units for various parameters and quanities, such as, 1ns for time, 1V for voltage, 1mA for current, 1kohm for resistance and 1pF for capacitance.
- It defines the operating conditions as "tt_025C_1v80".

Considering a two input and gate, and compare different two input and gate.
![vsd day_2 comparison btw and gates](https://github.com/simarthethi/iiitb-asic/assets/140998783/e933cdc5-24ab-4748-a94f-6d314459b441)

- The lib files conatins the power and timing information for the 4 possible outcomes.
- All three taken cells are 2 input and gates, but differ in their areas, and2_4 has a larger area than area2_2 and consequently more than and2_0.
- Having a larger area refers to the use of a wider cell. Wider cells will be faster, but consumes more power. This can be seen in the datials under the lib file.
</details>

<details>
<summary> Heirarchial vs Flat Synthesis </summary>
Under this section, we go over what is heirchial synthesis and flat synthesis. For this, we have taken the case of multiple_modul2s.v from verilog files to have a better unstanding.



```bash
simar-thethi@simar-thethi-Inspiron-3542:~/vsd/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files$ multiple_modules.v
```
![vsd day_2 gvimultiple module](https://github.com/simarthethi/iiitb-asic/assets/140998783/f08a2435-b0d5-4196-9413-42419fb33adf)

Gate level diagram
![Screenshot from 2023-08-16 00-21-41](https://github.com/simarthethi/iiitb-asic/assets/140998783/c2c11d4d-b7a4-4e0d-a920-d16e62f82c12)

We go to the directory where we find the model in verilog files
```bash
$ cd Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
$ yosys
read_liberty -lib ~/Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ~/Documents/ASICs/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
```
**Reading and Synthesis of the said module**
![vsd day_2 multiple module yosys](https://github.com/simarthethi/iiitb-asic/assets/140998783/f689253a-3682-4080-b4aa-06ac8d1436c7)
![vsd day_2 reading verilog file](https://github.com/simarthethi/iiitb-asic/assets/140998783/af199fa9-8b89-413c-8619-191c19e687b1)
![vsd day_2 generate netlist m_m](https://github.com/simarthethi/iiitb-asic/assets/140998783/ce6f9abf-f5e4-493f-ad6d-503905bd9300)

- we hit show and expect to attain a similar schematic we had drew
  ![vsd day_2 show graphical rep of m_m](https://github.com/simarthethi/iiitb-asic/assets/140998783/31a1f607-589b-44f1-b463-b5b793512e67)


- We get the image of the top module.
- We don't get to see the and and or gates. We see the modules u1 and u2, which are the instances of the gates.
- **This type of design is called an heirarchial design.**
- We generate the netlist file for the design.
```bash
write_verilog -noattr multiple_modules_hier.v
!gvim multiple_modules_hier.v  
```
![gvim of m_ hiererchial](https://github.com/simarthethi/iiitb-asic/assets/140998783/017232f1-274d-4a29-b288-aafd55ab7a3c)
![vsd day_2 gvim m_m hiererchial pt2](https://github.com/simarthethi/iiitb-asic/assets/140998783/aff0388c-a5d1-4d54-a903-243277e659fc)

- In the netlist generated, it is observed that the hierarchy is maintained. The top module has instances of sub moduke 1 and 2, and the two modules are seperately defined implementing the and and or gates.
- It is to be more, since this is CMOS technology, we implement the gates using a nand gate with inverted inputs for or gate and nor gate with inverted inputs for and gate.

Now we will look into flat design techcnique.
```bash
write_verilog -noattr multiple_modules_flat.v
!gvim multiple_modules_flat.v
```
![vsd day_2 gvim m_m flattop synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/4f3fb545-0eb5-4a0b-ac0d-a9d595935eaf)
![flattop synthesis pt2](https://github.com/simarthethi/iiitb-asic/assets/140998783/7700a0f5-c504-4388-94b8-9f621a23028a)

- In the new netlist, we don't see any instances of submodules such as u1 and u2.
- We get direct instances of and and or gates under the flat design.
- This type of design is known as flat desigin techniques.

```bash
flatten
show multiple_modules
```
![vsd day_2 show multiple module flat](https://github.com/simarthethi/iiitb-asic/assets/140998783/75a2d5e4-4bce-4b08-adcb-d3e6037e3f76)
We saw how to synthesis the top module, now we will look into synthesis of submodules.
![vsd say_2 show sub_module 1](https://github.com/simarthethi/iiitb-asic/assets/140998783/e7a8c22e-b586-47e0-8e14-e18bf1977fa9)
- We only see submodule 1, we don't get to see the multiple module or submodule 2.

</details>
<details>
<summary> Various Flop coding styles and optimizations </summary>
Under this section, we go through all the various types of flops available and how to design and 
code them efficiently. All the required files are presen in the folder verilog_files.
To understand the need of flops, we refer the example of a simple circuit with delays as 2ns for 
and gate and 1ns for or gate.
![Screenshot from 2023-08-16 01-14-56](https://github.com/simarthethi/iiitb-asic/assets/140998783/823b6384-2b96-4bf6-9f9e-29960f572b73)



