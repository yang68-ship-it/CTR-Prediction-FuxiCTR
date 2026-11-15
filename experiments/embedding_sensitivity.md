# Embedding Dimension Sensitivity

## Experimental Setup

使用 DeepFM，研究不同 Embedding 维度对预测效果和模型参数规模的影响。

Embedding Dim: 8, 16, 32

其他主要训练参数保持一致：

- Optimizer: Adam
- Learning Rate: 0.001
- Batch Size: 1024
- Maximum Epochs: 10
- Early Stopping Patience: 2
- Random Seed: 20261115

## Results

| Embedding Dim | Parameters | Epochs | Val AUC | Val LogLoss | Test AUC | Test LogLoss |
|---:|---:|---:|---:|---:|---:|---:|
| 8 | 3,273,711 | 3 | 0.773059 | 0.474296 | 0.769889 | 0.477265 |
| 16 | 6,183,959 | 3 | 0.773412 | 0.473758 | **0.770871** | 0.475868 |
| 32 | 12,004,455 | 3 | **0.773931** | **0.473322** | 0.770693 | **0.475698** |

## Observations

- Increasing Embedding Dim significantly increased the number of model parameters.
- Validation AUC improved as the Embedding dimension increased.
- Test AUC was highest at dimension 16, while Test LogLoss was lowest at dimension 32.
- Increasing the dimension from 16 to 32 nearly doubled the parameter count, but brought only marginal changes in test performance.

## Conclusion

Increasing Embedding Dim improved validation performance in this experiment, but did not consistently improve all test metrics.

Dimension 16 provides a reasonable balance between model size and prediction performance in the current experiment.

The results are based on a single random seed and require further validation.