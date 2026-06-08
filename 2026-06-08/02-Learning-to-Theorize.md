这篇工作的亮点不在于把 world model 做得更大，而在于重新定义“理解世界”这件事：理解不只是预测下一帧，更应该意味着能形成可复用、可组合的 explanatory theory。

# Learning to Theorize the World from Observation

## 基本信息

- 论文标题：Learning to Theorize the World from Observation
- 作者/机构：Doojin Baek、Gyubin Lee、Junyeob Baek、Hosung Lee、Sungjin Ahn
- 发布日期或版本日期：2026-06-04（arXiv v2；初版 2026-05-05）
- 主题标签：#WorldModel #TheoryBuilding #RepresentationLearning #Reasoning #NeuroSymbolic
- 论文链接：https://arxiv.org/abs/2605.03413
- PDF 链接：https://arxiv.org/pdf/2605.03413
- 项目链接：未见公开项目页
- 代码链接：未见公开代码
- 数据链接：未见单独公开数据页

## 核心问题

很多 world model 把“理解”定义为未来预测准确，但这未必等价于形成可解释、可迁移的世界知识。本文要回答的是：模型能否直接从非文本观测中学习出显式、可组合、可执行的 theory，而不仅仅是隐式地拟合观测分布？

## 方法概要

作者提出 Learning-to-Theorize（L2T）范式，并用 Neural Theorizer（NEO）做实例化。NEO 把 theory 表示为一种可执行的 latent program，相当于 learned Language of Thought；这些程序通过共享 transition model 执行，并由可重组的 primitive 组成，从而支持对新现象的组合式解释。

## 主要贡献

- 把 world understanding 从“预测式表征”转向“theory 式表征”。
- 提出 NEO，用 latent neural program 作为显式理论载体。
- 强调 explanation-driven generalization，而不是单纯观察到结果后的 pattern fitting。
- 为 world model、reasoning model 和 neuro-symbolic learning 之间搭了一条很清晰的桥。

## 关键实验或结果

- 论文摘要给出的核心结果是：NEO 可以从原始非文本观测中学习出可执行、可组合的理论表示。
- 这种表示支持对新现象的 explanation-driven generalization，而不是只能记忆训练分布中的输入输出关系。
- v2 在 2026-06-04 更新，说明作者近期仍在完善版本与实验呈现。

## 适合关注的原因

如果你对 world model、reasoning、agent memory 或 AI cognition 感兴趣，这篇很值得读，因为它试图把“theory formation”重新带回机器学习语境。相比纯扩模型或纯做 benchmark，它更像是在追问下一代通用表征应不应该具备怎样的结构。

## 局限性或待验证点

- 从摘要看，当前验证更偏 proof-of-concept，距离开放世界复杂环境还有明显距离。
- latent program 的可解释性是否足够强，还要看具体可视化和失败案例。
- 论文强调 theory 的组合性，但规模化到真实视频、真实机器人或互联网级数据时，训练稳定性与表示效率仍待验证。
- 代码和项目页尚未公开，短期复现门槛可能偏高。

## 对后续研究/应用的启发

后续可以把 L2T 思路和视频 world model、embodied policy、scientific discovery 等方向结合，让模型不仅预测会发生什么，还能表示“为什么会这样”。应用上，它对可解释仿真、可验证 agent reasoning 以及更具结构性的 memory system 都有启发价值。

## Obsidian 快速浏览总结

这篇论文把 world model 从“会预测”往“会形成理论”推进了一步，值得当作结构化理解路线的风向标。

## 标准化研究框架

**Research question：** 本文的研究问题是：机器能否从非文本观测中直接学习出显式、可执行且可组合的世界理论，而不只是学习隐式预测器。

**Literature：** 相关文献涉及 world models、self-supervised dynamics learning、developmental cognitive science、Language of Thought 与 neuro-symbolic reasoning。本文借用了认知科学中的 theory-building 视角来重塑机器学习问题定义。

**Theory：** 这里的“理论”不是社会科学因果理论，而是对世界生成机制的显式程序化解释。作者的核心理论主张是：真正的理解应体现在可组合、可执行的 explanatory structure 上，而不仅是压缩后的隐空间预测能力。

**Hypotheses：** 可等价表述为：如果模型学习到的是 theory-like representation，那么它应当比纯预测式表征更能解释新现象，并在组合泛化上表现更好。

**Method：** 方法是提出 L2T 学习范式，并以 NEO 为具体模型，通过 latent program induction 与共享 transition execution 学习理论表示。

**Data and Analysis：** 数据和分析主要围绕从观测恢复生成机制的实验设置展开。虽然摘要未展开具体数据集细节，但分析重点显然是解释能力、组合泛化和新现象上的表现。

**Findings：** 主要发现是 NEO 能够把观测映射为可执行的组合程序，并借此实现 explanation-driven generalization，说明 theory-building 表征在概念上是可行的。

**Conclusion：** 结论是世界理解可以被重新表述为 theory induction 问题，这为 future world models、reasoning systems 与可解释 agent 提供了新的建模方向。
