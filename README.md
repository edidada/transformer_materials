# transformer_materials
Transformer 的学习资料需要兼顾理论直觉与代码实现。以下是按学习路径整理的公开资源，从建立直觉到动手复现，再到深入细节。

第一步：建立直觉（必读）
在看代码之前，先搞懂数据在 Transformer 里是怎么流动的。

《The Illustrated Transformer》（图解 Transformer）：这是公认讲解最直观的文章，用动画式的图解一步步拆解注意力机制和数据流。有多个中文精译版可供阅读。

DeepLearning.AI 短课《How Transformer LLMs Work》：由 Jay Alammar（即上述图解作者）主讲，约 1 小时 44 分钟，涵盖分词、自注意力、Transformer 块以及 KV cache 等现代改进，适合快速建立系统性认知。

第二步：动手实现（CS336 核心要求）
CS336 作业 1 要求你独立写出模型，因此必须跟着代码动手。

Andrej Karpathy《Let's build GPT: from scratch》：YouTube 上的经典视频。他在视频里逐行手写代码，从零构建一个 GPT 模型，并讲解每个操作背后的原因。这是理解“自回归语言模型 + Transformer”最直接的途径。

中文开源复现项目（songyaolun/transformer-from-scratch）：提供完整的 PyTorch 手写教程，附带 Colab Notebook 可一键运行。内容覆盖词表构建、多头注意力、Encoder/Decoder 层组装以及训练推理，非常适合对照 CS336 作业进行练习。

另一份手写实现（yj-liuzepeng/transfomer）：同样是从零手写的代码库，附带理论详解文档，组件拆解清晰（MultiHeadAttention、PositionalEncoding、LayerNorm 等），适合作为参考实现对照学习。

第三步：深入原理与经典论文
动手实现之后，需要回到原始定义，把“为什么这样设计”讲清楚。

《Attention Is All You Need》（Vaswani et al., 2017，arXiv:1706.03762）：Transformer 的奠基论文。建议搭配实现一起读，重点关注缩放点积注意力、多头机制与位置编码的设计动机。

Harvard NLP《The Annotated Transformer》（nlp.seas.harvard.edu/annotated-transformer）：逐行 PyTorch 注释版论文实现，把数学公式和代码一一对应，是“读论文 + 看代码”的桥梁。

Lilian Weng《Attention? Attention!》（lilianweng.github.io）：系统梳理了注意力从 Bahdanau 注意力到自注意力、多头注意力的演进，适合补全背景脉络。

Jay Alammar《The Illustrated BERT》（jalammar.github.io/illustrated-bert）：用图解讲清楚 Transformer 在预训练语言模型（BERT/GPT）中的具体形态，帮助理解编码器与解码器的不同用法。

第四步：进阶主题与工程实践
当基础架构已经熟悉，可以进一步延伸到现代 LLM 的关键技术。

Stanford CS336 课程本身（cs336.stanford.edu）：从分词、架构、训练到推理的完整体系，作业从零实现并训练一个 GPT 类模型，是系统性进阶的标杆路径。

Andrej Karpathy《nanoGPT》（github.com/karpathy/nanoGPT）：极简、可读的 GPT 训练代码库，适合在 CS336 作业之外快速实验“训练一个自己的小模型”。

Hugging Face LLM 课程（huggingface.co/learn/llm-course）：覆盖分词、微调、对齐与部署的实战教程，配合 transformers 库可直接上手。

Hugging Face《Illustrating Reinforcement Learning from Human Feedback》（huggingface.co/blog/rlhf）：用图解讲清 RLHF 流程（SFT → 奖励模型 → PPO），是理解现代对齐训练最直观的资料。

补充：社区与持续跟进
- Papers with Code（paperswithcode.com）：按任务追踪最新论文与开源实现，适合长期跟进。
-  arXiv cs.CL / cs.LG 每日更新：关注注意力变体（如 FlashAttention、MQA/GQA）、长上下文（RoPE、ALiBi）、稀疏化与 MoE 等新方向。
- 本仓库 docs/ 目录：收录对关键模块的深入笔记（如自注意力数学形式、位置编码对比），作为上面的图文资料的代码级补充。