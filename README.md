# AMSA
This project is the official implementation of 'Coarse-to-Fine Embedded PatchMatch and Multi-Scale Dynamic Aggregation for Reference-based Super-Resolution', AAAI22

The code framework is mainly modified from [BasicSR](https://github.com/xinntao/BasicSR) and [MMSR](https://github.com/open-mmlab/mmediting) (Now reorganized as MMEditing). Please refer to the original repo for more usage and documents.

![Python 3.7](https://img.shields.io/badge/python-3.7-green.svg?style=plastic)
![pytorch 1.4.0](https://img.shields.io/badge/pytorch-1.4.0-green.svg?style=plastic)

[[Paper](https://arxiv.org/abs/2201.04358)]
[[Project Page](https://github.com/Zj-BinXia/AMSA)]

## Overview
![](AMSA/figs/process.jpg)

## Dependencies and Installation

- Python == 3.9.7
- PyTorch == 1.9.0
- CUDA >= 10.2
- GCC >= 7.5.0


0. Create Conda Environment
   ```bash
   conda create --prefix ./amsa_cu111 python=3.9.7
   conda activate ./amsa_cu111
   ```
1. Install Dependencies

   ```bash
   cd AMSA
   pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
   pip install mmcv==0.4.4
   pip install -r requirements.txt
   ```

1. Install MMSR and DCNv2

    ```bash
    python setup.py develop --user
    cd mmsr/models/archs/DCNv2
    python setup.py build develop --user
    ```


## Dataset Preparation

- Train Set: [CUFED Dataset](https://drive.google.com/drive/folders/1hGHy36XcmSZ1LtARWmGL5OK1IUdWJi3I)
- Test Set: [CUFED5 Dataset](https://drive.google.com/file/d/1Fa1mopExA9YGG1RxrCZZn7QFTYXLx6ph/view)

Please refer to [Datasets.md](datasets/DATASETS.md) for pre-processing and more details.

## Get Started

### Pretrained Models
Downloading the pretrained models from [GoogleDrive](https://drive.google.com/drive/folders/1XWv1O8l3-_VBWXRoPVV183ddYS31u-2_?usp=sharing) and put them under `experiments/pretrained_models folder`.
(part of the pretrained models are from this [link](https://drive.google.com/drive/folders/1dTkXMzeBrHelVQUEx5zib5MdmvqDaSd9?usp=sharing))
### Test

We provide quick test code with the pretrained model.

1. Modify the paths to dataset and pretrained model in the following yaml files for configuration.

    ```bash
    ./options/test/test_AMSA.yml
    ./options/test/test_AMSA_mse.yml
    ```

1. Run test code for models trained using **GAN loss**.

    ```bash
    python mmsr/test.py -opt "options/test/test_AMSA.yml"
    ```

   Check out the results in `./results`.

1. Run test code for models trained using only **reconstruction loss**.

    ```bash
    python mmsr/test.py -opt "options/test/test_AMSA_mse.yml"
    ```

   Check out the results in in `./results`


### Train

Downloading the pretrained feature extraction models from C2-Matching  [link](https://drive.google.com/drive/folders/1dTkXMzeBrHelVQUEx5zib5MdmvqDaSd9?usp=sharing) and put "feature_extraction.pth" under `experiments/pretrained_models folder`.

All logging files in the training process, *e.g.*, log message, checkpoints, and snapshots, will be saved to `./experiments` and `./tb_logger` directory.


1.  Train restoration network.
   ```bash
   # add the path to *pretrain_model_feature_extractor* in the following yaml
   # the path to *pretrain_model_feature_extractor* is the model obtained in C2-Matching
   ./options/train/stage3_restoration_gan.yml
   python mmsr/train.py -opt "options/train/stage3_restoration_gan.yml"

   # if you wish to train the restoration network with only mse loss
   # prepare the dataset path and pretrained model path in the following yaml
   ./options/train/stage3_restoration_mse.yml
   python mmsr/train.py -opt "options/train/stage3_restoration_mse.yml"
   ```

## Results

![](AMSA/figs/quan.jpg)

![](AMSA/figs/qual.jpg)

## Citation

   If you find our repo useful for your research, please consider citing our paper:

   ```bibtex
   @article{xia2022coarse,
  title={Coarse-to-Fine Embedded PatchMatch and Multi-Scale Dynamic Aggregation for Reference-based Super-Resolution},
  author={Xia, Bin and Tian, Yapeng and Hang, Yucheng and Yang, Wenming and Liao, Qingmin and Zhou, Jie},
  booktitle={AAAI},
  year={2022}
}
   ```
