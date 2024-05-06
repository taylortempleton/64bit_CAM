# 64-bit Content Addressable Memory

## Project Summary

Output: Create transistor-level schematic and mask-layout for 64-bit Content Addressable Memory (CAM), optimize for delay, power and area product.

Purpose: Build understanding of CAM function and design, physical design verifcation (pass DRC & LVS), and layout parasitic extraction (LPE).

Tools: Synopsys Custom Compiler, HSPICE,  StarRC, Linux, [NC State's 3nm FreePDK process design kit](https://eda.ncsu.edu/FreePDK/)


## Design Description
* CAMs are notable for allowing search of memory contents within one single clock cycle, specifying only the desired data. ("Is data 0x4a stored in memory?" "Yes, it is stored at address 2.")  The design needed to 1) write given test values to a given memory address and 2) when searching for a given value, return the correct memory address and a 'found' signal, indicating the search value was indeed stored in memory.
* Subunits
    * Bitcell: The team selected a 10T NOR type bit cell, as described in Pagiamtzis et. al. 2006.
    * Row Decoder: Dynamic NOR decoder.
    * Encoder/Found Logic: 3 4-bit gates used to create 8-to-3 bit encoder. 8-bit OR used to create 'found' logic.
    * Conditioners: ML pull up conditioners.
    * D Flip Flop: TPSC flip flops were used to avoid requiring 2 clock phases.
      
 ![](https://github.com/taylortempleton/64bit_CAM/edit/main/Docs/BlockDiagram_FinalReport.png)
  

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

## Schematics, Layouts, Waveforms & Statistics

## Lessons Learned & Next Steps

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
