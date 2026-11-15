# Baseline Comparison

## Experimental Setup

Dataset: Criteo 500K

| Split | Samples |
|---|---:|
| Train | 350,000 |
| Validation | 100,000 |
| Test | 50,000 |

主要训练参数：

- Optimizer: Adam
- Learning Rate: 0.001
- Batch Size: 1024
- Maximum Epochs: 10
- Early Stopping Patience: 2
- Random Seed: 20261115

## Results

| Model | Epochs | Val AUC | Val LogLoss | Test AUC | Test LogLoss |
|---|---:|---:|---:|---:|---:|
| LR | 10 | 0.763905 | 0.481453 | 0.761254 | 0.483803 |
| FM | 5 | 0.760212 | 0.488086 | 0.758528 | 0.490112 |
| DeepFM | 3 | **0.773412** | **0.473758** | **0.770871** | **0.475868** |

## Observations

- DeepFM achieved the best AUC and LogLoss in this experiment.
- FM performed worse than LR, indicating that introducing second-order feature interactions does not necessarily improve prediction performance.
- Compared with LR, DeepFM improved Test AUC by 0.009617 and reduced Test LogLoss by 0.007935.

All models used the same maximum epoch setting and early stopping strategy, although their actual training epochs differed.

## Conclusion

DeepFM performed best on the current Criteo 500K dataset. Further experiments with multiple random seeds and model ablation are needed to verify the stability of these results.