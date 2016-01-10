# Lab/Tutorial 1

In this tutorial, some contexts used from Vazgen Melikyan (Synopsys) and Hamid Nahmoodi (SFSU). All of tools and PDK are given thru Synopsys University Program.

## Introduction

In this tutorial, you will learn how to draw custom IC layout and simulate your design using 28/32/90nm technologies with Synopsys Custom Design Tools. This tutorial includes the detail steps of schematic and layout designs.

This manual assumes you are able to do some basic things in a Linux environment such as create
a folder, change directories....etc. If you want to learn how to use Linux here are many good
tutorials available on the web, such as this one: http://tldp.org/LDP/gs/node5.html.

* Fig1


Figure I.1
shows the design flow this tutorial will be implementing. In the first three parts of this manual
you will design and simulate a CMOS inverter using Custom DesignerSE in conjunction with
Hspice and WaveView to visually assemble the circuit schematic, simulate it, and view the
output waveforms. For further help you are encouraged to go to “Help” in the menu bar of
CosmosSE. You will use Custon DesignerSE to create a layout, and use Hercules to run a design
rule check (DRC) on the layout based on the technology process. You will also use Hercules to
make sure our inverter layout matches our schematic by running a Layout Versus Schematic
(LVS) check. Finally, you will use the inverter we create in a gate level design of a buffer.


## Part 1: Setup your design workspace

The first step is to login. Please refer to the login tutorial if you are having trouble logging in or
running the following commands. If you are using a Linux machine not connected to
hafez.sfsu.edu try using the following command to ensure you can use x- server:
ssh -l username -X hafez.sfsu.edu
To setup the library we will use the following command in the shell window:
cp /packages/synopsys/setup/lib.defs ./
cp /packages/process_kit/generic/generic_90nm/updated_oct2010/SAED_PDK90nm/display.tcl ./
(Notice that there is a space between cp and /packages for the second copy command above, and
also the space before ./)

Notice that the above commands need to be run once after your first login. You do not need to
rerun this command for future logins. Running the first copy command more than once can
overwrite saved directories resulting in lost files later on.
To setup all the software we will use the following commands in the shell window. These
commands must be run every time you use the Synopsys software:
csh
source /packages/synopsys/setup/full_custom.csh
Notice that the csh and source commands set the environment and need to be run every time you
login. To run an instance of Custom Designer simply type “cdesigner &”. Your command
window should look like the one shown in Fig.1.

* fig1

Custom Designer Console should open up (Fig.2).

* fig2

Use File  New Library to create a new library. A window will appear. Several lines in the
window are to be filled out to create a new library and several are not which are inactive and are
filled by default. Fill out the name field with a library name and fill out the directory field for a
place to save it. For the “Import File” field, click the dot so you can edit the text field and copy
and paste this file directory in the field:

/packages/process_kit/generic/generic_90nm/updated_oct2010/SAED_PDK90nm/techfiles/saed
90nm_1p9m_cd.tf
After you have filled out the name, directory, and import file, click OK. See Fig.3.

* fig3

## Part 2: Creating a cell view

Use File New CellView to create a new Cell View under the library that you create in part 1
(In this case called mylibrary). Enter a name for “Cell Name” and choose schematic for “View
Name”. For the “Editor” choose SE-schematic (see Fig.4). Click OK.

* fig4

After you click Ok new window will open up called schematic editor (Fig.5)

* fig5

In here we need to make sure that we are in right library.
From your console window select Tools Technology Manager and then make sure the
attachment of your library (in this case “mylibrary”) is SAED_PDK_90. If not, please click on it
and change it (Fig.6).

* fig6

Now go ahead and click on Add  Instance or simply click on this icon in the schematic
window. Select “SAED_PDK_90” for the library and select pmos4t and nmos4t for the cell
while placing their respective parts on the schematic. For pmos4t width, assign 0.5um and for
nmos4t width, assign 0.25um (Fig.7). You can also modify these properties later using the
property editor by going to Edit Properties  Property Editor and selecting the component
you want to modify in schematic view.

* fig7

After placing the pmos and nmos transistors, the schematic should look like figure 8 below.

* fig8

Next add wires to the schematic, click and draw wires to the circuit using the mouse pointer,
see figure 9 for wire connections. To deselect wire adding, press ESC. Now you need to give
names to your wires. Please click on . Then you will see a wire name space on top to enter
wire names. See Fig.10 for wire labeling.

* fig9

* fig10

Adding Pins
To add pins to the schematic, go to Add  Pin to add pins for input (VIN, AVDD, AVSS) and
output (VOUT) for your schematic. You can type in a name for the pin and select whether the
pin is an input or output port. Then place the pin on a wire or if the wire in schematic view
already has a name you can click on the wire and the pin will get the name of the wire. Note that
the pin names in schematic view should match the label names in layout view (AVDD, AVSS,
VIN, VOUT, etc) for future reference. See figure 11 and figure 12 for reference on how to add
pins. Afterwards your circuit should look similar to figure 13 below after you add the pins.
As a general convention, use uppercase letters for naming pins instead of lowercase letters.

* fig11

* fig12

* fig13

Save your schematic by clicking or go to Design  Save.
Now we want to create a symbol for the inverter schematic to use for future designs instead of
redrawing it every time. To create a symbol for the inverter, go to Design New CellView 
From CellView. Make sure library and cell names match and click OK. See figure 14 below for
reference.

* fig14

Now we have a transistor level model of an inverter (symbol). See figure 15 for reference.

* fig15

You may also modify the appearance of the inverter symbol here by using the shape tools, Add
 Shape. Now save and close the symbol window.
From the Custom Design Console, go to File  New  CellView and select mylibrary under
the library column. Enter a new name for “Cell Name” in this case I used inverter_testbench
and choose schematic for “View Name”. For the editor choose SE-schematic. Click OK. See
figure 16 for reference. Note that this schematic file will be used as a sandbox for circuits using
the inverter symbol we created earlier.

* fig16

Now that you have a new schematic window, go to Add  Instance. In the add instance
window, select “mylibrary” as the library, “inverter” as the cell, and “symbol” for the view to
select the inverter you just made and place it on the schematic. See figure 17 for reference.
Also in the add instance window, select “analogLib” for the library and choose: vsource, vpulse
and gnd for the cell while placing the part for each selection on the schematic.

* fig17

Now add wires to the circuit using Add  Wire and use Add Pin to add an output pin on the
VOUT signal of the inverter so the schematic looks like figure 18 below. Don’t worry if your
values for vpulse and vsource don’t match up with figure 18 since we will be modifying them
next.

* fig18

By clicking on and selecting a component in schematic view, you can edit a component’s
property. You can also use Edit Properties  Property Editor to edit the properties of the
parts. Select vpulse and modify its properties as shown in Fig.19. Select vsource and modify its
properties as shown in Fig.19.

* fig19

Your final schematic should look like figure 18 above with the applied property edits for vpulse
and vsource. The circuit is now ready for simulation. Also don’t forget to save your schematic by
clicking or go to Design  Save.

## Part 3: Simulation and analysis

In SAE, we will run a DC sweep and a transient analysis.
To run SAE, go to Tools menu SAE in the schematic window. This will launch the window in
Fig. 20, which consists of three primary sections. Section one contains the design variables.
Section Two contains the values being measures in the circuit. Section three displays the types of
analysis being run. See figure 20 below for reference.

* fig20

To setup the model files, go to Setup  Models Files. A model files window will open as
shown in figure 21 below. Next click on section one as shown in figure 21 and browse the
directory and select the SAED90nm.lib file. You can find the file in the following directory:
/packages/process_kit/generic/generic_90nm/updated_oct2010/SAED_PDK90nm/hspice/SAED
90nm.lib
In section two of the model files window (see figure 21), select TT_12 as your transistor type. Click OK when done.

* fig21

Next to setup analysis type, go to Setup  Analysis and the window in figure 22 will appear.
Stay on the general tab and select tran to setup the transient analysis type. Setup the remaining
options as shown in figure 22 and click Apply.

* fig22

In the same window, select dc to setup a DC sweep. Fill out the options as shown in figure 23
below. Click OK when done.

* fig23

The following step is to choose the desired simulations results and select the nodes in the circuit
to measure. In section TWO of Fig: 20 do the following steps:
To setup the circuit output voltage:
1) Click under the output field, and write “Vout” or a name for an output variable of the
inverter.
2) Click under the expression column and choose the output node from the schematic. In
this case, click on and select the wire labeled “VOUT” as shown below in figure 24
in the schematic window. You can also write an equation that uses the values of some
nodes in that schematic.
3) Under analysis, select the type of analysis you want to run. In this case, select dc and
tran to run the transient and DC analysis for this variable.
To setup the circuit input voltage:
1) Click under the output field in a new row, and write “Vin” or a name for an input
variable of the inverter.
2) In the same row, click under the expression column and choose the input node from
the schematic. In this case, click on and select the wire labeled “VIN” as shown
below in figure 24 in the schematic window.
3) Under analysis, select the type of analysis you want to run. In this case, select dc and
tran to run the transient and DC analysis for this variable.
To setup the circuit source current:
1) Click under the output field in a new row, and write “isupply” or a name for a current
variable.
2) In the same row, click under the expression column and choose the voltage source
from the schematic. In this case, click on and select the voltage source labeled
“V5” as shown below in figure 24 in the schematic window. Notice that current is being
measure rather than voltage.
3) Under analysis, select the type of analysis you want to run. In this case, select dc and
tran to run the transient and DC analysis for this variable.
Afterwards, the SAE window should look something similar to figure 25 below. Note
that the expression values in figure 25 may not match with your values which is fine
since those are dependent on the names used in the schematic for the voltage sources and
wires.

* fig24

* fig25

Now save your simulation setups by going to Session  Save State. In the new window that
opens, select OpenAccess from the three main categories at the top and give a name for the
session in the name field. Click OK when done. See figure 26 below for reference.

* fig26

To run the simulation, go to Simulation  Netlist and Run. The status of simulation is reported
in Custom Designer Console window. If you see “Simulation completed successfully” it means
that your simulation is successfully done (Fig.27).

* fig27

After running simulation successfully, a WaveView window will open up. You can select the
type of analysis you want to view by selecting the respective tab in the bottom left corner of the
window.
For the transient analysis waveform, click the tran tab in the bottom left corner. See figure 28
for the transient analysis. For the DC sweep waveform, click the dc tab in the bottom left corner.
See figure 29 for the dc sweep analysis
You now have run transient and dc analysis successfully.

* fig28

* fig29

## Part 4: Waveforn and analysis

The measurement tool in the WaveView window provides many methods for measuring the
waveforms. Here is a list of several features and measurements you can do in WaveView:
Zooming In and Out:
To zoom in on your waveform, click to do a vertical or horizontal zoom by dragging a box
over the waveform with the mouse. Click to unzoom. Also you can press X for a full unzoom
of the waveform.
Grouping and Ungrouping Signals:
First off, it is handy to know how to group and ungroup waveforms in WaveView. See figure 30
for ungrouping waveforms and see figure 31 for grouping waveforms.

* fig30

* fig31

Delay Measurements of Vin and Vout at 50% to 50%:
To measure delay between the input and output signals of the inverter at 50% select the tran tab
in the bottom left hand corner of the WaveView window. Group the Vout and Vin waveforms
together so the two waves overlap each other (see figure 31 on how to group signals). Open the
measurement tool by going to Tools  Measurement… or by clicking in the WaveView
window. Click the All tab in the measurement tool window and fill out the options as shown
below in figure 32. Click Ok when done.

* fig32

After clicking Ok, a delay measurement box will appear on the waveform. Just drag the box to
the waveform you want to measure (in this case the Vin and Vout overlapping waveforms) and
the delay value will appear in the box. You can also drag the delay measurement box along
different valid points of the waveform to get more delay values. See figure 33 below for the
delay measurements box.

* fig33

Rise/Fall Time Measurements at 90% and 10% for Vout:
To measure fall and rise time, select the tran tab in the bottom left hand corner of the WaveView
window and ungroup all the waveforms as described in figure 30. Open the measurement tool by
going to Tools  Measurement… or by clicking in the WaveView window. Click the All
tab in the measurement tool window and fill out the options as shown below in figure 34. Click
Ok when done.

* fig34

After clicking Ok, a rise/fall measurement box will appear on the waveform. You can drag the
rise/fall measurement box along the Vout waveform to get the rising and falling delay times.
Notice that when the rise/fall measurement box shows a rising red curve the tool is measuring
rising delay time from 10% of the signal to 90% of the signal. Also when the rise/fall
measurement box shows a falling green curve the tool is measuring the falling delay time from
90% of the signal to 10% of the signal. See figure 35 for reference, it shows two measurement
boxes and zooms in on Vout.

* fig35

Average Current Measurement:
To measure average current, select the tran tab in the bottom left hand corner of the WaveView
window and ungroup all the waveforms as described in figure 30. Delete the Vout and Vin
waveforms so only the isupply waveform shows. You can delete a waveform by selecting its
name in the signal list on the left side of the WaveView window and pressing delete on the
keyboard and clicking ok. You can always recover these signals later by clicking Plot on the
SAE window.
Open the measurement tool by going to Tools  Measurement… or by clicking in the
WaveView window. Scroll down in the menu window on the left and then click on the Average
measurement within the Level submenu as shown in Figure 36. Click Ok when done.

* fig36

After clicking Ok, an average measurement box will appear on the waveform. Drag the box
toward the waveform until it displays the average value. See figure 37 below for reference.

* fig37

Frequency Measurement:
To measure frequency, select the tran tab in the bottom left hand corner of the WaveView
window and ungroup all the waveforms as described in figure 30.
Open the measurement tool by going to Tools  Measurement… or by clicking in the
WaveView window. Click the All tab in the measurement tool window and fill out the options as
shown below in figure 38. Click Ok when done.

* fig38

After clicking Ok, a frequency measurement box will appear on the waveform. Drag the box
toward the waveform you want to measure until it displays the frequency value. See figure 39
below for reference.

* fig39



## Lab1

### Objective

Lab 1 is to learn how to design your circuit, generate netlist, and simulate given netlist for your layout design in lab 2. You will learn three IC design tools (Custom Designer, Waveform View, HSPICE) in this lab and the followings are expected to be delivered in your lab report.

### Deliverables

* A circuit design for Inverter design
* A netlist of the Inverter design
* DC analysis (V_in vs V_out) and transient analysis for Inverter design
* The I-V curve for P-MOS and choose different for choose 4 different V_GS

### Due

*
