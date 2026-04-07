# Joint Answering and Explanation for Visual Commonsense Reasoning

> PyTorch code and data organization instructions for joint answer prediction and rationale generation on Visual Commonsense Reasoning (VCR).

## Authors

> Zhenyang Li, Yangyang Guo, Kejie Wang, Yinwei Wei, Liqiang Nie, Mohan Kankanhalli

## Links

- **Paper**: [arXiv](https://arxiv.org/abs/2202.12626)
- **Code Repository**: [GitHub](https://github.com/iLearn-Lab/ACMMM24-AD-DRL)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Method / Framework](#method--framework)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Checkpoints / Models](#checkpoints--models)
- [Dataset / Benchmark](#dataset--benchmark)
- [Usage](#usage)
- [Demo / Visualization](#demo--visualization)
- [TODO](#todo)
- [Citation](#citation)
- [Acknowledgement](#acknowledgement)
- [License](#license)

---

## Updates

- [02/2022] Release paper / arXiv version
- [02/2022] Initial code release
- [TBD] Release precomputed logits / representations
- [TBD] Release checkpoints

---

## Introduction

This repository provides data organization instructions and PyTorch code for the paper **Joint Answering and Explanation for Visual Commonsense Reasoning**.

The project targets **Visual Commonsense Reasoning (VCR)**, where a model needs to predict both the correct answer and the supporting rationale. This repository includes training and evaluation pipelines built on top of multiple VCR baselines, together with the required data layout for reproducing the experiments.

The repository currently provides:

- training scripts
- evaluation scripts
- data organization instructions
- multiple model branches based on existing VCR baselines
- placeholders for pretrained checkpoints and precomputed representations

---

## Highlights

- Supports **joint answering and explanation** for **Visual Commonsense Reasoning**
- Includes training / evaluation pipelines for **R2C + Ours**, **CCN + Ours**, and **TAB-VCR + Ours**
- Provides a clear **dataset organization format** for train / val / test splits
- Suitable for **paper reproduction**, **benchmark comparison**, and **follow-up research**

---

## Method / Framework

This repository implements our method on top of three VCR baselines:

- **R2C + Ours**
- **CCN + Ours**
- **TAB-VCR + Ours**

If you have a framework figure, you can place it under `./assets/` and add it here later:

```markdown
![Framework](./assets/framework.png)
```

**Figure 1.** Overall framework of the method for joint answering and explanation on VCR.

---

## Project Structure

```text
.
├── data/
│   ├── train/
│   ├── val/
│   ├── test/
│   ├── train_pickles_first_sense_match/
│   ├── val_pickles_first_sense_match/
│   ├── test_pickles_first_sense_match/
│   └── vcr1images/
├── r2c_kd/                  # R2C-based implementation
├── CCN_kd/                  # CCN-based implementation
├── tab-vcr-master_kd/       # TAB-VCR-based implementation
└── README.md
```

Please adjust this section if your final repository structure differs from the current one.

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/iLearn-Lab/ACMMM24-AD-DRL.git
cd ACMMM24-AD-DRL
```

### 2. Prepare the environment and dataset

This repository is based on the following projects:

- [R2C](https://github.com/rowanz/r2c)
- [CCN](https://github.com/AmingWu/CCN)
- [TAB-VCR](https://github.com/Deanplayerljx/tab-vcr)

Please follow the corresponding repositories to:

- download the **VCR dataset**
- prepare the required runtime environment
- install dependencies for each baseline branch

### 3. Download precomputed QR->A logits and representations

> Download links are not provided in the original README yet. Please replace this section with the actual release links.

### 4. Organize the data files

Reorganize the dataset as follows:

```text
data
├── test_pickles_first_sense_match
├── train_pickles_first_sense_match
├── val_pickles_first_sense_match
├── vcr1images
├── train
│   ├── train.jsonl
│   ├── attribute_features_train.h5
│   ├── bert_da_answer_train.h5
│   ├── bert_da_rationale_train.h5
│   ├── new_tag_features_train.h5
│   ├── r2c_qr2a_train.h5
│   ├── ccn_qr2a_train.h5
│   └── tab_qr2a_train.h5
├── val
│   ├── val.jsonl
│   ├── attribute_features_val.h5
│   ├── bert_da_answer_val.h5
│   ├── bert_da_rationale_val.h5
│   ├── new_tag_features_val.h5
│   ├── r2c_qr2a_val.h5
│   ├── ccn_qr2a_val.h5
│   └── tab_qr2a_val.h5
└── test
    ├── test.jsonl
    ├── attribute_features_test.h5
    ├── bert_da_answer_test.h5
    ├── bert_da_rationale_test.h5
    └── new_tag_features_test.h5
```

---

## Checkpoints / Models

If you do not want to train from scratch, you can prepare released checkpoints here.

- **Precomputed QR->A logits / representations**: `TBD`
- **Model checkpoints**: `TBD`

Suggested directory:

```text
checkpoints/
```

> Please update this section once the actual checkpoint links are available.

---

## Dataset / Benchmark

- **Task**: Visual Commonsense Reasoning (VCR)
- **Dataset**: Please download the VCR dataset from the official resources referenced by the baseline repositories

Expected data layout:

```text
data/
├── train/
├── val/
└── test/
```

This project additionally relies on auxiliary HDF5 features and precomputed logits as shown in the data organization tree above.

---

## Usage

### Training

#### 1. R2C + Ours

```bash
cd r2c_kd/models && python train_kd_infonce.py -params=kd/model_kd_infonce.json -folder={path_to_save_model_checkpoints} -plot {plot_name}
```

#### 2. CCN + Ours

```bash
cd CCN_kd/train && python train_kd_infonce.py -params=../kd/model_kd_infonce.json -folder={path_to_save_model_checkpoints} -plot {plot_name}
```

#### 3. TAB-VCR + Ours

```bash
cd tab-vcr-master_kd/models && python my_train_kd_infonce.py -params=kd/default_kd_infonce.json -folder={path_to_save_model_checkpoints} -plot {plot_name}
```

### Evaluation

#### 1. R2C + Ours

```bash
cd r2c_kd/models && python eval_best_checkpoint.py -params {path_to_your_model_config} -folder {path_to_model_checkpoints}
```

#### 2. CCN + Ours

```bash
cd CCN_kd/train && python eval_best_checkpoint.py -params {path_to_your_model_config} -folder {path_to_model_checkpoints}
```

#### 3. TAB-VCR + Ours

```bash
cd tab-vcr-master_kd/models && python my_eval_best_checkpoint.py -params {path_to_your_model_config} -folder {path_to_model_checkpoints}
```

> The best model checkpoint should be saved with the name `best`.

---

## Demo / Visualization

A public demo or project page is not provided in the original README.

You may later add:

- qualitative examples
- visualization results
- framework figures
- external demo or video links

---

## TODO

- [ ] Add the official author list
- [ ] Add released links for precomputed logits / representations
- [ ] Add released checkpoint links
- [ ] Add framework / pipeline figure
- [ ] Add demo or qualitative visualization examples
- [ ] Replace the placeholder citation with the official BibTeX

---

## Citation

If you find this repository useful, please cite the paper. Replace the placeholder below with the official BibTeX if needed.

```bibtex
@article{joint_answering_explanation_vcr,
  title={Joint Answering and Explanation for Visual Commonsense Reasoning},
  author={To be updated},
  journal={arXiv preprint arXiv:2202.12626},
  year={2022}
}
```

---

## Acknowledgement

This repository is based on the following open-source projects:

- [R2C](https://github.com/rowanz/r2c)
- [CCN](https://github.com/AmingWu/CCN)
- [TAB-VCR](https://github.com/Deanplayerljx/tab-vcr)

We thank the authors of these projects for their open-source contributions.

---

## License

No explicit license is specified in the current repository materials.

If you plan to release this project publicly, please add a license file and update this section accordingly.
