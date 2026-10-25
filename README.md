# FIFO Verification in SystemVerilog

**Status: work in progress.** The FIFO design (RTL) is written. The SystemVerilog testbench is being built step by step while I learn verification. This README is updated as each part is finished.

## Design under test (`fifo.v`)
A synchronous FIFO written in Verilog.

- Parameterized width and depth (default: 8-bit data, 32 entries; depth must be a power of 2)
- Separate write and read pointers, plus an occupancy counter that drives the `full` and `empty` flags
- Synchronous reset
- Registered read: read data appears one clock cycle after an accepted read
- A write while full and a read while empty are ignored

## Planned verification environment
`generator -> mailbox -> driver -> DUT -> monitor -> mailbox -> scoreboard`

- **Transaction:** randomized write enable, read enable and data, with constraints
- **Generator, driver, monitor:** connected through mailboxes
- **Scoreboard:** queue-based reference model that checks read data (accounting for the one-cycle read latency) and the full/empty flags
- **Assertions (SVA):** flag and protocol checks
- **Functional coverage:** covergroups for FIFO states and operations, including write-while-full and read-while-empty

## Progress
- [x] FIFO design (`fifo.v`)
- [ ] Interface with clocking blocks
- [ ] Transaction class (randomization and constraints)
- [ ] Generator and driver
- [ ] Monitor
- [ ] Scoreboard with reference model
- [ ] Assertions (SVA)
- [ ] Functional coverage
- [ ] Directed corner-case tests (fill completely, drain completely, read at empty, write at full, simultaneous read and write)
- [ ] UVM version

## Tools
Verilog (design), SystemVerilog (testbench), EDA Playground (simulator to be added once chosen)

## Results
Will be added after the testbench is running: transactions run, errors found, coverage percentage and a waveform screenshot.

## What I'm learning
Notes on problems I hit and how I fixed them will be added here.
