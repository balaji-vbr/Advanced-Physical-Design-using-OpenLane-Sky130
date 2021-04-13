# Advanced-Physical-Design-using-OpenLane-Sky130

The aim of this repository is to give an  experied during the VSD Advanced Physical Design workshop using OpenLANE.

OpenLANE is an automated RTL to GDSII flow based on several components which include OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor. It is a tool started for true open source tape-out experience. The goal of OpenLANE is to produce clean GDSII without any human intervention. OpenLANE is tuned for Skywater 130nm open-source PDK and can be used to produce hard macros and chips.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/openlane.flow.1.png" width = 900>

The total workshop is divided into 5 days with lab activities on each day as follows

*DAY 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK.* <br />
*DAY 2 - Good floorplan vs bad floorplan and introduction to library cells.* <br />
*DAY 3 - Design library cell using Magic Layout and ngspice characterization.* <br />
*DAY 4 - Pre-layout timing analysis and importance of good clock tree.* <br />
*DAY 5 - Final steps for RTL2GDS using tritonRoute and openSTA.*

Tools used in this workshop were:

Yosys – for logic Synthesis <br />
Graywolf – for Placement and floor planning <br />
Ngspice- for pre-layout and post-layout simulation <br />
Qrouter – for Routing <br />
TritonCTS - Synthesizes the clock distribution network <br />
TritonRoute - Performs detailed routing from global routing guides <br />
abc - Performs technology mapping to standard cells described in the PDK <br />
eSim - for schematic editor <br />
Netgen – for LVS <br />
Magic – for Layout and Floorplanning <br />
Qflow – RTL2GDS integration <br />
OpenSTA & Opentimer - for Pre-layout and Post-layout Static timing analysis <br />

## **DAY 1 : Inception of open-source EDA, OpenLANE and Sky130 PDK**


 There are three subdirectories needed for the workshop:
 
 1. Skywater-pdk <br />
 2. Open_pdks <br />
 3. Sky130A  <br />

### **LAB:**

For invoking the OpenLane "*./flow.tcl*" is the script which runs the OpenLANE flow. Various software dependencies are needed to run OpenLANE. To import these into the OpenLANE tool we need to run: "*package require openlane 0.9*".

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%201/Screenshot%20(109).png" width = 700>

After preparing the design to run synthesis simply type "*run_synthesis*". 

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%201/Screenshot%20(110).png" width = 700>

This is the summary of cells in the design after running the synthesis.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%201/Screenshot%20(111).png" width = 700>


## **DAY 2 : Good floorplan vs bad floorplan and introduction to library cells**

In Floorplanning we typically set the Die and Core Area, Aspect Ratio etc., we also place the input and output pins.Two key descriptions of a floorplan are utilization and aspect ratio. The amount of area of the die core the standard cells are taking up is called utilization. In floorplanning we define locations for preplaced cells. Blockages are needed to ensure no standard cells are mapped where the preplaced cells are located.
Decoupling capacitors are placed local to preplaced cells during Floorplanning. Voltage drops associated with interconnect wires can heavily affect our noise margin or put it into an indeterminate state. Decoupling capacitor is a big capacitor located next to the macros to fix this problem. 


The next step after floorplanning is placement. The synthesized netlist has been mapped to standard cells and floorplanning phase has determined the standard cells rows, enabling placement. OpenLANE does placement in two stages which are "Global Placement" and "Detailed Placement" . In global placement, all cells are placed on the floorplan in a random manner. In Detailed Placement it legalizes placement of cells.

### **LAB:**

After the synthesis step to run floorplan in openlane simly type "*run_floorplan*".  The output the the floorplan phase is a DEF file which describes core area and placement of standard cell.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%202/Screenshot%20(113).png" width = 700>

To view our floorplan in Magic we need to provide three files as input Magic technology file, DEF file of floorplan and Merged LEF file.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%202/Screenshot%20(114).png" width = 700>

To run the placement after the synthesis step simply type "*run_placement*". 

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%202/Screenshot%20(115).png" width = 700>

And finally to view the placement in Magic we need to again provide the same three files whic are imput magic technology file, DEF file of placement and Merged LEF file.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%202/Screenshot%20(116).png" width = 700>


## **DAY 3 :  Design library cell using Magic Layout and ngspice characterization**

16 Mask CMOS Process : In this process we'll be able to create a CMOS involving the following steps.

- Selecting the Substrate : <br />
  In this step we select the base layer on which other regions will be formed. <br />
- Creating an active region for transistors : <br />
  In this step SiO2 and Si3N2 are deposited on the substrate and pockets are created using photoresist and lithography. <br />
- Formation of Nwell & Pwell : <br />
  In this step Pwell and nwell are formed using boron and phosphorus then placed it in a high temperature furnace. <br />
- Creating Gate terminal : <br />
  In this step we create a gate terminal for desired threshold value. <br />
- Formation of Source and Drain : <br />
  In this step we form the source and drain. <br />
- Creating the contacts & local interconnect : <br />
  In this step we remove the SiO2 using HF etch. After this titanium deposited using sputtering. <br />
- Formation Higher Level metal layer  : <br />
  In the final step upper layers of metals are deposited. <br />

### **LAB:**

For using the inverter design mag file we need to clone the repo from the github link https://github.com/nickson-jose/vsdstdcelldesign and run MAGIC tool using the Skylane130A tech file and inverter mag file.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(117).png" width = 700>

Select the specific layer/device by hovering over the object and pressing, s, iteratively, until you traverse the hierarchy to the specified object

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(118).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(121).png" width = 700>

By typing the command "*what*" in the tckon window we'll get the info.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(120).png" width = 700>

To extract the parasitic spice file for the associated layout first we need to create an extraction file it is done by.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(122).png" width = 700>

To run the simulation with ngspice, invoke the ngspice tool with the spice file as input:

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(123).png" width = 700>

The plot can be viewed by plotting the output vs time while sweeping the input:

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(124).png" width = 700>



## **DAY 4 : Pre-layout timing analysis and importance of good clock tree**

Using the GDS files generated by Magic the Place and routing (PnR) is performed. The information metal and pin is included. The PnR tool will use this LEF information, to perform interconnect routing in conjunction to routing guides generated from the PnR flow. The LEF files includes layer information, via information, and restricted DRC rules.
Standard cell pin placement is essential for DRC free PnR flow. To ensure a cell is aligned with routing grids in Magic we can display a grid on top of the gds file.

To analyze a circuit's timing performance designers will use static timing analysis tools (STA). In the pre clock tree synthesis the setup time to lauch clock is the main concern. Fixing slack violations can be debugged through performing STA analysis with OpenSTA, which is integrated in the OpenLANE tool. For the design to be complete, the worst negative slack needs to be above or equal to 0. If the slack is not in this range we should optimize the fanout value with openlane tool.

### **LAB:**

To ensure the pins are aligned and the cell is aligned in the routing grid in Magic we can display a grid.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(125).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(126).png" width = 700>

After generating the cell LEF files to iclude them in the openlane we need to overwrite the previous run to include the new configuration. So the additional line to include the extra cell LEF is <br />

"*openLANE_flow/designs/picorv32a/src/sky130_vsdinv.lef*" <br />
 
 Then we need to run synthesis again to check the cell has been integrated successfully.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(128).png" width = 700>

The delay of this cell is very large due to a high load capacitance due to high fanout. To fix this problem we can re-run synthesis.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(129).png" width = 700>

After running floorplan and standard cell placement in OpenLANE we are ready to insert our clock tree for sequential elements in our design. <br />
To run Clock Tree Synthesis simply type "*run_cts*".

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(130).png" width = 700>

Now a new .def file is generated which contains information of our design after CTS is performed. To view this netlist we need to invoke the .def file with the Magic tool:

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(131).png" width = 700>

We can perform STA analysis from within OpenLANE by invoking OpenROAD. In OpenROAD the timing analysis is done by creating a .db database file. 

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(132).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(133).png" width = 700>

This database file is created from the post-cts LEF and DEF files. To generate the .db files within OpenROAD.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(136).png" width = 700>


## **DAY 5 : Final steps for RTL2GDS using tritonRoute and openSTA**

After generating the clock tree network and also verifying the post STA analysis now routing can be done. Now to buid the Power Distibution Network (PDN) simply type "*generate_pdn*". This pdn will create a Power ring global to the entire core, Power straps to bring power into the center of the chip and create power rails for the standard cells

### **LAB:**

Openlane uses triton route as main routing engine for the physical implementations of the design, which takes place in two stages "Global routing" and "Detailed routing"

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(137).png" width = 700>

To run routing in openlane simply type "*run_routing*" and wait this process takes some time to finish.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(138).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(139).png" width = 700>

Finally post routing interconnect parasitics can be extracted to perform post-route STA analysis. The parasitics are extracted into a SPEF file. The SPEF extractor is not included within OpenLANE as of now.

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(140).png" width = 700>



## **Acknowledgements**
Mr.[Kunal Ghosh](https://www.vlsisystemdesign.com/about-me/) Co-founder of [VLSI System Design Pvt. Ltd](https://www.vlsisystemdesign.com/).

Mr. Nickson Jose - Teaching Assistant.

Ms. Praharsha - Teaching Assistant.

Ms. Akurathi Radhika - Teaching Assistant.
