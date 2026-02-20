# Similar Labelling – CIFAR-100 & ResNet-18

Experiments exploring **machine unlearning** techniques on CIFAR-100 using a standard ResNet-18.

Special focus on the **"similar labels"** strategy from:

> **Robust Machine Unlearning for Quantized Neural Networks via Adaptive Gradient Reweighting with Similar Labels**  
> Yujia Tong et al., ICCV 2025  

This notebook compares **similar-label unlearning** against aggressive random labeling and fixed random labeling — both in **class-level** and **sample-level** forgetting settings.

## What's in this repo

- `robustmul-yujiatong-iccv2025.ipynb`  
  Main notebook containing:
  - Standard training of ResNet-18 on CIFAR-100 (~58–59% test accuracy)
  - Class-level unlearning (forget one class, e.g. class 1)
  - Sample-level unlearning (forget random 10% of training set)
  - Three label-replacement strategies:
    1. **Aggressive random labeling** (new random wrong label every epoch)
    2. **Fixed random labeling** (one fixed wrong label per image, deterministic)
    3. **Similar labels** (closest wrong class in softmax probability space — core idea from the paper)

## Key Observations

### Class-level forgetting (forget one entire class)

| Strategy              | Forget Train Acc | Forget Test Acc | Retain Test Acc Drop | Notes |
|-----------------------|------------------|-----------------|----------------------|-------|
| Aggressive random     | ~1–2%            | ~1%             | ~3–4%                | Strong forgetting, noticeable collateral damage |
| Fixed random          | ~1–2%            | ~1%             | ~3–4%                | Very similar to aggressive |
| **Similar labels**    | ~0–2%            | ~0–1%           | ~0.5–1.5%            | **Clearly best utility preservation** |

→ Replacing the true label with the **probabilistically closest wrong class** creates much milder gradient perturbation than pure random wrong labels.

### Sample-level forgetting (random 10% of train set)

- Pure random/fixed label flipping → catastrophic forgetting of retain data (~14–16% final test acc)
- Similar labels alone → moderate degradation (~46% test acc after short fine-tuning)
- Concatenating retain data + relabeled forget data → retain accuracy actually **increases**, forget accuracy barely moves (turns into regular fine-tuning)

## Reference
Robust Machine Unlearning for Quantized Neural Networks via Adaptive Gradient Reweighting with Similar Labels - Yujia Tong et al (https://openaccess.thecvf.com/content/ICCV2025/papers/Tong_Robust_Machine_Unlearning_for_Quantized_Neural_Networks_via_Adaptive_Gradient_ICCV_2025_paper.pdf)
