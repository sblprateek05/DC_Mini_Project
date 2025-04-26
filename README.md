# DC Mini Project - NS-3 Simulation and Analysis

This project simulates and analyzes client loss ratios in a wireless network using ns-3, and visualizes the results.

---

## Project Structure

```
~/ns-3-dev/
├── main.sh
├── scratch/
│   └── main.cc
├── DC_Mini_Project/
│   ├── analyze.py
│   ├── plot.py
│   ├── plot2.py
│   ├── analyzeall.sh
│   ├── summerize.sh
│   ├── flowData/
│   │    ├── sv0-ps512/
│   │    └── sv0-ps1500/
│   ├── animData/
│   │    ├── sv0-ps512/
│   │    └── sv0-ps1500/
│   ├── analyzedData/
│   │    ├── sv0-ps512/
│   │    └── sv0-ps1500/
│   └── summarizedData/
└── (other ns-3 core files)
```

---

## How to Use

### 1. Run Simulations

```bash
cd ~/ns-3-dev/
bash main.sh
```

**main.sh**
- Creates directories:
  - `DC_Mini_Project/flowData/`
  - `DC_Mini_Project/flowData/sv0-ps512/`
  - `DC_Mini_Project/flowData/sv0-ps1500/`
  - `DC_Mini_Project/animData/`
  - `DC_Mini_Project/animData/sv0-ps512/`
  - `DC_Mini_Project/animData/sv0-ps1500/`
  - `DC_Mini_Project/analyzedData/`
  - `DC_Mini_Project/analyzedData/sv0-ps512/`
  - `DC_Mini_Project/analyzedData/sv0-ps1500/`
  - `DC_Mini_Project/summarizedData/`
- Builds ns-3.
- Runs simulations for node counts 2 to 30 for two packet sizes (512 and 1500 bytes).
- Moves FlowMonitor and NetAnim output files into appropriate folders.

### 2. Analyze Simulation Results

```bash
cd ~/ns-3-dev/DC_Mini_Project/
bash analyzeall.sh sv0-ps512
bash analyzeall.sh sv0-ps1500
```

**analyzeall.sh**
- Takes a configuration name as an argument (e.g., `sv0-ps512`).
- Analyzes each XML file using `analyze.py`.
- Generates `.txt` reports inside `analyzedData/<config>/`.
- Appends summarized client loss ratios to `summarizedData/<config>.csv`.

### 3. Summarize Important Metrics

```bash
bash summerize.sh sv0-ps512
bash summerize.sh sv0-ps1500
```

**summerize.sh**
- Takes a configuration name as an argument.
- Extracts and prints packet loss summaries from analyzed `.txt` files.

### 4. Plot and Compare Results

#### Main Plotting:
```bash
python3 plot.py
```

**plot.py**
- Reads `sv0-ps512.csv` and `sv0-ps1500.csv` from `summarizedData/`.
- Plots client loss ratio vs number of nodes.
- Saves the comparison plot as `summarizedData/client_loss_comparison.pdf`.

#### Optional Simple Plotting:
```bash
python3 plot2.py summarizedData/sv0-ps512.csv
python3 plot2.py summarizedData/sv0-ps1500.csv
```

**plot2.py**
- A lightweight plotting tool.
- Plots a simple visualization of client loss ratio for a single configuration.
- Saves the plot as a PDF next to the input `.csv` file.

---

## Output Files

- **FlowMonitor outputs** → `DC_Mini_Project/flowData/`
- **NetAnim animation files** → `DC_Mini_Project/animData/`
- **Analysis reports** → `DC_Mini_Project/analyzedData/`
- **Summarized CSV files** → `DC_Mini_Project/summarizedData/`
- **Comparison graph PDF** → `DC_Mini_Project/summarizedData/client_loss_comparison.pdf`

---

## Notes

- All scripts handle directory creation safely.
- All simulations run automatically for nodes 2 to 30.
- CSV files are generated automatically by `analyze.py`.
- The final graph cleanly compares RTS/CTS vs No RTS/CTS scenarios.
- Optional `plot2.py` is available for fast individual plotting.

---

> Project Developed for Data Communication Mini Project Assignment 🚀
