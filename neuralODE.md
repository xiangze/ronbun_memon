# Neural Ordinary Differential Equations

https://arxiv.org/abs/1806.07366

## 概要
ResNet
$$
を差分方程式として考え、その時間刻み無限小の極限をとったもの。
層の数が無限大の極限のニューラルネットと捉えることもできる。

ResNetなどの通常の深層学習のネットワークでは層ごとに重み変数がパラメーターとして存在するが、
Neural ODEではそれは単一の関数$f(x,\theta)$として表現される。

推論は数値計算で用いられる通常のODEソルバーで行うことができ、学習はadjoint methodと呼ばれる変
分法のような手法で勾配が層(時間)方向tに対する微分方程式で書け、ソルバーによって解くことができる。
必要な精度で時間刻みを調節すればよいため計算量、パラメーターの量を柔軟に最適な値に変えることができる。

同様に確率微分方程式に対してもニューラル化したものがNeural SDE

## 関連
Neural SDE: Score-Based Generative Modeling through Stochastic Differential　Equations 
https://openreview.net/pdf?id=PxTIG12RRHS
