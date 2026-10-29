# Transformer 架构深入笔记

本笔记作为 README 中图文资料的代码/数学级补充，聚焦 Transformer 各核心模块的定义、公式与设计动机。公式采用 LaTeX 书写，可直接在支持 MathJax 的渲染器中查看。

## 1. 自注意力（Self-Attention）

给定输入序列 `X ∈ R^{n×d}`（n 个 token，每个维度 d），先线性投影出查询、键、值：

```
Q = X W_Q,  K = X W_K,  V = X W_V      W_* ∈ R^{d×d_k}
```

缩放点积注意力计算每个位置与其他所有位置的关联权重：

```
Attention(Q, K, V) = softmax( Q K^T / sqrt(d_k) ) V
```

- `Q K^T` 衡量 query 与 key 的相似度；
- `sqrt(d_k)` 缩放是为了在 d_k 较大时防止点积过大导致 softmax 梯度消失；
- 输出是值的加权和，权重由相似度决定，因此每个位置的表示都“软汇聚”了全序列信息。

## 2. 多头注意力（Multi-Head Attention）

将 Q/K/V 切分为 h 个头，各自独立做注意力再拼接：

```
head_i = Attention( Q W_Q^i, K W_K^i, V W_V^i )
MultiHead(Q, K, V) = Concat(head_1, ..., head_h) W_O
```

不同头可在不同子空间学习不同的依赖模式（如局部语法、长距离指代），`W_O ∈ R^{h·d_k×d}` 负责融合。

## 3. 位置编码（Positional Encoding）

注意力本身对顺序置换不变，需要显式注入位置信息。

- 绝对位置（原始论文）：用正弦/余弦固定函数 `PE_{(pos,2i)} = sin(pos / 10000^{2i/d})`，可让模型外推相对位置。
- 相对位置 / 偏置（如 T5、ALiBi）：直接在注意力分数上叠加与距离相关的偏置，更利于长上下文。
- 旋转位置编码 RoPE：将位置信息以旋转矩阵形式乘入 Q、K，在较多现代 LLM（Llama 等）中使用，对长度外推较友好。

## 4. 前馈网络与残差归一化

每个注意力/前馈子层外包残差连接与层归一化（Pre-LN 为当前主流）：

```
x = x + Sublayer( LayerNorm(x) )
```

逐位置前馈网络（FFN）：

```
FFN(x) = max(0, x W_1 + b_1) W_2 + b_2
```

两层之间维度通常放大（如 d → 4d → d），为模型提供非线性容量。

## 5. 编码器 vs 解码器

- 编码器：双向自注意力（可见前后文），适合理解类任务（分类、NER、编码表示）。
- 解码器：带因果掩码的自注意力（只能看左侧），自回归生成文本。
- 编码器-解码器：解码器通过交叉注意力（Cross-Attention，K/V 来自编码器）获取源序列信息，典型用于翻译。

## 6. 现代变体与关注点

- FlashAttention：IO 感知的精确注意力算法，降低显存与计算，是当前训练/推理的基础设施。
- MQA / GQA：多个查询头共享一组 K/V 头，显著减少推理时的 KV cache 占用。
- 稀疏 / 线性注意力、MoE：在大模型规模下平衡参数与计算成本。

> 配合 README 中的《The Annotated Transformer》与 nanoGPT 阅读，可把上述公式逐一映射到代码实现。
