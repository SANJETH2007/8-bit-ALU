# 8-bit ALU in Verilog

A small, software-only digital design project for practicing RTL design and functional simulation. The ALU is combinational and accepts two 8-bit operands and a 3-bit operation selector.

## Operations

| `sel` | Operation | Result | `carry` |
|---|---|---|---|
| `000` | Addition | `A + B` truncated to 8 bits | Addition carry-out |
| `001` | Subtraction | `A - B` modulo 256 | Borrow (`A < B`) |
| `010` | AND | `A & B` | `0` |
| `011` | OR | `A \| B` | `0` |
| `100` | XOR | `A ^ B` | `0` |
| `101` | NOT | `~A` | `0` |
| `110` | Logical left shift by one | `A << 1` | `0` |
| `111` | Logical right shift by one | `A >> 1` | `0` |

The `zero` output is high when `result` is `8'b00000000`. `B` is unused by NOT and shift operations. Shift operations discard the shifted-out bit and leave `carry` low. The design has no clock or reset.

## Tools

- **Icarus Verilog** (`iverilog` and `vvp`) — compile and run the testbench.
- **GTKWave** — optional waveform viewer if you add VCD dumping to the testbench.
- **Yosys** — planned RTL synthesis step.
- **OpenSTA** — planned static timing analysis step.
- **OpenROAD or OpenLane with the SKY130 PDK** — planned physical-design flow.

Only the RTL and functional testbench are implemented in this starter. No synthesis, STA, or physical-design run has been completed.

## Run the simulation

Install Icarus Verilog for your operating system, then run one of these from the repository root.

### Windows PowerShell

```powershell
.\scripts\run_sim.ps1
```

### Linux or macOS

```sh
sh scripts/run_sim.sh
```

The scripts compile `rtl/alu.v` and `testbench/alu_tb.v`, then run a self-checking testbench. A successful run prints `PASS: all 13 ALU checks passed.` Build files are written under `build/`, which is ignored by Git.

To compile and run manually:

```sh
mkdir -p build
iverilog -g2012 -Wall -s alu_tb -o build/alu_sim rtl/alu.v testbench/alu_tb.v
vvp build/alu_sim
```

## Repository structure

```text
8-bit-alu-verilog-starter/
├── .gitignore
├── README.md
├── rtl/
│   └── alu.v
├── scripts/
│   ├── run_sim.ps1
│   └── run_sim.sh
└── testbench/
    └── alu_tb.v
```

## Implementation status

- **RTL simulation:** The starter includes a self-checking testbench for all eight operations, addition carry-out, subtraction borrow, zero results, and shift behavior. Run it locally with Icarus Verilog.
- **Synthesis:** Pending. No synthesized netlist or area report is included.
- **Static timing analysis (STA):** Pending. No constraints or timing report is included.
- **Physical design:** Pending. No floorplan, routed layout, or GDSII file is included.

Add real tool outputs to the repository only after running and reviewing the corresponding flow.
