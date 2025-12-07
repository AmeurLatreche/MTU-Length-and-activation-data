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

