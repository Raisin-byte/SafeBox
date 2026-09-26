# FPGA-Based Digital Safe Box with BCD Balance Management (Quartus Prime)

An end-to-end digital hardware system designed and simulated in Intel Quartus Prime, implementing a secure electronic safe lock with integrated financial balance bookkeeping using Binary-Coded Decimal (BCD) arithmetic.

Developed as part of the ECE-111: Digital System Lab curriculum at the University of Nicosia.

## 🛠️ Architecture & Core Modules

The system is structurally decoupled into three specialized sub-systems modeled via schematic capture and logic optimization:

### 1. Password Storage Block (Storage password)
* Sequential Logic: Implements 0-9 and 0-3 counters to sequentially capture digit inputs controlled via synchronized clock pulses (clk1, clk2).
* Bus Routing: Employs a 2-to-4 decoder paired with AND gating array to distribute data load pulses to 4 parallel registers, securely storing the full binary combination code.
* Control Flags: Features asynchronous global Reset lines to clear registers and overwrite data safely.

### 2. Access Control & Verification Block (Check the password)
* Combinational Verification: Utilizes multiple 4-bit hardware comparators executing bitwise validation of user-entered digits against active register states.
* State Control: Outputs comparison flags into a custom 4-input AND gate to generate the global UNLOCK status signal.
* Sequential Locking: Integrates a D Flip-Flop (DFF) to latch the lock/unlock state machine, robustly preventing glitching or unauthorized access during cycles.

### 3. BCD Arithmetic Balance Controller (Balance)
* BCD Computation: Features cascading BCD 4-bit adders managing financial deposit and withdrawal transactions.
* Mathematical Reliability: Implements hardware carry propagation logic to guarantee precise operations within BCD constraints, preventing invalid standard binary states (0xA to 0xF).

## 📊 Verification & Waveform Simulations

Functional validation was performed via Quartus Waveform Editor (VWF). High-fidelity simulations successfully verified:
* Sequential digit shifting and parallel register assignment for code entry (e.g., test vectors 1234).
* Deterministic locking mechanics when subjected to invalid passwords (e.g., brute-force test vectors 2348).
* Instantaneous global clearing upon triggering the Reset line.

## 📁 Repository Structure
* /src — Hardware schematic design files (.bdf) and block diagrams.
* /simulation — Vector Waveform Files (.vwf) demonstrating timing and state analysis.
* Digital_Safe_Box_Report.pdf — Complete 13-page engineering report detailing Karnaugh maps, truth tables, and full schematic maps.
