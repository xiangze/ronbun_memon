# Stochastic Normalizing Flows

確率的要素を入れることでサンプリングの表現力、効率が上がることを主張している。
同名の論文が2つある。

## その１
https://arxiv.org/abs/2002.06707

### 既存研究
- Normalizing Flowsはforward,reverse modeで学習される
- 可逆関数の変換には制約がある （サンプル空間がa non-trivial Lie groupにより制約される。 単峰型関数をベースにすることによるBi-Lipschitz constraints)

実装 https://github.com/noegroup/stochastic_normalizing_flows

### model式とtraining

forward / backward path  (y1, . . . , yT ),  (yT −1, . . . , y0). を確率に基づいてサンプルする

forward and backward pathの分布間KL divergenceが最小になるように学習を行う。

Asymptotically unbiased samplingである。

### Implementing SNFs via Annealed Importance Sampling
Langevin＋MCMC
(Annealed Importance Sampling https://arxiv.org/abs/physics/9803008)
### result

- 簡単な白黒画像データ、1次元2山ポテンシャル
をターゲット分布としたサンプリングでdivergenseが低いことを確認している。
- Alanine dipeptid(化合物)の様々な形状？のサンプリング
- VAEの推論に用いた場合 dataset MNIST,Fashion MNIST
-
### 関連研究

## その2
https://arxiv.org/abs/2002.09547

確率要素を入れたNormalizing Flowsの拡張

### 数値実験
- banana-shaped distributionのサンプリング
 p(x, y) ∝ exp( −1/2(x^2+1/2(x^2+y^2))

- MCMCの最適化にSDEを使う
p-ergodicなSDEで分布pを近似する

ターゲット分布に対するVI(変分推論)を使うことはMCMCの収束率を最適化することにつながる

pが１次元コーシー分布の場合

dZ_t=(-2σ(Z_t)^2 Z_t/(1+Z_t^2) +1/2 σ'(Z_t))dt+σ(Z_t)dB_t

パラメータσを適切に選ぶことが早い混合をもたらす。


## 実装について
普通のNormalizing Flows

pyro https://pyro.ai/examples/normalizing_flows_i.html
 
## 参考文献
- Neural SDE: Stabilizing Neural ODE Networks with Stochastic Noise https://arxiv.org/abs/1906.02355
 -  https://diffeqflux.sciml.ai/stable/examples/neural_sde/ DiffEqFlux.jlを用いた実装
- Score-Based Generative Modeling through Stochastic Differential Equations https://openreview.net/forum?id=PxTIG12RRHS
も関係するかもしれない
