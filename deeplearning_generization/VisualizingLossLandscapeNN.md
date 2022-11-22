https://arxiv.org/abs/1712.09913

論文調査　https://www.coyote009.com/loss-landscape
https://www.coyote009.com/wp-content/uploads/2022/03/li2018_visualizing_loss_landscape.pdf
- 例えば、Loss関数のFlatness/Sharpnessと、汎化性能に相関があるというこれまでの主張は本当か？
- 既存の取組み(1) • 重み空間中の2点間を結ぶ直線上のLoss関数のプロファイルをとる [Goodfellowなど]
- 

# 関連情報

「ニューラル ネットワーク最適化問題の質的特徴付け」の再検討 arxiv.org/abs/2012.06898 
2014年のGoodfellowらによる当時のよく分類できるネットワークの「目的関数は単純でほぼ凸形状をしている」という性質はMNISTより難しいデータセットと最先端のネットワークではなりたたないのではという指摘

## reference
https://medium.com/mlearning-ai/visualising-the-loss-landscape-3a7bfa1c6fdf
notebook付き　以下の実装の参考になる

## pytorch実装
https://github.com/xiangze/loss-landscape
pretraind weightをダウンロードして固定点近傍の1D,2D surfaceをplotできる．なぜかmpiに対応しているpython

https://github.com/xiangze/loss-landscape/blob/64ef4d57f8dabe79b57a637819c44e48eda98f33/plot_hessian_eigen.py#L60
巨大なヘッシアンの固有値算出、繰り返し法で最大、最小の固有値を求めている。
	ｰ>最大、最小値を取り除いていけば順次固有値が求まるのだろうか(素朴法)。QR分解とどっちがいい？

## 被引用リスト
https://scholar.google.co.jp/scholar?q=Visualizing+the+Loss+Landscape+of+Neural+Nets&hl=ja&as_sdt=0&as_vis=1&oi=scholart
https://www.google.com/search?q=Visualizing+the+Loss+Landscape+of+Neural+Nets&sourceid=chrome&ie=UTF-8

https://losslandscape.com/ LANDSCAPE

## 関係ありそうな論文
- [1710.05468] Generalization in Deep Learning
 	   arXiv:1710.05468 - Google 検索  1710.05468.pdf arXiv:1710.05468 - Google 検索
- [1703.04933] Sharp Minima Can Generalize For Deep Nets
- [1412.6544] Qualitatively characterizing neural network optimization problems
 -[2012.06898] 「ニューラル ネットワーク最適化問題の質的特徴付け」の再検討 2012.06898.pdf
- [1612.04010] An empirical analysis of the optimization of deep network loss surfaces	1612.04010.pdf	
- Topology of Learning in Artificial Neural Networks 1902.08160.pdf [1902.08160] Topology of Learning in Artificial Neural Networks
		
# Next step
- アトラクター(loss minimum)近傍以外のhessian(曲率)の数値計算　低次元多様体へ向かう次元削減の様子を見ることができるかもしれない
## 議論
- 生成モデルのサンプリングでは　平衡状態が仮定されているのだろうか
- 過渡状態、非平衡な軌道上の相体積に意味はあるのか．
- 過渡状態のヘッシアン固有値を求めるのは大変そう
