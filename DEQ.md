# Deep Equilibrium Models
https://arxiv.org/abs/1909.01377

## 概要

系列データに対してneural ODE（層数無限のDNN）として考えた時の不動点をblack-box RootFindingにより探す。

”暗黙的な微分”を使って解析的に解が解けるところがbackpopagationに対する利点 neural ODEの系譜なのでメモリ使用量が少ない。

self-attention transformers, trellis networksなどに対して適用している。

WikiText-103 データセットを用いた検証を行なっている。

本文9ページ

## 実装
https://github.com/locuslab/deq

## 関連？
一方でDNNの学習過程に平均場理論を適用することでは初期値を秩序相とカオス相の境界に置くことで勾配の消失、発散を起こさず学習ができるという研究がある。
 - Dynamical Isometry and a Mean Field Theory of CNNs: How to Train 10,000-Layer Vanilla Convolutional Neural Networks https://arxiv.org/abs/1806.05393
 - 数理科学 2020/11月号 深層神経回路網の幾何 統計神経力学とのつながり https://www.saiensu.co.jp/search/?isbn=4910054691108&y=2020 
