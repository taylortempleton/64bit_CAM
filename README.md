# 64-bit Content Addressable Memory

## Project Summary

Output: Create transistor-level schematic and mask-layout for 64-bit Content Addressable Memory (CAM), optimize for delay, power and area product.

Purpose: Build understanding of CAM function, physical design verifcation (pass DRC & LVS), and layout parasitic extraction (LPE).

Tools: Synopsys Custom Compiler, HSPICE,  StarRC, Linux, [NC State's 3nm FreePDK process design kit](https://eda.ncsu.edu/FreePDK/)


## Design Description
* CAMs are notable for allowing search of memory contents within a single clock cycle, specifying only search data. ("Is data 0x4a stored anywhere in memory?" "Yes, it is stored at address 2.")  The design needed to 1) write given test values to a given address and 2) return the correct memory address and a 'found' signal when searching for data stored in memory.
* Subunits
    * Bitcell: Unit cell storing data, created from cross coupled inverters.  The team selected a 10T NOR type bit cell, as described in Pagiamtzis et. al. 2006.
    * Row Decoder: Needed to decode the 3-bit write address to one of 8 row addresses. Dynamic NOR decoder.
    * Encoder/Found Logic: Needed to encode the 8 row addresses into a 8-bit found address.  3 4-bit OR gates used. 8-bit OR used to create 'found' logic, indicating a searched value is stored in memory.
    * Conditioners: Gate-clocked pmos transistors pull up matchlines, prior to search operation.
    * D Flip Flop: Needed to store final output steady for one clock cycle due to spec requirement.  True Single-Phase Clocked (TPSC) flip flops were used to avoid routing both clock phases. 

## Project Specs & Timing
1. 64 bit (8 bit x 8 bit) CAM
2. Inputs
    * WA<2:0> – write-address
    * WD<7:0> – write data
    * SD<7:0> – search data
    * WENB – write-enable bar (low = write, high = match)
    * CLK – clock
3. Outputs
    * MA<2:0> – match-address
    * FOUND – (high = match found, low = no match)
  
 ![](https://github.com/taylortempleton/64bit_CAM/blob/main/Docs/BlockDiagram_FinalReport.png)

## Schematics, Layouts, Waveforms & Statistics
![](https://github.com/taylortempleton/64bit_CAM/blob/main/Docs/CAM_Master_Layout.png)
![](https://github.com/taylortempleton/64bit_CAM/blob/main/Docs/STARRC_Output.png)

## Conclusions, Lessons Learned & Next Steps
1. Conclusions
* Area
* Density
* Energy
* EDA value:
3. Lessons Learned
* Design of sub-units needs to take into account integration.  The team had to redesign units during integration, because things like how buried power rail spacing was not considered.
3. Next steps
* Add true search conditioner
* Add advanced matchline conditioner
* Compare dynamic decoder to hierarchical decoder

## Sources & Team WorkLoad

| Team Member                | Actions            |
|----------------------|--------------------------------------|
| Benjamin Kubwimana         | Bitcell/array planning, schematic and lay-out. Encoder, matchline precharger and DFF layouts DRC and LVS pass checks, simulation and final report |
| Francis John       | Schematic for Encoder, DFF and Found logic. DFF layout DRC. Schematic simulation debug. Final Report |
| Taylor Templeton            | Schematics and layout for decoder, bitline and searchline drivers, Sub-unit layout integration, schematic and layout debug |

References
[1] K. Pagiamtzis and A. Sheikholeslami, "Content-addressable memory (CAM)
circuits and architectures: a tutorial and survey," in IEEE Journal of
Solid-State Circuits, vol. 41, no. 3, pp. 712-727, March 2006, doi:
10.1109/JSSC.2005.864128.
[2] Class notes “ECE 546” , Dr. W.R Davis.
