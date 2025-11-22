# Distribution-Shifted-Dataset-Creator
A Research-oriented dataset-creator tool: Creates shifted-variants of a given dataset for simulating realistic/challenging distributional shifted environments (out-off distribution conditions) for benchmarking ML models' robustness ability in any given task.

![jsd_partition_skin(1)](https://github.com/user-attachments/assets/6c10adc3-1a9a-4a06-a505-4b24a1be115a)

## How it works:

In brief, it works via a clustering-based approach exploiting the Jensen–Shannon divergence (JSD) as the core partitioning measure/metric; JSD measures the relative entropy in information given two distributions.
The algorithm begins with partitioning the dataset into two subsets. The process continues iteratively by computing the centroids of the two sets and reassigning the instances closest to each one. This process ends up with two high-JSD-separated sets corresponding to the train vs test. The algorithm converges extremely fast.


## Input/Output data structure:

The given version is implemented for image data; but can be easily extended to any type of data.
Given a dataset in the following format:
```
data/
├── class1/
    ├── instance_1_1, instance_1_2, ...
├── class2/                 
    ├── instance_2_1, instance_2_2, ...
...
```
It will create a shifted variant with user-defined shift magnitude and spliting ratio: train/val vs shifted-test sets in the following format:
```
shifted_data/
├── train/
    ├── class1/
        ├── instance_1_1, instance_1_2, ...
    ├── class2/                 
        ├── instance_2_1, instance_2_2, ...
├── val/
    ...
├── test (OOD)/
    ...
```

## How to Run/Use

1. Open CONFIGS.py -->
```bash
GENERAL_CONFIG = {

    "DEBUG": 1, # <----- If want to debug (very fast run), then put here: 1 // else for full put: 0

    "ROOT_PATH" :'../data/DISTRIBUTIONAL_DRIFTED', # <-----  replace < data > with the name of root datafolder, e.g. SKIN_CANCER
    # Due to size restrictions in GitHub download from:
    # LINK:
    # https://drive.google.com/file/d/1RcZsiCOuFFWXuEoiVptNvP7lDTGWlhvh/view?usp=sharing

    "STORAGE_PATH" :'../_models_storage', # your output storage folder path / this will be used next for ProtoNeX
    "train_dir" :'train',
    "val_dir" :'val',
    "test_dir" :'test',
    }

# left values are for full run | right values for fast run (debuging if was set with 1)
GenE_CONFIG = {
    "SIZE": [224, 64][GENERAL_CONFIG["DEBUG"]], # images size // good results also the 144 size.
    "N": [50, 10][GENERAL_CONFIG["DEBUG"]], # number of generated models / size of output model pool M
    "G": [5, 2][GENERAL_CONFIG["DEBUG"]], # number of total generations
    }
sel = int (GenE_CONFIG['N']/GenE_CONFIG['G']) # number of geneticaly evolved selected networks per generation --> which are progressively stored into the M output folder
N_g = [ GenE_CONFIG['N'],  GenE_CONFIG['N'] // 2 ][GENERAL_CONFIG["DEBUG"]] # number of randomly selected parent pairs
```
read carefully the config instructions inside and specify your desired configurations.

2. Then, just run:
```bash 
main.py
```
and will produce the output folder format described above.


