Theory of Space 值得看，不是因为它又造了一个 embodied benchmark，而是因为它把“主动探索下如何形成和修正空间 belief”这个更接近真实 agent 能力的问题单独拎出来了。读完后你会更清楚当前 foundation model 在 embodied spatial intelligence 上到底差在哪里。

# Theory of Space: Can Foundation Models Construct Spatial Beliefs through Active Exploration?

## 基本信息

- 论文标题：Theory of Space: Can Foundation Models Construct Spatial Beliefs through Active Exploration?
- 作者/机构：Pingyue Zhang、Zihan Huang、Yue Wang、Jieyu Zhang、Letian Xue、Zihan Wang、Qineng Wang、Keshigeyan Chandrasegaran、Ruohan Zhang、Yejin Choi、Ranjay Krishna、Jiajun Wu、Li Fei-Fei、Manling Li；公开页面可见作者来自相关高校与研究机构，OpenReview 页面未完整列出机构
- 发布日期或版本日期：OpenReview 发布 2026-05-27，最后修改 2026-06-01；GitHub 页面显示论文为 ICLR 2026
- 主题标签：#EmbodiedAI #SpatialReasoning #Benchmark #ActiveExploration #FoundationModels
- 论文链接：https://openreview.net/forum?id=c2cxLvsdUp
- PDF 链接：https://openreview.net/pdf?id=c2cxLvsdUp
- 项目链接：https://theory-of-space.github.io/
- 代码链接：https://github.com/mll-lab-nu/Theory-of-Space
- 数据链接：https://github.com/mll-lab-nu/Theory-of-Space ，视觉场景生成仓库：https://github.com/yw2544/ToS-vision-scenes

## 核心问题

具身智能不是只看懂当前视角，而是要在 partial observability 下主动探索环境、整合新旧信息、维护一致的空间认知地图，并在冲突出现时更新 belief。Theory of Space 的核心问题是：foundation models 是否真的具备这种 spatial belief construction、revision 和 exploitation 能力？

## 方法概要

作者把 Theory of Space 定义为三种耦合能力：Construct、Revision、Exploit。基于此，他们搭建 paired environments：一个是 text world，另一个是来自 ThreeDWorld 的 vision world。agent 可执行 Goto、Rotate、Observe、Query 等动作，目标不是完成具体家庭任务，而是进行 curiosity-driven exploration，建立完整准确的 spatial belief，再回答 route-level 和 survey-level 空间问题。

## 主要贡献

- 明确定义 Theory of Space，把 embodied spatial belief 当成核心能力而不是附属现象。
- 同时提供 text-based 与 vision-based 环境，便于区分“感知问题”和“推理问题”。
- 设计 active exploration、belief probing 与 belief revision 三类分析框架。
- 用显式 cognitive map probing 观察模型内部 belief 的正确性、稳定性、自我定位和不确定性判断。

## 关键实验或结果

- GitHub 公布的主动探索结果显示，在 vision world 中，Gemini-3 Pro 平均分约 57.3，GPT-5.2 约 46.0，说明即使强模型也远未解决问题。
- 在 text world 中，同类模型分数显著更高，例如 Gemini-3 Pro 可到 81.5，表明视觉感知与视觉 belief maintenance 是主要瓶颈。
- belief probing 结果指出：vision agents 的 perception、local-global consistency 与 stability 都明显更弱。
- belief revision 实验进一步显示，vision agents 存在明显 belief inertia，即看到新证据后仍难以覆盖旧的错误空间假设。

## 适合关注的原因

这篇工作特别适合正在做 embodied agent、spatial memory、navigation、world model 或 active perception 的读者。它提供了一个非常清晰的诊断框架：如果你的 agent 在长任务里迷路、重复探索、无法根据新观察修正计划，问题可能不只是 planner，而是底层 spatial belief 本身不稳定。

## 局限性或待验证点

- benchmark 环境仍然是构造化世界，与真实机器人场景之间存在 sim-to-real 距离。
- 当前指标更多测“空间 belief 能否形成”，并不直接等价于所有 embodied downstream task 成功率。
- 使用专门 action space 和任务协议后，结果会受到 prompt、tooling 与 inference budget 影响。
- 一些模型成绩来自特定闭源版本，后续快速迭代后分数可能变化，因此更适合作为诊断趋势而非永久排名。

## 对后续研究/应用的启发

后续应更明确地区分 perception bottleneck、memory bottleneck 与 revision bottleneck，并针对性设计 object-centric map、uncertainty-aware memory 和 active replanning 机制。工程侧也很直接：不要把空间错误都归咎于 planner，很多失败其实发生在“地图没建对”这一步。

## Obsidian 快速浏览总结

当前 embodied foundation model 最大的问题之一，不是不会规划，而是没能稳定建立和修正自己的空间心智地图。

## 标准化研究框架

**Research question：** 本文研究的问题是：foundation models 在主动探索、部分可观测环境中，能否构建、维护并修正一致的 spatial belief，以支持后续空间推理与行动。

**Literature：** 相关文献覆盖 embodied AI、active perception、spatial reasoning、cognitive map、navigation benchmark 与 multimodal foundation models。本文的切入点是把空间 belief 作为中间能力层进行显式评估。

**Theory：** 这里的理论不是社会科学因果理论，而是认知与具身智能中的等价理论框架：高质量 embodied behavior 依赖于可更新的内部空间表征；如果 belief construction 和 revision 失败，后续规划与执行会系统性退化。

**Hypotheses：** 可等价理解为：模型在 text world 会显著强于 vision world；主动探索比被动理解更能暴露空间 belief 缺陷；belief revision 会成为视觉模型的重要薄弱环节。

**Method：** 方法是提出 ToS benchmark，在文本与视觉环境中让 agent 进行主动探索，并通过 route-level、survey-level、belief probing 和动态 perturbation 任务测量 Construct、Revision、Exploit 三类能力。

**Data and Analysis：** 数据来自程序生成的多房间布局和 3D 视觉场景。分析包括主动探索分数、被动理解分数、认知地图探针指标、belief inertia 与 revision 正确率等。

**Findings：** 结果表明文本环境分数明显高于视觉环境；视觉感知是主要瓶颈，但 belief stability 与 belief revision 也同样脆弱；模型常在看到新证据后仍保留过时空间假设。

**Conclusion：** 结论是空间 belief 构建与修正仍是 embodied foundation models 的关键瓶颈，未来研究需要把主动感知、记忆一致性与 uncertainty-aware revision 放到核心位置。
