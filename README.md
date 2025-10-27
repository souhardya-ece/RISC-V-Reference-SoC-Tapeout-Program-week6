# RISC-V-Reference-SoC-Tapeout-Program-week6
## Introduction
In a microcontroller board at thr center you have the processor/soc and the other thing is connected like direct I2C,QSPI,GPIO,PWM,JTAG-Uart FTDI,QSPI(ADC) flash,I2C EEPROM,Vcc,Gnd.Package is the broder term like QFN 48 quad flat no leads.Inside the package there is chip. Pad is the thing through which we send the signal inside or outside the chip. Core is inside the chip and the die is the size of the chip. For example a Riscv soc consists of gpio bank ,sram,adc,dac,pll(all are founder ip) and digital blocks are called macros.. Foundery is factory where the chip is manufactured. IP is the intelectual property it have some amout of inteligence to de the task.
## ISA(RISC V instruction set architechture)
C program -> RTL -> Layout
### FLOW
Application softaware -> System software(os)(C/C++->compiler->instruction set(architechture of computer)(hardware language(.exe file))->assembler->000101010101)-> RTL-> synthesize-> PD->Hardware(layout)4
## Element of ASIC
RTL ip(github), EDA tools(qflow), PDK data(interface bw fab and the designer)(sky 130nm)
### RTL to GDSII flow
RTL: synthesis-> floor/power planning -> placement : PDK :-> Clock tree synthesis-> Routing-> Sign off: GDSII 
Syhthesis:- RTL to CKt from standared cell library.
Floor/Power planning :- Chip , macro floor planning. Vdd/vss
Placement:- palce cells on floor (global and detail placement)
CTS:- deliver clk to each seq element.
Routing:- inteconnection by metal layer.
Signoff:- physical verification(DRC,LVS), timing verification(STA)

Openlane is a open source flow for tape out experiment to produce clean GDSII. It have the strive soc family.

First of all inside the virtual box you have the VDI of openlane . It is to be run on ubuntu 18 lts version.
### Labs
```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
exit
```
### Output
### Calculation
Flop Ratio=Number of dff/Total number of cells*100=1613/14876=0.1084*100=10.84%

## Floorplan
Netlist is the connectivity bw the component. Die is the smll sc material on that ckt is implemented.Inside the die it have the core where the fundamental logic is placed.
utilization factor=area of netlist/total area of the core.
Aspect ratio=Heigh of the core/Width of the core.
If any unit is uses multiple times then we separate out as a block(ip/module;-memory,mux,comparator) and intantiated muiltiple times. The arrengement of these ip is called floorplanning.These are called preplaced cells. Onec it is palced it cannot be moved.

Decoupling capacitor is place bw the elements if any changes happen from 0->1 it get charges (Vdd') and 1->0 It discharges(Vss') if it is not in the NMH and NML then the charges are provided/Suck by this capacitor.This is for one block.
Let say in bw the block it haappns If the bus are 1->0 there is ground bounce and 0->1 (Voltage droop) if one vdd is kept place if multiple vdd occurs then this problem is solved(so it can get power to the nearest supply)=> Power planning.
Pin(i/o) is placed bw the die and core and the remaining portion are filled so that no block and wire are not placed(logical cell placement bolckage)
### Floorplan Labs
```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
// to see the floorplan on the magic
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
### Output
### Calculation
According to floorplan def
1000 Unit Diatance = 1 Micron
Die width in Unit distance=660685
Die height in Unit distance =671405
Die width in micron=660685/1000=660.685 Microns
Die Height in microns=671407/1000=671.405 Microns
Die area=443587.212425 sq microns.

## Placement And Routing
Every gate and the flop have the sq,rect shape all are in the libery(shape and the time information) There are diff types of libery of diff falvours. We place the standared cell on floor on to the optimized place.Sometimes the blocks are far away(hich r and c) from source so in that case we use buffers(repeaters) which replicate same signal after some time.
### Placement Lab
```
run_placement
// now to see the placement in magic
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
exit
```
### Output


