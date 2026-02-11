# Contrastive Unlearning – Clean Reproduction on CIFAR-10

Minimal, reproducible implementation of **Contrastive Unlearning**  
from the paper:

**"Contrastive Unlearning: A Contrastive Approach to Machine Unlearning"**  
Hong Kyu Lee, Qiuchen Zhang, Carl Yang, Jian Lou, Li Xiong  
arXiv:2401.10458 (accepted at **IJCAI 2025**)

[📄 Paper](https://arxiv.org/abs/2401.10458)

### Goal of this notebook

Show that a simple contrastive-style objective can achieve near-perfect forgetting of an entire class while preserving (or even slightly improving) performance on the retain classes — all in very few lines of code and short training time.

### Core Idea (from the paper)

Push forget-class feature embeddings **away** from retain-class embeddings in normalized (L2) feature space using a negative similarity loss:

```python
L_contrast = - mean( forget_feats @ retain_feats.T )

Combined with standard CE loss on retain samples to maintain utility.
```

#### Quick Results (CIFAR-10, ResNet-18, forget class = 3)
Split,Before Unlearning,After Unlearning,Δ
Retain Train Acc,78.43%,79.54%,+1.11%
Forget Train Acc,88.56%,0.00%,-88.56%
Retain Test Acc,77.62%,78.90%,+1.28%
Forget Test Acc,89.60%,0.00%,-89.60%
Unlearning time,—,~9.7 seconds,—
