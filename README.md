# iiitb-asic
This github repository contains the progress made in asic 

[Day 0](#day-0)
## Day 0
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

