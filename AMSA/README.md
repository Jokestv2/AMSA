# AMSA
This project is the official implementation of 'Coarse-to-Fine Embedded PatchMatch and Multi-Scale Dynamic Aggregation for Reference-based Super-Resolution', AAAI22

![Python 3.7](https://img.shields.io/badge/python-3.7-green.svg?style=plastic)
![pytorch 1.4.0](https://img.shields.io/badge/pytorch-1.4.0-green.svg?style=plastic)


## Dependencies and Installation

- Python == 3.9.7
- PyTorch == 1.9.0
- CUDA >= 10.2
- GCC >= 7.5.0


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

Please refer to [Datasets.md](datasets/DATASETS.md) for pre-processing and more details.



