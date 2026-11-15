# CTR Prediction with FuxiCTR

基于 FuxiCTR 和 PyTorch，在 Criteo 500K 数据集上复现 LR、FM、DeepFM，比较不同特征交互方式对 CTR 预测效果的影响，并进一步研究 DeepFM 的 Embedding 维度变化。

## Experiments

- 使用 Criteo 500K 完成数据预处理和特征编码。
- 基于 FuxiCTR 复现 LR、FM、DeepFM。
- 对比不同模型的 AUC 和 LogLoss。
- 开展 DeepFM Embedding Dim = 8/16/32 敏感性实验。

## Dataset

| Split | Samples |
|---|---:|
| Train | 350,000 |
| Validation | 100,000 |
| Test | 50,000 |

共 39 个特征字段，包括 13 个数值特征和 26 个类别特征。

## Baseline Comparison

| Model | Epochs | Val AUC | Test AUC | Test LogLoss |
|---|---:|---:|---:|---:|
| LR | 10 | 0.763905 | 0.761254 | 0.483803 |
| FM | 5 | 0.760212 | 0.758528 | 0.490112 |
| DeepFM | 3 | **0.773412** | **0.770871** | **0.475868** |

DeepFM 在本次实验中取得了最好的测试集表现。FM 没有超过 LR，说明增加二阶特征交互不一定直接带来性能提升。

## Embedding Dimension

| Embedding Dim | Parameters | Test AUC | Test LogLoss |
|---:|---:|---:|---:|
| 8 | 3,273,711 | 0.769889 | 0.477265 |
| 16 | 6,183,959 | **0.770871** | 0.475868 |
| 32 | 12,004,455 | 0.770693 | **0.475698** |

随着 Embedding 维度增加，模型参数量明显增长，但测试集指标没有持续改善。

## Training Configuration

| Parameter | Value |
|---|---|
| Framework | FuxiCTR 2.3.10 |
| Optimizer | Adam |
| Learning Rate | 0.001 |
| Batch Size | 1024 |
| Maximum Epochs | 10 |
| Early Stopping Patience | 2 |
| Random Seed | 20261115 |

## Repository Structure

```text
.
├── README.md
├── notebooks/
│   └── ctr_experiments.ipynb
├── experiments/
│   ├── baseline_comparison.md
│   └── embedding_sensitivity.md
└── .gitignore
```

## Notes

当前实验基于 Criteo 500K 子集和单次随机种子运行，尚未进行多随机种子验证。原始数据、处理后的数据和模型检查点不包含在仓库中。

后续计划：多随机种子实验、模型消融和进一步的特征交互分析。