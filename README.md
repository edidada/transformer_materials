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