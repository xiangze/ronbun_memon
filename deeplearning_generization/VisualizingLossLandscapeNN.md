# Visualizing Loss Landscape of NN
https://arxiv.org/abs/1712.09913

# 論文調査
https://www.coyote009.com/loss-landscape
https://www.coyote009.com/wp-content/uploads/2022/03/li2018_visualizing_loss_landscape.pdf
## 問い：学習しやすいネットワークとは？　アーキテクチャ？パラメーター？
   - loss関数の可視化で何かがわかるか
   - 例えば、Loss関数のFlatness/Sharpnessと、汎化性能に相関があるというこれまでの主張は本当か？
## 既存の取組み
   - (1) 重み空間中の2点間を結ぶ直線 $\theta_a=(1-a)\theta+a\theta$ 上のLoss関数のプロファイルをとる [Goodfellowなど]
   - (2) 1,2次元グリッド
   - 問題点 Reluなど活性化関数によるスケール不定性があり、mimimamuの幅がうまく見れない
　     - 例 $w_2Relu(w_1x+b)=w_1w_2x+w_2b_1+b_2$の $w_1,w_2$の間のスケール不定性
　 
## 仮説
小さいバッチサイズはflatな谷をもたらし汎化性能を高める　ー＞　↑の1D補間の可視化では(陰的？)正則化するとこの仮説と矛盾してしまう(どちらも言えてしまう)
## 提案
filterwise normalization

$$d_{ij} <= \frac{d_{ij}}{||d_{ij}||} || \theta_{ij} ||$$
jth filter,ith layer

## 実験
- CIFAR-10,9層VGG
    - 正則化してもflat/sharp minimaの関係が変わらない
- CIFAR-10,Resnet 20,56,110 skipある/なし
    - 層が深くなると凸性が下がるがskipあると緩和される(skipなしはchaotic landscape,汎化性がない)
    - skipなしは初期値によってはlocal minimaにはまり込む(本当？)
- 本当に凸/非凸性を見れているのか
    - ランダムな2Dの曲率は全次元の曲率の重み付き

- pathの可視化
    - ランダムに2変数をとっても動いてる方向にはほとんど当たらないのでPCAの最大値をplotする。ー＞既に低次元(多様体)にいるからこれをやらないといけないということか？)
    - 小さなbatch, 正則化は勾配に逆らう(山を乗り越えられるということ？)

# 関連情報

「ニューラル ネットワーク最適化問題の質的特徴付け」の再検討 arxiv.org/abs/2012.06898 
2014年のGoodfellowらによる当時のよく分類できるネットワークの「目的関数は単純でほぼ凸形状をしている」という性質はMNISTより難しいデータセットと最先端のネットワークではなりたたないのではという指摘

## reference
https://medium.com/mlearning-ai/visualising-the-loss-landscape-3a7bfa1c6fdf
1D,2D plotのnotebook付き　以下の実装の参考になる

## pytorch実装
https://github.com/xiangze/loss-landscape
pretraind weightをダウンロードして固定点近傍の1D,2D surfaceをplotできる．なぜかmpiに対応しているpython

https://github.com/xiangze/loss-landscape/blob/64ef4d57f8dabe79b57a637819c44e48eda98f33/plot_hessian_eigen.py#L60
巨大なヘッシアンの固有値算出、繰り返し法で最大、最小の固有値を求めている。
	ｰ>最大、最小値を取り除いていけば順次固有値が求まるのだろうか(素朴法)。QR分解とどっちがいい？

MPI、疎行列モジュールを使っているがどの程度の計算量が必要かは書いてない。

https://github.com/xiangze/loss-landscape/blob/64ef4d57f8dabe79b57a637819c44e48eda98f33/hess_vec_prod.py#L49
```python
def eval_hess_vec_prod(vec, params, net, criterion, dataloader, use_cuda=False):
    """
    Evaluate product of the Hessian of the loss function with a direction vector "vec".
    The product result is saved in the grad of net.
    Args:
        vec: a list of tensor with the same dimensions as "params".
        params: the parameter list of the net (ignoring biases and BN parameters).
        net: model with trained parameters.
        criterion: loss function.
        dataloader: dataloader for the dataset.
        use_cuda: use GPU.
    """

    if use_cuda:
        net.cuda()
        vec = [v.cuda() for v in vec]

    net.eval()
    net.zero_grad() # clears grad for every parameter in the net

    for batch_idx, (inputs, targets) in enumerate(dataloader):
        inputs, targets = Variable(inputs), Variable(targets)
        if use_cuda:
            inputs, targets = inputs.cuda(), targets.cuda()

        outputs = net(inputs)
        loss = criterion(outputs, targets)
        grad_f = torch.autograd.grad(loss, inputs=params, create_graph=True)

        # Compute inner product of gradient with the direction vector
        prod = Variable(torch.zeros(1)).type(type(grad_f[0].data))
        for (g, v) in zip(grad_f, vec):
            prod = prod + (g * v).cpu().sum()

        # Compute the Hessian-vector product, H*v
        # prod.backward() computes dprod/dparams for every parameter in params and
        # accumulate the gradients into the params.grad attributes
        prod.backward()
```
Hessianとvecとの積計算部分 学習後netのパラメーターの勾配を求め、vecとの内積を求めている。呼び出し先で最大、最小固有値を計算している。

```

    def hess_vec_prod(vec):
        hess_vec_prod.count += 1  # simulates a static variable
        vec = npvec_to_tensorlist(vec, params)
        start_time = time.time()
        eval_hess_vec_prod(vec, params, net, criterion, dataloader, use_cuda)
        prod_time = time.time() - start_time
        if verbose and rank == 0: print("   Iter: %d  time: %f" % (hess_vec_prod.count, prod_time))
        return gradtensor_to_npvec(net)
```


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
