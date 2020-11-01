# GaitGL


# NOTE
This repo is based on [GaitSet](https://github.com/AbnerHqC/GaitSet)


## Prerequisites

- Python 3.7
- PyTorch 1.1
- CUDA 10.2

### Dataset & Preparation
Download [OU-MVLP Dataset](http://www.am.sanken.osaka-u.ac.jp/BiometricDB/GaitMVLP.html).

**!!! ATTENTION !!! ATTENTION !!! ATTENTION !!!**

Before training or test, please make sure you have prepared the dataset
by this two steps:
- **Step1:** Organize the directory as: 
`your_dataset_path/subject_ids/walking_conditions/views`.
E.g. `OUMVLP/00001/00/000/`.
- **Step2:** Cut and align the raw silhouettes with `pretreatment_oumvlp.py`.
the silhouettes after pretreatment **MUST have a size of 64x64**.

#### Pretreatment
`pretreatment_oumvlp.py` uses the alignment method in
[this paper](https://ipsjcva.springeropen.com/articles/10.1186/s41074-018-0039-6).
Pretreatment your dataset by
```
python pretreatment_oumvlp.py --input_path='root_path_of_raw_dataset' --output_path='root_path_for_output'
```
- `--input_path` **(NECESSARY)** Root path of raw dataset.
- `--output_path` **(NECESSARY)** Root path for output.
- `--log_file` Log file path. #Default: './pretreatment.log'
- `--log` If set as True, all logs will be saved. 
Otherwise, only warnings and errors will be saved. #Default: False
- `--worker_num` How many subprocesses to use for data pretreatment. Default: 1

### Train
Train a model by
```bash
python train.py
```
- `--cache` if set as TRUE all the training data will be loaded at once before the training start.
This will accelerate the training.
**Note that** if this arg is set as FALSE, samples will NOT be kept in the memory
even they have been used in the former iterations. #Default: TRUE

### Evaluation
Evaluate the trained model by
```bash
python test_oumvlp.py
```
- `--iter` iteration of the checkpoint to load. #Default: 250000
- `--batch_size` batch size of the parallel test. #Default: 1
- `--cache` if set as TRUE all the test data will be loaded at once before the transforming start.
This might accelerate the testing. #Default: FALSE

#----------- CAISA-E---------------------------------
### Train
Train a model by
```bash
python train.py
```
**!!! ATTENTION !!! ATTENTION !!! ATTENTION !!!**
Pre-training parameters need to be added.
