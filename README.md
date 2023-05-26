
# VSD-HDP

This github repository summarizes the progress made in the VSD-HDP tapeout program. Quick links:

[Day 0](#day-0)

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

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
	
## Day 2

<details>
 <summary> Summary </summary>

I first synthesized a multiple module (made of two submodules) at the multiple module level (both in hierarchical and flattened forms) then at the submodule level. Synthesis at the submodule level is important for two reasons: 1-) when we have multiple instances of same module (we synthesize once and replicate this netlist multiple times and stitch together the replicas to get the multiple module netlist, and 2-) when we want to divide and conquer (in massive designs) so that the tool can generate a portion by portion of the overall netlist and then we can stitch together the netlist portions to get the multiple module netlist.
After that, I sumulated the different flop designs using iverilog and gtkwave, then synthesized the designs.
Finally, I synthesized 2 designs that were special; their synthesis used optimizations.

</details>	
	
<details>
 <summary> Verilog codes </summary>
The verilog codes of the multiple module (multiple_modules.v), the D-flipflop with asynchronous reset (dff_asyncres.v), the D-flipflop with asynchronous set (dff_async_set.v), the D-flipflop with synchronous reset (dff_syncres.v), their respective testbenches (tb_*), mult_2.v and mult_8.v are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>
	
<details>
 <summary> Synthesis: multiple_modules level </summary>
		
I used the following commands to synthesize and view the design of the hierarchical multiple module:
		
```bash		
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_modules.v>
yosys> synth -top <name: multiple_modules>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: multiple_modules>
yosys> write_verilog -noattr <name: multiple_modules_hier.v>
```
Below is the screenshot of the generated hierarchical design:
		
<img width="530" alt="hier" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/01.png">
	
Below is the screenshot of the generated hierarchical netlist:
		
<img width="645" alt="hiernetlist" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/02.png">

I used the following additional commands to synthesize and view the design of the flattened multiple module:
		
```bash
yosys> flatten
yosys> write_verilog -noattr <name: multiple_modules_flat.v>
```	
Below is the screenshot of the generated flattened design:
		
<img width="574" alt="flatten" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/05.png">

Below is the screenshot of the generated flattened netlist:
		
<img width="645" alt="flattennetlist" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/04.png">

</details>
<details>
 <summary> Synthesis: sub_module1 level </summary>
		
I used the following commands to view the synthesized design of the submodule:
		
```bash		
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_modules.v>
yosys> synth -top <name: sub_module1>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: sub_module1>
```
	
Below is the screenshot of the generated design:
		
<img width="418" alt="synth_submodule1" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/06.png">
		
</details>
<details>
<summary> Simulation: dff with asynchronous reset </summary>

I used the following commands to simulate the RTL design of the dff with asynchronous reset:
	
```bash	
iverilog <name verilog: dff_asyncres.v> <name testbench: tb_dff_asyncres.v>
./a.out
gtkwave <name vcd file: tb_dff_asyncres.vcd>
```	
	
Below is the screenshot of the simulation:
	
<img width="466" alt="asyncres" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/07.png">
	
</details>
<details>
<summary> Simulation: dff with asynchronous set </summary>
I used the following commands to simulate the RTL design of the dff with asynchronous set:
	
```bash	
iverilog <name verilog: dff_async_set.v> <name testbench: tb_dff_async_set.v>
./a.out
gtkwave <name vcd file: tb_dff_async_set.vcd>
```
	
Below is the screenshot of the simulation:
	
<img width="489" alt="asyncset" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/08.png">

</details>
<details>
<summary> Simulation: dff with synchronous reset </summary>
	
I used the following commands to simulate the RTL design of the dff with synchronous reset:
	
```bash	
iverilog <name verilog: dff_syncres.v> <name testbench: tb_dff_syncres.v>
./a.out
gtkwave <name vcd file: tb_dff_syncres.vcd>
```	
	
Below is the screenshot of the simulation:
	
<img width="476" alt="syncres" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/09.png">

</details>
<details>
 <summary> Synthesis: dff with asynchronous reset </summary>

I used the following commands to synthesize the design:
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_asyncres.v>
yosys> synth -top <name: dff_asyncres>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_asyncres>
```
Below is the screenshot of the synthesized design:
	
<img width="415" alt="asyncressynth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/10.png">
	
</details>
<details>
 <summary> Synthesis: dff with asynchronous set </summary>

I used the following commands to synthesize the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_async_set.v>
yosys> synth -top <name: dff_async_set>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_async_set>
```
Below is the screenshot of the synthesized design:
	
<img width="415" alt="asyncsetsynth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/11.png">
	
</details>
<details>
 <summary> Synthesis: dff with synchronous reset </summary>
	
I used the following commands to synthesize the design:
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_syncres.v>
yosys> synth -top <name: dff_syncres>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: dff_syncres>
```
Below is the screenshot of the synthesized design:
	
<img width="418" alt="syncressynth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/12.png">

</details>
<details>
 <summary> Synthesis: mult_2.v </summary>
	
I used the following commands to synthesize and view the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mult_2.v>
yosys> synth -top <name: mul2>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: mul2>
yosys> write_verilog -noattr <name: mul2_net.v>
```
	
Below is the screenshot of the synthesized design, note that no hardware was used (no cells are synthesised) as multiplying a 3-bit input by a power of two is equivalent to shifting for output:
	
<img width="453" alt="mul2" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/13.png">
	
Below is the screenshot of the netlist:
	
<img width="636" alt="mul2_net" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/14.png">
	

</details>
<details>
 <summary> Synthesis: mult_8.v </summary>
	
I used the following commands to synthesize and view the design:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: mult_8.v>
yosys> synth -top <name: mult8>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show <name: mult8>
yosys> write_verilog -noattr <name: mult8_net.v>
```
	
Below is the screenshot of the synthesized design, note that no hardware was used (no cells are synthesised) as multiplying a 3-bit input (special case) by a nine is equivalent to replicating the input twice for output:
	
<img width="414" alt="mult8" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/15.png">
	
Below is the screenshot of the netlist:
	
<img width="645" alt="mult8_net" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day2/16.png">


</details>
	
## Day 3
	
<details>
 <summary> Summary </summary>

I have synthesized designs with optimizations. Combinational logic optimizations include 1-) constant propagation (when the combination is just propagating a constant) and 2-) boolean logic optimization (when boolean rules are used to simplify the expression). Sequential logic optimizations include 1-) sequential constant propagation (when constant is propagated with clock involved), 2-) state optimization (when unused states are optimized), 3-) retiming (when logic is split to decrease timing of the different logic portions and increase frequency), and 4-) sequential logic cloning (when physical aware synthesis is done to optimize the floop plan)

</details>	
	
<details>
 <summary> Verilog codes </summary>

The verilog codes used (opt_*, dff_const*, tb_dff_const*, and counter_opt*) are taken from https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check.v </summary>
I used the below commands to view the synthesized design of opt_check.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check.v>
yosys> synth -top <name: opt_check>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 2-input and gate is realized as was expected when optimizations are applied:
	
<img width="676" alt="opt_check" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/01.png">

</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check2.v </summary>
	I used the below commands to view the synthesized design of opt_check2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check2.v>
yosys> synth -top <name: opt_check2>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
Below is the screenshot of the obtained optimized design, as we can see a 2-input or gate is realized as was expected when optimizations are applied:
	
<img width="676" alt="opt_check1" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/02.png">


</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check3.v </summary>
	
I used the below commands to view the synthesized design of opt_check3.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check3.v>
yosys> synth -top <name: opt_check3>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 3-input and gate is realized as was expected when optimizations are applied:
	
<img width="444" alt="opt_check3" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/03.png">


</details>
	
<details>
 <summary> Combinational logic optimizations: opt_check4.v </summary>
	
I used the below commands to view the synthesized design of opt_check4.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: opt_check4.v>
yosys> synth -top <name: opt_check4>
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see a 2-input xnor gate is realized as was expected when optimizations are applied:
	
<img width="474" alt="opt_check4" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/04.png">


</details>
		
<details>
 <summary> Combinational logic optimizations: multiple_module_opt.v </summary>
	
I used the below commands to view the synthesized design of multiple_module_opt.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_module_opt.v>
yosys> synth -top <name: multiple_module_opt>
yosys> flatten 
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see 2 and gates and 1 or gate are realized as was expected when optimizations are applied:
	
<img width="419" alt="multiple_module_opt" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/05.png">



</details>
	
<details>
 <summary> Combinational logic optimizations: multiple_module_opt2.v </summary>
	
I used the below commands to view the synthesized design of multiple_module_opt2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: multiple_module_opt2.v>
yosys> synth -top <name: multiple_module_opt2>
yosys> flatten 
yosys> opt_clean -purge
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, as we can see no standard cells are realized as was expected when optimizations are applied:
	
<img width="421" alt="multiple_module_opt2" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/06.png">



</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const1.v </summary>
	
I used the below commands to simulate the design of dff_const1.v:
	
```bash
iverilog <name verilog: dff_const1.v> <name testbench: tb_dff_const1.v>
./a.out
gtkwave tb_dff_const1.vcd
```	

Below is the screenshot of the obtained simulation, a we can see even when reset is zero, Q waits for next rising edge of clock:
	
<img width="578" alt="dff_const1" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/07.png">

	
I used the below commands to view the synthesized design of dff_const1.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const1.v>
yosys> synth -top <name: dff_const1>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design:
	
<img width="506" alt="dff_const1_synth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/08.png">



</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const2.v </summary>
	
I used the below commands to simulate the design of dff_const2.v:
	
```bash
iverilog <name verilog: dff_const2.v> <name testbench: tb_dff_const2.v>
./a.out
gtkwave tb_dff_const2.vcd
```	

Below is the screenshot of the obtained simulation, as we can see Q is one regardless of the value of reset and clock:
	
<img width="629" alt="dff_const2" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/09.png">

I used the below commands to view the synthesized design of dff_const2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const2.v>
yosys> synth -top <name: dff_const2>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design:
	
<img width="438" alt="dff_const2_synth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/10.png">


</details>

	
<details>
 <summary> Sequential logic optimizations: dff_const3.v </summary>
	
I used the below commands to simulate the design of dff_const3.v:
	
```bash
iverilog <name verilog: dff_const3.v> <name testbench: tb_dff_const3.v>
./a.out
gtkwave tb_dff_const3.vcd
```	

Below is the screenshot of the obtained simulation, as we can see Q does not follow Q1 immediately:
	
<img width="574" alt="dff_const3" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/11.png">

I used the below commands to view the synthesized design of dff_const3.v:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const3.v>
yosys> synth -top <name: dff_const3>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained design, the 2 flipflops are retained and optimization could not remove any of them:

<img width="651" alt="dff_const3synth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/12.png">


</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const4.v </summary>
	
I used the below commands to simulate the design of dff_const4.v:
	
```bash
iverilog <name verilog: dff_const4.v> <name testbench: tb_dff_const4.v>
./a.out
gtkwave tb_dff_const4.vcd
```	

Below is the screenshot of the obtained simulation, as we can see Q and Q1 are one regardless of clk and reset:

<img width="614" alt="dff_const4" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/13.png">
	
I used the below commands to view the synthesized design of dff_const4.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const4.v>
yosys> synth -top <name: dff_const4>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and no hardware was used as expected:
	
<img width="424" alt="dff_const4_synth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/14.png">

</details>
	
<details>
 <summary> Sequential logic optimizations: dff_const5.v </summary>
	
I used the below commands to simulate the design of dff_const5.v:
	
```bash
iverilog <name verilog: dff_const5.v> <name testbench: tb_dff_const5.v>
./a.out
gtkwave tb_dff_const5.vcd
```	

Below is the screenshot of the obtained simulation, as we can see when reset is zero, Q1 becomes one on the next rising edge of clk, and Q follows Q1 on the next rising edge of clk:

<img width="604" alt="dff_const5" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/15.png">

	
I used the below commands to view the synthesized design of dff_const5.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: dff_const5.v>
yosys> synth -top <name: dff_const5>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and the 2 flipflops are retained:
	
<img width="629" alt="dff_const5_synth" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/16.png">

</details>
	
<details>
 <summary> Sequential logic optimizations for unused outputs: counter_opt.v </summary>
	
I used the below commands to view the synthesized design of counter_opt.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: counter_opt.v>
yosys> synth -top <name: counter_opt>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and the only used output (count[0]) is present and 1 flipflop is used:
	
<img width="684" alt="counter_opt" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/17.png">
	
</details>
	
<details>
 <summary> Sequential logic optimizations for 3 used outputs: counter_opt2.v </summary>
	
I used the below commands to view the synthesized design of counter_opt2.v with optimizations:
	
```bash
yosys> read_liberty -lib <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> read_verilog <name of verilog file: counter_opt2.v>
yosys> synth -top <name: counter_opt2>
yosys> dfflibmap -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> abc -liberty <path to sky130_fd_sc_hd__tt_025C_1v80.lib>
yosys> show
```
	
Below is the screenshot of the obtained optimized design, and 3 flipflops are used in addition to the counting logic of all bits:
	
<img width="681" alt="counter_opt2" src="https://raw.githubusercontent.com/unixjet/VSDSquadron-assets/main/day3/18.png">
	
</details>

