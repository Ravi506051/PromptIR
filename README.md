# PromptIR: Prompting for All-in-One Blind Image Restoration (NeurIPS'23)

[Vaishnav Potlapalli](https://www.vaishnavrao.com/), [Syed Waqas Zamir](https://scholar.google.ae/citations?hl=en&user=POoai-QAAAAJ), [Salman Khan](https://salman-h-khan.github.io/) and [Fahad Shahbaz Khan](https://scholar.google.es/citations?user=zvaeYnUAAAAJ&hl=en)

[![paper](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2306.13090)


<hr />

> **Abstract:** *Image restoration involves recovering a high-quality clean image from its degraded
version. Deep learning-based methods have significantly improved image restora-
tion performance, however, they have limited generalization ability to different
degradation types and levels. This restricts their real-world application since it
requires training individual models for each specific degradation and knowing the
input degradation type to apply the relevant model. We present a prompt-based
learning approach, PromptIR, for All-In-One image restoration that can effectively
restore images from various types and levels of degradation. In particular, our
method uses prompts to encode degradation-specific information, which is then
used to dynamically guide the restoration network. This allows our method to
generalize to different degradation types and levels, while still achieving state-of-
the-art results on image denoising, deraining, and dehazing. Overall, PromptIR
offers a generic and efficient plugin module with few lightweight prompts that can
be used to restore images of various types and levels of degradation with no prior
information of corruptions.* 
<hr />

## Network Architecture

<img src = "mainfig.png"> 

## Installation and Data Preparation

See [INSTALL.md](INSTALL.md) for the installation of dependencies and dataset preperation required to run this codebase.

## Training

After preparing the training data in ```data/``` directory, use 
```
python train.py
```
to start the training of the model. Use the ```de_type``` argument to choose the combination of degradation types to train on. By default it is set to all the 3 degradation types (noise, rain, and haze).

Example Usage: If we only want to train on deraining and dehazing:
```
python train.py --de_type derain dehaze
```

## Testing

After preparing the testing data in ```test/``` directory, place the mode checkpoint file in the ```ckpt``` directory. The pretrained model can be downloaded [here](https://drive.google.com/file/d/1j-b5Od70pGF7oaCqKAfUzmf-N-xEAjYl/view?usp=sharingg), alternatively, it is also available under the releases tab. To perform the evalaution use
```
python test.py --mode {n}
```
```n``` is a number that can be used to set the tasks to be evaluated on, 0 for denoising, 1 for deraining, 2 for dehaazing and 3 for all-in-one setting.

Example Usage: To test on all the degradation types at once, run:

```
python test.py --mode 3
```

## Demo
To obtain visual results from the model ```demo.py``` can be used. After placing the saved model file in ```ckpt``` directory, run:
```
python demo.py --test_path {path_to_degraded_images} --output_path {save_images_here}
```
Example usage to run inference on a directory of images:
```
python demo.py --test_path './test/demo/' --output_path './output/demo/'
```
Example usage to run inference on an image directly:
```
python demo.py --test_path './test/demo/image.png' --output_path './output/demo/'
```
To use tiling option while running ```demo.py``` set ```--tile``` option to ```True```. The Tile size and Tile overlap parameters can be adjusted using ```--tile_size``` and ```--tile_overlap``` options respectively.




## Results
Performance results of the PromptIR framework trained under the all-in-one setting

<summary><strong>Table</strong> </summary>

<img src = "prompt-ir-results.png"> 

<summary><strong>Visual Results</strong></summary>

The visual results of the PromptIR model evaluated under the all-in-one setting can be downloaded [here](https://drive.google.com/drive/folders/1Sm-mCL-i4OKZN7lKuCUrlMP1msYx3F6t?usp=sharing)



## Citation
If you use our work, please consider citing:

    @inproceedings{potlapalli2023promptir,
      title={PromptIR: Prompting for All-in-One Image Restoration},
      author={Potlapalli, Vaishnav and Zamir, Syed Waqas and Khan, Salman and Khan, Fahad},
      booktitle={Thirty-seventh Conference on Neural Information Processing Systems},
      year={2023}
    }


## Contact
Should you have any questions, please contact pvaishnav2718@gmail.com


**Acknowledgment:** This code is based on the [AirNet](https://github.com/XLearning-SCU/2022-CVPR-AirNet) and [Restormer](https://github.com/swz30/Restormer) repositories.

## Local Inference Notes

This repository contains the upstream PromptIR research implementation. For local experiments, follow the upstream installation, dataset preparation, checkpoint, and testing instructions. Keep evaluation datasets separate from any training data and document the checkpoint, degradation setting, image preprocessing, and inference parameters used for each run.

When reporting image-restoration quality, use the metrics and evaluation protocol appropriate to the selected benchmark, and compare outputs using the same input images and settings. Preserve upstream attribution and licensing when sharing modifications.

## Project Development Notes

Record the exact checkpoint, preprocessing, image size, padding and tiling configuration for every inference run. Compare outputs consistently and preserve the original input alongside restored images.

For reproducibility, record source versions, environment and dependency versions, configuration, and actual test outputs. Clearly label sample data and illustrative results; never commit secrets or private data.

### Technical Deep Dive

For reproducible PromptIR inference, record the checkpoint, model configuration, degradation mode, input color space, normalization, padding strategy, and tile size/overlap. Keep input and restored images paired by filename and evaluate them with identical preprocessing. When ground-truth clean images exist, calculate suitable full-reference metrics such as PSNR and SSIM; otherwise use carefully qualified visual comparisons.

Suggested engineering checks: test dimensions that are not multiples of the model's required stride, verify padding is removed correctly, compare tiled and non-tiled outputs, and keep the evaluation split separate from training data. Preserve the original paper, code, and checkpoint attribution.

## Research Reproduction Notes

This repository contains the upstream PromptIR implementation. For reproducible inference experiments, record the checkpoint source, model configuration, input resolution, preprocessing and normalization, padding or tiling settings, and output directory.

When comparing restored images, use the same input images and settings across methods. If clean reference images are available, report suitable full-reference metrics such as PSNR and SSIM; otherwise describe the visual comparison as qualitative. Keep the original paper citation, authorship, and license information when sharing modified experiments.

## Image Restoration Evaluation Notes

- Evaluate restoration on paired, held-out images using clearly documented degradation settings.
- Report PSNR and SSIM where appropriate, while also inspecting visual artifacts and edge preservation.
- Keep input normalization, padding, tiling, and inference configuration consistent across comparisons.
- Record checkpoint provenance, image dimensions, tile size, overlap, and runtime settings for reproducibility.
- Compare outputs across degradation types; a metric improvement does not always guarantee perceptually better restoration.

## Local Research Notes

This repository contains the original PromptIR research implementation. Preserve the authors' attribution, paper references, and license terms when using or modifying this code.

For inference experiments, record the checkpoint, input resolution, padding or tiling strategy, overlap, and hardware environment. Compare restored outputs against the original inputs and, where ground truth exists, report PSNR/SSIM using a consistent evaluation protocol. Keep test images separate from training data and document any preprocessing differences.
