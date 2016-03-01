# Lab/Tutorial 4

In this tutorial, some contexts use Synopsys tutorials from Hamid Nahmoodi (SFSU) and John Sanguinetti (verilog dot com). All the tools and EDK are given thru Synopsys University Program. Some lab examples are referred from [MIT 6.375](http://csg.csail.mit.edu/6.375/6_375_2016_www/index.html) and [UCSD CSE141L](https://cseweb.ucsd.edu/classes/wi08/cse141L/Slides/verilog_deux.pdf).

## Introduction

In this tutorial, you will learn how to do RTL (register transfer level) design to build your circuit with HDL (hardware description language) for EDA (electronic design automation)

This work design for three weeks lab, so for your lab report, you need to design three sets of HDLs, which are 4-bit binary full adder, finite state machine, greatest common devisor (gcd), and finally full-chip design.


In this lab4, we introduce Synopsys RTL design toolkit, which are VCS, Design Compiler, IC Compiler, VCS RTL Verification solution.


In this lab, you need to review at least 2 hours for the following website to review your Verilog programming skill, debugging method, and design examples. After 2 hours review, you need to follow RTL design step to make the final layout with design automation process.



## Lab4 Schedule

Lab4 is 3-week lab and here are the details for given lab

- Lab4-week1: Verilog Review, 4-bit full adder Chip, FSM chip design.

- Lab4-week2: RTL Practical Programming for your GCD design.

- Lab4-week3: Full-chip synthesis design and layout for Synopsys ChipTop processor with Timing, Area, and Power Analysis of PrimeTime


## Lab4-Week1: Part 1. HDL (Hardware Description Language)- Verilog Language

We will use Verilog, which is standardized as IEEE 1364, a hardware description language (HDL) used to model electronic systems. It is most commonly used in the design and verification of digital circuits at the register-transfer level (RTL) of abstraction. ([refer Wikipedia](https://en.wikipedia.org/wiki/Verilog))

Here is Verilog tutorials consist of 5 Chapters as follows:

| Chapter  | Title | Detail |
| -------- | ------ | ------- |
| 1 | Introduction, Hierarchy, and Modeling Structures. | This section provides background about the history of Verilog. It also introduces some of the basic structures of Verilog models. |
| 2 | Syntax, Lexical Conventions, Data Types, and Memories | This section addresses the syntax and semantics of the core features of the language. |
| 3 | Expressions and Simulation Mechanics | This section covers the components of Verilog expressions and the order of execution in Verilog models. |
| 4 | Gate Level Modeling | This section covers gate level modeling constructs. It covers the semantics of Verilog primitives, port expressions, delays, strengths, and user-defined primitives. |
| 5 | Behavioral and Register Transfer Level Modeling | This section covers the remainder of the language basics: assignments of all kinds, control constructs, time and event controls, tasks and functions, and examples. |

You need to review from chapter 1 thru Chapter 5, Chapter 5-9 can be references for your Verilog programming.

You need to provide all your answers for the each question to get checked off at the end of the lab. So please open text editor/ms office word and write down all the answers to show TA for the check-off.

Go to the following Verilog tutorial

__[Click here for Verilog Tutorial](http://vol.verilog.com/VOL/main.htm)__

You should finish this tutorial first for 2 hours at least.


There is better explanation for Verolog Operators [Click Here](https://embeddedmicro.com/tutorials/mojo/verilog-operators) - Thanks, Brandon

__This lab requires individual lab! You cannot do any partner work anymore.__


## Lab4-Week1: Part 2. Synopsys Verilog Compiler Simulator (Verilog Compiler ) Tutorial

For the Verilog editor, `vi` or `emacs` is recommended, but if you're beginner of Linux system, you can use `nano`, it's your choice.

Synopsys Verilog Compiler Simulator is a tool from Synopsys specifically designed to simulate and debug designs. This tutorial basically describes how to use VCS, simulate a verilog description of a design and learn to debug the design. VCS also uses VirSim, which is a graphical user interface to VCS used for debugging and viewing the waveforms.

There are three main steps in debugging the design, which are as follows
1. Compiling the Verilog/VHDL source code.
1. Running the Simulation.
1. Viewing and debugging the generated waveforms.

You can interactively do the above steps using the VCS tool. VCS first compiles the
verilog source code into object files, which are nothing but C source files. VCS can
compile the source code into the object files without generating assembly language files.
VCS then invokes a C compiler to create an executable file. We use this executable file to
simulate the design. You can use the command line to execute the binary file which
creates the waveform file

In this tutorial, we would be using a simple counter example . Find the verilog code and
testbench at the end of the tutorial.

- RTL Source code:

[counter.v](https://raw.githubusercontent.com/tkimva/ucr-eecs168/master/lab4/counter.v)

- Testbench of RTL:

[counter_tb.v](https://raw.githubusercontent.com/tkimva/ucr-eecs168/master/lab4/counter_tb.v)

From server, you can create your RTL folder and download

Under your eecs168 folder,

```
mkdir lab4-rtl
cd lab4-rtl
mkdir counter
cd counter
```

and download two files

```
wget https://raw.githubusercontent.com/tkimva/ucr-eecs168/master/lab4/counter.v
wget https://raw.githubusercontent.com/tkimva/ucr-eecs168/master/lab4/counter_tb.v
```

1. In the “lab4-rtl” directory, compile the verilog source code by typing the following at the
machine prompt.
```
vcs counter_tb.v counter.v +v2k
```

You can see the following successful compilation message

```
Warning-[LNX_OS_VERUN] Unsupported Linux version
  Linux version 'CentOS release 6.7 (Final)' is not supported on 'x86_64'
  officially, assuming linux compatibility by default. Set VCS_ARCH_OVERRIDE
  to linux or suse32 to override.
  Please refer to release notes for information on supported platforms.

                         Chronologic VCS (TM)
         Version K-2015.09-SP1-1 -- Mon Feb 22 13:43:12 2016
               Copyright (c) 1991-2015 by Synopsys Inc.
                         ALL RIGHTS RESERVED

This program is proprietary and confidential information of Synopsys Inc.
and may be used and disclosed only as authorized in a license agreement
controlling such use and disclosure.

Parsing design file 'counter_tb.v'
Parsing design file 'counter.v'
Top Level Modules:
       timeunit
       counter_testbench
TimeScale is 1 ns / 10 ps
Starting vcs inline pass...
2 modules and 0 UDP read.
recompiling module timeunit
recompiling module counter_testbench
Both modules done.
make: Warning: File `filelist.cu' has modification time 0.17 s in the future
make[1]: Warning: File `filelist.cu' has modification time 0.16 s in the future
rm -f _csrc*.so linux_scvhdl_*.so pre_vcsobj_*.so share_vcsobj_*.so
make[1]: warning:  Clock skew detected.  Your build may be incomplete.
make[1]: Warning: File `filelist.cu' has modification time 0.15 s in the future
make[1]: warning:  Clock skew detected.  Your build may be incomplete.
if [ -x ../simv ]; then chmod -x ../simv; fi
g++  -o ../simv   -Wl,-rpath-link=./ -Wl,-rpath='$ORIGIN'/simv.daidir/ -Wl,-rpath=./simv.daidir/ -Wl,-rpath='$ORIGIN'/simv.daidir//scsim.db.dir  -m32 -m32 -rdynamic   amcQwB.o objs/amcQw_d.o   _22827_archive_1.so  SIM_l.o       rmapats_mop.o rmapats.o rmar.o  rmar_llvm_0_1.o rmar_llvm_0_0.o          /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libzerosoft_rt_stubs.so /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libvirsim.so /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/liberrorinf.so /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libsnpsmalloc.so    /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libvcsnew.so /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libsimprofile.so /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libuclinative.so   -Wl,-whole-archive /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/libvcsucli.so -Wl,-no-whole-archive          /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/vcs_save_restore_new.o /usr/local/synopsys/K-2015.09-SP1-1/linux/lib/ctype-stubs_32.a -ldl  -lc -lm -lpthread -ldl
../simv up to date
make: warning:  Clock skew detected.  Your build may be incomplete.
CPU time: .132 seconds to compile + .249 seconds to elab + .230 seconds to link
```


Here, the `+v2k` option is used if you are using Verilog IEE 1364-2000 syntax; otherwise there
is no need for the option.

By default the output of compilation would be a executable binary file is named `simv`.
You can specify a different name with the -o compile-time option. VCS compiles the
source code on a module by module basis. You can incrementally compile your design
with VCS, since VCS compiles only the modules which have changed since the last
compilation.

Now, execute the simv command line with no arguments. You should see the output
from both vcs and simulation and should produce a waveform file called counter.dump in
your working directory.

```
./simv
```

Simulation result will be shown as below

```
Chronologic VCS simulator copyright 1991-2015
Contains Synopsys proprietary information.
Compiler version K-2015.09-SP1-1; Runtime version K-2015.09-SP1-1;  Feb 22 13:45 2016
time=    0 ns, clk=0, reset=0, out=xxxx
time=   10 ns, clk=1, reset=0, out=xxxx
time=   11 ns, clk=1, reset=1, out=xxxx
time=   20 ns, clk=0, reset=1, out=xxxx
time=   30 ns, clk=1, reset=1, out=xxxx
time=   31 ns, clk=1, reset=0, out=0000
time=   40 ns, clk=0, reset=0, out=0000
time=   50 ns, clk=1, reset=0, out=0000
time=   51 ns, clk=1, reset=0, out=0001
time=   60 ns, clk=0, reset=0, out=0001
time=   70 ns, clk=1, reset=0, out=0001
time=   71 ns, clk=1, reset=0, out=0010
time=   80 ns, clk=0, reset=0, out=0010
time=   90 ns, clk=1, reset=0, out=0010
time=   91 ns, clk=1, reset=0, out=0011
time=  100 ns, clk=0, reset=0, out=0011
time=  110 ns, clk=1, reset=0, out=0011
time=  111 ns, clk=1, reset=0, out=0100
time=  120 ns, clk=0, reset=0, out=0100
time=  130 ns, clk=1, reset=0, out=0100
time=  131 ns, clk=1, reset=0, out=0101
time=  140 ns, clk=0, reset=0, out=0101
time=  150 ns, clk=1, reset=0, out=0101
time=  151 ns, clk=1, reset=0, out=0110
time=  160 ns, clk=0, reset=0, out=0110
time=  170 ns, clk=1, reset=0, out=0110
All tests completed sucessfully


$finish called from file "counter_tb.v", line 55.
$finish at simulation time  171.0 ns
           V C S   S i m u l a t i o n   R e p o r t
Time: 171000 ps
CPU Time:      0.350 seconds;       Data structure size:   0.0Mb
Mon Feb 22 13:45:00 2016

```



## Lab4-Week1: Part 3. Design Compiler for Synthesis

In this tutorial you will gain experience using Synopsys Design Compiler (DC) to perform hardware synthesis. A synthesis tool takes an RTL hardware description and a standard cell library as input and produces a gatelevel netlist as output. The resulting gate-level netlist is a completely structural description with standard cells only at the leaves of the design.

Internally, a synthesis tool performs many steps including high-level RTL optimizations, RTL to unoptimized boolean logic, technology independent optimizations, and finally technology mapping to the available standard cells. Good RTL designers will familiarize themselves with the target standard cell library so that they can develop an intuition on how their RTL will be synthesized into gates.

In this tutorial you will use Synopsys Design Compiler to elaborate the RTL for our example 4-bit full adder circuit, set optimization constraints, synthesize the design to gates, and prepare various area and timing reports. You will also learn how to read the various DC text reports and how to use the graphical Synopsys Design Vision tool to visualize the synthesized design.

First, go to `lab4-rtl` folder and make workspace folder for `4-bit full adder`

open 'vi', 'emacs', or 'nano' to edit this file

```
nano fa_4bit.v
```

`fa_4bit.v` file should contain the following code

```
module fa_4bit( cin, cout, ain, bin, sum );

	input cin;
	input [3:0] ain, bin;
	output [3:0] sum;
	output cout;

	assign {cout,sum} = ain + bin + cin;

endmodule // fa_4bit

```

One Verilog file is ready. We need to do SYNTHESIS, which is a transformation process from RTL to gate-level design (another synthesized Verilog). Type the following command to launch Design Compiler.

```
dc_shell
```

- launch dc_shell for design compiler.
![fig1](images/fig1.png)

_**Fig. 1. Launch Design Compiler**_

- launch gui_start for design vision, which is GUI interface for design compiler
![fig2](images/fig2.png)

_**Fig. 2. Launch Design Vision for GUI Version of Design Compiler**_

First we need to choose Synopsys 90nm model for design process.

- File-> Setup and choose model for your library
![fig3](images/fig3.png)

_**Fig. 3. Choose Setup for library setup.**_

click Link library and put the following paths
- Link library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/saed90nm_fr/LM/saed90nm_typ.db
```
- Target Library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/saed90nm_fr/LM/saed90nm_typ.db
```
- Symbol Library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/icons/saed90nm.sdb
```

![fig4](images/fig4.png)

_**Fig. 4. Application setup window**_

Now, we need to set logic VDD and VSS net wire name.

in the dc_shell command shell at the bottom, the following inputs should be typed.

```
set mw_logic1_net "VDD"
```
![fig5](images/fig5.png)

_**Fig. 5. VDD Setup**_

```
set mw_logic0_net "VSS"
```
![fig6](images/fig6.png)

_**Fig. 6. VSS Setup**_


Use your 4-bit full adder you already typed.

You already made new Verilog file, (fa_4bit.v)


Syntax error checking for your Verilog file.

```
analyze -format verilog "fa_4bit.v"
```

Elaborate your design module, during elaboration DC will report all state inferences. This is a good way to verify that latches and flip-flops are not being accidentally inferred.

```
elaborate fa_4bit -architecture verilog -library DEFAULT
```

Link your design module

```
link
```

The check_design command checks that the design is consistent. You will not be able to synthesize your design until you eliminate all ERRORS. Many WARNINGS are not an issue, but it is still useful to skim through this output.

```
check_design
```

Compile your design module, The `compile` command begins the actual synthesis process that transforms your design into a gate-level netlist.

```
compile
```

After your compilation done, you need to create schematic of the synthesized RTL code.

Once you click the symbol (fa_4bit), you can see how it was compiled/synthesized.

We finished the synthesis and we need to generate output file for IC Compiler for layout.

```
write -format ddc -output "fa_4bit_synthesized.ddc"
```

We also need to create gate-level verilog synthesized file.

```
write -format verilog -output "fa_4bit_synthesized.v"
```

Now, we need to write a design constraint file.

```
write_sdc -nosplit "fa_4bit_const.sdc"
```

Now, it's time to use IC Compiler, so you need to exit Design Compiler

```
exit
```

Now, it's ready for placement and router for your IC.

## Lab4-Week1: Part 4. IC Compiler (ICC) for Placement and Routing Layout

In this tutorial you will gain experience transforming a gate-level netlist into a placed and routed layout using Synopsys IC Compiler (ICC). ICC takes a synthesized gate-level netlist and a standard cell library as input, then produces layout as an output.

To launch IC Compiler, you need to run the following command in the linux shell.

The first goal of a Place and Route (P&R) tool is to determine where each gate should be located on the physical chip (the placement portion of place and route). This process leverages heuristic algorithms to group related gates together in hopes of minimizing routing congestion and wire delay. Typically P&R tools will focus their effort on minimizing the delay through the critical path, and to this end will resize gates, insert new buffers, and even perform local re-synthesis. Additionally, P&R tools often have secondary algorithms to help reduce area for non-critical paths. After the placement, ICC will attempt to route the design while minimizing wire delay. Along with the routing, P&R tools often handle clock tree synthesis, power routing, and block level floorplanning.

For this tutorial we will generate layout for the gate-level netlist of the 4-bit full adder circuit synthesized in the previous section. Once the netlist has successfully been placed and routed, you should be able to see all the instantiated standard cells and routed metals of the physical implementation. We will then use the IC Compiler GUI to visualize the layout of your final placed and routed design.

```
icc_shell
```

To use GUI interface, you need to run the following command in the icc shell.

```
gui_start
```

![fig18](images/fig18.png)

_**Fig. 18. ICC launch**_

![fig19](images/fig19.png)

_**Fig. 19. ICC GUI launch**_

![fig20](images/fig20.png)

_**Fig. 20. Application Setup**_

click Link library and choose

- Link library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/saed90nm_fr/LM/saed90nm_typ.db
```
- Target Library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/saed90nm_fr/LM/saed90nm_typ.db
```

- Symbol Library
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/icons/saed90nm.sdb
```

![fig21](images/fig21.png)

_**Fig. 21. Setup the library in the application setup**_

![fig22](images/fig22.png)

_**Fig. 22. Create Library**_


Now, we need to create our own library

For the new library path, just click the folder button and choose the
current folder.

File-> Create library and type your new library name `fa_4bit_icc`

and then, you need to choose Technology file as follows:


```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/tech/saed90nm.tf
```

for input reference libraries, you need to add the following file.

```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/saed90nm_fr
```


make sure open library is checked

![fig23](images/fig23.png)

_**Fig. 23. Create Library**_


![fig24](images/fig24.png)

_**Fig. 24. TLU+**_

The parasitic RC (Resistance Capacitance) for interconnect is estimated through the use of TLU+ models, generated using STAR-RCXT an extraction tool from synopsys. TLU+ contains resistance and capacitance look up tables and model ultra deep submicron process effects. Now, we setup TLU+ for the parasitic RC model.

Next, you need to set TLU+

File-> Set TLU+

Max TLU+ file:
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/tlup/saed90nm_1p9m_1t_Cmax.tluplus
```

Min TLU+ file:
```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/tlup/saed90nm_1p9m_1t_Cmin.tluplus
```

Layer name mapping file

```
/usr/local/synopsys/pdk/SAED90_EDK/SAED_EDK90nm_REF/references/ChipTop/ref/tlup/tech2itf.map
```

![fig25](images/fig25.png)

_**Fig. 25. TLU+ setup**_


Now, we can start layout, so we need to import design

File-> Import -> Read Verilog, choose verilog and click [Add] button to add
synthesized verilog design what we made `fa_4bit_synthesized.v` and
click okay, then layout window will open below.

![fig26](images/fig26.png)

_**Fig. 26. Import Verilog**_

![fig27](images/fig27.png)

_**Fig. 27. Read Verilog**_

![fig28](images/fig28.png)

_**Fig. 28. Read synthesized gate-level Verilog**_

Now we can see the standard cells as layout


File->Import Design, choose SDC and import `fa_4bit_const.sdc` you
exported from Design Compiler.

![fig29](images/fig29.png)

_**Fig. 29. Standard Cell View**_

![fig30](images/fig30.png)

_**Fig. 30. Synopsys Design Constraints (SDC)**_

You need to save at least now for your design.

Go to File->Save

![fig32](images/fig32.png)

_**Fig. 32. Save your design**_

![fig33](images/fig33.png)

_**Fig. 33. Save your design**_

Now, we need to create the floorplan. Floorplan -> Create Floorplan

For the spacing between core are and terminals, we can set 10um for
left, right, bottom, and top.


Now, we need to create power-ground network.

Go to Preroute -> Derive Power Ground Connection.

![fig34](images/fig34.png)

_**Fig. 34. Derive Power Ground Connection**_



Click Manual connection and put "VDD" in the power net and "VSS" in
the Ground net. Also put "VDD" in the Power pin and "VSS" in the
Ground pin. Create port should be "Top"

![fig35](images/fig35.png)

_**Fig. 35. Derive Power Ground Connection**_

Now, we need to write a floor plan.
Go to Floorplan-> Create Floorplan

![fig36](images/fig36.png)

_**Fig. 36. Floor plan**_


```
create_floorplan -use_vertical_row -start_first_row -left_io2core 20 -bottom_io2core 20 -right_io2core 20 -top_io2core 20
```
![fig37](images/fig37.png)

_**Fig. 37. Floor plan**_

![fig38](images/fig38.png)

_**Fig. 38. Floor plan is ready**_


Let's do placement now

```
create_fp_placement
```
![fig39](images/fig39.png)

_**Fig. 39. Floor plan is ready**_

![fig40](images/fig40.png)

_**Fig. 40. Standard cell placed**_

Now, we make floorplan rail for VDD and VSS.

```
synthesize_fp_rail \
  -power_budget "1000" -voltage_supply "1.2" -target_voltage_drop "250" \
  -output_dir "./pna_output" -nets "VDD VSS" -create_virtual_rails "M1" \
  -synthesize_power_plan -synthesize_power_pads -use_strap_ends_as_pads
```
![fig42](images/fig42.png)

_**Fig. 42. Rail Placed**_

Once your rail is okay, you need to commit for the real rail in your design.

```
commit_fp_rail
```

![fig44](images/fig44.png)

_**Fig. 44. Rail Placed**_

After finishing placement, we need to have metal wire routing. So we need to have two following steps for the routing.

```
route_opt -initial_route_only
```

```
route_opt -skip_initial_route -effort low
```


![fig47](images/fig47.png)

_**Fig. 47. Routing Done**_

Finally, we need standard cell fillers, which are used to fill any spaces between regular library cells to avoid planarity problems. They are need when the density of the required metal or layer has not meet the foundry or fabrication requirement. Thus, you need to add it whether it is low or high frequency.

By the following command, we can put standard cell fillers.

```
insert_stdcell_filler \
 -cell_with_metal "SHFILL1 SHFILL2 SHFILL3" \
 -connect_to_power "VDD" -connect_to_ground "VSS"
```

![fig49](images/fig49.png)

_**Fig. 49. Final Layout after putting standard cell filler**_


## Lab4-Week2 : RTL Practical Programming for your GCD design.

### Design GCD Design

#### Part 1. Complete your RTL for GCD

**Caution! You have to train your Verilog skill youself to make this code. TA will not be easily helpful for your Verilog code debugging. Please refer __[Verilog Tutorial](http://vol.verilog.com/VOL/main.htm)__**.

Lab4-week2, we work on GCD algorithm, which is a popular algorithm for computing greatest common divisor (GCD) (TA provides some incomplete RTL designs for GCD algorithm, students complete RTL code and synthesize and generate Layout finally)

Here is GCD algorithm.

Following is the Euclid’s algorithm to compute GCD of two numbers, A and B. The algorithm was reported by J. Stein in 1967 and is available on the web at http://www.nist.gov/dads/HTML/binaryGCD.html (link is perhaps inactive) and also at http://en.wikipedia.org/wiki/Binary_GCD_algorithm.



- Euclid's Algorithm for GCD (in C):

```
#include <stdio.h>


int GCD( int inA, int inB) {
  int done = 0;
  int swap = 0;

  int A = inA;
  int B = inB;

  while ( !done )
    {
      if ( A < B ) // if A < B, swap values
        {
          swap = A; A = B;
          B = swap;
        }
      else if ( B != 0 ) // subtract as long as B isn’t 0
        A = A - B;
      else
        done = 1;
    }
  return A;
}

int main(void) {
// this can be testbench

  int inA = 20;
  int inB = 30;
  int out = 0;

  out = GCD( inA, inB );

  printf("Input inA = %d\n",inA);
  printf("Input inB = %d\n",inB);
  printf("GCD Output of inA and inB = %d\n",out);

  return 0;
}
```

Now, we need to implement this in hardware.

Here is behavioral Verilog code for GCD. What is wrong with this approach? Basically, it does not synthesize due to data dependent loop in hardware.

```
module gcdGCDUnit_behavior#( parameter W = 16 )
  (
  input  [W-1:0] inA, inB,
  output [W-1:0] out
  );
    reg [W-1:0] A, B, out, swap;
    integer     done;
    always @(*)
    begin
      done = 0;
      A = inA; B = inB;
      while ( !done )
        begin
          if ( A < B )
            swap = A;
            A = B;
            B = swap;
          else if ( B != 0 )
            A = A - B;
          else
            done = 1;
        end
      out = A;
    end
endmodule
```

The above behavioral description of the GCD unit describes the functionality of the module. While this is sufficient for VCS RTL simulation, the Design Compiler and IC Compiler cannot properly synthesize netlist from this description. Because of this, you must rewrite the behavioral description using “synthesizable” RTL code. For this, you will apply a structural design approach which involves describing the circuit design in terms of its registers, connections, and other modules. This process is referred to as Register Transfer Level Design.

The first step is to derive the module in terms of its Data Path and Control Unit. The Data Path contains the registers, logic and math modules. The Control Unit contains the logic that drives the control signals for the Data Path. This is typically accomplished using a Finite State Machine which was part of your tutorial example in Chapter 5.

Here is some methodology how we can make some RTL Design from behavioral RTL design.


- __1st step:__ Start with behavioral and find out what hardware constructs you’ll need the followings
  - Registers (for state)
  - Functional units
    1. Adders / Subtractors
    1. Comparators
    1. ALU’s

    Above behavioral code. Let's find functional unit samples.
    ```
    A = inA; B = inB; => State -> Registers

    A<B => Need comparator

    B != 0 => Need another comparator

    A= A - B: Need subtractor
    ```


- __2nd step:__ Define module ports

  Define module ports



- __3rd step:__ Implement the modules
  - Two step process
    1. Define datapath
    1. Define control/ control path



The detail methodology and GCD RTL can be found [this slides](https://cseweb.ucsd.edu/classes/wi08/cse141L/Slides/verilog_deux.pdf)

Total system block is look like below.


We provide three following incomplete RTL designs (Verilog) from above behavioral code for GCD algorithm. You should complete this file to go next part.

- GCD Top Design: `gcd_rtl.v`
- GCD Control: `gcd_ctrl.v`
- GCD Data Path: `gcd_dpath.v`

![GCD RTL Design](images/GCD_RTL.png)

_**GCD RTL Design Block**_

you need to download incomplete GCD RTL design [here](https://raw.githubusercontent.com/tkimva/ucr-eecs168/master/lab4/GCD_RTL.tgz)



To test your GCD Testbench with RTL Design successfully, you need to pass the following VCS testing toolkit (referred from MIT 6.375)
```
vcs -PP +lint=all,noVCDE +v2k -timescale=1ns/10ps +define+CLOCK_PERIOD=0.5 gcd_rtl_tb.v gcd_ctrl.v gcd_dpath.v gcd_rtl.v -v vcTest.v -v vcTestSource.v -v vcTestSink.v -v vcQueues.v -v vcStateElements.v
```


If your RTL still has error, then your `simv` result will be the following
```
[tkim@kepler rtl_students]:./simv +verbose=1
Chronologic VCS simulator copyright 1991-2015
Contains Synopsys proprietary information.
Compiler version K-2015.09-SP1-1; Runtime version K-2015.09-SP1-1;  Feb 29 16:49 2016
 Entering Test Suite: gcdGCDUnit_rtl
VCD+ Writer K-2015.09-SP1-1 Copyright (c) 1991-2015 by Synopsys Inc.
  + Running Test Case: gcdGCDUnit_rtl
     [ FAILED ] Test ( Is sink finished? ) failed

$finish called from file "gcd_rtl_tb.v", line 124.
$finish at simulation time               154650
           V C S   S i m u l a t i o n   R e p o r t
Time: 1546500 ps
CPU Time:      0.640 seconds;       Data structure size:   0.0Mb
Mon Feb 29 16:49:37 2016
[tkim@kepler rtl_students]:
```

If you successfully finished your RTL, then your `simv` result will be the following
```
[tkim@kepler rtl_students]:./simv +verbose=1
Chronologic VCS simulator copyright 1991-2015
Contains Synopsys proprietary information.
Compiler version K-2015.09-SP1-1; Runtime version K-2015.09-SP1-1;  Feb 29 16:50 2016
 Entering Test Suite: gcdGCDUnit_rtl
VCD+ Writer K-2015.09-SP1-1 Copyright (c) 1991-2015 by Synopsys Inc.
  + Running Test Case: gcdGCDUnit_rtl
     [ passed ] Test ( vcTestSink ) succeeded, [ 0003 == 0003 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0007 == 0007 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0005 == 0005 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0001 == 0001 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0028 == 0028 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 000a == 000a ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0005 == 0005 ]
     [ passed ] Test ( vcTestSink ) succeeded, [ 0000 == 0000 ]
     [ passed ] Test ( Is sink finished? ) succeeded

$finish called from file "gcd_rtl_tb.v", line 124.
$finish at simulation time               154650
           V C S   S i m u l a t i o n   R e p o r t
Time: 1546500 ps
CPU Time:      0.640 seconds;       Data structure size:   0.0Mb
Mon Feb 29 16:50:13 2016
[tkim@kepler rtl_students]:
```

#### Part 2. Synthesis and layout for GCD
After you finished your RTL design, then you need to synthesize with Design Compiler and generate a layout with IC Compiler.

##### Design Compiler and IC Compiler for GCD

GCD requires clock and you also need to synthesize clock tree. For your GCD, every step is the same as 4-bit full adder example from RTL to Layout except the following extra steps.

###### Design Compiler Changes for GCD.

- After `check_design` in Design Compiler, you need to build clock period constraint as extra step before compile
```
create_clock clk -name idea_clock1 -period 1
```

- Instead of `compiler` in Design Compiler, you use faster compiler variants (`compiler_ultra`) with clock option.
```
compiler_ultra -gate_clock -no_autoungroup
```

###### IC Compiler Changes for GCD.

- For the floorplan, enough sizes are needeed. Use 30 instead of 20.

```
create_floorplan -use_vertical_row -start_first_row -left_io2core 30 -bottom_io2core 30 -right_io2core 30 -top_io2core 30
```

- For the clock synthesize, you need to generate clock tree after `commit_fp_rail`.
```
clock_opt -only_cts -no_clock_route
```

```
route_zrt_group -all_clock_nets -reuse_existing_global_route true
```
- For Routing one more after `insert_stdcell_filler`
```
route_opt -incremental -size_only
```
- Extra final step, Generate the post place and route netlist, the constraint file, and parasitics files to generate power estimates.
```
change_names -rules verilog -hierarchy
```

```
write_verilog "gcdGCDUnit_rtl.output.v"
```

```
write_sdf "gcdGCDUnit_rtl.output.sdf"
```

```
write_sdc "gcdGCDUnit_rtl.output.sdc"
```

```
extract_rc -coupling_cap
```

```
write_parasitics -format SBPF -output "gcdGCDUnit_rtl.output.sbpf"
```


- Final GCD layout ready.

![Fig. 51](images/GCD_layout.png)

_**Fig. 51. Final GCD Layout**_





## Lab4-Week3 (Incomplete) : Full-chip synthesis design and layout for Synopsys ChipTop processor with Timing, Area, and Power Analysis of PrimeTime

### Summary of what you did for lab4-week1

![Fig. 50](images/synopsys_tool_flow.png)

_**Fig. 50. Full RTL and Physical Toolflow for IC design**_

So far, we used Verilog Compiler Simulator (VCS) for RTL simulation, Design Compiler for Logic Synthesis, and IC Compiler for Layout. Now, we will use PrimeTime which is signoff tool and enable accurate delay and power estimations.

Signoff users have a few key requirements for their signoff tool of choice, runtime and capacity to handle their largest chip size requirements, efficient multi-scenario analysis to verify timing across all corners and modes, margin control to reduce over-design and maximize chip performance, and accuracy to ensure correlation to silicon. The Synopsys PrimeTime Suite addresses these requirements by delivering fast, memory-efficient scalar and multicore computing, distributed multi-scenario analysis and ECO fixing, using variation-aware Composite Current Source (CCS) modeling that extends static timing analysis to include crosstalk timing, noise, power and constraint analysis.

It delivers HSPICE accurate signoff analysis that helps pinpoint problems prior to tapeout thereby reducing risk, ensuring design integrity, and lowering the cost of design. This industry gold-standard solution improves designers' productivity by delivering fast turnaround on development schedules for large and small designs while ensuring first-pass silicon success through greater predictability and the highest accuracy.

- See more at: http://www.synopsys.com/Tools/Implementation/SignOff/Pages/PrimeTime.aspx#sthash.qfYroAvS.dpuf





## Lab4 Logistics

### Objective

In this tutorial, you will learn how to do RTL (register transfer level) design to build your circuit with HDL (hardware description language) for EDA (electronic design automation)

This work design for three weeks lab, so for your lab report, you need to design three sets of HDLs, which are 4-bit binary full adder, finite state machine, greatest common devisor (gcd), and finally full-chip design.


In this lab4, we introduce Synopsys RTL design toolkit, which are VCS, Design Compiler, IC Compiler, VCS RTL Verification solution.

### Deliverables for your lab report.

* Name, SID, Session(021,022), ENGR ID, UCR NetID, your partner name

---- week1 checkoff from here

  * Answers of all the questions from Verilog tutorial in Chapter 1 to 5.

  * Simulation result of example counter.

  * The result of gate-level for 4-bit full adder, fa_4bit_synthesized.v

  * Final layout in Fig 49 for 4-bit full adder.

---- until here for week1 check off

---- week 2 checkoff

  * Complete three Verilog file (gcd_rtl.v gcd_dpath.v gcd_ctrl.v)

  * Final Layout in Figure 51

---- week 2 check off

* week 3 checkoff

  * TBA

* Some of the issues if you have (One paragraph)

### What to submit

* Lab report (PDF format)

file name should be following

`lab3-[My UCR NET ID].pdf`

for example, my UCR Net ID is `tkim049`, so filename should be

`lab4-tkim049.pdf`

* Tar and Zip your design folder you made

`cd ~/eecs168/lab4-rtl` or you made

`tar -cvzf lab4-[My UCR NET ID].tgz ./`

for example, my ucr Net ID is `tkim049`, so do like following

`tar -cvzf lab4-tkim049.tgz ./`

* You need to submit two files (\*.pdf, \*.tgz) in iLearn

### Lab Report Due

* eecs168-021: by 11:59pm on 3/14
* eecs168-022: by 11:59pm on 3/16

### Checkoff

* First week: Refer above deliverables

* Second week: Refer above deliverables

* Three week: Refer above deliverables
