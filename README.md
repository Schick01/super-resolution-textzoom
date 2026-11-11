# Super-Resolution on TextZoom: HiT-SRF vs SAFMN

## Overview
This project compares two Single Image Super-Resolution techniques, evaluated on the same dataset, with the same adaptation protocol and the same metrics: **HiT-SRF** (a Transformer-based model) and **SAFMN** (a lightweight CNN). Both are pretrained on DF2K and adapted to **TextZoom**, a real-world dataset of photographed scene-text images, through fine-tuning with an identical recipe (L1 loss, Adam, learning rate 1e-5, 2000 iterations, fully unfrozen network).

This project was developed for the Computer Vision course at the University of Catania, Master's Degree in Computer Science (prof. S. Battiato, F. Guarnera — Academic Year 2025-2026), by Alessandro Sciacca (Method 1 - HiT-SRF) and Lorenzo Comis (Method 2 - SAFMN).

## Key Features
The key features of this project are:

**Zero-shot vs fine-tuned evaluation**: both models are first evaluated as-is (zero-shot) and then fine-tuned on TextZoom, to isolate how much adaptation — rather than architecture — contributes to the result.

**Quantitative evaluation**: PSNR, SSIM and LPIPS computed on the same test set (the `easy` subset of TextZoom), with paired image-by-image comparison to assess statistical significance.

**Efficiency comparison**: parameter count, training time and inference time are measured for both models, showing the quality-vs-cost trade-off between the Transformer and the CNN.

## Results

| Model | Parameters | Training (min) | Inference (ms/img) |
|---|---|---|---|
| HiT-SRF | 846,944 | 44.6 | 173.1 |
| SAFMN | 227,820 | 1.1 | 8.2 |

| Method | PSNR (dB) | SSIM | LPIPS |
|---|---|---|---|
| Bicubic (baseline) | 23.42 ± 0.14 | 0.7359 ± 0.0054 | 0.1691 ± 0.0045 |
| HiT-SRF zero-shot | 23.56 ± 0.14 | 0.7404 ± 0.0056 | 0.1559 ± 0.0045 |
| **HiT-SRF fine-tuned** | **25.56 ± 0.12** | **0.8346 ± 0.0039** | **0.0676 ± 0.0025** |
| SAFMN zero-shot | 23.57 ± 0.14 | 0.7406 ± 0.0056 | 0.1579 ± 0.0045 |
| SAFMN fine-tuned | 24.89 ± 0.11 | 0.8157 ± 0.0041 | 0.0772 ± 0.0025 |

Zero-shot, the two architectures are indistinguishable — the shared pretraining data, not the architecture, decides the outcome out of domain. Fine-tuning drives all the gains: HiT-SRF ends up 0.67 dB ahead, but SAFMN reaches 69% of that improvement at roughly 1/21st of the inference cost.

## Repository Contents
- `super_resolution_textzoom.ipynb` — full pipeline: dataset preparation, both methods (zero-shot + fine-tuning), evaluation and comparison.
- `project_report.pdf` — full project report (Italian).

## Dataset & Pretrained Models
This repository does not include the TextZoom dataset or pretrained model weights, as they are third-party resources:
- Dataset: [TextZoom (ECCV 2020)](https://github.com/WenjiaWang0312/TextZoom)
- Method 1: [HiT-SR (ECCV 2024)](https://github.com/XiangZ-0/HiT-SR)
- Method 2: [SAFMN (ICCV 2023)](https://github.com/sunny2109/SAFMN)
