🚀 **APB Master-Slave Interface Project**

A Verilog-based APB Master-Slave interface demonstrating memory-mapped read/write operations with a simple FSM-based APB Master and a memory-based APB Slave.

🌟 **Project Overview**
This project implements a simple Advanced Peripheral Bus (APB) system:

APB Master (apb_m) – Generates control signals, performs read/write operations.

APB Slave (apb_s) – Stores data in memory, responds to master requests.

Top Module (top) – Connects Master and Slave for simulation or synthesis.

✅ Fully synchronous
✅ Active-low reset support
✅ APB3-like interface for learning and testing

📦 **Modules**
1️⃣ **APB Master (apb_m)**

States: idle → setup → enable

Inputs:

Signal	Description
pclk	APB clock
presetn	Active-low reset
addrin[3:0]	Address to access
datain[7:0]	Data to write
wr	Write enable (1=write, 0=read)
newd	Indicates a new transaction request
prdata[7:0]	Data from slave
pready	Slave ready

Outputs:

Signal	Description
psel	Slave select
penable	Enable for APB transaction
paddr[3:0]	Address to slave
pwdata[7:0]	Write data to slave
pwrite	Write control signal
dataout[7:0]	Data read from slave

Functionality:

Waits for newd=1 in idle state

Prepares transaction in setup state

Completes read/write in enable state

2️⃣ **APB Slave (apb_s)**

States: idle → write → read

Inputs:

Signal	Description
pclk, presetn	Clock and reset
paddr[3:0]	Address from master
psel	Slave select
penable	APB enable
pwdata[7:0]	Data from master
pwrite	Write enable

Outputs:

Signal	Description
prdata[7:0]	Data read by master
pready	Slave ready

Functionality:

16 × 8-bit memory storage

Handles read/write transactions per APB protocol

Signals ready when transaction completes

3️⃣ **Top Module (top)**

Purpose: Connects Master and Slave for simulation.

Inputs:

Signal	Description
clk	System clock
rstn	Active-low reset
wr	Write enable
newd	New data request
ain[3:0]	Address input
din[7:0]	Data input

Output:

Signal	Description
dout[7:0]	Data read from slave

Connections: Master outputs feed slave inputs; slave outputs feed master inputs.


🛠 **Simulation / Usage**

Instantiate top in a testbench.

Apply clk, rstn, wr, newd, ain, din.

Observe dout for read operations.

Use waveform viewers like GTKWave or ModelSim for debugging.

🎯 **Features**

Simple APB protocol simulation

Modular design: Master and Slave separate

Memory-mapped read/write support

Fully synchronous design with reset
