# VSDBabySoC: Complete Design Flow

## Introduction: VSDBabySoC Overview

VSDBabySoC is a compact, educational SoC integrating RVMYTH (RISC-V CPU), high-multiplication PLL, and a 10-bit DAC. Its key aim is reliable digital-analog integration and IP calibration for comprehensive hardware experimentation.

## System Details and Components

- **RVMYTH**: RISC-V CPU for digital processing.
- **PLL**: 8x multiplier Phase-Locked Loop for clock stability.
- **DAC**: 10-bit precision Digital-to-Analog Converter for external analog interfacing.

<img width="1248" height="698" alt="image" src="https://github.com/user-attachments/assets/251c13e7-a06f-4ff9-a137-ac15bf674a56" />
 
  

***

## Problem Statement

This guide develops a diminutive open-source SoC allowing digital RISC-V computation, robust clocking, and direct analog interfacing for TV/mobile applications via Sky130 technology. The documentation focuses on hands-on learning and practical verification.

***

## Essential Concepts

- **SoC Definition**: A chip integrating digital/analog IPs for versatile embedded tasks.
- **RVMYTH**: Educational RISC-V CPU core for small-scale applications.
- **PLL**: Synchronizes and stabilizes system clock signals.
- **DAC**: Translates digital outputs to analog signals for real-world devices.

***

## Directory and Project Structure

```txt
VSDBabySoC/
├── src/
│   ├── include/
│   └── module/
└── output/
└── compiled_tlv/
```

***

## Environment Setup and Repository Cloning

To start, prepare the workspace and clone the project:

```bash
mkdir VLSI
cd ~/VLSI
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
ls src/module/
```
<img width="817" height="401" alt="image" src="https://github.com/user-attachments/assets/7c9f22b0-dd3e-4862-b5db-19103d030d5b" />

Verify the presence of essential modules in the directory.

***

## TLV-to-Verilog Conversion for RVMYTH

Convert TL-Verilog to Verilog for simulation as follows:

```bash
# Step 1: Install python3-venv (if not already installed)
sudo apt update
sudo apt install python3-venv python3-pip

# Step 2: Create and activate a virtual environment
cd ~/VLSI/VSDBabySoC/
python3 -m venv sp_env
source sp_env/bin/activate

# Step 3: Install SandPiper-SaaS inside the virtual environment
pip install pyyaml click sandpiper-saas

# Step 4: Convert rvmyth.tlv to Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/

# Step 5: Deactivate the environment
deactivate
```
## Log
```bash
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ python3 -m venv sp_env
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ source sp_env/bin/activate
(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ pip install pyyaml click sandpiper-saas
Collecting pyyaml
  Using cached pyyaml-6.0.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl.metadata (2.4 kB)
Collecting click
  Using cached click-8.3.0-py3-none-any.whl.metadata (2.6 kB)
Collecting sandpiper-saas
  Using cached sandpiper_saas-1.1.0-py3-none-any.whl.metadata (1.7 kB)
Collecting Path (from sandpiper-saas)
  Using cached path-17.1.1-py3-none-any.whl.metadata (6.5 kB)
Collecting argparse (from sandpiper-saas)
  Using cached argparse-1.4.0-py2.py3-none-any.whl.metadata (2.8 kB)
Collecting requests (from sandpiper-saas)
  Using cached requests-2.32.5-py3-none-any.whl.metadata (4.9 kB)
Collecting charset_normalizer<4,>=2 (from requests->sandpiper-saas)
  Using cached charset_normalizer-3.4.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl.metadata (36 kB)
Collecting idna<4,>=2.5 (from requests->sandpiper-saas)
  Using cached idna-3.10-py3-none-any.whl.metadata (10 kB)
Collecting urllib3<3,>=1.21.1 (from requests->sandpiper-saas)
  Using cached urllib3-2.5.0-py3-none-any.whl.metadata (6.5 kB)
Collecting certifi>=2017.4.17 (from requests->sandpiper-saas)
  Using cached certifi-2025.8.3-py3-none-any.whl.metadata (2.4 kB)
Using cached pyyaml-6.0.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (807 kB)
Using cached click-8.3.0-py3-none-any.whl (107 kB)
Using cached sandpiper_saas-1.1.0-py3-none-any.whl (5.3 kB)
Using cached argparse-1.4.0-py2.py3-none-any.whl (23 kB)
Using cached path-17.1.1-py3-none-any.whl (23 kB)
Using cached requests-2.32.5-py3-none-any.whl (64 kB)
Using cached certifi-2025.8.3-py3-none-any.whl (161 kB)
Using cached charset_normalizer-3.4.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (151 kB)
Using cached idna-3.10-py3-none-any.whl (70 kB)
Using cached urllib3-2.5.0-py3-none-any.whl (129 kB)
Installing collected packages: argparse, urllib3, pyyaml, Path, idna, click, charset_normalizer, certifi, requests, sandpiper-saas
Successfully installed Path-17.1.1 argparse-1.4.0 certifi-2025.8.3 charset_normalizer-3.4.3 click-8.3.0 idna-3.10 pyyaml-6.0.3 requests-2.32.5 sandpiper-saas-1.1.0 urllib3-2.5.0
(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
You have agreed to our Terms of Service here: https://makerchip.com/terms.
INFORM(0) (PROD_INFO):
	SandPiper(TM) 1.14-2022/10/10-beta-Pro from Redwood EDA, LLC
	(DEV) Run as: "java -jar sandpiper.jar --bestsv --noline -p verilog --outdir=out --nopath -i ./rvmyth.m4out.tlv -o rvmyth.v
	For help, including product info, run with -h.

INFORM(0) (LICENSE):
	Licensed to "Redwood EDA, LLC" as: Full Edition.

INFORM(0) (FILES):
	Reading "./rvmyth.m4out.tlv"
	to produce:
		Translated HDL File: "out/rvmyth.v"
		Generated HDL File: "out/rvmyth_gen.v"

(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ 
```

```txt
ls src/module/
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module$ ls
avsddac.v   pseudo_rand_gen.sv  rvmyth.tlv                       testbench.v
avsdpll.v   pseudo_rand.sv      rvmyth.v                         vsdbabysoc.v
clk_gate.v  rvmyth_gen.v        testbench.rvmyth.post-routing.v
```

***

## Simulation Workflow

### Pre-Synthesis Simulation Steps

Setup output directory and run simulation:

```bash
cd ~/VLSI/VSDBabySoC/
mkdir -p output/pre_synth_sim
iverilog -o /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/testbench.v
```
<img width="814" height="650" alt="image" src="https://github.com/user-attachments/assets/dd0d6ec9-1f74-44fc-ad73-e1264f20a65d" />
***

### Waveform Analysis in GTKWave

Open the VCD file for signal visualization:

```bash
cd output/pre_synth_sim
./pre_synth_sim.out
```

### Simulation Log

[Read Here](https://github.com/Pathan-Rehman/PathanRehman_RISC-V-SoC-Tapeout-Program_VSD_Week_2/blob/main/Lab/SimulationLog.md)

### Waveform Viewing
```bash
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```
Drag relevant signals: CLK, reset, OUT (DAC), RV_TO_DAC[9:0].

<img width="1052" height="615" alt="image" src="https://github.com/user-attachments/assets/8191efa5-2070-41d8-9cd4-0b03922b8feb" />
 
This screenshot highlights the correct toggling behavior of the clock (periodic changes), the response to reset (initialization phase), and propagation of digital OUT and RV_TO_DAC values through the simulation cycle. This shows functional correctness and timing relationships between the components.

The signals shown in the figure are described as follows:  
- **CLK**: The clock input to the RVMYTH core, originally generated by the PLL.  
- **reset**: The reset input signal for the RVMYTH core, sourced externally.  
- **OUT**: The output signal from the VSDBabySoC module's DAC. Due to simulation limitations, this behaves digitally, which is not an accurate reflection of its true analog nature.  
- **RV_TO_DAC[9:0]**: The 10-bit output port from the RVMYTH core, which corresponds to the value stored in register #17.  
- **OUT (real datatype)**: A real-valued wire representing the DAC's analog output, which can be viewed by changing the signal's data format in the simulator to Analog → Step.

***

### DAC Analog Output Verification

Switch DAC OUT signal to analog mode in GTKWave.

<img width="960" height="779" alt="image" src="https://github.com/user-attachments/assets/a526d61b-9f98-49eb-9561-5bb16d7f7585" />


<img width="1056" height="608" alt="image" src="https://github.com/user-attachments/assets/d6bceaab-5181-4f01-b51b-599c29919774" />

 
Here, OUT (DAC) is displayed in analog step mode. The waveform confirms that digital values from RV_TO_DAC are correctly converted and output as stepped analog signals—demonstrating successful digital-to-analog interfacing in the BabySoC simulation.

This screenshot further illustrates sustained analog output transitions, showing smooth conversion and verification of 10-bit DAC resolution, vital for confirming signal fidelity.

***

## Troubleshooting

- **Module Redefinition Errors**: Avoid duplicating module includes.
- **Path Resolution Failures**: Double-check -I flags and explicit paths.

***

# Yosys Synthesis Tutorial for BabySoC

## Overview

This guide demonstrates the synthesis process of the BabySoC project using the Yosys Open SYnthesis Suite. It covers command usage, the correct handling of file paths, and provides solutions for common synthesis errors.

***

## Directory Structure

Make sure the following project structure is set up:

```
~/Desktop/labs/Week2/VLSI/VSDBabySoC/
├── src/
│   ├── include/           # Verilog include files
│   ├── module/            # Verilog modules (vsdbabysoc.v, clkgate.v, rvmyth.v, etc)
│   └── lib/               # Liberty files (sky130fdschdtt025C1v80.lib, avsddac.lib, avsdpll.lib)
```
All paths provided in commands below match those seen in actual flows.

***

## Step-by-Step Synthesis Flow

### 1. Launch Yosys

Start Yosys from your working directory:

```sh
cd ~/Desktop/labs/Week2/VLSI/VSDBabySoC/src
yosys
```

***

### 2. Load Liberty Cell Libraries

Load the technology cell library (example for Sky130):

```yosys
read_liberty -lib /home/vsdtapeout/Desktop/labs/Week_1/Day_1/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsddac.lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsdpll.lib
```
<img width="822" height="610" alt="image" src="https://github.com/user-attachments/assets/09e61736-eae1-402f-879f-b65297e6f0e1" />

If the library contains definitions, you should see "Imported XXX cell types from liberty file".

***

### 3. Read Verilog Source Files

Indicate SV (SystemVerilog) support and all include/module paths. Avoid typographical errors in commands or filenames:

```yosys
read_verilog -sv -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include/ -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoc/src/module/ /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/vsdbabysoc.v /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/clk_gate.v /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/rvmyth.v
```
<img width="823" height="609" alt="image" src="https://github.com/user-attachments/assets/22ea9913-9278-4f4b-893d-068893e53331" />

The above paths must exist; adjust them as per your actual directory. If successful, you'll see "Successfully finished Verilog frontend".

***

### 4. Specify the Top Module

Set the top-level module for synthesis (usually `vsdbabysoc`):

```yosys
synth -top vsdbabysoc
```
<img width="827" height="789" alt="image" src="https://github.com/user-attachments/assets/ac6fbf92-d994-4b22-b39b-270372b875fa" />

This will trigger module hierarchy and process netlist conversion with messages such as "Analyzing design hierarchy... Top module Used module..." and "Creating decoders for process...".

***

### 5. Technology Mapping

Map RTL to gates using ABC and techmap:

```yosys
# Automatic, as part of 'synth'
```
Expect log reports with extracted gate counts and optimized modules (e.g., "Extracted 4089 gates and 5280 wires to a netlist network with 1188 inputs and 216 outputs").

***

### 6. Run Design Checks

```yosys
check
```
<img width="603" height="212" alt="image" src="https://github.com/user-attachments/assets/4a70ce88-d118-40e6-a099-60826a35abfb" />

This checks for obvious structural problems in your synthesized design.

***

### 7. Write the Synthesized Netlist

Export your final synthesized Verilog netlist:

```yosys
write_verilog vsdbabysoc_synth_net.v
abc -liberty /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 

```
Netlist files are typically written in the working directory.

***

### 8. Visualize the Synthesized Design

For visual inspection, use:

```yosys
show vsdbabysoc
```
<img width="1050" height="310" alt="image" src="https://github.com/user-attachments/assets/d6b5d48d-8936-47f4-8fd6-ebf0c63b0881" />
If multiple modules are present, specify only one module due to Graphviz format limitations ("ERROR: For formats different than 'ps' or 'dot' only one module must be selected"). By default, results are stored in `/home/vsdtapeout/.yosys_show.dot`.

***

## Common Errors & Solutions

| Error Message | Cause | Solution |
|---------------|-------|----------|
| `ERROR Missing function on output GCLK of cell ...` | Liberty file lacks function definition for some output | Fix .lib file or use correct version |
| `ERROR syntax error, unexpected TOKID ...` | File is not valid Verilog/SystemVerilog | Check syntax using a simulator (Icarus Verilog recommended) |
| `ERROR Cant open input file ... for reading No such file or directory` | File path typo, or file missing | Double-check directory and filenames |
| `ERROR Re-definition of module ...` | Module loaded twice | Ensure each file is loaded only once |
| `ERROR Cant open include file ...` | Include file missing or path wrong | Verify/include directory and file names |
| `ERROR Command syntax error No filename given.` | Syntax error in Yosys command | Follow documented syntax, use help |
| `WARNING: Font family 'Times-Roman' is not available, using 'Ubuntu Sans 11'` | Graphviz font not installed | Usually not fatal, just an info message |

***

## Tips for Successful Synthesis

- Validate Verilog modules in a simulator before Yosys synthesis to catch subtle syntax issues (Yosys parser is not very descriptive for errors).
- Always use absolute paths for scripts to avoid directory confusion.
- Organize modules, includes, and libraries separately for clarity.
- Read the log output for warnings about memory/register transformations or dead code removal.
- Use `check` for sanity of final netlist before downstream tools.

***

# Post-Synthesis of VSDBabySoC

***

## 1. Launch Yosys

```bash
yosys
```

Start the Yosys synthesis tool. This opens the Yosys interactive shell where you can enter synthesis commands.

<img width="814" height="605" alt="image" src="https://github.com/user-attachments/assets/fd430366-995c-463a-a9fe-f9f8cb1ea421" />

***

## 2. Read the Main Verilog Module

```bash
read_verilog /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/vsdbabysoc.v
```

This command loads the main Verilog source file of your design into Yosys. It parses the RTL code and converts it into Yosys's internal representation.

<img width="822" height="237" alt="image" src="https://github.com/user-attachments/assets/5e82492f-1a75-41d7-838a-afda9357fe8a" />

***

## 3. Read Additional Verilog Modules with Include Paths

```bash
read_verilog -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include/ /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/rvmyth.v

read_verilog -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include/ /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/clk_gate.v
```

These commands load additional Verilog modules required by your design. The `-I` option specifies the directory for included files (like headers or macros). This ensures all dependencies are resolved.

<img width="820" height="615" alt="image" src="https://github.com/user-attachments/assets/9292c8a5-3f46-4a7a-9c36-08f2fe40d4b4" />


***

## 4. Load Liberty Cell Libraries

```bash
read_liberty -lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsdpll.lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsddac.lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

This command loads the standard cell libraries in Liberty format. These libraries contain timing, power, and area information for the cells used in synthesis and technology mapping.

<img width="818" height="613" alt="image" src="https://github.com/user-attachments/assets/0813d972-0245-4872-a203-04fae198b871" />

***

## 5. Synthesize the Design with Top Module

```bash
synth -top vsdbabysoc
```

This runs the generic synthesis process on the design, targeting the specified top module `vsdbabysoc`. It performs RTL elaboration, optimization, and prepares the design for mapping to standard cells.

<img width="817" height="616" alt="image" src="https://github.com/user-attachments/assets/8403593b-d50a-4c5f-b4d9-010010020fa6" />

***

## 6. Map Flip-Flops to Standard Cells

```bash
dfflibmap -liberty /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

This step maps all flip-flops in the design to the flip-flop cells defined in the Liberty library. It ensures the flip-flops are technology-specific and compatible with the target process.

<img width="815" height="612" alt="image" src="https://github.com/user-attachments/assets/c960d730-95f5-4a1b-822f-c9841b9d9a94" />

***

## 7. Technology Mapping and Optimization with ABC

```bash
abc -liberty /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib -script +strash;scorr;ifraig;retime{D};strash;dch,-f;map,-M,1{D}
```

This command invokes the ABC tool integrated in Yosys for advanced logic optimization and technology mapping. The script applies a sequence of transformations:

- `+strash`: Structural hashing to reduce logic.
- `scorr`: Structural correlation.
- `ifraig`: Iterative functional reduction.
- `retime{D}`: Retiming to optimize registers.
- `dch,-f`: Don't care optimization.
- `map,-M,1{D}`: Map logic to standard cells with specific constraints.

This step improves area, timing, and power characteristics.

<img width="820" height="615" alt="image" src="https://github.com/user-attachments/assets/4792df63-fb6b-4a06-b789-42c76f4cd0b9" />

***

## 8. Flatten the Hierarchy

```bash
flatten
```

This command removes all module hierarchy, producing a flat netlist. Flattening simplifies the design for downstream tools like place-and-route but can make debugging harder.

<img width="462" height="163" alt="image" src="https://github.com/user-attachments/assets/ad77fe72-c1ee-427b-9d9e-e8c552fff8a6" />


***

## 9. Set Undefined Signals to Zero

```bash
setundef -zero
```

This replaces any undefined signals in the design with constant zero. This avoids simulation or synthesis issues caused by unknown values.

<img width="760" height="88" alt="image" src="https://github.com/user-attachments/assets/c8cfe015-6bcc-419d-a86c-35254b75f0c7" />

***

## 10. Clean Unused Wires and Cells

```bash
clean -purge
```

This removes any unused wires, cells, or logic from the design, reducing netlist size and complexity.

<img width="491" height="75" alt="image" src="https://github.com/user-attachments/assets/b4f0874c-6830-482f-83e3-30e2175f01b6" />


***

## 11. Rename Nets and Cells for Readability

```bash
rename -enumerate
```

This renames nets and cells with simple enumerated names (e.g., `net1`, `cell2`) to make the netlist easier to read and analyze.


***

## 12. Print Synthesis Statistics

```bash
stat
```

This command prints statistics about the synthesized design, such as the number of wires, cells, and memory elements. It helps verify the synthesis results.

<img width="390" height="274" alt="image" src="https://github.com/user-attachments/assets/a6371a64-9fd4-438e-b725-bf4b1c387029" />

***

## 13. Write the Synthesized Verilog Netlist

```bash
write_verilog -noattr /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/vsdbabysoc.synth.v
```

This exports the final synthesized netlist to a Verilog file without any synthesis attributes (`-noattr`). This netlist is technology-mapped and optimized, ready for place-and-route or further analysis.

<img width="809" height="194" alt="image" src="https://github.com/user-attachments/assets/0f499bf1-e1b7-4c5d-a283-fecc76555dd7" />

***

# Post Synthesis Simulation and Waveforms

## Compile the Testbench

Before running the iverilog command, copy the necessary standard cell and primitive models: These files must be present in the same directory as the testbench (src/module) to resolve all module references during compilation.

To ensure that the synthesized Verilog file (vsdbabysoc.synth.v) is available in the src/module directory for further processing or simulation, you can copy it from the output directory to the src/module directory. Here is the step to do that:

Run the following iverilog command to compile the testbench:

```bash
iverilog -o /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/output/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include/ -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/ /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/testbench.v
```

| **Option / Argument**                                                      | **Purpose / Description**                                                            |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `iverilog`                                                                 | Icarus Verilog compiler used to compile Verilog files into a simulation executable.  |
| `-o /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/output/post_synth_sim.out` | Specifies the output binary file for simulation.                                     |
| `-DPOST_SYNTH_SIM`                                                         | Defines the macro `POST_SYNTH_SIM` (used in testbench to switch simulation modes).   |
| `-DFUNCTIONAL`                                                             | Defines `FUNCTIONAL` to use behavioral models instead of detailed gate-level timing. |
| `-DUNIT_DELAY=#1`                                                          | Assigns a unit delay of `#1` to all gates for post-synthesis simulation.             |
| `-I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include`                              | Adds the `include` directory to the search path for `\`include\` directives.         |
| `-I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module`                               | Adds the `module` directory to the include path for additional module references.    |
| `/home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/testbench.v`                      | Specifies the testbench file as the top-level design for simulation.                 |

#### ❗Note - You may encounter this error:
```bash
$ iverilog -o /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/testbench.v
/home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/sky130_fd_sc_hd.v:74452: syntax error
I give up.
```
_To resolve this : Update the syntax in the file sky130_fd_sc_hd.v at or around line 74452._

###### Change:
```bash
`endif SKY130_FD_SC_HD__LPFLOW_BLEEDER_FUNCTIONAL_V
```
###### To:
```bash
`endif // SKY130_FD_SC_HD__LPFLOW_BLEEDER_FUNCTIONAL_V
```
### **Step 2: Navigate to the Post-Synthesis Simulation Output Directory**
```bash
cd output/
```
---
### **Step 3: Run the Simulation**

```bash
./post_synth_sim.out
```
<img width="808" height="291" alt="image" src="https://github.com/user-attachments/assets/a8056627-e4c5-4c6f-8f2a-4bea01418cb9" />
---

### **Step 4: View the Waveforms in GTKWave**

```bash
gtkwave post_synth_sim.vcd
```
---

<img width="1051" height="580" alt="image" src="https://github.com/user-attachments/assets/9976a3b2-b160-4be5-bb9c-c7b31ca23f61" />

## Comparing Pre-Synthesis and Post-Synthesis Output

To ensure that the synthesis process did not alter the original design behavior, the output from the pre-synthesis simulation was compared with the post-synthesis simulation.

Both simulations were run using GTKWave, and the resulting waveforms were observed.

<img width="1051" height="562" alt="image" src="https://github.com/user-attachments/assets/1aefb89d-70b5-4ad8-81b2-4fd186aa5e9d" />

<img width="1051" height="580" alt="image" src="https://github.com/user-attachments/assets/9976a3b2-b160-4be5-bb9c-c7b31ca23f61" />

✅ _The outputs match exactly, confirming that the functionality is preserved across the synthesis flow._

_This validates that the synthesized netlist is functionally equivalent to the RTL design._

# VSDBabySoC basic timing analysis

## Prepare Required Files

To begin static timing analysis on the VSDBabySoC design, you must organize and prepare the required files in specific directories.

```bash
# Create a directory to store Liberty timing libraries
vsdtapeout@pathanrehman:~/Desktop/labs/Week3$ mkdir -p examples/timing_libs/
vsdtapeout@pathanrehman:~/Desktop/labs/Week3$ ls timing_libs/
avsddac.lib  avsdpll.lib  sky130_fd_sc_hd__tt_025C_1v80.lib
vsdtapeout@pathanrehman:~/Desktop/labs/Week3$ mkdir -p examples/BabySoC
vsdtapeout@pathanrehman:~/Desktop/labs/Week3$ ls BabySoC/
vsdbabysoc_synthesis.sdc  vsdbabysoc.synth.v
```
These files include:

Standard cell library: sky130_fd_sc_hd__tt_025C_1v80.lib

IP-specific Liberty libraries: avsdpll.lib, avsddac.lib

Synthesized gate-level netlist: vsdbabysoc.synth.v

Timing constraints: vsdbabysoc_synthesis.sdc

## Run the script Using Docker

To run this script interactively using Docker:

```bash
docker run -it -v /home/vsdtapeout/Desktop/labs/Week3/examples/BabySoC:/data opensta
```

Below is the TCL script to run complete min/max timing checks on the SoC:

```vsdbabysoc_min_max_delays.tcl
# Load Liberty Libraries (standard cell + IPs)
read_liberty -min /data/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max /data/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib

read_liberty -min /data/timing_libs/avsdpll.lib
read_liberty -max /data/timing_libs/avsdpll.lib

read_liberty -min /data/timing_libs/avsddac.lib
read_liberty -max /data/timing_libs/avsddac.lib

# Read Synthesized Netlist
read_verilog /data/BabySoC/vsdbabysoc.synth.v

# Link the Top-Level Design
link_design vsdbabysoc

# Apply SDC Constraints
read_sdc /data/BabySoC/vsdbabysoc_synthesis.sdc

# Generate Timing Report
report_checks
```

<img width="848" height="889" alt="image" src="https://github.com/user-attachments/assets/f18e8dd0-16b2-49b6-829c-f12fca9810a6" />


## ⚠️ Possible Error Alert

You may encounter the following error when running the script:

```bash
Warning: /data/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 23, default_fanout_load is 0.0.
Warning: /data/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 1, library sky130_fd_sc_hd__tt_025C_1v80 already exists.
Warning: /data/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 23, default_fanout_load is 0.0.
Error: /data/timing_libs/avsdpll.lib line 54, syntax error
```

## ✅ Fix:

This error occurs because Liberty syntax does not support // for single-line comments, and more importantly, the { character appearing after // confuses the Liberty parser. Specifically, check around line 54 of avsdpll.lib and correct any syntax issues such as:

```bash
//pin (GND#2) {
//  direction : input;
//  max_transition : 2.5;
//  capacitance : 0.001;
//}
```

## ✔️ Replace with:

```bash
/*
pin (GND#2) {
  direction : input;
  max_transition : 2.5;
  capacitance : 0.001;
}
*/
```

<img width="665" height="553" alt="image" src="https://github.com/user-attachments/assets/cd4c9b51-0f5d-48ed-a485-c3cec09c5f65" />


This should allow OpenSTA to parse the Liberty file without throwing syntax errors.

After fixing the Liberty file comment syntax as shown above, you can rerun the script to perform complete timing analysis for VSDBabySoC:

<img width="829" height="585" alt="image" src="https://github.com/user-attachments/assets/163320f6-71d4-4f3a-b257-2d80924613a6" />

### VSDBabySoC PVT Corner Analysis (Post-Synthesis Timing)
Static Timing Analysis (STA) is performed across various **PVT (Process-Voltage-Temperature)** corners to ensure the design meets timing requirements under different conditions.

### Critical Timing Corners

**Worst Max Path (Setup-critical) Corners:**
- `ss_LowTemp_LowVolt`
- `ss_HighTemp_LowVolt`  
_These represent the **slowest** operating conditions._

**Worst Min Path (Hold-critical) Corners:**
- `ff_LowTemp_HighVolt`
- `ff_HighTemp_HighVolt`  
_These represent the **fastest** operating conditions._

 **Timing libraries** required for this analysis can be downloaded from:  
🔗 [Skywater PDK - sky130_fd_sc_hd Timing Libraries](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing)

Below is the script that can be used to perform STA across the PVT corners for which the Sky130 Liberty files are available.

<details>
<summary><strong>sta_across_pvt.tcl</strong></summary>

```shell
 set list_of_lib_files(1) "sky130_fd_sc_hd__tt_025C_1v80.lib"
 set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v65.lib"
 set list_of_lib_files(3) "sky130_fd_sc_hd__ff_100C_1v95.lib"
 set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
 set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
 set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
 set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
 set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
 set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
 set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
 set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
 set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
 set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v76.lib"

 read_liberty /data/timing_libs/avsdpll.lib
 read_liberty /data/timing_libs/avsddac.lib

 for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
 read_liberty /data/timing_libs/$list_of_lib_files($i)
 read_verilog /data/BabySoC/vsdbabysoc.synth.v
 link_design vsdbabysoc
 current_design
 read_sdc /data/BabySoC/vsdbabysoc_synthesis.sdc
 check_setup -verbose
 report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > /data/BabySoC/STA_OUTPUT/min_max_$list_of_lib_files($i).txt

 exec echo "$list_of_lib_files($i)" >> /data/BabySoC/STA_OUTPUT/sta_worst_max_slack.txt
 report_worst_slack -max -digits {4} >> /data/BabySoC/STA_OUTPUT/sta_worst_max_slack.txt

 exec echo "$list_of_lib_files($i)" >> /data/BabySoC/STA_OUTPUT/sta_worst_min_slack.txt
 report_worst_slack -min -digits {4} >> /data/BabySoC/STA_OUTPUT/sta_worst_min_slack.txt

 exec echo "$list_of_lib_files($i)" >> /data/BabySoC/STA_OUTPUT/sta_tns.txt
 report_tns -digits {4} >> /data/BabySoC/STA_OUTPUT/sta_tns.txt

 exec echo "$list_of_lib_files($i)" >> /data/BabySoC/STA_OUTPUT/sta_wns.txt
 report_wns -digits {4} >> /data/BabySoC/STA_OUTPUT/sta_wns.txt
 }
```

</details>

| **Command**               | **Purpose**                       | **Explanation**                                                                                                              |
| ------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `report_worst_slack -max` | Report Worst Setup Slack          | Outputs the **most negative setup slack** (WNS) in the design for the current PVT corner.                                    |
| `report_worst_slack -min` | Report Worst Hold Slack           | Outputs the **most negative hold slack** in the design for the current PVT corner.                                           |
| `report_tns`              | Report Total Negative Slack (TNS) | Prints the **sum of all negative slacks** (across all violating paths). Reflects how widespread timing violations are.       |
| `report_wns`              | Report Worst Negative Slack (WNS) | Prints the **single worst slack** (i.e., the most timing-violating path). Indicates severity of the critical path violation. |

after running opensta in the docker to run the script file use the below command

```shell
source /data/sta_across_pvt.tcl
```

After executing the above script, you can find the generated timing reports in the STA_OUTPUT directory:

```shell
vsdtapeout@pathanrehman::~/Desktop/labs/Week3/examples/BabySoC/STA_OUTPUT$ ls
min_max_sky130_fd_sc_hd__ff_100C_1v65.lib.txt  min_max_sky130_fd_sc_hd__ss_100C_1v40.lib.txt  min_max_sky130_fd_sc_hd__ss_n40C_1v44.lib.txt  sta_worst_max_slack.txt
min_max_sky130_fd_sc_hd__ff_100C_1v95.lib.txt  min_max_sky130_fd_sc_hd__ss_100C_1v60.lib.txt  min_max_sky130_fd_sc_hd__ss_n40C_1v76.lib.txt  sta_worst_min_slack.txt
min_max_sky130_fd_sc_hd__ff_n40C_1v56.lib.txt  min_max_sky130_fd_sc_hd__ss_n40C_1v28.lib.txt  min_max_sky130_fd_sc_hd__tt_025C_1v80.lib.txt
min_max_sky130_fd_sc_hd__ff_n40C_1v65.lib.txt  min_max_sky130_fd_sc_hd__ss_n40C_1v35.lib.txt  sta_tns.txt
min_max_sky130_fd_sc_hd__ff_n40C_1v76.lib.txt  min_max_sky130_fd_sc_hd__ss_n40C_1v40.lib.txt  sta_wns.txt
```
#### Timing Summary Across PVT Corners (Post-Synthesis STA Results)
The following timing summary table was collected by running STA across 13 PVT corners using OpenSTA. 

Metrics such as Worst Hold Slack, Worst Setup Slack, WNS, and TNS were extracted from the output reports.

<img width="1621" height="628" alt="Screenshot 2025-10-11 174312" src="https://github.com/user-attachments/assets/b0f936eb-84af-4aa8-a634-56fb4d8e0da3" />

# BabySoC Physical Design & Post-Route SPEF Generation

This document presents the complete physical design implementation of the BabySoC using OpenROAD, covering all stages from floorplanning to post-route parasitic extraction (SPEF generation). The objective of this task is to integrate the theoretical and practical aspects of digital design by executing a full RTL-to-GDSII flow on a real System-on-Chip (SoC).

Through this exercise, the BabySoC design undergoes floorplan definition, standard cell placement, routing, and parasitic extraction to reflect a realistic ASIC design process. Each stage is explored to understand how physical parameters—such as floorplan constraints, placement density, and routing topology—affect timing performance and design closure.

The outcome of this work is a fully placed and routed BabySoC layout, accompanied by a generated SPEF file that enables post-route Static Timing Analysis (STA). This provides insight into how parasitic effects influence signal delay and how accurate timing verification is performed in professional VLSI design environments.

Comprehensive screenshots, step-by-step procedures, and observations are documented to demonstrate the design flow, tools used, challenges encountered, and verification results.

### Setup and Prepare Project Directory
Clone or set up the directory structure as follows:
```txt
VSDBabySoC/
├── src/
│   ├── include/
│   │   ├── sandpiper.vh
│   │   └── other header files...
│   ├── module/
│   │   ├── vsdbabysoc.v      # Top-level module integrating all components
│   │   ├── rvmyth.v          # RISC-V core module
│   │   ├── avsdpll.v         # PLL module
│   │   ├── avsddac.v         # DAC module
│   │   └── testbench.v       # Testbench for simulation
└── output/
└── compiled_tlv/         # Holds compiled intermediate files if needed
```

We need the above files for further steps, to get the above files you need to follow from the begininng of this document.

## Timing Graphs using openSTA

#### Input Files

- `*.v`  : Gate-level Verilog Netlist  
- `*.lib` : Liberty Timing Libraries  
- `*.sdc` : Synopsys Design Constraints (clocks, delays, false paths)  
- `*.sdf` : Annotated Delay File (optional)  
- `*.spef`: Parasitics (RC extraction)  
- `*.vcd` / `*.saif` : Switching Activity for Power Analysis 

#### Clock Modeling Features

- `Generated Clocks`: Derived from existing clocks  
- `Latency`: Clock propagation delay  
- `Source Latency`: Insertion delay from clock source to input  
- `Uncertainty`: Jitter or skew margins  
- `Propagated vs. Ideal`: Real vs. ideal clock network modeling  
- `Gated Clock Checks`: Verifies clocks that are enabled conditionally  
- `Multi-Frequency Clocks`: Analyzes multiple domains  

#### Exception Paths

Timing exceptions refine analysis for real behavior:

- `set_false_path` — Ignores invalid functional paths  
- `set_multicycle_path` — Allows multiple clock cycles  
- `set_max_delay` / `set_min_delay` — Custom timing limits

#### Delay calculation

- `Integrated Dartu/Menezes/Pileggi RC effective capacitance algorithm`

Models effective capacitance for RC networks to compute realistic gate and net delays. It balances accuracy and runtime using an efficient algorithm developed for timing engines.

- `External delay calculator API`
    
Allows plugging in custom delay calculators for advanced or proprietary models (e.g., layout-aware or temperature-adaptive models). Useful for integrating tool flows beyond standard Liberty data.

#### Timing Analysis and Reporting

OpenSTA provides a rich set of commands for analyzing timing paths, delays, and setup/hold checks:

- `report_checks`  
  Reports timing violations across specified paths using options like `-from`, `-through`, and `-to`. Supports multi-path analysis to any endpoint.

  ```tcl
  report_checks -from [get_pins U1/Q] -to [get_pins U2/D]
  ```
#### Timing Paths 

`What do you mean by Timing Paths?`
* It Refer to the logical paths a signal takes through a digital circuit from its source to its destination, including sequential and combinational elements. STA analyzes timing paths to determine their delay, setup and hold times, and other timing parameters specified in the constraints. Timing paths are categorized into combinatorial and sequential, and the critical path is the longest path in the design with the maximum operating frequency.

#### Timing Path Elements
   
Timing path elements in STA are the start point, where a signal originates, the end point, where it terminates, and the combinational logic elements, such as gates, that the signal passes through. Timing paths are traced to determine the overall delay and timing performance of the digital circuit.

**Start Point**: Is the point where the signal originates or enters the digital circuit. This point is typically an input port of the design, where the signal is first introduced to the circuit.

The start point of a timing path can be either:

- An input port, where data enters the design, or

- The clock pin of a register, where data is launched on a clock edge.

**End Point:** Is the point where the signal terminates or leaves the digital circuit. This point is typically an output port of the design, where the signal is outputted from the circuit.

The end point of a timing path can be either:

- A register's data input pin (D pin), where data is captured by the clock edge, or

- An output port, where data must be available at a specific time.

**Combinational Logic:** Combinational logic elements are the building blocks of a digital circuit and are used to perform logic operations on the signals passing through the circuit. These elements do not store any information, and the output of a combinational logic element is solely determined by the input values at that moment.

The diagram illustrates four distinct timing paths:

Path 1: Input to Register (in2reg)

Path 2: Register to Register (reg2reg)

Path 3: Register to Output (reg2out)

Path 4: Input to Output (in2out)

<img width="646" height="521" alt="image" src="https://github.com/user-attachments/assets/42c9e24a-598e-4302-8244-c5a4440e0461" />

#### Setup and Hold Checks

-> **What is Setup Check?**
* Is the minimum time that the data must be stable before the clock edge, and if this time is not met, it can lead to setup violations, resulting in incorrect data being stored in the sequential element. The setup check is essential to ensure correct timing behavior of a digital circuit and prevent data loss or other timing-related issues.
* The setup time of a flip-flop depends on the technology node, operating conditions, and other factors. The value of the setup time is usually provided in the logic libraries.

-> **What is Hold Check?**
* Is the minimum amount of time that the data must remain stable after the clock edge, and if this time is not met, it can lead to hold violations, resulting in incorrect data being stored in the sequential element. The hold check is necessary to prevent issues such as data corruption, metastability, and other timing-related problems in digital circuits.

#### Slack Calculation 

Setup and hold slack is defined as the difference between data required time and data arrivals time. 

>Setup slack = Data required time - Data arrival time

>Hold slack = Data arrival time - Data required time

-> **What is Data Arrival Time?**
* The time taken by the signal to travel from the start point to the end point of the digital circuit. 

-> **What is Data Required Time?** 
* The time for the clock to traverse through the clock path of the digital circuit. 

-> **What is Slack?** 
* It is difference between the desired arrival times and the actual arrival time for a signal. 
* Positive Slack indicates that the design is meeting the timing and still it can be improved. 
* Zero slack means that the design is critically working at the desired frequency. 
* Negative slack means, design has not achieved the specified timings at the specified frequency.
* Slack has to be positive always and negative slack indicates a violation in timing.

#### Common SDC Constraints

In Static Timing Analysis (STA), **Synopsys Design Constraints (SDC)** are used to define the behavior, environment, and timing requirements of a digital design. These constraints are categorized based on their function and purpose.

**Operating Conditions** are set using the `set_operating_conditions` command, which defines the process-voltage-temperature (PVT) corner used during analysis.

**Wire-Load Models** such as `set_wire_load_mode`, `set_wire_load_model`, and `set_wire_load_selection_group` are used to estimate interconnect capacitance and resistance based on fanout and hierarchy when post-layout parasitics are unavailable.

**Environmental Constraints** define the electrical behavior of I/Os. The `set_drive` and `set_driving_cell` commands model input driving strength or source cell characteristics. Output loads are described using `set_load` or `set_fanout_load`. Additional attributes like `set_input_transition` (input slew) and `set_port_fanout_number` (expected output fanout) further refine environment models.

**Design Rule Constraints** ensure physical design adherence. These include `set_max_capacitance` to limit load, `set_max_fanout` to cap number of loads, and `set_max_transition` to restrict slew for signal integrity and EM/IR compliance.

**Timing Constraints** are the core of STA. `create_clock` defines primary clocks, while `create_generated_clock` handles derived clocks. Clock behavior is further detailed using `set_clock_latency`, `set_clock_transition`, and `set_clock_uncertainty`. Timing analysis can be guided with `set_propagated_clock` to consider actual delays, or `set_disable_timing` to ignore specific paths.

Signal timing is modeled using `set_input_delay` and `set_output_delay`. The `set_input_delay` command specifies when input data arrives relative to the clock edge, crucial for setup/hold timing analysis. The `set_output_delay` command defines the required time by which output signals must be valid, helping STA tools verify that data is launched and captured within acceptable timing windows.

**Timing Exceptions** allow control over non-functional or multi-cycle paths. `set_false_path` removes paths from analysis, `set_max_delay` restricts path delay, and `set_multicycle_path` increases the allowed number of clock cycles for timing paths that do not need single-cycle timing closure.

Lastly, **Power Constraints** help manage dynamic and leakage power budgets using `set_max_dynamic_power` and `set_max_leakage_power`. These are especially useful in power-aware synthesis and verification flows.


| Category              | Commands                                                                 |
|-----------------------|--------------------------------------------------------------------------|
| **Operating Conditions** | `set_operating_conditions`                                                |
| **Wire-load Models**     | `set_wire_load_mode`  <br> `set_wire_load_model` <br> `set_wire_load_selection_group` |
| **Environmental**        | `set_drive` <br> `set_driving_cell` <br> `set_load` <br> `set_fanout_load` <br> `set_input_transition` <br> `set_port_fanout_number` |
| **Design Rules**         | `set_max_capacitance` <br> `set_max_fanout` <br> `set_max_transition`         |
| **Timing**               | `create_clock` <br> `create_generated_clock` <br> `set_clock_latency` <br> `set_clock_transition` <br> `set_disable_timing` <br> `set_propagated_clock` <br> `set_clock_uncertainty` <br> `set_input_delay` <br> `set_output_delay` |
| **Exceptions**           | `set_false_path` <br> `set_max_delay` <br> `set_multicycle_path`              |
| **Power**                | `set_max_dynamic_power` <br> `set_max_leakage_power`                          |

## Installation of OpenSTA

**Note:** Installation instructions are adapted from the official OpenSTA repository:
🔗 https://github.com/parallaxsw/OpenSTA

#### Step 1: Clone the Repository

```bash
git clone https://github.com/parallaxsw/OpenSTA.git
cd OpenSTA
```

<img width="1212" height="308" alt="image" src="https://github.com/user-attachments/assets/54074358-10de-42b4-b986-ace9c5e8bef4" />

#### Step 2: Build the Docker Image
```bash
\docker build --file Dockerfile.ubuntu22.04 --tag opensta .
```
This builds a Docker image named opensta using the provided Ubuntu 22.04 Dockerfile. All dependencies are installed during this step.

<img width="1219" height="503" alt="image" src="https://github.com/user-attachments/assets/6a6f053a-2d2c-4f27-85c6-8174875c23b1" />

#### Step 3: Run the OpenSTA Container
To run a docker container using the OpenSTA image, use the -v option to docker to mount direcories with data to use and -i to run interactively.
```bash
\docker run -i -v $HOME:/data opensta
```
<img width="858" height="148" alt="image" src="https://github.com/user-attachments/assets/5e8f146a-f3b7-491e-8e9c-3cd32b90b9dc" />

You now have OpenSTA installed and running inside a Docker container. After successful installation, you will see the % prompt—this indicates that the OpenSTA interactive shell is ready for use.

### VSDBabySoC basic timing analysis

#### Prepare Required Files

To begin static timing analysis on the VSDBabySoC design, you must organize and prepare the required files in specific directories.

```bash
# Create a directory to store Liberty timing libraries
~/Desktop/VLSI/VSDBabySoC/OpenSTA$ mkdir -p examples/timing_libs/
~/Desktop/VLSI/VSDBabySoC/OpenSTA/examples$ ls timing_libs/
avsddac.lib  avsdpll.lib  sky130_fd_sc_hd__tt_025C_1v80.lib
# Create a directory to store synthesized netlist and constraint files
~/Desktop/VLSI/VSDBabySoC/OpenSTA$ mkdir -p examples/BabySoC
~/Desktop/VLSI/VSDBabySoC/OpenSTA/examples$ ls BabySoC/
gcd_sky130hd.sdc vsdbabysoc_synthesis.sdc  vsdbabysoc.synth.v
```
These files include:

- Standard cell library: sky130_fd_sc_hd__tt_025C_1v80.lib

- IP-specific Liberty libraries: avsdpll.lib, avsddac.lib

- Synthesized gate-level netlist: vsdbabysoc.synth.v

- Timing constraints: vsdbabysoc_synthesis.sdc

These files include:

- Standard cell library: sky130_fd_sc_hd__tt_025C_1v80.lib

- IP-specific Liberty libraries: avsdpll.lib, avsddac.lib

- Synthesized gate-level netlist: vsdbabysoc.synth.v

- Timing constraints: vsdbabysoc_synthesis.sdc

Below is the TCL script to run complete min/max timing checks on the SoC:

<details>
<summary><strong>vsdbabysoc_min_max_delays.tcl</strong></summary>
  
```shell
# Load Liberty Libraries (standard cell + IPs)
read_liberty -min /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib

read_liberty -min /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/avsdpll.lib
read_liberty -max /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/avsdpll.lib

read_liberty -min /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/avsddac.lib
read_liberty -max /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/avsddac.lib

# Read Synthesized Netlist
read_verilog /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/BabySoC/vsdbabysoc.synth.v

# Link the Top-Level Design
link_design vsdbabysoc

# Apply SDC Constraints
read_sdc /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/BabySoC/vsdbabysoc_synthesis.sdc

# Generate Timing Report
report_checks
```

</details>

| **Line of Code**                                       | **Purpose**                | **Explanation**                                                                                    |
| ------------------------------------------------------ | -------------------------- | -------------------------------------------------------------------------------------------------- |
| `read_liberty -min ...sky130...` & `-max ...sky130...` | Load standard cell library | Loads the **typical PVT corner** for both min (hold) and max (setup) timing analysis.              |
| `read_liberty -min/-max avsdpll.lib`                   | Load PLL IP Liberty        | Includes Liberty timing views of the **PLL IP** used in the design.                                |
| `read_liberty -min/-max avsddac.lib`                   | Load DAC IP Liberty        | Includes Liberty timing views of the **DAC IP** used in the design.                                |
| `read_verilog vsdbabysoc.synth.v`                      | Load synthesized netlist   | Loads the gate-level Verilog netlist of the **VSDBabySoC** design.                                 |
| `link_design vsdbabysoc`                               | Link top-level module      | Links the hierarchy using `vsdbabysoc` as the **top module** for timing analysis.                  |
| `read_sdc vsdbabysoc_synthesis.sdc`                    | Load constraints           | Loads SDC file specifying **clock definitions, input/output delays, and false paths**.             |
| `report_checks`                                        | Run timing analysis        | Generates a default **setup timing report**. Add `-path_delay min_max` to see both hold and setup. |

execute it inside the Docker container:

```shell
\docker run -it -v $HOME:/data opensta /data/VLSI/VSDBabySoC/OpenSTA/examples/BabySoC/vsdbabysoc_min_max_delays.tcl
```
⚠️ **Possible Error Alert**

You may encounter the following error when running the script:

```shell
Warning: /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 23, default_fanout_load is 0.0.
Warning: /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 1, library sky130_fd_sc_hd__tt_025C_1v80 already exists.
Warning: /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.lib line 23, default_fanout_load is 0.0.
Error: /data/Desktop/VLSI/VSDBabySoC/OpenSTA/examples/timing_libs/avsdpll.lib line 54, syntax error
```

✅ **Fix:**

This error occurs because Liberty syntax does not support // for single-line comments, and more importantly, the { character appearing after // confuses the Liberty parser. Specifically, check around _line 54 of avsdpll.lib_ and correct any syntax issues such as:

```shell
//pin (GND#2) {
//  direction : input;
//  max_transition : 2.5;
//  capacitance : 0.001;
//}
```
✔️ **Replace with:**
```shell
/*
pin (GND#2) {
  direction : input;
  max_transition : 2.5;
  capacitance : 0.001;
}
*/
```
This should allow OpenSTA to parse the Liberty file without throwing syntax errors.

<img width="284" height="494" alt="image" src="https://github.com/user-attachments/assets/daf7a7a1-c565-4b6a-b2dc-9057726f0eba" />

After fixing the Liberty file comment syntax as shown above, you can rerun the script to perform complete timing analysis for VSDBabySoC:

<img width="1227" height="775" alt="image" src="https://github.com/user-attachments/assets/e0d19f6f-1926-48b0-bba3-0b82fd12dd20" />

### VSDBabySoC PVT Corner Analysis (Post-Synthesis Timing)
Static Timing Analysis (STA) is performed across various **PVT (Process-Voltage-Temperature)** corners to ensure the design meets timing requirements under different conditions.

### Critical Timing Corners

**Worst Max Path (Setup-critical) Corners:**
- `ss_LowTemp_LowVolt`
- `ss_HighTemp_LowVolt`  
_These represent the **slowest** operating conditions._

**Worst Min Path (Hold-critical) Corners:**
- `ff_LowTemp_HighVolt`
- `ff_HighTemp_HighVolt`  
_These represent the **fastest** operating conditions._

 **Timing libraries** required for this analysis can be downloaded from:  
🔗 [Skywater PDK - sky130_fd_sc_hd Timing Libraries](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing)

OpenROAD is an open-source, fully automated RTL-to-GDSII flow for digital integrated circuit (IC) design. It supports synthesis, floorplanning, placement, clock tree synthesis, routing, and final layout generation. OpenROAD enables rapid design iterations, making it ideal for academic research and industry prototyping.

### `Steps to Install OpenROAD and Run GUI`

### 1. Clone the OpenROAD Repository

## 🧩 Step 1: Install Prerequisites
Update your system and install core build tools:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential cmake clang g++ gcc git python3 python3-dev \
  libboost-all-dev libtcl tcl-dev tcllib libreadline-dev zlib1g-dev flex bison \
  swig libpcre3-dev qtbase5-dev liblemon-dev libspdlog-dev libeigen3-dev libffi-dev \
  pkg-config libjson-c-dev libzstd-dev
```
<img width="731" height="506" alt="image" src="https://github.com/user-attachments/assets/a6247bdd-997c-41ba-8a70-10a1c0503002" />


## 📦 Step 2: Clone the Repositories
Install OpenROAD-flow scripts (wrapper for Yosys, OpenROAD, etc.):

```bash
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts.git
cd OpenROAD-flow-scripts
```

<img width="735" height="550" alt="image" src="https://github.com/user-attachments/assets/488efc4e-9b5d-4af6-9bfd-5cb4748fbe69" />


## ⚙️ Step 3: Run the Setup Script
Run the setup installer (this installs all required third-party libraries):

```bash
sudo ./setup.sh
```
This step sets up everything OpenROAD depends on — including Boost, SWIG, Abseil, and more.

<img width="733" height="553" alt="image" src="https://github.com/user-attachments/assets/8037084b-dfee-4aee-b488-33230373b7da" />


## 🏗️ Step 4: Build OpenROAD Locally
Now build OpenROAD itself using the automated build script:

```bash
./build_openroad.sh --local
```
💡 This step takes about 30–45 minutes depending on cores and RAM.

<img width="739" height="561" alt="image" src="https://github.com/user-attachments/assets/7240918e-381d-41dd-9530-e4635b434222" />

If tests fail to build (common Google Test issue), you can skip them:

```bash
./build_openroad.sh --local --disable-tests
```

<img width="742" height="553" alt="image" src="https://github.com/user-attachments/assets/00d86fd0-4f8e-4be0-99d1-b92f6a095070" />


## Step 5: Verify Installation

```bash
source ./env.sh
yosys -help  
openroad -help
yosys --version
openroad --version
verilator --version
```

<img width="739" height="553" alt="image" src="https://github.com/user-attachments/assets/45f0116e-f618-4a7c-89fa-eccd548c3f65" />


## Step 6: Run the OpenROAD Flow

```bash
cd flow
make
```

<img width="739" height="557" alt="image" src="https://github.com/user-attachments/assets/8e6ab8eb-8031-4e7d-a1c4-c45c9d997cac" />


## Step 7. Launch the graphical user interface (GUI) to visualize the final layout

```bash
 make gui_final
```

<img width="1847" height="921" alt="image" src="https://github.com/user-attachments/assets/ad232497-44f9-40a1-abaa-d4943aba5a81" />


✅ Installation Complete! You can now explore the full RTL-to-GDSII flow using OpenROAD.

### `ORFS Directory Structure and File formats`

OpenROAD-flow-scripts/

```plaintext
├── OpenROAD-flow-scripts             
│   ├── docker           -> It has Docker based installation, run scripts and all saved here
│   ├── docs             -> Documentation for OpenROAD or its flow scripts.  
│   ├── flow             -> Files related to run RTL to GDS flow  
|   ├── jenkins          -> It contains the regression test designed for each build update
│   ├── tools            -> It contains all the required tools to run RTL to GDS flow
│   ├── etc              -> Has the dependency installer script and other things
│   ├── setup_env.sh     -> Its the source file to source all our OpenROAD rules to run the RTL to GDS flow
```
<img width="733" height="274" alt="image" src="https://github.com/user-attachments/assets/6bfbb4cc-4bf0-4975-aaf1-500317e6d25b" />

Inside the `flow/` Directory

```plaintext
├── flow           
│   ├── design           -> It has built-in examples from RTL to GDS flow across different technology nodes
│   ├── makefile         -> The automated flow runs through makefile setup
│   ├── platform         -> It has different technology note libraries, lef files, GDS etc 
|   ├── tutorials        
│   ├── util            
│   ├── scripts                 
```
<img width="736" height="212" alt="image" src="https://github.com/user-attachments/assets/87fc885a-bed0-42c6-a3c5-16f816febe98" />

# Floorplan and Placement of VSDBabySoC in OpenROAD

###  `RTL2GDS Flow for VSDBabySoC: Initial Steps`

1. **Create Directories:**
   - Inside `OpenROAD-flow-scripts/flow/designs/sky130hd/`, create a folder named `vsdbabysoc`.
   - Create another folder named `vsdbabysoc` in `OpenROAD-flow-scripts/flow/designs/src/` and place all Verilog files here.

2. **Copy Folders:**
   - From your `VSDBabySoC` folder, copy the following folders into `sky130hd/vsdbabysoc`:
     - **gds:** Contains `avsddac.gds`, `avsdpll.gds`.
     - **include:** Contains `sandpiper.vh`, `sandpiper_gen.vh`, `sp_default.vh`, `sp_verilog.vh`.
     - **lef:** Contains `avsddac.lef`, `avsdpll.lef`.
     - **lib:** Contains `avsddac.lib`, `avsdpll.lib`.

3. **Copy Constraint and Configuration Files:**
   - Copy `vsdbabysoc_synthesis.sdc` into `sky130hd/vsdbabysoc`.
   - Copy `macro.cfg` and `pin_order.cfg` into `sky130hd/vsdbabysoc`.

4. **Create Config File:**
   - Create a `config.mk` file in `sky130hd/vsdbabysoc` with the required configuration details. 

<details> <summary><strong>config.mk</strong></summary>

```
   # Design and Platform Configuration
   export DESIGN_NICKNAME = vsdbabysoc
   export DESIGN_NAME = vsdbabysoc
   export PLATFORM    = sky130hd

  # Design Paths
  export vsdbabysoc_DIR = /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/$(DESIGN_NICKNAME)

  # Explicitly list Verilog files for synthesis
   export VERILOG_FILES = /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/vsdbabysoc.v \
                         /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/rvmyth.v \
                         /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/clk_gate.v


  # Include Directory for Verilog Header Files
   export VERILOG_INCLUDE_DIRS = $(vsdbabysoc_DIR)/include

  # Constraints File
    export SDC_FILE = $(vsdbabysoc_DIR)/vsdbabysoc_synthesis.sdc

  # Additional GDS Files
    export ADDITIONAL_GDS = $(vsdbabysoc_DIR)/gds/avsddac.gds \
                            $(vsdbabysoc_DIR)/gds/avsdpll.gds

  # Additional LEF Files
   export ADDITIONAL_LEFS = $(vsdbabysoc_DIR)/lef/avsddac.lef \
                            $(vsdbabysoc_DIR)/lef/avsdpll.lef

  # Additional LIB Files
   export ADDITIONAL_LIBS = $(vsdbabysoc_DIR)/lib/avsddac.lib \
                            $(vsdbabysoc_DIR)/lib/avsdpll.lib

 # Pin Order and Macro Placement Configurations
   export FP_PIN_ORDER_CFG = $(vsdbabysoc_DIR)/pin_order.cfg
   export MACRO_PLACEMENT_CFG = $(vsdbabysoc_DIR)/macro.cfg

 # Clock Configuration
   export CLOCK_PORT = CLK
   export CLOCK_NET  = $(CLOCK_PORT)
   export CLOCK_PERIOD = 20.0

# Floorplanning Configuration
  export DIE_AREA   = 0 0 1600 1600
  export CORE_AREA  = 10 10 1590 1590

# Routing Configuration
export GRT_ALLOW_CONGESTION = 1
export GRT_ADJUSTMENT = 0.2
export GLOBAL_ROUTE_ARGS = -allow_congestion -verbose

# Skip the optimization step that is causing the crash.
# (The log showed it was doing 0 repairs anyway).
export SKIP_INCREMENTAL_REPAIR = 1

# Forces standard cells to stay 20 microns away from macros
export MACRO_PLACE_HALO = 20 20

# Increase the spacing (pitch) between Horizontal Power Straps (Met5)
# The default is usually around 180. We increase it to create gaps.
export FP_PDN_HPITCH = 200

# Routing Configuration
export MAX_ROUTING_LAYER = met4

# Placement Configuration
  export PLACE_PINS_ARGS = -exclude left:0-400 -exclude left:1200-1600

# Tuning for Timing and Buffers
  export TNS_END_PERCENT     = 95
  export REMOVE_ABC_BUFFERS  = 1
  export CTS_BUF_DISTANCE    = 300
  export SKIP_GATE_CLONING   = 1

 # Magic Tool Configuration
   export MAGIC_ZEROIZE_ORIGIN = 0
   export MAGIC_EXT_USE_GDS    = 1

```
</details>

This script sets up environment variables and configurations for the design and synthesis of a System-on-Chip (SoC) using the OpenROAD flow. The design is based on the "vsdbabysoc" and targets the "sky130hd" platform.

--------

### `Key Components of config.mk`

#### Design and Platform Configuration
- **DESIGN_NICKNAME & DESIGN_NAME**: Both are set to "vsdbabysoc," serving as the identifier for the design project.
- **PLATFORM**: Specifies the technology platform as "sky130hd," indicating the process node and design rules to be used.

#### Design Paths
- **vsdbabysoc_DIR**: Defines the directory path for the design files as `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc`. This path is constructed using the DESIGN_NICKNAME variable, ensuring consistency and easy access to design resources.

#### Verilog Files for Synthesis
- **VERILOG_FILES**: Lists the Verilog source files required for synthesis:
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/vsdbabysoc.v`: The main Verilog file for the SoC design.
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/rvmyth.v`: A module within the design, possibly a RISC-V core or related component.
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc/clk_gate.v`: A module for clock gating, used to manage power consumption by controlling clock signals.

#### Verilog Header Files
- **VERILOG_INCLUDE_DIRS**: Specifies the directory for Verilog header files as `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/include`.

#### Constraints and Additional Files
- **SDC_FILE**: Points to the constraints file for synthesis located at `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/vsdbabysoc_synthesis.sdc`.
- **ADDITIONAL_GDS**: Lists additional GDS files required for the design:
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/gds/avsddac.gds`
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/gds/avsdpll.gds`
- **ADDITIONAL_LEFS**: Lists additional LEF files:
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lef/avsddac.lef`
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lef/avsdpll.lef`
- **ADDITIONAL_LIBS**: Lists additional LIB files:
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lib/avsddac.lib`
  - `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lib/avsdpll.lib`

#### Pin Order and Macro Placement
- **FP_PIN_ORDER_CFG**: Configuration file for pin order located at `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/pin_order.cfg`.
- **MACRO_PLACEMENT_CFG**: Configuration file for macro placement located at `/home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/macro.cfg`.

#### Clock Configuration
- **CLOCK_PORT & CLOCK_NET**: Defines the clock port and net as `CLK`.
- **CLOCK_PERIOD**: Sets the clock period to `20.0` units.

#### Floorplanning Configuration
- **DIE_AREA**: Specifies the die area dimensions as `0 0 1600 1600`.
- **CORE_AREA**: Specifies the core area dimensions as `20 20 1590 1590`.

#### Placement Configuration
- **PLACE_PINS_ARGS**: Arguments for pin placement, excluding certain areas on the die:
  - `-exclude left:0-600`
  - `-exclude left:1000-1600`
  - `-exclude right:*`
  - `-exclude top:*`
  - `-exclude bottom:*`

#### Timing and Buffer Tuning
- **TNS_END_PERCENT**: Sets the target negative slack end percentage to `100`.
- **REMOVE_ABC_BUFFERS**: Enables removal of ABC buffers, set to `1`.
- **CTS_BUF_DISTANCE**: Sets the buffer distance for clock tree synthesis to `600`.
- **SKIP_GATE_CLONING**: Skips gate cloning during synthesis, set to `1`.

#### Magic Tool Configuration
- **MAGIC_ZEROIZE_ORIGIN**: Configuration for zeroizing the origin, set to `0`.
- **MAGIC_EXT_USE_GDS**: Configuration for using GDS files, set to `1`.

This setup script is crucial for defining the environment and parameters needed for successful synthesis and layout of the "vsdbabysoc" design on the "sky130hd" platform, ensuring that all necessary files and configurations are in place for the design flow.

# Macro Configuration File Documentation

The `macro.cfg` file defines the placement coordinates and orientation for hardware macros in a chip design layout, typically used in VLSI/ASIC design flows.

## File Format

Each line in the configuration file follows this syntax pattern:

```
<macro_name> <x_coordinate> <y_coordinate> <orientation>
```

## Configuration Breakdown

### PLL Macro
```
pll 200 950 N
```

- **Macro Name**: `pll` (Phase-Locked Loop)
- **X Coordinate**: 200 (horizontal placement position)
- **Y Coordinate**: 950 (vertical placement position)
- **Orientation**: `N` (North - standard upright orientation)

The PLL is a critical clock generation and management circuit positioned at coordinates (200, 950) with standard North orientation.

### DAC Macro
```
dac 150 250 MY
```

- **Macro Name**: `dac` (Digital-to-Analog Converter)
- **X Coordinate**: 150 (horizontal placement position)
- **Y Coordinate**: 250 (vertical placement position)
- **Orientation**: `MY` (Mirror Y - flipped along the Y-axis)

The DAC macro handles digital-to-analog conversion and is placed at coordinates (150, 250) with Y-axis mirroring applied.

## Orientation Values

Common orientation flags include:
- **N**: North (0° rotation, standard)
- **S**: South (180° rotation)
- **E**: East (90° clockwise)
- **W**: West (90° counter-clockwise)
- **MY**: Mirror Y-axis
- **MX**: Mirror X-axis

## Usage

This configuration file is typically consumed by place-and-route tools during the physical design phase to ensure proper macro placement and avoid routing congestion.

## Edit global_route.tcl

The Fix: Comment Out the "Extra" Optimizations
Since we cannot disable this step via config.mk, we must comment it out in the Tcl script. You don't need Power Recovery for this design anyway.

Step 1: Open the Script Open the file global_route.tcl in your text editor. (It is likely located at flow/scripts/global_route.tcl or inside your scripts folder).

Step 2: Comment Out Power Recovery Find the section that looks like this (around line 100-110) and add # to the start of every line to disable it:

```Tcl
# ----------------- COMMENT THIS BLOCK OUT -----------------
# log_cmd global_route -start_incremental
# recover_power_helper
# # Route the modified nets by rsz journal restore
# log_cmd global_route -end_incremental {*}$res_aware \
#   -congestion_report_file $::env(REPORTS_DIR)/congestion_post_recover_power.rpt
# -----------------------------------------------------------
```

<details> <summary><strong>global_route.tcl</strong></summary>
   
      utl::set_metrics_stage "globalroute__{}"
      source $::env(SCRIPTS_DIR)/load.tcl
      erase_non_stage_variables grt
      load_design 4_cts.odb 4_cts.sdc
      
      # This proc is here to allow us to use 'return' to return early from this
      # file which is sourced
      proc global_route_helper { } {
        source_env_var_if_exists PRE_GLOBAL_ROUTE_TCL
   
     set res_aware ""
     append_env_var res_aware ENABLE_RESISTANCE_AWARE -resistance_aware 0
   
     proc do_global_route { res_aware } {
       set all_args [concat [list \
         -congestion_report_file $::global_route_congestion_report] \
         $::env(GLOBAL_ROUTE_ARGS) {*}$res_aware]
   
       log_cmd global_route {*}$all_args
     }
     set additional_args ""
     append_env_var additional_args dbProcessNode -db_process_node 1
     append_env_var additional_args VIA_IN_PIN_MIN_LAYER -via_in_pin_bottom_layer 1
     append_env_var additional_args VIA_IN_PIN_MAX_LAYER -via_in_pin_top_layer 1
   
     pin_access {*}$additional_args
   
     set result [catch { do_global_route $res_aware } errMsg]
   
     if { $result != 0 } {
       if { !$::env(GENERATE_ARTIFACTS_ON_FAILURE) } {
         write_db $::env(RESULTS_DIR)/5_1_grt-failed.odb
         error $errMsg
       }
       write_sdc -no_timestamp $::env(RESULTS_DIR)/5_1_grt.sdc
       write_db $::env(RESULTS_DIR)/5_1_grt.odb
       return
     }
   
     set_placement_padding -global \
       -left $::env(CELL_PAD_IN_SITES_DETAIL_PLACEMENT) \
       -right $::env(CELL_PAD_IN_SITES_DETAIL_PLACEMENT)
   
     set_propagated_clock [all_clocks]
     estimate_parasitics -global_routing
   
     if { [env_var_exists_and_non_empty DONT_USE_CELLS] } {
       set_dont_use $::env(DONT_USE_CELLS)
     }
   
     if { !$::env(SKIP_INCREMENTAL_REPAIR) } {
       if { $::env(DETAILED_METRICS) } {
         report_metrics 5 "global route pre repair design"
       }

    # Repair design using global route parasitics
    repair_design_helper
    if { $::env(DETAILED_METRICS) } {
      report_metrics 5 "global route post repair design"
    }

    # Running DPL to fix overlapped instances
    # Run to get modified net by DPL
    log_cmd global_route -start_incremental
    log_cmd detailed_placement
    # Route only the modified net by DPL
    log_cmd global_route -end_incremental {*}$res_aware \
      -congestion_report_file $::env(REPORTS_DIR)/congestion_post_repair_design.rpt

    # Repair timing using global route parasitics
    puts "Repair setup and hold violations..."
    estimate_parasitics -global_routing

    repair_timing_helper

    if { $::env(DETAILED_METRICS) } {
      report_metrics 5 "global route post repair timing"
    }

    # Running DPL to fix overlapped instances
    # Run to get modified net by DPL
    log_cmd global_route -start_incremental
    log_cmd detailed_placement
    # Route only the modified net by DPL
    log_cmd global_route -end_incremental {*}$res_aware \
      -congestion_report_file $::env(REPORTS_DIR)/congestion_post_repair_timing.rpt
     }


      #  log_cmd global_route -start_incremental
      #  recover_power_helper
     # Route the modified nets by rsz journal restore
      #  log_cmd global_route -end_incremental {*}$res_aware \
    -congestion_report_file $::env(REPORTS_DIR)/congestion_post_recover_power.rpt

     if {
       !$::env(SKIP_ANTENNA_REPAIR) &&
       [env_var_exists_and_non_empty MAX_REPAIR_ANTENNAS_ITER_GRT]
     } {
    puts "Repair antennas..."
    repair_antennas -iterations $::env(MAX_REPAIR_ANTENNAS_ITER_GRT)
    check_placement -verbose
    check_antennas -report_file $::env(REPORTS_DIR)/grt_antennas.log
     }

     puts "Estimate parasitics..."
     estimate_parasitics -global_routing

     report_metrics 5 "global route"

     # Write SDC to results with updated clock periods that are just failing.
     # Use make target update_sdc_clock to install the updated sdc.
     source [file join $::env(SCRIPTS_DIR) "write_ref_sdc.tcl"]

     write_guides $::env(RESULTS_DIR)/route.guide
     write_db $::env(RESULTS_DIR)/5_1_grt.odb
     write_sdc -no_timestamp $::env(RESULTS_DIR)/5_1_grt.sdc
      }

      global_route_helper
</details>

### Another Fix thanks to the [@BitopanBaishya](https://github.com/BitopanBaishya)

He modified the macro_place_util.tcl file so that it reads the macro.cfg as follows:

He replaced
```
log_cmd rtl_macro_placer {*}$all_args
```
with
```
  # Manual macro placement using macro.cfg
if { [env_var_exists_and_non_empty MACRO_PLACEMENT_CFG] } {

set fp [open $::env(MACRO_PLACEMENT_CFG) r]
while {[gets $fp line] >= 0} {
# skip empty and comment lines
if {[regexp {^\s*$} $line]} continue
if {[regexp {^#} $line]} continue

# Parse: <macro> <x> <y> <orient>
scan $line "%s %f %f %s" macro x y orient

puts "Placing macro $macro at ($x, $y) orient $orient"
place_macro -macro_name $macro -location "$x $y" -orientation $orient
}
close $fp
}
```

### `File Structure After Setup`

```shell
pathanrehman@pathanrehman:~/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/src/vsdbabysoc$ ls -ltrh
total 3.1M
-rw-rw-r-- 1 pathanrehman pathanrehman  590 Nov 13 20:54 vsdbabysoc.v
-rwxrwxr-x 1 pathanrehman pathanrehman 1.3K Nov 13 20:54 testbench.v
-rw-rw-r-- 1 pathanrehman pathanrehman  603 Nov 13 20:54 testbench.rvmyth.post-routing.v
-rw-rw-r-- 1 pathanrehman pathanrehman 1.7K Nov 13 20:54 clk_gate.v
-rw-rw-r-- 1 pathanrehman pathanrehman  947 Nov 13 20:54 avsdpll.v
-rw-rw-r-- 1 pathanrehman pathanrehman 1.1K Nov 13 20:54 avsddac.v
-rw-rw-r-- 1 pathanrehman pathanrehman  17K Nov 13 21:00 rvmyth.v
-rw-rw-r-- 1 pathanrehman pathanrehman  19K Nov 13 21:00 rvmyth_gen.v
-rw-rw-r-- 1 pathanrehman pathanrehman  50K Nov 13 21:21 primitives.v -> /home/pathanrehman/Desktop/VLSI/VLSI/sky130RTLDesignAndSynthesisWorkshop/my_lib/verilog_model/primitives.v
-rw-rw-r-- 1 pathanrehman pathanrehman 749K Nov 13 21:22 vsdbabysoc.synth.v
-rw-rw-r-- 1 pathanrehman pathanrehman 2.3M Nov 13 21:29 sky130_fd_sc_hd.v
```

```shell
pathanrehman@pathanrehman:~/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc$ ls -ltrh
total 32K
-rw-rw-r-- 1 pathanrehman pathanrehman   73 Nov 13 20:54 vsdbabysoc_synthesis.sdc
-rw-rw-r-- 1 pathanrehman pathanrehman   62 Nov 13 20:54 pin_order.cfg -> /home/pathanrehman/Desktop/VLSI/VSDBabySoC/src/layout_conf/vsdbabysoc/pin_order.cfg
-rw-rw-r-- 1 pathanrehman pathanrehman   28 Nov 13 20:54 macro.cfg -> /home/pathanrehman/Desktop/VLSI/VSDBabySoC/src/layout_conf/vsdbabysoc/macro.cfg
drwxrwxr-x 2 pathanrehman pathanrehman 4.0K Nov 13 20:54 lef
drwxrwxr-x 2 pathanrehman pathanrehman 4.0K Nov 13 20:54 include
drwxrwxr-x 2 pathanrehman pathanrehman 4.0K Nov 13 20:54 gds
-rw-rw-r-- 1 pathanrehman pathanrehman 2.2K Nov 15 18:45 config.mk
drwxrwxr-x 2 pathanrehman pathanrehman 4.0K Nov 15 18:59 lib

```

#### Now go to terminal and run the following commands:

```shell
# Navigate to the OpenROAD flow scripts directory
cd OpenROAD-flow-scripts
# Source the environment setup script
source env.sh
# Change to the flow directory
cd flow
```

<img width="739" height="78" alt="image" src="https://github.com/user-attachments/assets/a4234057-f153-4d86-869f-e019408d9070" />

----
 
### `Run Synthesis`

```shell
# Ensure you are in the 'flow' directory before running the synthesis command
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk clean_all
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk synth
```

This command runs the synthesis process using the specified design configuration file `config.mk` for the `vsdbabysoc` design on the `sky130hd` platform.

<img width="729" height="522" alt="image" src="https://github.com/user-attachments/assets/365b89cf-1a00-460b-868a-ef061486d576" />


<img width="736" height="526" alt="image" src="https://github.com/user-attachments/assets/2194192e-b0fc-451d-843c-691b0106f342" />


#### Synthesis netlist

```shell
~/OpenROAD-flow-scripts/flow$ gvim results/sky130hd/vsdbabysoc/base/1_1_yosys.v
```
<img width="888" height="889" alt="image" src="https://github.com/user-attachments/assets/df6724dc-eef8-4081-a322-d4158a3a5e64" />


#### Synthesis Stats

```shell
~/OpenROAD-flow-scripts/flow$ gvim reports/sky130hd/vsdbabysoc/base/synth_stat.txt
```

<img width="889" height="910" alt="image" src="https://github.com/user-attachments/assets/fe6f964e-b87c-497a-b862-2d7aa74f42db" />


<details> <summary><strong>synth_stat.txt</strong></summary>

```

20. Printing statistics.

=== vsdbabysoc ===

        +----------Local Count, excluding submodules.
        |        +-Local Area, excluding submodules.
        |        | 
     6715        - wires
     6715        - wire bits
     1285        - public wires
     1285        - public wire bits
        7        - ports
        7        - port bits
     6605 5.29E+04 cells
        1        -   avsddac
        1        -   avsdpll
        1   11.261   sky130_fd_sc_hd__a2111o_1
        6    52.55   sky130_fd_sc_hd__a2111oi_0
        8   70.067   sky130_fd_sc_hd__a211o_1
       26  195.187   sky130_fd_sc_hd__a211oi_1
       17  127.622   sky130_fd_sc_hd__a21boi_0
       31  232.723   sky130_fd_sc_hd__a21o_1
      884 4.42E+03   sky130_fd_sc_hd__a21oi_1
        7   61.309   sky130_fd_sc_hd__a21oi_2
       15  150.144   sky130_fd_sc_hd__a221o_1
       37  324.061   sky130_fd_sc_hd__a221oi_1
       24  210.202   sky130_fd_sc_hd__a22o_1
      222 1.67E+03   sky130_fd_sc_hd__a22oi_1
        1    21.27   sky130_fd_sc_hd__a22oi_4
        1   11.261   sky130_fd_sc_hd__a2bb2o_2
        4   35.034   sky130_fd_sc_hd__a2bb2oi_1
        2   20.019   sky130_fd_sc_hd__a311o_1
       15  131.376   sky130_fd_sc_hd__a311oi_1
        8   70.067   sky130_fd_sc_hd__a31o_2
       53  331.568   sky130_fd_sc_hd__a31oi_1
        1    10.01   sky130_fd_sc_hd__a32o_1
        3   26.275   sky130_fd_sc_hd__a32oi_1
        3   26.275   sky130_fd_sc_hd__a41oi_1
        2   12.512   sky130_fd_sc_hd__and2_0
       10    62.56   sky130_fd_sc_hd__and2_1
       14   87.584   sky130_fd_sc_hd__and3_1
       34  127.622   sky130_fd_sc_hd__buf_1
        9   45.043   sky130_fd_sc_hd__buf_2
        1    7.507   sky130_fd_sc_hd__buf_4
        3   33.782   sky130_fd_sc_hd__buf_6
      548 2.06E+03   sky130_fd_sc_hd__clkbuf_1
        4   15.014   sky130_fd_sc_hd__clkinv_1
        1    3.754   sky130_fd_sc_hd__conb_1
     1144 2.29E+04   sky130_fd_sc_hd__dfxtp_1
        4   80.077   sky130_fd_sc_hd__fa_1
      100   1251.2   sky130_fd_sc_hd__ha_1
      104  390.374   sky130_fd_sc_hd__inv_1
       56  630.605   sky130_fd_sc_hd__mux2_2
       92  920.883   sky130_fd_sc_hd__mux2i_1
        1   22.522   sky130_fd_sc_hd__mux2i_4
       69  1553.99   sky130_fd_sc_hd__mux4_2
     1461  5484.01   sky130_fd_sc_hd__nand2_1
       28  175.168   sky130_fd_sc_hd__nand2b_1
      213 1.07E+03   sky130_fd_sc_hd__nand3_1
       40  300.288   sky130_fd_sc_hd__nand3b_1
       70   437.92   sky130_fd_sc_hd__nand4_1
        2   17.517   sky130_fd_sc_hd__nand4b_1
      284 1.07E+03   sky130_fd_sc_hd__nor2_1
       52  325.312   sky130_fd_sc_hd__nor2b_1
       74  370.355   sky130_fd_sc_hd__nor3_1
        9   67.565   sky130_fd_sc_hd__nor3b_1
        1   12.512   sky130_fd_sc_hd__nor3b_2
       25    156.4   sky130_fd_sc_hd__nor4_1
        1    8.758   sky130_fd_sc_hd__nor4b_1
        1   11.261   sky130_fd_sc_hd__o2111a_1
        8   70.067   sky130_fd_sc_hd__o2111ai_1
        3   30.029   sky130_fd_sc_hd__o211a_1
       51  382.867   sky130_fd_sc_hd__o211ai_1
       30  225.216   sky130_fd_sc_hd__o21a_1
      397 1.99E+03   sky130_fd_sc_hd__o21ai_0
        8   40.038   sky130_fd_sc_hd__o21ai_1
       10   75.072   sky130_fd_sc_hd__o21bai_1
       27  236.477   sky130_fd_sc_hd__o221ai_1
       36  315.302   sky130_fd_sc_hd__o22a_1
       31  193.936   sky130_fd_sc_hd__o22ai_1
        2   17.517   sky130_fd_sc_hd__o2bb2ai_1
        1    10.01   sky130_fd_sc_hd__o311a_1
        6    52.55   sky130_fd_sc_hd__o311ai_0
        5   43.792   sky130_fd_sc_hd__o31a_1
       34  255.245   sky130_fd_sc_hd__o31ai_1
        1   12.512   sky130_fd_sc_hd__o31ai_2
        2   20.019   sky130_fd_sc_hd__o32a_1
        4   35.034   sky130_fd_sc_hd__o32ai_1
        1   11.261   sky130_fd_sc_hd__o41a_1
        5   43.792   sky130_fd_sc_hd__o41ai_1
        2   12.512   sky130_fd_sc_hd__or2_0
        1    6.256   sky130_fd_sc_hd__or2_1
        8   50.048   sky130_fd_sc_hd__or2_2
       28  175.168   sky130_fd_sc_hd__or3_1
        1    8.758   sky130_fd_sc_hd__or3b_1
        2   17.517   sky130_fd_sc_hd__or3b_2
        4   30.029   sky130_fd_sc_hd__or4_1
       47  411.645   sky130_fd_sc_hd__xnor2_1
       22  192.685   sky130_fd_sc_hd__xor2_1

   Area for cell type \avsdpll is unknown!
   Area for cell type \avsddac is unknown!

   Chip area for module '\vsdbabysoc': 52874.460800
     of which used for sequential elements: 22901.964800 (43.31%)

```
</details>

----------

### `Run Floorplan`

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```
<img width="735" height="527" alt="image" src="https://github.com/user-attachments/assets/9da357a6-abc7-45c5-b55f-ae6d5f2fef36" />


This command initiates the floorplanning process for the `vsdbabysoc` design using the specified configuration file `config.mk` on the `sky130hd` platform.

#### Floorplan Error and Fix

❗**Note:** You may encounter the following error:

```shell
[ERROR STA-0164] .../vsdbabysoc/lib/avsdpll.lib line 54, syntax error
Error: floorplan.tcl, 4 STA-0164
```

**Fix:**
This error is caused by commented block structures in your Liberty file avsdpll.lib. OpenROAD’s parser does not tolerate partially commented blocks like:

```shell
//pin (GND#2) {
//  direction : input;
//  max_transition : 2.5;
//  capacitance : 0.001;
//}
```

✅ To fix it, simply delete the entire commented block starting at line 54:

After saving the changes, re-run the floorplan step and the flow should proceed without syntax errors. 

#### Floorplan Result (GUI)

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_floorplan
```

<img width="1211" height="697" alt="image" src="https://github.com/user-attachments/assets/18c89dcd-6ddf-4d32-ad7b-98df16f6e5ec" />
<img width="1280" height="728" alt="image" src="https://github.com/user-attachments/assets/734a8cb0-48fb-4e9d-8994-46eb0d163794" />

------

### `Run Placement`

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```
This command executes the placement process for the `vsdbabysoc` design, utilizing the configuration file `config.mk` on the `sky130hd` platform to arrange the circuit components optimally within the defined floorplan.

<img width="1285" height="720" alt="image" src="https://github.com/user-attachments/assets/e40ec7e0-dab9-4177-a00d-b9d1424a2276" />

<img width="1285" height="728" alt="image" src="https://github.com/user-attachments/assets/7ba9a0d6-ecfa-4e93-9b90-58d0e94d7b02" />


#### Placement Result (GUI)

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_place
```
<img width="1284" height="726" alt="image" src="https://github.com/user-attachments/assets/41cacfab-899a-4000-a74d-d35b40e47cc0" />

To view the Placement Density heatmap in OpenROAD:

Go to **Tools → Heat maps → Placement Density** → **✓ Show numbers**

<img width="1281" height="728" alt="image" src="https://github.com/user-attachments/assets/5a63a429-408a-4417-99c4-186585a4493b" />

### `run cts`

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk cts
```

<img width="741" height="527" alt="image" src="https://github.com/user-attachments/assets/20916df1-a169-47f4-84b4-7102227e5f92" />


**CTS Result (GUI)**

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_cts
```

This image shows the Clock Tree Synthesis (CTS) stage, highlighting a placed clock buffer (clkbuf_leaf_209_CLK) with its properties displayed in the Inspector, including position, orientation, and connectivity details.

<img width="1850" height="894" alt="image" src="https://github.com/user-attachments/assets/b40be0b7-bd18-4955-b220-06a1414a37c1" />


This image shows the **Clock Tree Viewer** after CTS, illustrating the clock buffer distribution on the layout and a histogram of clock insertion delays, indicating balanced clock skew across the sinks.

<img width="1852" height="915" alt="image" src="https://github.com/user-attachments/assets/1f6d2a62-c10d-4085-9164-52da46584376" />

This image shows the **Setup Timing Report**, presenting a list of timing paths with key metrics such as:

- **Required Time**
- **Arrival Time**
- **Slack**
- **Skew**
- **Logic Delay**
- **Logic Depth**
- **Fanout**

All paths have **positive slack**, confirming that the design meets **setup timing requirements**.

<img width="1214" height="802" alt="image" src="https://github.com/user-attachments/assets/32773245-f127-4a15-8515-4b211e53f2a4" />


This image displays the **Hold Timing Report**, showing timing paths with details such as:

- **Required Time**
- **Arrival Time**
- **Slack**
- **Skew**
- **Logic Delay**
- **Fanout**

All paths listed have **positive slack**, indicating that the design meets **hold timing requirements** and is free from hold violations.

<img width="1216" height="802" alt="image" src="https://github.com/user-attachments/assets/6ffbf071-8d7f-4974-b531-922fdcfca7a9" />


This image shows the **Setup Slack Histogram** after CTS. The histogram represents the distribution of endpoint slack values, all of which are positive, indicating that there are no setup timing violations.

<img width="1215" height="797" alt="image" src="https://github.com/user-attachments/assets/631effb7-9daa-468e-bce3-397dafb16368" />


This image shows the **Hold Slack Histogram** after CTS. The histogram represents the distribution of hold slack values for all endpoints. All values are positive, confirming that the design meets hold timing requirements without any violations.

<img width="1213" height="793" alt="image" src="https://github.com/user-attachments/assets/c84684c0-939c-4ea1-a947-4510429a2ae3" />


Zoomed-in view of the design after CTS, showing inserted clock buffers and routing connections.

<img width="1212" height="795" alt="image" src="https://github.com/user-attachments/assets/733c7e18-d530-4628-b3f4-ea6417317a4e" />


<img width="1210" height="796" alt="image" src="https://github.com/user-attachments/assets/96bcac61-2b8d-41c3-82ed-73a5ed873f11" />


**CTS final report:**

```shell
gvim /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/reports/sky130hd/vsdbabysoc/base/4_cts_final.rpt
```

<details> <summary><strong>4_cts_final.rpt</strong></summary>

```



==========================================================================
cts final report_tns
--------------------------------------------------------------------------
tns max 0.00

==========================================================================
cts final report_wns
--------------------------------------------------------------------------
wns max 0.00

==========================================================================
cts final report_worst_slack
--------------------------------------------------------------------------
worst slack max 6.31

==========================================================================
cts final report_clock_min_period
--------------------------------------------------------------------------
clk period_min = 4.69 fmax = 213.35

==========================================================================
cts final report_clock_skew
--------------------------------------------------------------------------
Clock clk
   0.95 source latency core.CPU_result_a4[2]$_DFF_P_/CLK ^
  -0.83 target latency core.CPU_Dmem_value_a5[4][8]$_SDFFE_PP0P_/CLK ^
   0.00 CRPR
--------------
   0.12 setup skew


==========================================================================
cts final report_checks -path_delay min
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a2$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_reset_a3$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.15    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01    0.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00    0.24 ^ clkbuf_2_2_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.11    0.12    0.24    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_2_0_CLK (net)
                  0.12    0.00    0.48 ^ clkbuf_4_9__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.09    0.11    0.21    0.69 ^ clkbuf_4_9__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_9__leaf_CLK (net)
                  0.11    0.00    0.69 ^ clkbuf_leaf_13_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     9    0.03    0.05    0.16    0.85 ^ clkbuf_leaf_13_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_13_CLK (net)
                  0.05    0.00    0.85 ^ core.CPU_reset_a2$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.02    0.29    1.14 v core.CPU_reset_a2$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_reset_a2 (net)
                  0.02    0.00    1.14 v core.CPU_reset_a3$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_4)
                                  1.14   data arrival time

                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.15    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01    0.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00    0.24 ^ clkbuf_2_2_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.11    0.12    0.24    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_2_0_CLK (net)
                  0.12    0.00    0.48 ^ clkbuf_4_11__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     8    0.11    0.13    0.23    0.71 ^ clkbuf_4_11__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_11__leaf_CLK (net)
                  0.13    0.00    0.71 ^ clkbuf_leaf_12_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    12    0.04    0.06    0.17    0.88 ^ clkbuf_leaf_12_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_12_CLK (net)
                  0.06    0.00    0.88 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_4)
                          0.00    0.88   clock reconvergence pessimism
                         -0.03    0.85   library hold time
                                  0.85   data required time
-----------------------------------------------------------------------------
                                  0.85   data required time
                                 -1.14   data arrival time
-----------------------------------------------------------------------------
                                  0.29   slack (MET)



==========================================================================
cts final report_checks -path_delay max
--------------------------------------------------------------------------
Startpoint: core.CPU_is_slli_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.15    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01    0.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00    0.24 ^ clkbuf_2_2_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.11    0.12    0.24    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_2_0_CLK (net)
                  0.12    0.00    0.48 ^ clkbuf_4_8__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     5    0.19    0.20    0.28    0.76 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8__leaf_CLK (net)
                  0.20    0.00    0.76 ^ clkbuf_leaf_3_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.19    0.96 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_3_CLK (net)
                  0.06    0.00    0.96 ^ core.CPU_is_slli_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.05    0.31    1.27 ^ core.CPU_is_slli_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_is_slli_a3 (net)
                  0.05    0.00    1.27 ^ place432/A (sky130_fd_sc_hd__buf_4)
    20    0.09    0.26    0.27    1.54 ^ place432/X (sky130_fd_sc_hd__buf_4)
                                         net431 (net)
                  0.26    0.00    1.54 ^ _07509_/S (sky130_fd_sc_hd__mux2i_4)
     1    0.00    0.12    0.26    1.80 ^ _07509_/Y (sky130_fd_sc_hd__mux2i_4)
                                         _02621_ (net)
                  0.12    0.00    1.80 ^ place389/A (sky130_fd_sc_hd__buf_4)
    34    0.23    0.61    0.53    2.33 ^ place389/X (sky130_fd_sc_hd__buf_4)
                                         net388 (net)
                  0.61    0.01    2.34 ^ _07689_/S0 (sky130_fd_sc_hd__mux4_2)
     3    0.01    0.12    0.64    2.98 v _07689_/X (sky130_fd_sc_hd__mux4_2)
                                         _02798_ (net)
                  0.12    0.00    2.98 v _07690_/B (sky130_fd_sc_hd__and2_1)
     1    0.00    0.04    0.18    3.16 v _07690_/X (sky130_fd_sc_hd__and2_1)
                                         _02799_ (net)
                  0.04    0.00    3.16 v _07691_/B1 (sky130_fd_sc_hd__a211o_1)
     2    0.01    0.07    0.28    3.45 v _07691_/X (sky130_fd_sc_hd__a211o_1)
                                         _02800_ (net)
                  0.07    0.00    3.45 v _08380_/B (sky130_fd_sc_hd__nand3_1)
     1    0.00    0.08    0.09    3.54 ^ _08380_/Y (sky130_fd_sc_hd__nand3_1)
                                         _03472_ (net)
                  0.08    0.00    3.54 ^ _08381_/D_N (sky130_fd_sc_hd__nor4b_1)
     1    0.01    0.63    0.54    4.08 ^ _08381_/Y (sky130_fd_sc_hd__nor4b_1)
                                         _03473_ (net)
                  0.63    0.00    4.08 ^ _08382_/B1 (sky130_fd_sc_hd__o32ai_1)
     2    0.02    0.25    0.33    4.41 v _08382_/Y (sky130_fd_sc_hd__o32ai_1)
                                         _03474_ (net)
                  0.25    0.00    4.41 v place266/A (sky130_fd_sc_hd__buf_4)
     2    0.01    0.04    0.23    4.64 v place266/X (sky130_fd_sc_hd__buf_4)
                                         net265 (net)
                  0.04    0.00    4.64 v _08383_/B (sky130_fd_sc_hd__nand2_1)
     1    0.01    0.12    0.11    4.75 ^ _08383_/Y (sky130_fd_sc_hd__nand2_1)
                                         _03475_ (net)
                  0.12    0.00    4.75 ^ _08384_/A2_N (sky130_fd_sc_hd__a2bb2oi_2)
    11    0.05    0.63    0.51    5.26 ^ _08384_/Y (sky130_fd_sc_hd__a2bb2oi_2)
                                         _03476_ (net)
                  0.63    0.00    5.26 ^ _08817_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.13    0.14    5.40 v _08817_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00837_ (net)
                  0.13    0.00    5.40 v core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.40   data arrival time

                         11.00   11.00   clock clk (rise edge)
                          0.00   11.00   clock source latency
     1    0.15    0.00    0.00   11.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01   11.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23   11.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00   11.24 ^ clkbuf_2_1_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.09    0.11    0.23   11.47 ^ clkbuf_2_1_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_1_0_CLK (net)
                  0.11    0.00   11.47 ^ clkbuf_4_7__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.11    0.13    0.22   11.69 ^ clkbuf_4_7__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_7__leaf_CLK (net)
                  0.13    0.00   11.69 ^ clkbuf_leaf_44_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.04    0.06    0.17   11.86 ^ clkbuf_leaf_44_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_44_CLK (net)
                  0.06    0.00   11.86 ^ core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.00   11.86   clock reconvergence pessimism
                         -0.14   11.71   library setup time
                                 11.71   data required time
-----------------------------------------------------------------------------
                                 11.71   data required time
                                 -5.40   data arrival time
-----------------------------------------------------------------------------
                                  6.31   slack (MET)



==========================================================================
cts final report_checks -unconstrained
--------------------------------------------------------------------------
Startpoint: core.CPU_is_slli_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

Fanout     Cap    Slew   Delay    Time   Description
-----------------------------------------------------------------------------
                          0.00    0.00   clock clk (rise edge)
                          0.00    0.00   clock source latency
     1    0.15    0.00    0.00    0.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01    0.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00    0.24 ^ clkbuf_2_2_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.11    0.12    0.24    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_2_0_CLK (net)
                  0.12    0.00    0.48 ^ clkbuf_4_8__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     5    0.19    0.20    0.28    0.76 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_8__leaf_CLK (net)
                  0.20    0.00    0.76 ^ clkbuf_leaf_3_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    13    0.04    0.06    0.19    0.96 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_3_CLK (net)
                  0.06    0.00    0.96 ^ core.CPU_is_slli_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
     1    0.00    0.05    0.31    1.27 ^ core.CPU_is_slli_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
                                         core.CPU_is_slli_a3 (net)
                  0.05    0.00    1.27 ^ place432/A (sky130_fd_sc_hd__buf_4)
    20    0.09    0.26    0.27    1.54 ^ place432/X (sky130_fd_sc_hd__buf_4)
                                         net431 (net)
                  0.26    0.00    1.54 ^ _07509_/S (sky130_fd_sc_hd__mux2i_4)
     1    0.00    0.12    0.26    1.80 ^ _07509_/Y (sky130_fd_sc_hd__mux2i_4)
                                         _02621_ (net)
                  0.12    0.00    1.80 ^ place389/A (sky130_fd_sc_hd__buf_4)
    34    0.23    0.61    0.53    2.33 ^ place389/X (sky130_fd_sc_hd__buf_4)
                                         net388 (net)
                  0.61    0.01    2.34 ^ _07689_/S0 (sky130_fd_sc_hd__mux4_2)
     3    0.01    0.12    0.64    2.98 v _07689_/X (sky130_fd_sc_hd__mux4_2)
                                         _02798_ (net)
                  0.12    0.00    2.98 v _07690_/B (sky130_fd_sc_hd__and2_1)
     1    0.00    0.04    0.18    3.16 v _07690_/X (sky130_fd_sc_hd__and2_1)
                                         _02799_ (net)
                  0.04    0.00    3.16 v _07691_/B1 (sky130_fd_sc_hd__a211o_1)
     2    0.01    0.07    0.28    3.45 v _07691_/X (sky130_fd_sc_hd__a211o_1)
                                         _02800_ (net)
                  0.07    0.00    3.45 v _08380_/B (sky130_fd_sc_hd__nand3_1)
     1    0.00    0.08    0.09    3.54 ^ _08380_/Y (sky130_fd_sc_hd__nand3_1)
                                         _03472_ (net)
                  0.08    0.00    3.54 ^ _08381_/D_N (sky130_fd_sc_hd__nor4b_1)
     1    0.01    0.63    0.54    4.08 ^ _08381_/Y (sky130_fd_sc_hd__nor4b_1)
                                         _03473_ (net)
                  0.63    0.00    4.08 ^ _08382_/B1 (sky130_fd_sc_hd__o32ai_1)
     2    0.02    0.25    0.33    4.41 v _08382_/Y (sky130_fd_sc_hd__o32ai_1)
                                         _03474_ (net)
                  0.25    0.00    4.41 v place266/A (sky130_fd_sc_hd__buf_4)
     2    0.01    0.04    0.23    4.64 v place266/X (sky130_fd_sc_hd__buf_4)
                                         net265 (net)
                  0.04    0.00    4.64 v _08383_/B (sky130_fd_sc_hd__nand2_1)
     1    0.01    0.12    0.11    4.75 ^ _08383_/Y (sky130_fd_sc_hd__nand2_1)
                                         _03475_ (net)
                  0.12    0.00    4.75 ^ _08384_/A2_N (sky130_fd_sc_hd__a2bb2oi_2)
    11    0.05    0.63    0.51    5.26 ^ _08384_/Y (sky130_fd_sc_hd__a2bb2oi_2)
                                         _03476_ (net)
                  0.63    0.00    5.26 ^ _08817_/A1 (sky130_fd_sc_hd__a21oi_1)
     1    0.00    0.13    0.14    5.40 v _08817_/Y (sky130_fd_sc_hd__a21oi_1)
                                         _00837_ (net)
                  0.13    0.00    5.40 v core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
                                  5.40   data arrival time

                         11.00   11.00   clock clk (rise edge)
                          0.00   11.00   clock source latency
     1    0.15    0.00    0.00   11.00 ^ pll/CLK (avsdpll)
                                         CLK (net)
                  0.01    0.01   11.01 ^ clkbuf_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.18    0.19    0.23   11.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_0_CLK (net)
                  0.19    0.00   11.24 ^ clkbuf_2_1_0_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     4    0.09    0.11    0.23   11.47 ^ clkbuf_2_1_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_2_1_0_CLK (net)
                  0.11    0.00   11.47 ^ clkbuf_4_7__f_CLK/A (sky130_fd_sc_hd__clkbuf_16)
     7    0.11    0.13    0.22   11.69 ^ clkbuf_4_7__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_4_7__leaf_CLK (net)
                  0.13    0.00   11.69 ^ clkbuf_leaf_44_CLK/A (sky130_fd_sc_hd__clkbuf_16)
    10    0.04    0.06    0.17   11.86 ^ clkbuf_leaf_44_CLK/X (sky130_fd_sc_hd__clkbuf_16)
                                         clknet_leaf_44_CLK (net)
                  0.06    0.00   11.86 ^ core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
                          0.00   11.86   clock reconvergence pessimism
                         -0.14   11.71   library setup time
                                 11.71   data required time
-----------------------------------------------------------------------------
                                 11.71   data required time
                                 -5.40   data arrival time
-----------------------------------------------------------------------------
                                  6.31   slack (MET)



==========================================================================
cts final report_check_types -max_slew -max_cap -max_fanout -violators
--------------------------------------------------------------------------

==========================================================================
cts final max_slew_check_slack
--------------------------------------------------------------------------
0.24299751222133636

==========================================================================
cts final max_slew_check_limit
--------------------------------------------------------------------------
1.4953149557113647

==========================================================================
cts final max_slew_check_slack_limit
--------------------------------------------------------------------------
0.1625

==========================================================================
cts final max_fanout_check_slack
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_fanout_check_limit
--------------------------------------------------------------------------
1.0000000150474662e+30

==========================================================================
cts final max_capacitance_check_slack
--------------------------------------------------------------------------
0.013586003333330154

==========================================================================
cts final max_capacitance_check_limit
--------------------------------------------------------------------------
0.021067000925540924

==========================================================================
cts final max_capacitance_check_slack_limit
--------------------------------------------------------------------------
0.6449

==========================================================================
cts final max_slew_violation_count
--------------------------------------------------------------------------
max slew violation count 0

==========================================================================
cts final max_fanout_violation_count
--------------------------------------------------------------------------
max fanout violation count 0

==========================================================================
cts final max_cap_violation_count
--------------------------------------------------------------------------
max cap violation count 0

==========================================================================
cts final setup_violation_count
--------------------------------------------------------------------------
setup violation count 0

==========================================================================
cts final hold_violation_count
--------------------------------------------------------------------------
hold violation count 0

==========================================================================
cts final report_checks -path_delay max reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_is_slli_a3$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: max

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.25    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.28    0.76 ^ clkbuf_4_8__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.20    0.96 ^ clkbuf_leaf_3_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.96 ^ core.CPU_is_slli_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.31    1.27 ^ core.CPU_is_slli_a3$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.27    1.54 ^ place432/X (sky130_fd_sc_hd__buf_4)
   0.26    1.80 ^ _07509_/Y (sky130_fd_sc_hd__mux2i_4)
   0.53    2.33 ^ place389/X (sky130_fd_sc_hd__buf_4)
   0.65    2.98 v _07689_/X (sky130_fd_sc_hd__mux4_2)
   0.18    3.16 v _07690_/X (sky130_fd_sc_hd__and2_1)
   0.28    3.45 v _07691_/X (sky130_fd_sc_hd__a211o_1)
   0.09    3.54 ^ _08380_/Y (sky130_fd_sc_hd__nand3_1)
   0.54    4.08 ^ _08381_/Y (sky130_fd_sc_hd__nor4b_1)
   0.33    4.41 v _08382_/Y (sky130_fd_sc_hd__o32ai_1)
   0.23    4.64 v place266/X (sky130_fd_sc_hd__buf_4)
   0.11    4.75 ^ _08383_/Y (sky130_fd_sc_hd__nand2_1)
   0.51    5.26 ^ _08384_/Y (sky130_fd_sc_hd__a2bb2oi_2)
   0.14    5.40 v _08817_/Y (sky130_fd_sc_hd__a21oi_1)
   0.00    5.40 v core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/D (sky130_fd_sc_hd__dfxtp_1)
           5.40   data arrival time

  11.00   11.00   clock clk (rise edge)
   0.00   11.00   clock source latency
   0.00   11.00 ^ pll/CLK (avsdpll)
   0.23   11.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.23   11.47 ^ clkbuf_2_1_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.22   11.69 ^ clkbuf_4_7__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.17   11.86 ^ clkbuf_leaf_44_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00   11.86 ^ core.CPU_Xreg_value_a4[16][29]$_SDFFE_PP0P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.00   11.86   clock reconvergence pessimism
  -0.14   11.71   library setup time
          11.71   data required time
---------------------------------------------------------
          11.71   data required time
          -5.40   data arrival time
---------------------------------------------------------
           6.31   slack (MET)



==========================================================================
cts final report_checks -path_delay min reg to reg
--------------------------------------------------------------------------
Startpoint: core.CPU_reset_a2$_DFF_P_
            (rising edge-triggered flip-flop clocked by clk)
Endpoint: core.CPU_reset_a3$_DFF_P_
          (rising edge-triggered flip-flop clocked by clk)
Path Group: clk
Path Type: min

  Delay    Time   Description
---------------------------------------------------------
   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.25    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.21    0.69 ^ clkbuf_4_9__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.16    0.85 ^ clkbuf_leaf_13_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.85 ^ core.CPU_reset_a2$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_1)
   0.29    1.14 v core.CPU_reset_a2$_DFF_P_/Q (sky130_fd_sc_hd__dfxtp_1)
   0.00    1.14 v core.CPU_reset_a3$_DFF_P_/D (sky130_fd_sc_hd__dfxtp_4)
           1.14   data arrival time

   0.00    0.00   clock clk (rise edge)
   0.00    0.00   clock source latency
   0.00    0.00 ^ pll/CLK (avsdpll)
   0.23    0.23 ^ clkbuf_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.25    0.48 ^ clkbuf_2_2_0_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.23    0.71 ^ clkbuf_4_11__f_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.17    0.88 ^ clkbuf_leaf_12_CLK/X (sky130_fd_sc_hd__clkbuf_16)
   0.00    0.88 ^ core.CPU_reset_a3$_DFF_P_/CLK (sky130_fd_sc_hd__dfxtp_4)
   0.00    0.88   clock reconvergence pessimism
  -0.03    0.85   library hold time
           0.85   data required time
---------------------------------------------------------
           0.85   data required time
          -1.14   data arrival time
---------------------------------------------------------
           0.29   slack (MET)



==========================================================================
cts final critical path target clock latency max path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path target clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path source clock latency min path
--------------------------------------------------------------------------
0

==========================================================================
cts final critical path delay
--------------------------------------------------------------------------
5.4019

==========================================================================
cts final critical path slack
--------------------------------------------------------------------------
6.3128

==========================================================================
cts final slack div critical path delay
--------------------------------------------------------------------------
116.862585

==========================================================================
cts final report_power
--------------------------------------------------------------------------
Group                  Internal  Switching    Leakage      Total
                          Power      Power      Power      Power (Watts)
----------------------------------------------------------------
Sequential             4.38e-03   3.79e-04   9.27e-09   4.76e-03  38.9%
Combinational          8.75e-04   1.94e-03   9.60e-09   2.82e-03  23.0%
Clock                  2.62e-03   2.04e-03   2.19e-09   4.67e-03  38.1%
Macro                  0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
Pad                    0.00e+00   0.00e+00   0.00e+00   0.00e+00   0.0%
----------------------------------------------------------------
Total                  7.88e-03   4.37e-03   2.11e-08   1.23e-02 100.0%
                          64.3%      35.7%       0.0%

```
</details>


### `run routing`

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk route
```

<img width="736" height="531" alt="image" src="https://github.com/user-attachments/assets/e42452f6-061c-4eb7-9e62-ff454e9e76f7" />

<img width="1288" height="728" alt="image" src="https://github.com/user-attachments/assets/a6910fb7-411a-42d9-8cf2-aa49ec42dd7e" />

**Routing Result (GUI)**

```shell
make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk gui_route
```
This image shows the **post-routing stage**. The highlighted net `VCO_IN` is fully routed, with its details such as signal type, wire type, and bounding box displayed in the Inspector.

<img width="1919" height="913" alt="image" src="https://github.com/user-attachments/assets/4b19bc05-841d-4f75-8b69-bf9a37c917ac" />


<img width="1919" height="912" alt="image" src="https://github.com/user-attachments/assets/670c2967-ffd9-4604-bb21-03f78cc0cc96" />

This image shows the **Routing Congestion Heatmap** after the routing stage. Areas with higher congestion are highlighted in **red**, while green regions indicate lower congestion. The highlighted net `_01595_` is fully routed, and its properties such as bounding box and connectivity details are shown in the Inspector.

<img width="1919" height="917" alt="image" src="https://github.com/user-attachments/assets/9496be76-bec7-4cd7-8814-e88dd1f22720" />

#### <ins>Formula for Congestion:</ins>

The routing congestion percentage is calculated as:

**Congestion (%) = (Used Routing Tracks ÷ Available Routing Tracks) × 100**

Where:
- **Used Routing Tracks** = Number of tracks occupied by wires in a specific region.
- **Available Routing Tracks** = Total routing capacity of that region.

#### <ins>Techniques to Reduce Routing Congestion:</ins>

1. **Increase Core Area / Die Size**
   - Enlarging the die provides more routing tracks and reduces congestion.
   
2. **Adjust Placement Density**
   - Lower the target density during placement to leave whitespace for routing.
   
3. **Add Placement Blockages**
   - Create routing blockages or halos around macros to avoid routing choke points.
   
4. **Cell Padding**
   - Add extra spacing between standard cells to reduce local congestion.
   
5. **Macro Repositioning**
   - Move large macros toward the periphery and keep enough channel spacing.
   
6. **Use Higher Metal Layers**
   - Assign global nets or critical signals to higher metal layers for better routing resources.
   
7. **Routing Layer Adjustment**
   - Allow more routing layers in congested designs.
   
8. **Congestion-Driven Placement**
   - Enable congestion-aware algorithms during placement in the EDA tool.
     
#### <ins>Timing Report after Routing:<ins>

After completing routing, run the following in the OpenROAD GUI → Scripting window:

```shell
report_checks
```

This command provides a detailed timing analysis of critical paths.

In the example below, the design meets timing with Slack = 5.94 ns (MET)

<img width="1596" height="903" alt="image" src="https://github.com/user-attachments/assets/e5b01577-630e-495e-81e9-1bf9fa2de7d6" />

The image shows various **log and JSON files** generated by the OpenROAD flow for each stage (e.g., floorplan, placement, CTS, routing, and filler cell insertion). These files provide detailed execution reports and design data for debugging and analysis.

<img width="1534" height="136" alt="image" src="https://github.com/user-attachments/assets/d57a8d0b-e33f-41f4-ad9e-2cd85aaa9ac4" />

### 🔄 Convert `.odb` to `.def` in OpenROAD

Follow the steps below to export a DEF file from an existing OpenDB (`.odb`) database.

```shell
cd ~/OpenROAD-flow-scripts
source env.sh
cd flow
openroad
# Load the .odb database file
read_db /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/results/sky130hd/vsdbabysoc/base/5_2_route.odb
# Write out the DEF file
write_def /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/results/sky130hd/vsdbabysoc/base/5_2_route.def
```
<img width="1605" height="452" alt="image" src="https://github.com/user-attachments/assets/e891a32e-505b-4fea-b1ae-3e68e14f0fd9" />

```shell
gvim /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/results/sky130hd/vsdbabysoc/base/5_2_route.def
```

<img width="1603" height="897" alt="image" src="https://github.com/user-attachments/assets/0c2dd2bb-3da7-45c2-8e6a-51b9af55d59a" />

### `VSDBabySoC post_route SPEF generation`

This section covers the step-by-step procedure to generate the **post-route Standard Parasitic Exchange Format (SPEF)** and **post-placement Verilog netlist** for the `VSDBabySoC` design using OpenROAD. These outputs are essential for accurate timing analysis and signoff after the routing stage. The SPEF file captures parasitic RC effects from the physical layout, while the updated Verilog reflects the final net connections post-placement and routing.

### `Step 1: Launch OpenROAD`

Before starting OpenROAD, set up the environment and navigate to the flow directory:

```bash
cd ~/OpenROAD-flow-scripts
source env.sh
cd flow/
openroad
```

<img width="1607" height="243" alt="image" src="https://github.com/user-attachments/assets/1a26815e-9ca3-4368-9a9c-5fc554f6d07c" />

### `Step 2: Load Design and Technology Files`

Once inside the OpenROAD shell, run the following commands in sequence to load the required design and technology data for VSDBabySoC:

These files describe the physical dimensions and metal/via layers for standard cells and macros:
```shell
read_lef /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lef/sky130hd.lef
read_lef /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lef/avsdpll.lef
read_lef /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/lef/avsddac.lef
```

This file contains timing and power data for the standard cells:
```shell
read_liberty /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/platforms/sky130hd/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

The DEF file represents the post-route physical layout of the design:
```shell
read_def /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/results/sky130hd/vsdbabysoc/base/5_2_route.def
```

<img width="1598" height="810" alt="image" src="https://github.com/user-attachments/assets/1dd0edee-58b8-41d5-afc4-b680e1e43e84" />

### `Step 3: RC Extraction and Output Generation`

After loading the LEF, Liberty, and DEF files, run the following commands to define the process corner and extract parasitics using the available `.calibre`-format model:

#### 🔹 1. Define Process Corner
Set the process corner using the available Calibre-based extraction rules file:

```tcl
define_process_corner -ext_model_index 0 /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/external-resources/open_pdks/sky130/openlane/rules.openrcx.sky130A.nom.calibre
```

#### 🔹 2. Extract Parasitics

Run parasitic extraction using the same file:

```shell
extract_parasitics -ext_model_file /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/external-resources/open_pdks/sky130/openlane/rules.openrcx.sky130A.nom.calibre
```

#### 🔹 3. Write SPEF File
Save the extracted parasitics:

```shell
write_spef /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/vsdbabysoc.spef
```

#### 🔹 4. Write Post-Placement Verilog Netlist
Save the netlist after placement and routing:

```shell
write_verilog /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/vsdbabysoc_post_place.v
```

<img width="738" height="291" alt="image" src="https://github.com/user-attachments/assets/0316c9e2-b1e7-4ac8-9996-d0f15eec04bd" />

The Standard Parasitic Exchange Format (SPEF) file captures the resistance and capacitance (RC) parasitics of interconnects extracted from the routed layout. This file is essential for accurate post-route static timing analysis (STA) as it models real-world wire delays caused by metal layers and vias. Tools like OpenSTA read the SPEF file to compute timing paths that reflect true physical behavior after routing. Generating and inspecting the SPEF ensures that your design is signoff-ready with precise timing estimates.

```shell
gvim /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/vsdbabysoc.spef
```

<img width="1602" height="899" alt="image" src="https://github.com/user-attachments/assets/f7a33941-a113-41aa-b223-cb0d6b0ca752" />

The post-placement Verilog netlist represents the logical connectivity of the design after placement and routing have been completed. This version of the netlist includes any modifications made by optimization or physical synthesis during the backend flow and ensures consistency with the final layout. It is used in downstream verification flows and enables correlation between logical simulation and physical implementation. Writing this netlist is crucial for timing closure and for validating the final connectivity of the design.

```shell
gvim /home/pathanrehman/Desktop/VLSI/OpenROAD-flow-scripts/flow/designs/sky130hd/vsdbabysoc/vsdbabysoc_post_place.v
```

<img width="1598" height="900" alt="image" src="https://github.com/user-attachments/assets/3dbf8d0c-82b3-4182-bfb1-6fa2b79cd925" />

This makes the end of flow of VSDBabySoC from architecture to post-layout. And this work all done by me (Pathan Rehman Ahmed Khan) from start to finish.
