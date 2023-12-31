# iiitb-asic
This github repository contains the progress made in asic 

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)

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


- Considering the input goes from 0 to 1 for a and b and simultaneously, 1 to 0 for c.
- Ideally for the transition from (001) to (110), the output should have been a constant at 1,
but because of the delay, we get outout as 0 for a brief period of 2ns.
- This is called a glitch.
![Screenshot from 2023-08-16 01-17-36](https://github.com/simarthethi/iiitb-asic/assets/140998783/32a7f827-b33c-4083-9ae7-ed5ddd611cba)

- More the number of combinational circuits, more number of glitches appear, giving a glitchy output.
- To avoid this, we need an element to store the value. Comes the flops into picture.
- We use a D flipflop. They are a storage element. They are placed between combinational circuits and changes value only at clock edge.
![Screenshot from 2023-08-16 01-19-10](https://github.com/simarthethi/iiitb-asic/assets/140998783/6f21888e-78ba-4fb3-a203-feb739b160ac)

- We need to initailise the flops, else the combinational circuits gives a garbage value. For this purpose we have reset and set pins. They can be asynchoronous and synchronous.

Types of flops

- Flops can be designed to be asynchronous or synchronous. It depends on whether the flop is sensitive to the reset and set parameters.
- Under asynchronous, the flop is sensitive to the reset or set, ie the design checks for them and the moment, reset is encountered, the output is pulled to 0 irrespective of the clock. For asynchronous set, the output is pulled to 1.
- The circuit design and timing diagram along with verilog code is displayed under the image below under column 1.
- Under the case of synchronous reset, the output is pulled to 0 at the next clock cycle. The design and timing diagram along the verilog code is shown under the column 2 of the image below.
- Sync reset can be understodd as the input is pulled to 0, thus output becomes 0 for next clock cycle.

![Screenshot from 2023-08-16 01-22-20](https://github.com/simarthethi/iiitb-asic/assets/140998783/770b73ce-325c-42c9-9e86-35995680fd99)

Now, we go through simuations of async reset, async set and sync async reset and observe the waveforms using gtkwave to have a better understand.

**RTL code for dff_asyncres**
```bash
module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
On execution of iverilog and gtkwave we get
![vsd day_2 dff asyncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/63ca8084-3fb8-4bc6-a631-690fd92672d0)
![vsd day_2 gtkwave dff asyncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/00e0eca2-13f9-41eb-9ed1-7604185aa593)
- We can observe that the output q goes to 0 when the reset is encountered.
- Now we synthesis the design using yosys.

![vsd day_2yosys dff asyncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/e8c03f69-9d14-4824-bf0a-535504d8bec8)
![vsd day_2 reading dff ayncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/dd54d587-e4e1-4128-8a79-68370e35b5e2)

**RTL design of dff_async_set**
```bash
module dff_async_set ( input clk ,  input async_set , input d , output reg q );
always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule
```
- upon execution on terminal using iverilog and gtkwave
![vsd day_2 dff async set](https://github.com/simarthethi/iiitb-asic/assets/140998783/fc3ff189-8c67-478a-9ce3-fe12772e468c)
![gtkwave dff async set](https://github.com/simarthethi/iiitb-asic/assets/140998783/2f11ebf4-4daa-4b12-b53f-dd841782cf6d)

- We can observe that the output q goes to 1 as soon as we encounter the set irrespective of that clock. -Now we synthesis the design using yosys.
![vsd day_2 graphical dff  asynset](https://github.com/simarthethi/iiitb-asic/assets/140998783/d64f3b85-e656-4ac1-b58b-a48b000f0274)

**RTL code for dff_syncres**
```bash
module dff_syncres ( input clk ,  input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if(sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
- Upon executing iverilog and gtkwave
![vsd day_2 syncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/988d2164-d386-4cbe-9de9-bf4178a15979)
![gtkwave dff syncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/541ecbfa-0abd-4983-bee4-27ba81108523)
- It is observed that the output q is set to 0 at the next clock pulse when the reset is encountered, thus it is the case of sync reset.
- Now we synthesis the design using yosys.
![vsd day_2 graphical repp dff syncres](https://github.com/simarthethi/iiitb-asic/assets/140998783/b473d2c0-9789-472f-bd15-7e33485c943f)

</details>
<details>
<summary> Interesting Optimisations</summary>
Under this section we look into two interesting cases and how they are executed and designed.

First we look into mul2.v

- Code for mul2.v
```bash
module mul2 (input [2:0] a, output [3:0] y);
	assign y = a * 2;
endmodule
```
- The block diagram and the truth table for the executed logic is shown under.
![Screenshot from 2023-08-16 02-08-26](https://github.com/simarthethi/iiitb-asic/assets/140998783/d9b3bdff-8374-463d-913c-88db7e39d59b)

- From these, we are able to infer that the logic requires the input to be multiplied with 2, and upon checking the output it is the input with 1'b0 padding.
- Thus the design for the logic needs no hardware to be mapped.
- We will confirm this using yosys.
![Screenshot from 2023-08-16 02-11-02](https://github.com/simarthethi/iiitb-asic/assets/140998783/c746b58e-d304-4586-a3a5-6b4b272ac42f)

- From the yosys synthesis, we observe the number of cells in design is 0 and there is no hardware to be mapped. These have been highlighted in the picture above.
- The schematic attained shows a similar result.
- This was done in case of multiplication with 2. For multiplication with 4, we give 2'b00 padding and for 8, we give 3'b000 padding. This goes on.

Now, we look into another special case.

- Condider a 3bit number a[2:0], and the logic to be implemented is that the output y[5:0] is equal to 9 times of a[2:0].
- Code for execution
```bash
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule
```
- explanation
![Screenshot from 2023-08-16 02-13-28](https://github.com/simarthethi/iiitb-asic/assets/140998783/df14eb46-1a54-4e03-a098-54ce543cf23e)

- Multiplcation with 9 can be seen as multiplication with 8 and plus 1.
- We know multiplication with 8 is equal to 3'b000 padding, and adding the same 3 bit number to the padded number comes of as concatanation of {a,a}.
- Thus there are no standard cell required for the design. We verify this using yosys.
![Screenshot from 2023-08-16 02-15-45](https://github.com/simarthethi/iiitb-asic/assets/140998783/20c612e7-3e59-4b14-9931-2d1810ede082)

- We see that there are no standard cells required.
- We see the concatanation operation done in the netlist.
</details>

## Day 3
<details>
<summary> Summary </summary>
I have synthesized designs with optimizations. Combinational logic optimizations include 1-) 
constant propagation (when the combination is just propagating a constant) and 2-) boolean logic 
optimization (when boolean rules are used to simplify the expression). Sequential logic 
optimizations include 1-) sequential constant propagation (when constant is propagated with clock 
involved), 2-) state optimization (when unused states are optimized), 3-) retiming (when logic is 
split to decrease timing of the different logic portions and increase frequency), and 4-) 
sequential logic cloning (when physical aware synthesis is done to optimize the floop plan)
</details>
<details>
<summary> Introduction to Optimizations </summary>
Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient. This is achieved by the synthesis tool using various techniques and gives us the most optimized circuit.

**Techniques for optimization for combinational logic**:

- Constant propagation which is Direct optimizxation technique
- Boolean logic optimization using K-map or Quine McKluskey

Here is an example for **Constant Propagation**
![Screenshot from 2023-08-16 02-25-21](https://github.com/simarthethi/iiitb-asic/assets/140998783/ab9cedb8-4671-4beb-a244-0cbe24c3f7db)
In the above example, if we considor the trasnsistor level circuit of output Y, it has 6 MOS trasistors and when it comes to invertor, only 2 transistors will be sufficient. This is achieved by making A as contstant and propagating the same to output.
**Techniquies for Sequentional logic otimizations**
Below are the various techniques used for sequential logic optimisations:
- Basic
   Sequential contant propagation
- Advanced
   State optimisation
   Retiming
   Sequential Logic Cloning (Floor Plan Aware Synthesis)

-  The input of D ff is grounded, ir d=0, and the reset parameter is given. Here even if the
  reset is given or not the output output of the flop is constant at 0, hence the overall outcome
  is constant.
   ![Screenshot from 2023-08-16 03-38-37](https://github.com/simarthethi/iiitb-asic/assets/140998783/ae8fb30a-17b9-4ab9-9a64-0a96a03283bc)
- Now taking the same circuit, but instead of reset, we give set. Now when the set is 1, the flop
output follows set. As soon as set is removed, the output goes to 0 at the next positive clock
edge. Thus now we can't remove the flop from design, Thus we retain the flop.
![Screenshot from 2023-08-16 03-41-14](https://github.com/simarthethi/iiitb-asic/assets/140998783/a95b3c4d-6e08-4362-a4e4-7cd7fa167e01)
**Advanced Methods for Sequential logic Optimisation**

- State optimization in ASIC design is about finding the best trade-offs among performance, power
efficiency, area utilization, and other design objectives to create an effective and efficient
custom integrated circuit for a particular application.
- Re-timing is the technique used to optimize the timing performance of a digital circuit by
moving registers (flip-flops) to different locations within the circuit without changing its
functionality. The primary goal of retiming is to improve the critical path delay, which is the
longest path through the logic circuit that determines the maximum operating frequency.
- Sequential logic cloning or flip-flop cloning or state machine cloning is the technique used to
replicate or duplicate certain portions of sequential logic circuits. This technique is employed
to improve performance, reduce critical path delays, or optimize power consumption in a design
without altering its functional behavior.



</details>
<details>
<summary> Combinational logic optimizations </summary>

Let's consider an example concurrent statement assign **y=a?(b?c:(c?a:0)):(!c)**

The above expression is using a ternary operator which realizes a series of multiplexers, however, when we write the boolean expression at outputs of each mux and simplify them further using boolean reduction techniques, the outout y turns out be just **~(a^c)**

Command to optimize the circuit by yosys is
```bash
yosys> opt_clean -purge
```
opt_clean remove unused cells and wires. The -purge switch removes internal nets if they have a 
public name. This command identifies wires and cells that are unused and removes them. This 
command can be used to clean up after the commands that do the actual work.



In case of multiple models, it is important to flatten the design then followup with 
optimization.

**Lab 1-opt_check.v**
**RTL code**
```bash
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```
- after synthesis on yosys
![vsd day_3 opt_check graphical rep](https://github.com/simarthethi/iiitb-asic/assets/140998783/e183fdc0-3fea-40e3-ac35-2d4f7102d49e)

**Lab_2 opt_check2.v**
**RTL code**
```bash
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```
- Hardware after synthesis on yosys
![vsd day_3 opt_check2 graphical re](https://github.com/simarthethi/iiitb-asic/assets/140998783/25d4ad53-b091-4e73-a021-0710b05f49c2)

**Lab_3 opt_check3.v**
**RTL code**
```bash
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```
- hardware after synthesis on yosys
![vsd day_3 pot_check3 graphical_rep](https://github.com/simarthethi/iiitb-asic/assets/140998783/ced19225-4aba-4b54-b8b8-aa20aa73f2f6)

**Lab_4 opt_check4.v**
**RTL code**
```bash
module opt_check4 (input a , input b , input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
 endmodule
```
- Hardware  after synthesis on yosys
![vsd day_3 optcheck4](https://github.com/simarthethi/iiitb-asic/assets/140998783/4c160fee-16f7-4caa-abe3-ba6365af6e3c)
**Lab_5 multiple_module_opt.v
**RTL code**
```bash
module sub_module1(input a , input b , output y);
 assign y = a & b;
endmodule


module sub_module2(input a , input b , output y);
 assign y = a^b;
endmodule


module multiple_module_opt(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
sub_module2 U3 (.a(b), .b(d) , .y(n3));

assign y = c | (b & n1); 


endmodule
```
- Hardware after synthesis on yosys
![multiple module opt](https://github.com/simarthethi/iiitb-asic/assets/140998783/e9973120-4219-459f-bb08-12173655c4ec)
**Lab_6 multiple_modules_opt2.v**
**RTL code**
```bash
 module sub_module(input a , input b , output y);
 assign y = a & b;
endmodule



module multiple_module_opt2(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
sub_module U2 (.a(b), .b(c) , .y(n2));
sub_module U3 (.a(n2), .b(d) , .y(n3));
sub_module U4 (.a(n3), .b(n1) , .y(y));


endmodule
```
- Hardware after yosys synthesis
![multiple module opt2](https://github.com/simarthethi/iiitb-asic/assets/140998783/e5acbb37-713d-43b2-a533-35605cc4bcf2)
</details>

<details>
<summary> Sequentional Logic Optimizations </summary>

**Lab_1 dff_const1.v**
**RTL code**
```bash
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end

endmodule
```
- Simulation on iverilog and gtkwave
![vsd day_3 dff const1 gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/0c34fb67-1edc-499f-a9f3-254c67ee0c22)
- optimization using yosys
![vsd day_3 dff const optimized ckt](https://github.com/simarthethi/iiitb-asic/assets/140998783/1f70cea5-cf81-47db-b429-f56f5ce9db23)

**Lab_2 dff_const2.v**
**RTL code**
```bash
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end

endmodule
```
- Simulation using iverilog and yosys
![vsd day_3 dff const2 gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/a3e79097-aab1-4e1a-b36e-cee7ab287d04)
- optimization using yosys
![vsd_day3 dff const2 optimized](https://github.com/simarthethi/iiitb-asic/assets/140998783/61312886-25c4-4840-9181-ff5e2d14516a)

**Lab_3 dff_const3.v**
**RTL code**
```bash
module dff_const2(input clk, input reset, output reg q);
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
-simaulation using iverilog and gtkwave
![vsd day_3 dff const3 gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/0929ca11-3c57-4b02-81fe-7c852c639f36)
-optimization using yosys
![vsd day_3 dff const3 optimized](https://github.com/simarthethi/iiitb-asic/assets/140998783/7f4abd61-ba2a-4c14-bc6a-237cfaff5c74)

**Lab_4 dff_const4.v**
**RTL code**
```bash
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
-Simulation using iverilog and gtkwave
![vsd day_3 dff const4 gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/a7cf35e9-8991-4f3d-9086-c77e7b44a12c)
-optimization using yosys
![vsd day_3 dff const4 optimized](https://github.com/simarthethi/iiitb-asic/assets/140998783/d9f5472b-57ae-47d6-9c11-ade0bced8a5d)

**Lab_5 dff_const5.v**
**RTL code**
```bash

module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b0;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
-simulation using iverilog and gtkwave
![vsd day_3 dff const5 gtkwve](https://github.com/simarthethi/iiitb-asic/assets/140998783/1aed74f1-3d7b-4a4f-9015-04132931a247)

-optimization using yosys
![vsd day_3 dff const5 optimized](https://github.com/simarthethi/iiitb-asic/assets/140998783/5f300a0e-6cd2-44b5-8cd1-d325cec47001)
</details>

<details>
<summary> Sequential optimizations for unused outputs </summary>
Under this section, we look into how yosys synthesizer optimises the design in case of unused 
bits in the output. For this we have taken a 3 bit counter. In case 1, only the LSB is taken as 
final output, thus the first two are left unused. In case two, we take the entire 3 bits as 
output.
	
![Screenshot from 2023-08-16 04-06-54](https://github.com/simarthethi/iiitb-asic/assets/140998783/eedb31eb-4f6e-4410-b2e3-451949e77d43)
**Lab_1 using count[0]**
**RTL code**
```bash
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
-synthesis using yosys
![vsd day_3synthesis counter_opt](https://github.com/simarthethi/iiitb-asic/assets/140998783/4fe0b2f0-cf01-4021-bcbd-4d0da528d393)
![vsd day_3 counter opt rep](https://github.com/simarthethi/iiitb-asic/assets/140998783/dd3a6bdf-be61-4155-9974-fc74b8c9a107)

**Lab_2 using all three bits count[2] and count[1] and count[0]
**RTL code**
```bash
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[2:0] == 3'b100;

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end
```
- synthesis using yosys
![vsd day_3 counter_opt2](https://github.com/simarthethi/iiitb-asic/assets/140998783/4e5ce863-ebb2-415a-95ed-7138ede79eca)
![counter opt2 plot](https://github.com/simarthethi/iiitb-asic/assets/140998783/5b922011-1080-4f1e-ae08-e2903129ee52)
- In the yosys generation, we see the design has encorporated 3 dff for the 3 bit counter.
- It is evident that the yosys synthesizer optimizes for the unsed bits in the output. This so important as illustrated because it saves a ton of space, and speed, and improves efficiency of the final design.
 </details> 

## Day 4
<details>
<summary> Summary </summary>
performed Gate Level Simulation (GLS). GLS is when the testbench is run with the netlist as 
design under test to ensure there are no synthesis and simulation mismatches, and it is important 
as it 1-) verifies the logical correctness of the post-synthesis design and 2-) ensures the 
timing of design is met. Synthesis and simulation mismatches can happen due to a lot of reasons 
including missing sensitivity list (some signal changes are not captured by the circuit because 
they are missing from the sensitivity list), blocking vs non-blocking assignments (inside an 
always block, "=" statements inside it are blocking meaning they are executed in order they are 
written, assignments (<=) on the other hand are non-blocking so they are executed in parallel => 
non-blocking should be used with sequential circuits. Note that the synthesis will yield same 
circuit with blocking and non-blockin; it will yield what would be obtained as if the statements 
where written in non-blocking format, so in case they weren't written as such a mismatch will 
occur with the simulation), and non-standard verilog coding.
</details>

<details>
<summary> GLS, Synthesis-Simulation mismatch and Blocking,Non-blocking statements </summary>
**GLS concepts and flow**
What is GLS-Gate Level Simulation?
GLS is generating the simulation output by running test bench with netlist file generated from 
synthesis as design under test. Netlist is logically same as RTL code, therefore, same test bench 
can be used for it.

Why GLS?
We perform this to verify logical correctness of the design after synthesizing it. Also ensuring 
the timing of the design is met.

Below picture gives an insight of the procedure. Here while using iverilog, we also include gate 
level verilog models to generate GLS simulation.
![Screenshot from 2023-08-16 10-10-17](https://github.com/simarthethi/iiitb-asic/assets/140998783/f3254e33-17b1-4e83-9564-9f490256d985)

**Synthesis Simulation Mismatch**
There are three main reasons for Synthesis Simulation Mismatch:
      -Missing sensitivity lis in always block
      -blocking vs non-blocking assignments
      -Non standard verilog coding
*Missing Sensitivity List*
To understand this we use examples for a mux with different sensitivity

-Code 1
```bash
module mux1 (input sel , i0, i1 ,
output reg y);

always@(sel)
begin
if(sel)
	y=i1;
else
	y=i0;
end

endmodule
```
-Code 2
```bash
module mux (input sel , i0, i1 ,
output reg y);

always@(*) 
begin
if(sel)
	y=i1;
else
	y=i0;
end

endmodule
```
- Mux 1 is sensitive to changes is changes in latches, ie the output y will change only at the changes of sel. Thus the changes of inputs i1 and i0 are not displayed in the output.
- Mux 2 is sensitive to all three, so when high sel, output covers all changes in i1, and for low sel, all changes in i0 are covered.
- Now, the simulation and synthesis of mux 2 wont have any mismatch.
- But mux1 will have mismatch,as simulators work on sensitivity list and the simulation will behave as a double edge triggered latch, while the synthesizer converts the logic into netlist and doesn't look into sensitivity list, thus synthesis will behave as a 2 input MUX.

*Blocking and Non-blocking statements*
Blocking statements execute the statemetns in the order they are written inside the always block. 
Non-Blocking statements execute all the RHS and once always block is entered, the values are 
assigned to LHS. This will give mismatch as sometimes, improper use of blocking statements can 
create latches.
</details>
<details>
<summary> Lab- GLS Synth Simulation Mismatch </summary>

**Lab_1 ternary_operator_mux.v**
**RTL code**
```bash
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule
```
- Simulation using iverilog and yosys
![vsd day_4 ternary opt mux gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/5fea5a54-8d17-4474-bba5-80814a15f877)
- now we synthesis using yosys
![vsd day_4 ternary opt mux rep](https://github.com/simarthethi/iiitb-asic/assets/140998783/36e4b12e-bf63-4fe9-b320-8557d3290f3a)
- generated netlist
![ternary opt mux netlist](https://github.com/simarthethi/iiitb-asic/assets/140998783/6302ab44-d863-4b35-a82c-30836382b975)
-Running GLS using the netlist file generated during yosys
![vsd day_4 ternary opt mux gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/751550ac-e06f-4154-82d9-7952c37582b2)
**it is clear that both simulatons are same**

**Lab_2 bad_mux.v**
**RTL code**
```bash

module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
- Simulation using iverilog and gtkwave
![vsd day_4 bad mux gtkwave before synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/b4e41291-3f57-491b-9b28-b63bddea772e)
- synthesis using Yosys
![vsd day_4 bad mux synthesis graphical rep](https://github.com/simarthethi/iiitb-asic/assets/140998783/773e30b0-6a3d-4af9-b610-ee91e184caac)
- netlist generated during synthesis
![bad mux netlist](https://github.com/simarthethi/iiitb-asic/assets/140998783/ac877677-9d5c-4206-8636-902a6a9e41b7)
- Running GLS using netlist file generated during yosys
![vsd day_4 bad_mux gtkwave after synthesis ](https://github.com/simarthethi/iiitb-asic/assets/140998783/2c19cc52-e422-46cd-8683-f7d9ab7b29f2)
- Under this, we see a clear mismatch between the simulation and synthesis designs. The RTL file
and netlist files aren't the same logic implemention. This happened due to the sensitivity
listing under the RTL file.
</details>
<details>
<summary> Lab on Synthesis_Simulation Mismatch and Blocking </summary>
In thissection we willlook into the mismatch between simulation and synthesis caused due to the blocking statements.
	
**RTL code**
```bash
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule
```
- Running the simulation using iverilog and gtkwave
![vsdday_4 caveat gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/64c9b28b-0f3e-4cf8-b142-9fa03b31f12f)
- Synthesis using yosys
![vsd day_4 blocking caveat graph repo](https://github.com/simarthethi/iiitb-asic/assets/140998783/c700acb8-26bb-41e8-8aa2-f0f0ac8da629)
- Netlist generated
![blocking caveat netlist](https://github.com/simarthethi/iiitb-asic/assets/140998783/d0f5a262-35f1-40ff-8fa6-e0e077ccff7f)
- Running GLS on the netlist file generated using iverilog and gtkwave
![gtkwaave blocking caveat after synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/ebcf9efc-9385-4077-9666-4ea88154c07d)
  
- It is seen that the waveform matches with the expected output for d=((a|b).c).
- There is clear mismatch between the simulation and synthesis in this case. This happended coz
we used blocking statements, and while simulation, the design makes a flop, which wasn't the
intention of the original design.
</details>

## Day 5

<details>
<summary> Summary </summary>
I have first learned about "if" and "case" statements which are used inside always blocks.
</details>
<details>
<summary> If and Case constructs </summary>
	
***if costruct***
The construct *if* is mainly used to create priority logic. In a nested if else construct, the 
conditions are given priority from top to bottom. Only if the condition is satisfied, if 
statement is executed and the compiler comes out of the block. If condition fails, it checks for 
next condition and so on as shown below.
**Syntax for nested if else**
```bash
if (<condition 1>)
begin
-----------
-----------
end
else if (<condition 2>)
begin
-----------
-----------
end
else if (<condition 3>)
.
.
.
```
**Dangers of *if* construct**
If use a bad coding style i.e, using incomplete if else constructs will infer a latch. We 
definetly don't require an unwanted latch in a combinational circuit. When an incomplete 
construct is used, if all the conditions are failed, the input is latched to the output and 
hence we don't get desired output unless we need a latch.
![IMG_20230816_111616](https://github.com/simarthethi/iiitb-asic/assets/140998783/ddf54009-3560-4056-bfd5-7810b133108f)

***Case construct***
**syntax**
```bash
case(statement)
  case1: begin
       --------
	 --------
	 end
 case2: begin
	     --------
	 --------
	 end
 default:
 endcase
```
In case construct, the execution checks for all the case statements and whichever satisfies the 
statement, that particular statement is executed.If there is no match, the default statement is 
executed. But here unlike if construct, the execution doesn't stop once statement is satisfied, 
but it continues further.

**Caveats in Case**
Caveats in case occur due to two reasons. One is **incomplete case statements** and the other is **partial assignments in case statements**.
</details>
<details>
<summary> Lab on Incomplete *if*</summary>

**LAB_1 incomp_if**
**RTL code for incom_if.v**
```bash
module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule
```
- simulation using iverilog and gtkwave
![vsd day_5 incom_if gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/29b90c22-cb5c-4c8c-ac67-238c29b7cd41)
- synthesis using yosys
![vsd day_5 incomp_if synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/e1a4e220-8620-4c00-8253-378ede40af1f)
- It is seen that there has been an inferred latch formation due to incomplete if-else
condtional statements.

**LAB_2 incomp_if2**
**RTL code for incomp_if2.v**
```bash

module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
	else if (i2)
		y <= i3;

end
endmodule
```
- Simulation using iverilog and gtkwave
![vsd day_5 incom_if2 gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/56f51005-8fd8-448c-b778-42f25d9311bb)
- Synthesis using yosys
![vsd day_5 incomp_if2 synth](https://github.com/simarthethi/iiitb-asic/assets/140998783/c7a0c01a-2003-4ee4-8f7d-9dce2a6d75b2)
![vsd day_5 incomp_if2 show](https://github.com/simarthethi/iiitb-asic/assets/140998783/ce48e310-2d87-4e94-9130-ce6556610663)
- It is seen that there has been an inferred latch formation due to incomplete if-else
condtional statements.

</details>
<details>
<summary> LAB on **case** construst </summary>
Here we'll look into various situations with case statement under simulation and synthesis

**LAB_1 wihout default**
We look into the formation of inffered latcg due toomission of default case.

**RTL code for incomp_case.v**
```bash
module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
end
endmodule
```
- Running RTL simulation using iverilog and gtkwave
![vsd day_5 incom_case simulation](https://github.com/simarthethi/iiitb-asic/assets/140998783/5b311344-175a-4d74-b750-d5ebe71f1b3c)
- synthesis using yosys
![vsd day_5 synthesis incomp_case](https://github.com/simarthethi/iiitb-asic/assets/140998783/723ff490-8f67-4207-a24a-cdabb8302e80)
![vsd day_5 incomp case show](https://github.com/simarthethi/iiitb-asic/assets/140998783/fb4ced45-ffc8-46fa-9684-199b146925f8)
- It is seen due to omission of default case we have an inferred latch in hardware design

  **LAB_2 with default**
  We'll look into how default cae removes the frmation of a latch

  **RTL code for comp_case.v**
  ```bash
  module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
  always @ (*)
  begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
		default : y = i2;
	endcase
  end
  endmodule
  ```
- Running simulation using verilog and gtkwave
![vsd day_5 comp_case gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/4bd1f25f-76ad-4a5a-8263-a0021e5a3311)
- running synthesis using yosys
![vsd day_5 comp_case synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/559201e0-6067-4c47-85fe-9c1fc0c15a33)
![vs day_5 comp_case show](https://github.com/simarthethi/iiitb-asic/assets/140998783/f20a705b-3b9c-42ac-b5b9-1dd5a14a694b)
- here we see no inferred latch

**LAB_3 partial case assignment**
we look into how partial case assignments cause the formation of inferred latch.

**RTL code for partial _case_assign.v**
```bash
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
			end
		2'b01 : y = i1;
		default : begin
		           x = i1;
			   y = i2;
			  end
	endcase
end
endmodule
```
- Running simulation using iverilog and gtkwave
![Screenshot from 2023-08-16 19-25-50](https://github.com/simarthethi/iiitb-asic/assets/140998783/deae3245-013e-4612-bb61-cbee4554b29d)
- Synthesis using yosys
![partial case assign synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/5e479854-53ba-431f-ab1f-55ffffc5c2be)
![partial case assign show](https://github.com/simarthethi/iiitb-asic/assets/140998783/9b0c4465-b497-4b9a-a768-30802fc5937d)
- Its is noticed that we have a latch in the design of the hardware even when we didn't had one in RTL file. This is due to the partial case assignment.

**LAB_4 the bad Case**
Under this, we look into the case of a bad case, which has simulation synthesis mismatch due to 
the improper assignment for case 1'b1?. This leads to formation of inferred latches.

**RTL code for bad_case.v**
```bash
module bad_case (input i0 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
always @(*)
begin
	case(sel)
		2'b00: y = i0;
		2'b01: y = i1;
		2'b10: y = i2;
		2'b1?: y = i3;
		//2'b11: y = i3;
	endcase
end

endmodule￼
```
- Simulation using iverilog and gtkwave
![vsd day_5 bad case gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/dc006af1-1880-4887-811f-a84f9525ac46)
- Synthesis using yosys
![vsd day_5 bad_case synth](https://github.com/simarthethi/iiitb-asic/assets/140998783/7bb2c7a2-7282-4df0-ab47-de2f79bf2210)
- Running GLS using iverilog and gtkwave fromnetlist obtained under synthesis
![bad case post synthesis gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/e1c51e15-e2fa-45ee-a594-6accce683124)
- We can see the mismatching under GLS and RTL simulation. This is due to improper assignment and formation of latches which weren't a part of the intended logic design.
</details>

<details>
<summary> for loop and for generate </summary>
	
**For Loop**

- For look is used in always block
- It is used for excecuting expressions alone

**Generate For loop**

- Generate for loop is used for instantaing hardware
- It should be used only outside always block

For loop can be used to generate larger circuits like 256:1 multiplexer or 1-256 demultiplexer 
where the coding style of smaller mux is not feesible and can have human errors since we would 
need to include huge number of combinations.

FOR Generate can be used to instantiate any number of sub modules with in a top module. For 
example, if we need a 32 bit ripple carry adder, instead of instantiating 32 full adders, we can 
write a generate for loop and connect the full adders appropriately.
</details>

<details>
<summary> LAB on **for** and **for generate** </summary>

**LAB_1 mux using Generate**

- Under this, we implement a mux using for loop.
- Advantage of this method over if-case method is that we don't have to write multiple lines.
- For a 64 input mux, using if-case we need over 64 lines of code, whereas the same can be done under 5-6 lines using for loop.
**RTL code for mux_generate.v**
```bash
module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
wire [3:0] i_int;
assign i_int = {i3,i2,i1,i0};
integer k;
always @ (*)
begin
for(k = 0; k < 4; k=k+1) begin
	if(k == sel)
		y = i_int[k];
end
end
endmodule
```
- Running RTL simulation using and gtkwave
![vsd day_5 mu_generate gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/953a29a1-ada4-4f8e-b1e0-6fce9ac82153)
- Synthesis using yosys
![vsd day_5 mux generate synthesis](https://github.com/simarthethi/iiitb-asic/assets/140998783/c12a66fe-5b0e-45e0-8033-7a8b40678902)
![mux_generate show](https://github.com/simarthethi/iiitb-asic/assets/140998783/54bf882d-10e7-4921-abc0-82109db6334e)
- Running GLS using iverilog and gtkwave after generationg netlist using yosys
![post synthesis mux geneate gtkwvae](https://github.com/simarthethi/iiitb-asic/assets/140998783/00cbfb0b-a7b8-43ef-b4cb-e0978de213f5)
- It is observed that both the RTL simulation and GLS have same output waveform. Thus we have
the correct design.

**LAB_2 demux using generate**
Under this, We follow up with the implementation of demux

**RTL code for demux_generate.v**
```bash
module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
for(k = 0; k < 8; k++) begin
	if(k == sel)
		y_int[k] = i;
end
end
endmodule
```
- Simulation using iverilog and gtkwave
![demux gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/e00d4fa3-60a2-40ec-8399-f2a18d88fab2)
- Syntheis using yosys
![demux synthesis show](https://github.com/simarthethi/iiitb-asic/assets/140998783/681d567a-223a-4422-b01b-af002420f0a9)
- Running GLS using iverilog and gtkwave after generating netlist on yosys
![demux gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/3a9e32c9-1915-41fd-8543-c152d73797dd)
- We see that both the waveforms for GLS and RTL simulation are the same. Thus we have the correct logic implementataion for demux.

**LAB_3 ripple carry adder**

- Under this, we look into implementation of an 8 bit ripple carry adder.
- In this we need 8 single bit adders, that is instantiate single bit full adder 8 times. We implement generate for for making this into a simple and shorter code.

**RTL code for rca.v**
```bash
module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
wire [7:0] int_sum;
wire [7:0]int_co;

genvar i;
generate
	for (i = 1 ; i < 8; i=i+1) begin
		fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
	end

endgenerate
fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule
```
- RTL simulation using iverilog and gtkwave
![vsd day_5  rca gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/711cda0d-1c87-428f-9892-c7ca8cc9fc30)
- synthesis using yosys and rca grahical representaion
![vsd day_5 rca show](https://github.com/simarthethi/iiitb-asic/assets/140998783/34511043-9e31-4a5f-9ba2-aa1a90c8950f)
- show fa
![vsdday_5 fa show](https://github.com/simarthethi/iiitb-asic/assets/140998783/377bb07e-15b4-4e1b-b69f-914363061a06)
- Running GLS using iverilog and gtkwave after generating a netlist using yosys
![vsd day_rca post synthesis gtkwave](https://github.com/simarthethi/iiitb-asic/assets/140998783/5e8ebbfd-aa3b-4b07-95bc-f4b50ef4a090)
- We see the same simulation and GLS waveform, thus the ripple carry adder logic is correct and
has been correctly synthesizer. The advantage of using generate for is that we have to
instantiate once and the code multiple copies, ie multiple instances as defined.
</details>
