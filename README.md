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

## **DAY 1**

### **Inception of open-source EDA, OpenLANE and Sky130 PDK**

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


## **DAY 2**

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


## **DAY 3**

16 Mask CMOS Process : In this process we'll be able to create a CMOS involving the following steps.

Selecting the Substrate : In this step we select the base layer on which other regions will be formed. <br />
Creating an active region for transistors : In this step SiO2 and Si3N2 are deposited on the substrate and pockets are created using photoresist and lithography. <br />
Formation of Nwell & Pwell : In this step Pwell and nwell are formed using boron and phosphorus then placed it in a high temperature furnace. <br />
Creating Gate terminal : In this step we create a gate terminal for desired threshold value. <br />
Formation of Source and Drain : In this step we form the source and drain. <br />
Creating the contacts & local interconnect : In this step we remove the SiO2 using HF etch. After this titanium deposited using sputtering. <br />
Formation Higher Level metal layer  : In the final step upper layers of metals are deposited. <br />

### **LAB:**

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(117).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(118).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(120).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(121).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(122).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(123).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%203/Screenshot%20(124).png" width = 700>



## **DAY 4**

### **LAB:**

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(125).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(126).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(128).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(129).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(130).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(131).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(132).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(133).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%204/Screenshot%20(136).png" width = 700>


## **DAY 5**

### **LAB:**

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(137).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(138).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(139).png" width = 700>

<img src = "https://github.com/balaji-vbr/Advanced-Physical-Design-using-OpenLane-Sky130/blob/main/Images/DAY%205/Screenshot%20(140).png" width = 700>

