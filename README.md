# MemNet-PyTorch

## Overview

This repository contains an op-for-op PyTorch reimplementation
of [MemNet: A Persistent Memory Network for Image Restoration](https://arxiv.org/abs/1708.02209v1).

## Table of contents

- [MemNet-PyTorch](#memnet-pytorch)
    - [Overview](#overview)
    - [Table of contents](#table-of-contents)
    - [Download weights](#download-weights)
    - [Download datasets](#download-datasets)
    - [How Test and Train](#how-test-and-train)
        - [Test](#test)
        - [Train model](#train-model)
        - [Resume train model](#resume-train-model)
    - [Result](#result)
    - [Contributing](#contributing)
    - [Credit](#credit)
        - [MemNet: A Persistent Memory Network for Image Restoration](#memnet-a-persistent-memory-network-for-image-restoration)

## Download weights

- [Google Driver](https://drive.google.com/drive/folders/17ju2HN7Y6pyPK2CC_AqnAfTOe9_3hCQ8?usp=sharing)
- [Baidu Driver](https://pan.baidu.com/s/1yNs4rqIb004-NKEdKBJtYg?pwd=llot)

## Download datasets

Contains DIV2K, DIV8K, Flickr2K, OST, T91, Set5, Set14, BSDS100 and BSDS200, etc.

- [Google Driver](https://drive.google.com/drive/folders/1A6lzGeQrFMxPqJehK9s37ce-tPDj20mD?usp=sharing)
- [Baidu Driver](https://pan.baidu.com/s/1o-8Ty_7q6DiS3ykLU09IVg?pwd=llot)

Please refer to `README.md` in the `data` directory for the method of making a dataset.

## How Test and Train

Both training and testing only need to modify the `config.py` file.

### Test

- line 31: `upscale_factor` change to `2`.
- line 33: `mode` change to `test`.
- line 70: `model_path` change to `results/pretrained_models/IDN_x2-TB291-c21dcaa0.pth.tar`.

### Train model

- line 31: `upscale_factor` change to `2`.
- line 33: `mode` change to `train`.
- line 35: `exp_name` change to `IDN_x2`.

### Resume train model

- line 31: `upscale_factor` change to `2`.
- line 33: `mode` change to `train`.
- line 35: `exp_name` change to `IDN_x2`.
- line 48: `resume` change to `samples/IDN_x2/epoch_xxx.pth.tar`.

## Result

Source of original paper results: [https://arxiv.org/pdf/1803.09454v1.pdf](https://arxiv.org/pdf/1803.09454v1.pdf)

In the following table, the psnr value in `()` indicates the result of the project, and `-` indicates no test.

| Method | Scale |          Set5 (PSNR/SSIM)           |          Set14 (PSNR/SSIM)          |         BSD100 (PSNR/SSIM)          |        Urban100 (PSNR/SSIM)         |
|:------:|:-----:|:-----------------------------------:|:-----------------------------------:|:-----------------------------------:|:-----------------------------------:|
|  IDN   |   2   | 37.83(**37.59**)/0.9600(**0.9598**) | 33.30(**33.00**)/0.9148(**0.9135**) | 32.08(**
31.91**)/0.8985(**0.8974**) | 31.27(**30.68**)/0.9196(**0.9138**) |
|  IDN   |   3   |     34.11(**-**)/0.9253(**-**)      |     29.99(**-**)/0.8354(**-**)      |     28.95(**
-**)/0.8013(**-**)      |     27.42(**-**)/0.8359(**-**)      |
|  IDN   |   4   |     31.82(**-**)/0.8903(**-**)      |     28.25(**-**)/0.7730(**-**)      |     27.41(**
-**)/0.7297(**-**)      |     25.41(**-**)/0.7632(**-**)      |

```bash
# Download `IDN_x2-TB291-c21dcaa0.pth.tar` weights to `./results/pretrained_models`
# More detail see `README.md<Download weights>`
python ./inference.py --inputs_path ./figure/barbara_lr.png --output_path ./figure/barbara_sr.png --weights_path ./results/pretrained_models/IDN_x2-TB291-c21dcaa0.pth.tar
```

Input:

<span align="center"><img width="720" height="576" src="figure/barbara_lr.png"/></span>

Output:

<span align="center"><img width="720" height="576" src="figure/barbara_sr.png"/></span>

```text
Build IDN model successfully.
Load IDN model weights `./results/pretrained_models/IDN_x2-TB291-c21dcaa0.pth.tar` successfully.
SR image save to `./figure/barbara_sr.png`
```

## Contributing

If you find a bug, create a GitHub issue, or even better, submit a pull request. Similarly, if you have questions,
simply post them as GitHub issues.

I look forward to seeing what the community does with these models!

## Credit

### MemNet: A Persistent Memory Network for Image Restoration

_Ying Tai, Jian Yang, Xiaoming Liu, Chunyan Xu_ <br>

**Abstract** <br>
Recently, very deep convolutional neural networks (CNNs) have been attracting considerable attention in image
restoration. However, as the depth grows, the long-term dependency problem is rarely realized for these very deep
models, which results in the prior states/layers having little influence on the subsequent ones. Motivated by the fact
that human thoughts have persistency, we propose a very deep persistent memory network (MemNet) that introduces a memory
block, consisting of a recursive unit and a gate unit, to explicitly mine persistent memory through an adaptive learning
process. The recursive unit learns multi-level representations of the current state under different receptive fields.
The representations and the outputs from the previous memory blocks are concatenated and sent to the gate unit, which
adaptively controls how much of the previous states should be reserved, and decides how much of the current state should
be stored. We apply MemNet to three image restoration tasks, i.e., image denosing, super-resolution and JPEG deblocking.
Comprehensive experiments demonstrate the necessity of the MemNet and its unanimous superiority on all three tasks over
the state of the arts. Code is available at this [https URL](https://github.com/tyshiwo/MemNet).

[[Paper]](https://arxiv.org/pdf/1708.02209v1.pdf) [[Author's implements (MATLAB)]](https://github.com/tyshiwo/MemNet)

```bibtex
@inproceedings{Tai-MemNet-2017,
  title={MemNet: A Persistent Memory Network for Image Restoration},
  author={Tai, Ying and Yang, Jian and Liu, Xiaoming and Xu, Chunyan},
  booktitle={Proceedings of International Conference on Computer Vision},
  year={2017}
}
```
