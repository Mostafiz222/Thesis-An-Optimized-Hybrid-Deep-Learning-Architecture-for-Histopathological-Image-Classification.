# Efficient Adaptation of CLIP for Resource-Constrained Histopathological Image Classification

> A parameter-efficient fine-tuning framework for adapting CLIP to histopathological image classification using limited computational resources.

## Overview

Large vision-language models such as **CLIP** achieve strong generalization across many visual tasks, but adapting them to specialized medical domains typically requires expensive full fine-tuning.

This project proposes a **selective fine-tuning strategy** that adapts only the **final Transformer block** of the CLIP image encoder while keeping the remaining pretrained weights frozen. This enables efficient domain adaptation with significantly lower computational requirements than conventional fine-tuning.

The framework is evaluated on the **PathMNIST** histopathological image dataset and demonstrates that selective adaptation provides improved classification performance while remaining practical for consumer-grade hardware.
## Key Features

- Parameter-efficient adaptation of CLIP ViT-B/32
- Selective fine-tuning of only the final Transformer block
- Lightweight MLP classification head
- Resource-efficient training on a single NVIDIA GTX 1650 (4 GB)
- Comprehensive comparison with multiple pretrained architectures and classifiers
- Medical image classification on the PathMNIST benchmark


## Research Motivation

Most high-performing medical image classification methods require either:

- Full fine-tuning of large foundation models
- High-end GPUs
- Large computational budgets

This work investigates whether **partial adaptation of CLIP** can provide a better balance between:

- Classification accuracy
- Computational efficiency
- Memory consumption

for resource-constrained environments.

---

# Methodology

The proposed framework consists of two stages:

1. **Feature Extraction**
   - OpenAI CLIP ViT-B/32 image encoder

2. **Classification**
   - Two-layer MLP classifier

Unlike the baseline, which keeps the entire CLIP encoder frozen, the proposed method unfreezes only the **last Transformer block**, allowing the model to learn domain-specific representations while preserving most pretrained knowledge.

## Dataset

**PathMNIST**

- 107,180 RGB histopathology images
- Image size: 32 × 32
- 9 tissue classes

Dataset split:

| Split | Images |
|-------:|-------:|
| Training | 89,996 |
| Validation | 10,004 |
| Test | 7,180 |

Images are resized to **224 × 224** and normalized using CLIP preprocessing statistics before training.

---

## Training Configuration

| Parameter | Value |
|-----------|-------|
| Backbone | CLIP ViT-B/32 |
| Optimizer | Adam |
| Batch Size | 64 |
| Epochs | 5 |
| Mixed Precision | FP16 |
| GPU | NVIDIA GTX 1650 (4 GB) |
| Trainable Parameters | ~5.4 Million |



---

# Experimental Results

## Baseline Performance

The frozen CLIP + MLP model achieved:

- **Test Accuracy:** **89.76%**

---

## Proposed Model

Selective fine-tuning improved performance to:

| Metric | Score |
|--------|------:|
| Test Accuracy | **91.80%** |
| Training Accuracy | **96.11%** |
| Macro F1-score | **88.90%** |

Compared with the frozen baseline, the proposed approach achieved:

- Higher classification accuracy
- Better class separation
- Improved Macro F1-score
- Efficient training using consumer-grade hardware



---

## Comparison with Previous Work

The proposed framework achieves competitive performance compared with recent PathMNIST methods while requiring significantly less computational hardware than many state-of-the-art approaches.




# Dataset

The dataset is **not included** in this repository due to GitHub storage limitations.

Please download **PathMNIST** from the official MedMNIST project and place it inside the project directory before training.

---


# Technologies Used

- Python
- PyTorch
- OpenAI CLIP (ViT-B/32)
- Torchvision
- NumPy
- Scikit-learn
- Matplotlib

---

# Limitations

Current limitations include:

- Evaluation performed only on PathMNIST
- Only one parameter-efficient fine-tuning strategy investigated
- Performance on minority classes remains challenging
- Generalization to other medical imaging modalities was not evaluated



---

# Future Work

Potential directions include:

- Investigating LoRA and adapter-based tuning
- Fine-tuning multiple Transformer blocks
- Extending to additional MedMNIST datasets
- Incorporating explainable AI methods
- Addressing class imbalance through advanced augmentation and loss re-weighting

--

# Acknowledgements

- OpenAI CLIP
- MedMNIST
- PyTorch
- The authors of PathMNIST and related medical imaging research
