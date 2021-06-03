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

確率要素を入れた連続的Normalizing Flowsの拡張

## 概要で語られる課題
一般に学習過程をSDEで記述したい。stochastic SDE deep latent gaussian modelの極限
　ノイズ、敵対的データに対する頑健性
    形式的に置き換える方法もある(A Complete Recipe for Stochastic Gradient MCMC  https://arxiv.org/pdf/1506.04696.pdf)
normalizing flowの連続極限においてSDEベースの方法を一般的な形で構築したい->難しい

- Girsanovの定理を満たすような変分推論を構築する。それに異なるドリフト係数によって2つのSDKの解(事前、事後分布)の分布間のKL divergenseを推定することができる()。(もう一つの方は(https://arxiv.org/abs/2002.06707)が有限ステップで
forward/backwardのKL divergence(KL[pX//µX] or KL[µX//pX])を最小化するというステップを提示している。)
- stochastic adjoint 法を使ってSDEをVAEのモデルとして記述している()
- 確率演算はSDEの近似解(backward解)としては不良推定なため　理論的正当化は難しい
 -  難しさは拡散項の非対角成分に由来する
 -  高階adaptive SDE solver,乱数の種から構成されるのブラウン運動の複雑な平均
既存の方法では理論的正当化は難しい

変分推論とMCMCをベイジアン計算(確率的計算)のなかに位置付ける研究
- 複数の可逆MCをVIに組み込む(Markov Chain Monte Carlo and Variational Inference: Bridging the Gap https://arxiv.org/abs/1410.6460) HMCに対して(https://arxiv.org/pdf/1609.08203.pdf)
- kerneled Stein discrepancyからくる手法を用いてstochastic gradient Langevinのstep幅を決定する
- Langevin flowがstochastic MCMCとSDEの関係から提唱されている
- Langevin flowはSDEのlog-likelihoodの近似と言える

## contribution

SDEから作られた生成モデルをnormalizing flowを用いて近似する手法
理論の鍵はrough path theory
これによって
- autoencoderを使った任意のSDEに対する密度推定、最尤推定、 変分近似が可能になる
- 任意の連続的normalizing flowで実装できる
- neural ODEのアプローチをSDEに移行できる
- 
### Rough Path Theory
 SDEのpathの性質
 ODEの解で近似できるということが言える
 https://arxiv.org/abs/2009.08295
 
### Stratonovich formへの変換と

### Wong–Zakai approximations
roughなpathの近似方法

### Main result(定理)
```
Using Wong–Zakai approximations, a Stratonovich SDE can be uniformly approximated in Hölder norm by random ODEs
```

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
