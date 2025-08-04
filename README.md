# Verilog SPI Protocol Implementation

## Overview

This repository contains a Verilog implementation of the Serial Peripheral Interface (SPI) protocol using a Master-Slave communication model. The project includes Verilog code for the SPI module and a corresponding testbench for simulation and waveform verification.

## Features

- Implements SPI Master-Slave communication with 8-bit data transfer.
- Supports bidirectional data transmission: receives data via MOSI and transmits via MISO.
- Includes a clock divider to generate SPI clock from a 50 MHz system clock.
- LED indicators (via output ports) for visualizing state and data.
- Testbench generates waveform output using $dumpvars for verification.

## File Structure

├── tt_um_suba.v # Verilog code for SPI Master-Slave
├── tb.v # Testbench for SPI simulation
├── tb.vcd # VCD waveform output (generated after simulation)
├── README.md # Project Documentation


## Module Description

### SPI Module (tt_um_suba.v)

Implements the SPI protocol using a basic finite state machine (FSM) to handle data reception and transmission.

*Inputs:*

- clk: 50 MHz system clock.
- rst_n: Active-low reset.
- ena: Enable signal (kept high).
- ui_in[2:0]:  
  - ui_in[0]: Additional reset control.  
  - ui_in[1]: Chip Select (CS).  
  - ui_in[2]: MOSI (Master Out, Slave In).

*Outputs:*

- uo_out[0]: MISO (Master In, Slave Out).
- uo_out[1]: SPI clock output (for observation).
- uo_out[2]: Duplicate SPI clock.
- uo_out[7:3]: Unused, set to 0.

*Other Ports:*

- uio_in, uio_out, uio_oe: Not used, tied to zero for simplicity.

### Clock Divider

Generates SPI clock from the 50 MHz input clock to synchronize SPI communication.

## Testbench (tb.v)

Simulates SPI communication by sending two 8-bit data transactions and validating outputs through waveform analysis.

*Test Sequence:*

1. Apply reset.
2. Begin first SPI transaction: assert CS low, send 8-bit data over MOSI.
3. End transaction: de-assert CS.
4. Wait, then start second transaction with different 8-bit data.
5. Observe MISO and clock signals via waveform viewer .

## Simulation

To simulate the SPI module:

1. Use a Verilog simulator like  **Xilinx Vivado.
2. Run the testbench (tb.v) to verify correct functionality.
3. Use a waveform viewer  to open tb.vcd and inspect signal behavior (CS, MOSI, MISO, SPI Clock).

## Future Improvements

- Support for configurable clock division ratio.
- Extend to SPI multi-slave support.
- Parameterized data width.
- Enhanced FSM with interrupt or buffer support.
