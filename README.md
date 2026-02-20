# Unlearning-Research-Paper-Implementations
A collection of reproducible implementations of state-of-the-art research papers in **machine unlearning**. This repository aims to provide  easy-to-run codebases for benchmarking, ablation studies, and further research in machine unlearning.
---

## Overview

Machine unlearning addresses the growing need to remove the influence of specific data from already-trained models — efficiently, with minimal performance degradation on retained data, and without retraining from scratch.
This repo focuses on **practical post-hoc and approximate unlearning methods** evaluated mainly on **image classification** (CIFAR-10/20/100, ResNet-18 / variants).

## ✅ Implemented Methods – Folder ↔ Paper Mapping

| Folder                  | Paper Title / Method                                                                 | Venue   | Year | arXiv / Link                                                                 | Core Idea (1-liner)                                      |
|-------------------------|--------------------------------------------------------------------------------------|---------|------|------------------------------------------------------------------------------|----------------------------------------------------------|
| `BadTeacher`           | Can Bad Teaching Induce Forgetting? Unlearning in Deep Networks using an Incompetent Teacher | AAAI    | 2023 | [arXiv:2205.08096](https://arxiv.org/abs/2205.08096)                        | Use deliberately incompetent (scrambled) teacher to induce forgetting via distillation |
| `SSD`                   | Fast Machine Unlearning Without Retraining Through Selective Synaptic Dampening     | AAAI    | 2024 | [arXiv:2308.07707](https://arxiv.org/abs/2308.07707)                        | dampen most forget-relevant parameters using Fisher information |
| `SimilarLabel`        | Robust Machine Unlearning for Quantized Networks via Adaptive Gradient Reweighting with Similar Labels | ICCV    | 2025 |  [arXiv:2503.13917](https://arxiv.org/pdf/2503.13917)            | Replace forget labels with probabilistically-closest wrong class → milder gradients |
| `CScore_Relearning_Attack`     | From Dormant to Deleted: Tamper-Resistant Unlearning Through Weight-Space Regularization | NeurIPS       | 2025    | [arXiv:2505.22310](https://arxiv.org/abs/2505.22310)   | Measure unlearning quality by how quickly forget set can be relearned even when finetuned on retain data |
| `Contrastive Unlearning`     | Contrastive Unlearning: A Contrastive Approach to Machine Unlearning     | IJCAI       | 2025    | [arXiv:2401.10458](https://arxiv.org/pdf/2401.10458) |Contrastive loss insipired unlearning|
