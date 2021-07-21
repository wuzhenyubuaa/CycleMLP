# A MLP-like Architecture for Dense Prediction

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Python 3.8](https://img.shields.io/badge/python-3.8-green.svg)



<p align="middle">
  <img src="figures/teaser.png" height="300" />
  &nbsp;&nbsp;&nbsp;&nbsp;
  <img src="figures/flops.png" height="300" />
</p>

# Updates

- (22/07/2021) Initial release.



# Model Zoo

We provide CycleMLP models pretrained on ImageNet 2012.

| Model                | Parameters | FLOPs    | Top 1 Acc. | Download |
| :------------------- | :--------- | :------- | :--------- | :------- |
| CycleMLP-B1          | 15M        |  2.1G    |  78.9%     |          |
| CycleMLP-B2          | 27M        |  3.9G    |  81.6%     |          |
| CycleMLP-B3          | 38M        |  6.9G    |  82.4%     |          |
| CycleMLP-B4          | 52M        |  10.1G   |  83.0%     |          |
| CycleMLP-B5          | 76M        |  12.3G   |  83.2%     |          |


# Usage


## Install

- PyTorch 1.7.0+ and torchvision 0.8.1+
- [timm](https://github.com/rwightman/pytorch-image-models/tree/c2ba229d995c33aaaf20e00a5686b4dc857044be):
```
pip install 'git+https://github.com/rwightman/pytorch-image-models@c2ba229d995c33aaaf20e00a5686b4dc857044be'

or

git clone https://github.com/rwightman/pytorch-image-models
cd pytorch-image-models
git checkout c2ba229d995c33aaaf20e00a5686b4dc857044be
pip install -e .
```
- fvcore (optional, for FLOPs calculation)
- mmcv, mmdetection, mmsegmentation (optional)

## Data preparation

Download and extract ImageNet train and val images from http://image-net.org/.
The directory structure is:

```
│path/to/imagenet/
├──train/
│  ├── n01440764
│  │   ├── n01440764_10026.JPEG
│  │   ├── n01440764_10027.JPEG
│  │   ├── ......
│  ├── ......
├──val/
│  ├── n01440764
│  │   ├── ILSVRC2012_val_00000293.JPEG
│  │   ├── ILSVRC2012_val_00002138.JPEG
│  │   ├── ......
│  ├── ......
```

## Evaluation
To evaluate a pre-trained CycleMLP-B5 on ImageNet val with a single GPU run:
```
python main.py --eval --model CycleMLP_B5 --resume path/to/CycleMLP_B5.pth --data-path /path/to/imagenet
```


## Training

To train CycleMLP-B5 on ImageNet on a single node with 8 gpus for 300 epochs run:
```
python -m torch.distributed.launch --nproc_per_node=8 --use_env main.py --model CycleMLP_B5 --batch-size 128 --data-path /path/to/imagenet --output_dir /path/to/save
```


# License

CycleMLP is released under MIT License.