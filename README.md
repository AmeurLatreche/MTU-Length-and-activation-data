# MTU-Length-and-activation-data

Overview

The software used is Mathematica

This repository contains muscle–tendon unit (MTU) lengths and processed EMG signals for one participant (Sub03) performing 8 lower-limb tasks over 25 s each:

- walk
- run
- hop
- sit-to-stand

For each task, data are provided for 10 lower-limb muscles:
TA (tibialis anterior)
LG (lateral gastrocnemius)
MG (medial gastrocnemius)
Sol (soleus)
VL (vastus lateralis)
RF (rectus femoris)
VM (vastus medialis)
BF (biceps femoris, long head)
ST (semitendinosus)
GM (gluteus maximus)

The dataset is intended for use in musculoskeletal simulations, EMG-driven models, and studies of neuromuscular control across different functional tasks.
File structure
1. MTU length files (.mot)

Raw MTU lengths exported from OpenSim:

Sub03_(1)walk1_MTU length_10 muscles for 25s.mot
Sub03_(2)run1_MTU length_10 muscles for 25s.mot
Sub03_(3)hop1_MTU length_10 muscles for 25s.mot
Sub03_(4)sts1_MTU length_10 muscles for 25s.mot
Sub03_(5)sts2_MTU length_10 muscles for 25s.mot
Sub03_(6)hop2_MTU length_10 muscles for 25s.mot
Sub03_(7)run2_MTU length_10 muscles for 25s.mot
Sub03_(8)walk2_MTU length_10 muscles for 25s.mot

2. EMG + MTU files (_Sqrt_NormalizedIemg_Lmtu_10muscles.xls)

For each task, EMG and MTU length are combined in an Excel file:

Sub03_(1)walk1_Sqrt_NormalizedIemg_Lmtu_10muscles.xls
...
Sub03_(8)walk2_Sqrt_NormalizedIemg_Lmtu_10muscles.xls


---

## Data format

### MTU length files (`.mot`)
The `.mot` files are OpenSim storage files (tabular, TSV-like) and typically contain:
- Header lines (metadata)
- A `time` column (s)
- One column per muscle MTU length signal

> **Note:** In the Mathematica notebook, the numeric data are read starting from **row 8** (i.e., the first 7 rows are treated as header).

### EMG + MTU combined files (`.xls`)
Each combined Excel file contains (per trial):
- 3 header rows (dataset and column descriptors)
- A data table with:
  - `frame`
  - `time`
  - for each muscle: paired columns **(I EMG, L MTU)**

The paired structure is repeated 10 times in the fixed muscle order described above.

---

## Mathematica notebook: what we did (`The script.nb`)

All post-processing and packaging were done in **Wolfram Mathematica** using the notebook `The script.nb`.  
The notebook performs four main steps:

### 1) Import MTU length from OpenSim `.mot`
- The notebook sets the working directory to the folder containing the OpenSim `.mot` files (`SetDirectory[...]`).
- It loads each `.mot` file with `Import[file,"TSV"]`.
- It extracts the time vector and MTU columns from **row 8 onward**.

### 2) Re-order MTU columns into a consistent muscle order
OpenSim exports can have different column ordering. To enforce a consistent order across trials, the notebook remaps MTU columns using a fixed index vector:

**Muscle order enforced throughout the notebook:**
1. TA  
2. LG  
3. MG  
4. Sol  
5. VL  
6. RF  
7. VM  
8. BF (long head)  
9. ST  
10. GM  

This ensures that MTU-length vectors always align with the same muscle order in the exported `.xls` files.

### 3) Build the combined EMG + MTU Excel files
For each trial:
- The notebook prepares three header rows:
  - row 1: filename/descriptor
  - row 2: muscle names (with spacing to reflect paired columns)
  - row 3: column labels (`frame`, `time`, then repeating `I EMG`, `L MTU`)
- It then creates one data row per frame:
  - `frame`, `time`,
  - then for each muscle: **I EMG** (processed EMG) followed by **L MTU** (MTU length)

Finally, it exports:
- `Sub03_(*)*_Sqrt_NormalizedIemg_Lmtu_10muscles.xls`

### 4) Optional baseline standardization (“changed initial status”)
The notebook also contains an optional post-processing step that creates a baseline-adjusted version of each combined `.xls` file:
- It identifies a reference index at **t = 5.0 s**
- **MTU length baseline**: for each muscle, it stabilizes the initial MTU segment by setting early samples to a constant reference value (based on a median-crossing logic).
- **EMG baseline**: for each muscle, it finds a minimum EMG value within a short window and sets EMG to **0** from the beginning of the trial up to that point (to remove early offsets / pre-activation artifacts).
- It exports the adjusted file as:
  - `*_changed initial status.xls`

> Different tasks may use different window lengths for the EMG baseline trimming step (because walking/running/hopping/STS have different cycle timing).

---

## How to reproduce the processing
1. Open `The script.nb` in Mathematica.
2. Update all `SetDirectory["..."]` paths to match your local folder structure:
   - the folder containing the MTU `.mot` files
   - the output folder where `.xls` files will be written
3. Evaluate the notebook cells top-to-bottom to generate:
   - the combined `*_Sqrt_NormalizedIemg_Lmtu_10muscles.xls` files
   - optionally, the `*_changed initial status.xls` files

---

## Notes / intended use
This dataset is intended for:
- musculoskeletal simulation workflows (e.g., mapping MTU length trajectories to muscle models),
- EMG-driven modeling,
- neuromuscular control analyses and task comparisons (walk/run/hop/STS).



