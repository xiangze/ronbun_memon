# Rho-Tau Bregman Information and the Geometry of Annealing Paths
https://arxiv.org/abs/2209.07481

https://download.dsf.tuhh.de/ig4ds22/slides/IG4DS-RobBrekelmans.pdf

## 概要
- Annealing pathに対応したdivergence $\rho-\tau$の定義
- 各温度の準加法平均的(logなｄ凸関数を適応したあとの加法)になる

MCMCは簡単な分布をaneailing path,transision kernelを介して複雑な分布にしてサンプリングする方法？

Annealing Importance samplingは正規化されていない密度に対してもサンプリング
$x_T \sim \pi_T(x)$とUnbiased Estimator(尤度比?)を求めてくれる。


密度の幾何平均
$\pi^{geo}_\beta:=\pi_0^{1-\beta}(x)\pi_1^{\beta}(x) $

$\log\pi^{geo}_\beta=(1-\beta)\log\pi_0(x)+\beta\log\pi_1(x) $

$\log -> \log_q$と一般化できる。

$\pi^{geo}_\beta:=\argmin_r (1-\beta)D_{KL}(\pi_0//r)+\beta D_{KL}(r//\pi_1) $ (geometrical path)
$\pi^{q}_\beta:=\argmin_r (1-\beta)D_A^\alpha(\pi_0//r)+\beta D_A^\alpha(\pi_1//r) $ (q-path)
と言えるらしい。($D_A^\alpha$はαダイバージェンス)

"重心" $\argmin_r E_{\nu(u)}D(u//r)$($\nu$は測度？)を見つけることと等価になる。
任意のBregman divergenceに対して唯一最小の$r^*$があると言える(Banerjee2005)。Jensenの不等式のgapを最小化することにも相当する。

単調な表現関数$\rho(\pi)=\log_q\pi$

![architecture](../img/Bregman_min.jpeg)

## alpha-divergence

## f-divergence

## 3 Rho-Tau Bregman Information

#### Theorem 1  Rho-Tau Bregman Informationに関して
正規化されていない測度$\mathbf{\pi} =\{\pi_i(x)\}^N$,混合比のweight $\mathbf{\beta}=\{\beta_i\}^N, \sum_i \beta_i=1$に対して
($\rho$を使って)分解可能なBregman divergence$D_f[\rho(\pi_a)//\rho(\pi_b)]$,生成子$\Psi_f$に対して
$\mathcal{I}_{f,\rho}(\pi,\beta):=\min_r \sim_i \beta_i D_f[]$

は一意な最小$r^*$

## 4 例

 Rho-Tau Bregman Informationは他のdivergenceを包含する
- KL divergence
$\rho(\pi)=\pi , f(\rho)=\rho\log \rho - \rho+1, \tau(\pi)=\log \pi$ 
の関係がある。

mixture path

- JS divergence
対称なdivergence
$ D_{JS}(P//Q):=\alpha D_{KL}(P∣∣M)+\alpha D_{KL}(Q∣∣M)$
$(M=\alpha (P+Q))$

GANへの応用例
https://qiita.com/YusukeOhnishi/items/5c648109a62d538b5721
f-GANs in an Information Geometric Nutshell https://arxiv.org/abs/1707.04385

### gaugeについて
$\tau $
$\rho$

f=

## 5 関連
- Renyi Divergence
geometric anealing path

- Wong & Zhang 2021

## 関連文献
- Rho–tau embedding and gauge freedom in information geometry
https://www.semanticscholar.org/paper/Rho%E2%80%93tau-embedding-and-gauge-freedom-in-information-Naudts-Zhang/4cc8867c646be1065ed85671de2f107cd63fa939
http://dx.doi.org/10.1007/s41884-018-0004-6

Thermodynamic Variational Inference https://arxiv.org/abs/2007.00642
https://arxiv.org/abs/1907.00031
