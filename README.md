# AXI-Lite-Memory
SystemVerilog constrained-random verification environment for a 32-bit AXI4-Lite Memory Controller Slave IP. Features an OOP testbench (Generator, Driver, Monitor, Scoreboard) verified in Vivado XSim.
A 32-bit **AXI4-Lite Memory Controller Slave IP** accompanied by a class-based **SystemVerilog Object-Oriented Programming (OOP)** verification environment. The project validates write/read channel handshakes, memory storage integrity, response codes, and reset behavior using Constrained Random Verification (CRV).

---

## 📌 Features

* **Design Under Test (DUT):**
  * Fully compliant ARM AXI4-Lite Slave protocol interface.
  * 32-bit data and 32-bit address widths (word-addressable memory array).
  * Independent read and write channel control logic.
* **Verification Environment:**
  * Modular, class-based SystemVerilog OOP environment.
  * Automated **Scoreboard** with a dynamic golden reference model.
  * Constrained-random sequence generation for thorough protocol testing.
  * Pin-level driving and sampling via a SystemVerilog `virtual interface`.

---

## 🏗️ Verification Architecture

The testbench components communicate using SystemVerilog `mailbox` primitives and synchronize transaction processing across driver, monitor, and scoreboard stages:

```text
                    +---------------------------------------------------+
                    |              SystemVerilog Testbench              |
                    |                                                   |
+----------------+  |   +-----------+     +--------+     +-----------+  |
|                |  |   | Generator | --> | Driver | --> |           |  |
|                |  |   +-----------+     +--------+     |   AXI     |  |
| AXI4-Lite DUT  | <==>                       |          | Interface |  |
| (Memory Slave) |  VIF +------------+        v          | (axi_if)  |  |
|                |  |   | Scoreboard | <--- Monitor <--- |           |  |
|                |  |   +------------+                   +-----------+  |
+----------------+  +---------------------------------------------------+
