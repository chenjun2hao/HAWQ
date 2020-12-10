<p align="center">
  <img src="imgs/resnet18_TC.png" width="840">
  <br />
  <br />
  </p>

# HAWQ: Hessian AWare Quantization

HAWQ is an advanced quantization library written for PyTorch. HAWQ enables low-precision and mixed-precision uniform quantization, with direct hardware implementation through TVM.

For more details please see:

- [HAWQ-V3 lightning talk in TVM Conference](https://www.youtube.com/watch?v=VRiujqKU254)
- [HAWQ-V2 presentation in NeurIPS'20](https://neurips.cc/virtual/2020/public/poster_d77c703536718b95308130ff2e5cf9ee.html)

## Installation

* [PyTorch](http://pytorch.org/) version >= 1.4.0
* Python version >= 3.6
* For training new models, you'll also need NVIDIA GPUs and [NCCL](https://github.com/NVIDIA/nccl)
* **To install HAWQ** and develop locally:
```bash
git clone https://github.com/Zhen-Dong/HAWQ.git
cd HAWQ
pip install -r requirements.txt
```

## Getting Started
### Quantization-Aware Training
An example to run uniform 8-bit quantization for resnet50 on ImageNet. 
```
export CUDA_VISIBLE_DEVICES=0
python quant_train.py -a resnet50 --epochs 90 --lr 0.0001 --batch-size 128 --data /path/to/imagenet/ --pretrained --save-path /path/to/checkpoints/ --act-range-momentum=0.99 --wd 1e-4 --data-percentage 0.0001 --fold-BN 1 --fix-BN 1 --checkpoint-iter -1 --quant-scheme uniform8
```

### Inference Acceleration
* [Instructions on Hardware Implementation through TVM](tvm_benchmark/README.md)

## Experimental Results
**Table I and Table II in [HAWQ-V3: Dyadic Neural Network Quantization](https://arxiv.org/abs/2011.10680)**

Model | Quantization | Model Size(MB) | BOPS(G) | Accuracy(%) | Download
---|---|---|---|---|---
`ResNet18` | Floating Points | 44.6 | 1858 | 71.47 | [resnet18_baseline](https://drive.google.com/drive/folders/1C2EpDnRkCFwrH5drwLQRDmlsiQNKN9Nc?usp=sharing)
`ResNet18` | W8A8            | 11.1 | 116  | 71.56 | [resnet18_uniform8](https://drive.google.com/drive/folders/1BbJfgkzGVyPNlXrAO9TbZrVQMqFt99JM?usp=sharing)
`ResNet18` | Mixed Precision | 6.7  | 72   | 70.22 | [resnet18_mp]()
`ResNet18` | W4A4            | 5.8  | 34   | 68.45 | [resnet18_uniform4]()

Model | Quantization | Model Size(MB) | BOPS(G) | Accuracy(%) | Download
---|---|---|---|---|---
`ResNet50` | Floating Points | 97.8 | 3951 | 77.72 | [resnet50_baseline](https://drive.google.com/drive/folders/1C-R8gM2HF8sKi6MPJibopeb8JGklcVUW?usp=sharing)
`ResNet50` | W8A8            | 24.5 | 247  | 77.58 | [resnet50_uniform8](https://drive.google.com/drive/folders/19xmwcVJzJANGagCESZAcwAJbIhRBJy4J?usp=sharing)
`ResNet50` | Mixed Precision | 18.7 | 154  | 75.39 | [resnet50_mp]()
`ResNet50` | W4A4            | 13.1 | 67   | 74.24 | [resnet50_uniform4]()

More results and models are available in the [model zoo](model_zoo.md).  \
To download the quantized models through wget, please refer to a simple command in [model zoo](model_zoo.md).

## Related Works
  - [HAWQ-V3: Dyadic Neural Network Quantization](https://arxiv.org/abs/2011.10680)
  - [HAWQ-V2: Hessian Aware trace-Weighted Quantization of Neural Networks (NeurIPS 2020)](https://arxiv.org/abs/1911.03852)
  - [HAWQ: Hessian AWare Quantization of Neural Networks With Mixed-Precision (ICCV 2019)](https://openaccess.thecvf.com/content_ICCV_2019/html/Dong_HAWQ_Hessian_AWare_Quantization_of_Neural_Networks_With_Mixed-Precision_ICCV_2019_paper.html)


## License

HAWQ is released under the [MIT license](LICENSE).
