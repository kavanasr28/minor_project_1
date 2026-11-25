# 4-Bit Ripple Carry Adder (Verilog HDL)

RTL design and functional verification of a 4-bit ripple carry adder constructed hierarchically from 1-bit full adder modules in Verilog HDL.

## Repository Structure

| File | Description |
| :--- | :--- |
| `full_adder.v` | 1-bit full adder module computing sum and carry-out from three 1-bit inputs (`a`, `b`, `cin`). |
| `four_bit_adder.v` | Top-level 4-bit adder module instantiating four 1-bit full adders in a ripple-carry chain. |
| `tb_four_bit_adder.v` | Self-checking / stimulus testbench verifying addition across input combinations and carry propagation. |

## Architecture Overview

* **1-Bit Full Adder (`full_adder`):**
  * **Inputs:** `a`, `b`, `cin`
  * **Outputs:** `sum`, `cout`
  * **Logic:** $\text{sum} = a \oplus b \oplus c_{\text{in}}$, $\text{cout} = (a \cdot b) + (c_{\text{in}} \cdot (a \oplus b))$
* **4-Bit Adder (`four_bit_adder`):**
  * **Inputs:** `a[3:0]`, `b[3:0]`, `cin`
  * **Outputs:** `sum[3:0]`, `cout`
  * **Operation:** Cascades the `cout` of each bit stage into the `cin` of the next significant bit stage.

## Simulation & Verification

To compile and run the testbench using Icarus Verilog (`iverilog`) and GTKWave on Ubuntu:

```bash
iverilog -o adder_sim full_adder.v four_bit_adder.v tb_four_bit_adder.v
vvp adder_sim
gtkwave adder.vcd
