# What Are Bayesian Neural Network Posteriors Really Like
https://arxiv.org/abs/2104.14421

比較的大きなデータセット( CIFAR image classification datasets,IMDB dataset)に対してHMC,SGMCMCを適用し特性を見ている

(1) BNNs can achieve significant performance gains over standard training and deep ensembles

(2) a single long HMC chain can provide a comparable representation of the posterior to multiple shorter chains

(3) in contrast to recent studies, we find posterior tempering is not needed for near-optimal performance, with little evidence for a "cold posterior" effect, which we show is largely an artifact of data augmentation; 

(4) BMA performance is robust to the choice of prior scale, and relatively similar for diagonal Gaussian, mixture of Gaussian, and logistic priors; 

(5) Bayesian neural networks show surprisingly poor generalization under domain shift; 

(6) while cheaper alternatives such as deep ensembles and SGMCMC methods can provide good generalization

## 実装
著者によるTPU,JAX実装がある

https://github.com/google-research/google-research/tree/master/bnn_hmc


## 参考文献
