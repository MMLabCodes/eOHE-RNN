# eOHE-RNN

An algorithm to perform embedded One Hot Encoding (eOHE) on categorical data.

## Overview

This project uses the RNN model from ``Chemical language models enable navigation in sparsely populated chemical space (https://doi.org/10.1038/s42256-021-00368-1)'' from  Michael A. Skinnider, et. al. (https://github.com/skinnider/low-data-generative-models), and it has been modified to handle two different ways to perform eOHE, denominated eOHE-V1 and eOHE-V2.

## Info

Authors: Emilio Alexis de la Cruz Nuñez-Andrade, Isaac Vidal-Daza, James W. Ryan, Rafael Gómez-Bombarelli, Francisco J. Martín-Martínez


Swansea University, Massachusetts Institute of Technology, Universidad de Granada, 2023

## Installation

A `eohe_environment.yml` file has been provided with the necessary packages to run this project, to install it just run:

```bash
conda env create -f eohe_environment.yml
```
And you can activate it following the next command:

```bash
conda activate eohe
```

## eOHE Method

The description of Embedded One-Hot Encoding (eOHE) method can be found in our article:
"Embedded machine-readable molecular representation for more resource-efficient deep learning applications"



## Usage

To run the script, use the following command for SMILES and DeepSMILES:

```bash
python train_model.py --smiles_file QM9_sizes/qm9_smiles_size_1000_index_1.csv --embedding_size 0 --reduction_type reduction1 --output_dir QM9_m0_size_1000_index_1_enc_1 --batch_size 128 --sample_size 100000

python train_model.py --smiles_file QM9_sizes/qm9_deepsmiles_size_1000_index_1.csv --embedding_size 0 --reduction_type reduction1 --output_dir QM9_m1_size_1000_index_1_enc_1 --batch_size 128 --sample_size 100000

``` 
For the case of SELFIES, it is necessary to add the flag --selfies

```bash
python train_model.py --smiles_file QM9_sizes/qm9_selfies_size_1000_index_1.csv --selfies --embedding_size 0 --reduction_type reduction1 --output_dir QM9_m2_size_1000_index_1_enc_1 --batch_size 128 --sample_size 100000 
``` 

| Keyword          |  Status   | Description                                                                           |
|------------------|-----------|---------------------------------------------------------------------------------------|
| --smiles_file    | Mandatory | Path to subset that will be used to train model                                       |
| --embedding_size | Mandatory | Must be `0` in order to use OHE, eOHE-V1 or eOHE-V2                                   |
| --reduction_type | Mandatory | Choose one: `-reduction0` (OHE), `-reduction1` (eOHE-V1), `-reduction2` (eOHE-V2)     |
| --output_dir     | Mandatory | Directory to save results of training                                                 |
| --batch_size     | Mandatory | Our test were performed with batch size of `128`                                      |
| --sample_size    | Mandatory | Our test were performed with sample size of `100000`                                  |


The structure to name the output directories was:
{Database}_m{Molecular_encoding_index}_size_{subset_size}_index_{subset_index}_enc_{encoding_method}

| Keyword                    |  Possible values                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------|
| Database                   |  `QM9`, `GDB`, or  `ZINC`                                                                   |
| Molecular_encoding_index   | `0` for SMILES, `1` for DeepSMILES and `2` for SELFIES                                      |
| subset_size                | `1000`, `2500`, `5000`, ..., `500000`, check the available sizes in each database directory |
| subset_index               | `1`, `2`, `3`, ..., `10`                                                                    |
| encoding_method            | `0` for OHE, `1` for eOHE-V1 and `2` for eOHE-v2                                            |



``smiles_file.csv`` file must not have header. 

For quick testing, please select any of the smiles files subsets from QM9_sizes, GDB_sizes or ZINC_sizes 
directories from QM9, GDB or ZINC databases, respectively.

For example
 ``-smiles_file QM9_sizes/qm9_smiles_size_1000_index_1.csv``

## Contributing

Please log bugs through GitHub.


