# Neural SDE: Stabilizing Neural ODE Networks with Stochastic Noise 

https://arxiv.org/abs/1906.02355

dropoutの他に"shake-shake regularization","stochastic depth"を表現することができる。

back propagationの式をSDEとして書ける。

## Robustness

## 実験
単にdropoutを入れるのに比べ推論時にノイズを加えることで性能が向上している。

隠れ層に対するperturbationsの程度が小さくなり攻撃に対して頑健になる。

## 実装
 https://diffeqflux.sciml.ai/stable/examples/neural_sde/

## 関連研究
Infinitely Deep Bayesian Neural Networks with Stochastic Differential Equations https://arxiv.org/abs/2102.06559
