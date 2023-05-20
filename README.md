
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)
[Day 1](#day-1)

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

<img width="642" alt="yosys-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/01-install-yosys.png">


Below is the screenshot showing sucessful launch:

<img width="568" alt="yosys" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/02-yosys.png"/>

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

<img width="644" alt="OpenSTA-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/03-build-OpenSTA.png">


Below is the screenshot showing sucessful launch:

<img width="570" alt="OpenُSTA" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/04-OpenSTA.png">

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

<img width="641" alt="ngspice-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/05-build-ngspice.png">


Below is the screenshot showing sucessful launch:

<img width="573" alt="ngspice" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/06-ngspice.png">

</details>
 <details>
 <summary> iverilog </summary>


 I installed iverilog using the following command:
  ```bash
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="iverilog-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/07-install-iverilog.png">


 Below is the screenshot showing sucessful launch:
 
 <img width="560" alt="iverilog" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/08-iverilog.png">

</details>
 <details>
 <summary> gtkwave </summary>


 I installed gtkwave using the following command:
  ```bash
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:

<img width="568" alt="gtkwave-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/09-install-gtkwave.png">


Below is the screenshot showing sucessful launch:

<img width="572" alt="gtkwave" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/10-gtkwave.png">

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
 
 <img width="570" alt="magic-installation" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/11-install-magic.png">


Below is the screenshot showing sucessful launch:

<img width="635" alt="magic" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day0/12-magic.png">
</details>

## Day 1

<details>
 <summary> Summary </summary>

This section shows how I simulated and synthesized a 2x1 mux using iverilog and yosys respectively. iverilog generates from the RTL design and its testbench a value changing dump file (vcd). gtkwave is the tool used to plot the simulation results of the design. Yosys is a tool which synthesizes RTL designs into a netlist. It is also used to test the synthesized netlist when we provide it with a testbench.

</details>	
	
<details>
 <summary> Verilog codes </summary>
The verilog codes of the 2x1 mux (good_mux.v) and its testbench (tb_good_mux.v) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>

 <details>
 <summary> Simulation: iverilog and gtkwave </summary>
 
 I used the following commands to simulate and view the plots of the RTL design:
	
 ```bash
 iverilog <name verilog: good_mux.v> <name testbench: tb_good_mux.v>
 ./a.out
 gtkwave tb_good_mux.vcd
 ```
	
 Below is the screenshot of the gtkwave plots:

 <img width="639" alt="Screen Shot 2023-05-09 at 9 21 02 PM" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day1/01.png">

 </details>

<details>
 <summary> Synthesis: Yosys </summary>
	
 In the directory of the verilog files, I used the following commands to synthesize and view the synthesized deisgn:
	
 ```bash
yosys> read_liberty -lib <path to lib file>
yosys> read_verilog <path to verilog file>
yosys> synth -top <top_module_name: good_mux>
yosys> abc -liberty <path to lib file>
yosys> show
 ```
 Below is the screenshot of the synthesized design:
	
	
 <img width="504" alt="Screen Shot 2023-05-09 at 9 56 15 PM" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day1/02.png">

	
 I used the following commands to generate the netlist:
 ```bash
 yosys> write_verilog <file_name: good_mux_net.v>
 yosys> write_verilog -noattr <file_name: good_mux_net.v>
 ```
 
 Below is the screenshot of the generated netlist:
 <img width="636" alt="Screen Shot 2023-05-09 at 10 04 07 PM" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day1/03.png">
 
 </details>
	
