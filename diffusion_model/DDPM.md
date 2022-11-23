https://arxiv.org/abs/2006.11239

# 概要
画像生成用拡散モデル　画像にガウシアンノイズをかける過程の平均値$μ_\theta(x_t, t)$を変分ベイズにより学習し、それから同州されるスコア関数$\eps_\theta(x,t)$として画像をサンプリングする。

FID scoreがGANに比べて良いという評価結果

# 実装
- https://github.com/hojonathanho/diffusion

latent diffusion

- diffuser https://github.com/huggingface/diffusers
にも実装がある。
   - https://github.com/huggingface/diffusers/tree/main/src/diffusers/models Unet,VAE,attentionなどの部品ネットワーク置き場
   - https://github.com/huggingface/diffusers/blob/main/src/diffusers/pipelines/ddpm/pipeline_ddpm.py　乱数生成、Unetに入れる、拡散過程の適用
   - https://github.com/huggingface/diffusers/blob/main/src/diffusers/schedulers/scheduling_ddpm.py 関数stepが拡散過程本体　_init はα,βの計算
 
同じ場所に発展的な研究実装もおいてある
 - https://github.com/huggingface/diffusers/blob/main/src/diffusers/schedulers/scheduling_ddpm.py　
など

-コードと数式の対置 https://nn.labml.ai/diffusion/ddpm/index.html

