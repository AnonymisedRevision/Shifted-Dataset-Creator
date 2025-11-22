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
