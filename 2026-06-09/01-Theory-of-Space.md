Theory of Space 值得排在第一篇，因为它不再把 embodied intelligence 当成“看图答题”的扩展，而是明确追问：模型能不能靠主动探索建立、修正并利用自己的空间信念。

# Theory of Space: Benchmarking Active Spatial Belief Construction and Revision in Foundation Models for Embodied Agents

## 基本信息

- 论文标题：Theory of Space: Benchmarking Active Spatial Belief Construction and Revision in Foundation Models for Embodied Agents
- 作者/机构：Pingyue Zhang、Zihan Huang、Yue Wang、Jieyu Zhang、Letian Xue、Zihan Wang、Qineng Wang、Keshigeyan Chandrasegaran、Ruohan Zhang、Yejin Choi、Ranjay Krishna、Jiajun Wu、李飞飞、Manling Li；作者列表显示包含 Stanford、University of Washington、Carnegie Mellon 等团队成员
- 发布日期或版本日期：2026-05-27（OpenReview）；最后修改 2026-06-01
- 主题标签：#EmbodiedAI #SpatialReasoning #ActiveExploration #Benchmark #FoundationModels
- 论文链接：https://openreview.net/forum?id=c2cxLvsdUp
- PDF 链接：https://openreview.net/pdf?id=c2cxLvsdUp
- 项目链接：未见独立项目页
- 代码链接：未见公开代码
- 数据链接：未见独立公开数据页

## 核心问题

多模态 foundation model 在被动 perception 和 reasoning 上已经很强，但真实具身任务要求模型在部分可观测环境中主动获取信息、构建认知地图，并在新证据出现后及时修正旧信念。本文要回答的是：现有 foundation models 是否真的具备这种 active spatial belief construction 与 revision 能力？

## 方法概要

作者提出 Theory of Space 这一评测设定，把空间智能定义为 agent 在 partial observability 下通过 self-directed exploration 构建、更新并利用 spatial belief 的能力。具体实现上，论文设计了文本环境和视觉环境，不是让模型直接解固定下游任务，而是先进行以 curiosity 为目标的探索；核心诊断机制是 spatial belief probing，即在每一步提示模型显式暴露其“内部认知地图”，从而量化 belief quality。

## 主要贡献

- 提出 Theory of Space 这一更贴近 embodied intelligence 本质的 benchmark 目标，而不是继续停留在被动空间问答。
- 用 textual 和 visual 两类环境测试主动探索下的 spatial belief construction。
- 引入 spatial belief probing，让“模型到底记住了什么”可以被直接测量，而不是只看最终任务成败。
- 诊断出三个关键瓶颈：Active-Passive Gap、探索低效，以及 belief instability / belief inertia。

## 关键实验或结果

- 论文报告了明显的 Active-Passive Gap：例如 GPT-5.2 在需要自主收集信息时，表现从 57.1 降到 46.0。
- 模型探索过程表现出高冗余和低系统性，效率不如 program-based proxies，但结果也没有更好。
- belief probing 显示，perception 是初始瓶颈，但更严重的问题是全局 spatial belief 会随时间退化。
- false belief paradigm 暴露出明显的 Belief Inertia：模型难以及时覆盖已经过时的旧先验，视觉模型尤甚。

## 适合关注的原因

如果你关心 embodied agents、robot navigation、interactive multimodal reasoning 或 world model evaluation，这篇非常值得看。它把“空间理解”从静态 benchmark 拉回到一个更真实的问题：agent 是否真的能边探索边形成可修订的 internal map。这个问题会直接影响后续 benchmark 设计、memory architecture 和 planning loop。

## 局限性或待验证点

- 当前结果来自 workshop 论文，结论很有启发性，但仍需更大规模主会或后续扩展验证。
- belief probing 依赖 prompting 让模型显式表达内部状态，这与真实隐式状态未必完全一致。
- 文中强调 curiosity-driven exploration 的评测价值，但它与具体下游控制任务的对应关系仍有进一步量化空间。
- 公开项目页和代码尚未看到，短期复现与扩展门槛偏高。

## 对后续研究/应用的启发

后续工作可以把 spatial belief 当成一等公民，而不是把地图、记忆和推理都塞进同一段上下文里。对应用来说，无论是 household agent、web agent 里的 GUI spatial grounding，还是移动机器人探索，都应该单独检查 belief update 是否稳定，而不只是看 final success rate。

## Obsidian 快速浏览总结

这篇论文说明 foundation model 的空间智能短板不只是“看不准”，更是“不会主动补信息，也不会稳定改信念”。

## 标准化研究框架

**Research question：** 本文的研究问题是：在部分可观测环境中，foundation models 能否通过主动探索构建、修正并利用空间信念，而不仅是在给定完整观察时回答空间问题。

**Literature：** 相关文献涵盖 embodied AI、spatial reasoning、active exploration、认知地图以及多模态 foundation model evaluation。本文的切入点是指出既有研究更多评估被动空间理解，而非主动 belief construction。

**Theory：** 本文不是社会科学式理论检验，但其等价理论主张是：真正的 embodied spatial intelligence 应包含 belief construction、belief revision 与 belief exploitation 三个环节，而不仅是静态 perception + QA。

**Hypotheses：** 论文虽非显式假设检验，但可等价理解为：现有 foundation models 在主动探索设定下会显著弱于被动设定；模型存在探索低效、belief instability 和 belief inertia 等系统性缺陷。

**Method：** 方法上构建了 Theory of Space benchmark，在文本与视觉环境中要求模型进行 curiosity-driven exploration，并通过 spatial belief probing 持续读取模型的显式认知地图。

**Data and Analysis：** 数据与分析围绕文本和视觉环境中的探索轨迹展开，评估包括主动与被动设定对比、belief quality 测量、下游任务表现、以及 false belief 条件下的修正能力诊断。

**Findings：** 主要发现是现有模型存在明显 Active-Passive Gap，探索效率低，空间信念会随时间退化，并且面对新证据时往往难以覆盖过时先验。

**Conclusion：** 结论是 embodied foundation models 的空间短板不只在 perception，更在主动探索与信念更新机制，因此未来系统需要更明确的 belief-centric memory 与 planning design。
