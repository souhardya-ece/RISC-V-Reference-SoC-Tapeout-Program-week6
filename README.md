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

First of all inside the virtual box you have the VDI of openlane . It is to be run on ubuntu 18 lts version. Whenevere you working you are on cd ~/Deaktop/work/tools/openlane_working_dir/openlane directory



