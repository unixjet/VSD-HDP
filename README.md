
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)

## Day 0

I installed the following tools:
 <details>
 <summary> Yosys </summary>


 I installed Yosys using the following commands:
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install
```
Below is the screenshot showing sucessful installation:

<img width="642" alt="yosys-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/01-install-yosys.png">


Below is the screenshot showing sucessful launch:

<img width="568" alt="yosys" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/02-yosys.png"/>

</details>
 <details>
 <summary> OpenSTA </summary>


 I installed and built OpenSTA (including the needed packages) using the following commands:
 ```bash
sudo apt-get install cmake clang gcc tcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
Below is the screenshot showing sucessful installation:

<img width="644" alt="OpenSTA-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/03-build-OpenSTA.png">


Below is the screenshot showing sucessful launch:

<img width="570" alt="OpenُSTA" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/04-OpenSTA.png">

</details>
 <details>
 <summary> ngspice </summary>


 I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:
 ```bash
tar -zxvf ngspice-40.tar.gz
cd ngspice-40
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
Below is the screenshot showing sucessful installation:

<img width="641" alt="ngspice-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/05-build-ngspice.png">


Below is the screenshot showing sucessful launch:

<img width="573" alt="ngspice" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/06-ngspice.png">

</details>
 <details>
 <summary> iverilog </summary>


 I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="iverilog-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/07-install-iverilog.png">


 Below is the screenshot showing sucessful launch:
 
 <img width="560" alt="iverilog" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/08-iverilog.png">

</details>
 <details>
 <summary> gtkwave </summary>


 I installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="gtkwave-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/09-install-gtkwave.png">


Below is the screenshot showing sucessful launch:

<img width="572" alt="gtkwave" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/10-gtkwave.png">

</details>
 <details>
 <summary> magic </summary>


 I installed magic using the following commands:
  ```bash
sudo apt-get install -y m4
sudo apt-get install -y tcsh
sudo apt-get install -y csh
sudo apt-get install -y libx11-dev
sudo apt-get install -y tcl-dev tk-dev
sudo apt-get install -y libcairo2-dev
sudo apt-get install -y mesa-common-dev libglu1-mesa-dev
sudo apt-get install -y libncurses-dev
sudo apt-get install -y magic
 ```
 Below is the screenshot showing sucessful installation:
 
 <img width="570" alt="magic-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/11-install-magic.png">


Below is the screenshot showing sucessful launch:

<img width="635" alt="magic" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/12-magic.png">
</details>
