# Point-GNN: Graph Neural Network for 3D Object Detection in a Point Cloud
https://openaccess.thecvf.com/content_CVPR_2020/papers/Shi_Point-GNN_Graph_Neural_Network_for_3D_Object_Detection_in_a_CVPR_2020_paper.pdf

点群データをグラフ化したものに対するgraph neural netによる物体検出

## 既存の方法
点群を
- 格子Voxelとその中の点の数で表現(c.f. NDT localizer)
- 近傍点の集合で表現(c.f. PointNet)
- 近い点を結んだgraphで表現 (c.f GNN)

## 関連研究

## 手法
素朴なGNN

$v_{t+1} =g^t (ρ {e^t_{ij} | (i,j) ¥in E},v_i^t)  $

$e^t_{ij} =f^t (v_i^t,v_j^t,)$
(2)

 - v: vertex
 - e: edge
 - t:iteration回数

に対してVertexの状態sを隣接Vertex x のsで更新するようにし(3), さらにvertexからの変位Δxで表現するのが本手法（auto-registration)( 4)

$s_i^{t+1}=g^t (ρ {f^t (x_j -x_i ,s_j^t) | (i,j) ¥in E},s_i^t) $ (3)

$ ∆x_i^t t = h^t(s^t_i) $
$ s_i^{t+1} =g^t ({f^t (x_j -x_i ＋ Δx_i^t ,s_j^t)},s_i^t) $ 

(4)

最終的に3つのMLP,edgeに沿ったaggregationによって構成される(5)。

$ ∆x_i^t t = MLP_h^t(s^t_i) $
$ e_ij^t=MLP_f^t ([x_j-x_i+Δx_i^j,s_j^t])
$ s_i[{t+1}=MLP_g^t(Max (e_{ij} |(i.j) ¥in E } ))_+s_i^t $

### loss
- average cross-entropy loss as the classification loss
- localization loss (位置のずれのHurber loss)
- L1 regularization to each MLP
の和

### Box Merging and Scoring
出力される複数の重複するbounding boxの併合(RCNNなのでも行われる)。occluded objectに対して
merged box by considering the entire overlapped box cluster

confidence Intersection-of-Union (IoU)

## 評価結果
dataset KITTI のLiDAR data
Car, Pedestrian and Cyclistに対してのaverage precision Pedestrianに対してはVoxelNetの方が高い
 
### Data Augmentation

## 実装コード
tensorflow
https://github.com/WeijingShi/Point-GNN

pytorch geometricを使っている

https://github.com/rui-qian/Point-GNN.pytorch-1
https://colab.research.google.com/drive/1D45E5bUK3gQ40YpZo65ozs7hg5l-eo_U?usp=sharing

性能のまとめサイト
https://paperswithcode.com/paper/point-gnn-graph-neural-network-for-3d-object/review/

## 関連研究
https://www.sciencedirect.com/science/article/abs/pii/S0925231220315150

https://paperswithcode.com/task/3d-point-cloud-classification

