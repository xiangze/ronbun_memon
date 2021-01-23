# Stochastic Normalizing Flows

## その１
https://arxiv.org/abs/2002.06707

 https://github.com/noegroup/stochastic_normalizing_flows

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
 
