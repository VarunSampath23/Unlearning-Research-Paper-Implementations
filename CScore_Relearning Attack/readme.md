# Tamper-Resistant Unlearning? — Relearning Attacks on Machine Unlearning Methods

Reproducing and extending the core empirical finding from:

**"From Dormant to Deleted: Tamper-Resistant Unlearning Through Weight-Space Regularization"**  
[arXiv:2505.22310](https://arxiv.org/abs/2505.22310)

**TL;DR**: Most popular approximate unlearning methods on CIFAR-100 (Gradient Ascent, SCRUB, NegGrad+, Random Relabelling, etc.) appear to forget target examples — until you fine-tune the "unlearned" model **only on the retain set**. Forget-set accuracy often recovers dramatically (80–100%), showing the knowledge was never truly removed.

## 🎯 Goal of this repository

Demonstrate — in a clean, reproducible way — that many state-of-the-art unlearning algorithms are highly vulnerable to a simple **retain-set-only relearning attack**, even when using a principled subset selection strategy (lowest C-Score samples of a target class).

## 📊 Main results (CIFAR-100, ResNet-18)

| Method              | Forget Acc (after unlearning) | Forget Acc (after retain-only relearning) | Retain Acc (final) | Test Acc (final) | Notes                              |
|---------------------|-------------------------------|--------------------------------------------|--------------------|------------------|------------------------------------|
| No unlearning       | ~98%                          | —                                          | ~99.97%            | ~69.5%           | Original trained model             |
| Gradient Ascent     | ~2–10%                        | ~94–100%                                   | ~96–99%            | ~65–69%          | Very strong recovery               |
| BadTeacher          | ~0–5%                         | ~90–100%                                   | ~97–99%            | ~66–69%          | Similar vulnerability              |
| SCRUB               | ~10–20%                       | ~80–96%                                    | ~89–92%            | ~71–72%          | Moderate recovery                  |
| NegGrad+ (λ=100)    | ~0%                           | ~88–96%                                    | ~98–99%            | ~68–69%          | Retain stays very strong           |
| Random Relabelling  | ~66%                          | ~98–100%                                   | ~95%               | ~58–69%          | Still highly recoverable           |

→ Conclusion: Standard unlearning metrics (forget acc right after unlearning) are misleading. Retain-only fine-tuning is a strong practical attack.

## ✨ Features of this implementation

- CScore-based forgetting: removes the **lowest-confidence 10%** of apple images (most "atypical" examples)
- Clean modular evaluation loop for relearning attacks
- Multiple popular unlearning baselines implemented and attacked
- Checkpoint saving for original + unlearned models
- Simple, self-contained notebook (`CScoreRelearningAttack.ipynb`)

