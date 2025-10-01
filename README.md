# apb_without_wait_states


**Project Overview**

This project implements a simple Advanced Peripheral Bus (APB) Master-Slave interface using Verilog. The design consists of:

**APB Master (apb_m)** – generates control signals, handles read/write operations.

**APB Slave (apb_s)** – responds to master requests, stores data in a small memory.

**Top Module (top)** – connects master and slave to demonstrate a working APB communication.

The design is fully synchronous with an active-low reset (rstn) and operates on a single clock (clk).

Modules
1. **APB Master (apb_m)**

States: idle, setup, enable

Inputs:

pclk – APB clock

presetn – Active-low reset

addrin[3:0] – Address to access in the slave

datain[7:0] – Data to write to the slave

wr – Write enable (1 = write, 0 = read)

newd – Indicates a new transaction request

prdata[7:0] – Data read from slave

pready – Slave ready signal

Outputs:

psel – Slave select

penable – Enable signal for APB transaction

paddr[3:0] – Address sent to slave

pwdata[7:0] – Write data to slave

pwrite – Write control signal

dataout[7:0] – Data read from slave

Functionality:

Waits in idle until newd is asserted.

Moves to setup state to prepare address/data.

Moves to enable to complete the APB transaction.

Handles both read and write operations.


2.**APB Slave (apb_s)**


States: idle, write, read

Inputs:

pclk, presetn – Clock and reset

paddr[3:0] – Address from master

psel – Slave select

penable – APB enable

pwdata[7:0] – Data from master

pwrite – Write enable

Outputs:

prdata[7:0] – Data read by master

pready – Indicates slave is ready

Functionality:

Stores data in an 8-bit memory array of 16 locations.

Handles write and read requests based on APB protocol.

Signals ready when the transaction is completed.

3. **Top Module (top)**

Purpose: Connects master and slave modules for simulation or synthesis.

Inputs:

clk – System clock

rstn – Active-low reset

wr – Write enable

newd – New data request

ain[3:0] – Address input

din[7:0] – Data input

Output:

dout[7:0] – Data output from slave (read operation)

Connections:

Master outputs (psel, penable, paddr, pwdata, pwrite) are connected to slave inputs.

Slave outputs (prdata, pready) are fed back to master.


**Design Features:**

Implements APB3-like protocol for easy learning and testing.

Fully synchronous with reset handling.

Modular design for master/slave separation.

Simple memory-mapped read/write transactions.
