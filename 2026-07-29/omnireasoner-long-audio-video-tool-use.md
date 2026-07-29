# OmniReasoner

Spotlight：论文把长视频推理中的成本瓶颈变成“是否放大细节”的决策问题：先低成本扫描，全局建立候选，再按需调用高代价工具，这一“选择式放大”思路很像真实生产里可扩展的 multimodal Agent 设计。

- 论文标题：OmniReasoner: Thinking with Long Audio-Video via Native Tool Use
- 作者：Yu Chen, Caorui Li, Ziyu Xiong, Yidong Wang, Mingqi Gao, Shuman Liu, Biao Liu, Chunfeng Yang, Anxiang Zeng, Haibo Zhang, Chaofan Chen
- 机构（如可得）：未在 arXiv 页面直接给出机构信息
- 发布日期或版本日期：2026-07-21（v1）
- 主题标签：#LLM #Multimodal #ToolUse #VisionLanguageModel #Reasoning
- 论文链接：[https://arxiv.org/abs/2607.19339v1](https://arxiv.org/abs/2607.19339v1)
- PDF 链接：[https://arxiv.org/pdf/2607.19339v1](https://arxiv.org/pdf/2607.19339v1)
- 项目/代码/数据链接（如可得）：Code：https://github.com/RockyChen0205/OmniReasoner

## 核心问题
- 长音视频中关键证据稀疏且跨模态，统一高保真处理会带来高算力和高延迟。
- 现有方法常在整段输入都高采样，效率低且不稳定。
- 模型需要学会“在何时调用工具、在何处放大细节、如何保持时序一致性”。

## 方法概要
- 先用低成本全局预览建立候选推理轨迹，再按需触发 zoom-in tool 进行局部高保真检索。
- 提出 TimeAnchor：统一不同采样率下的时间锚点映射，避免工具调用后上下文错位。
- 用 Temporal Augmented Data Engine 合成 tool-use 轨迹（视频编辑与合成）来做后训练数据，减少人工标注成本。
- 同时采用 SFT + RL 训练，强化模型在何时调用工具与何时回答之间的决策权衡。

## 主要贡献
- 将“长音视频推理”中的时序与计算分配建模为工具调用决策问题。
- TimeAnchor 给出跨尺度时间对齐机制，提升连续工具调用的一致性。
- Temporal Augmented Data Engine 使 tool-use 训练可扩展，降低数据构造门槛。

## 关键实验或结果
- 在 omnimodal 与视频类 benchmark 上，提出的方法在答案准确率与时间定位（temporal grounding）上均有提升。
- 相比不做精细化放大策略的 baseline，能把高保真计算集中在高信息密度区域。
- 论文称其提升在多任务上都可见，但未披露完整表格数字（在现有摘要层面以机制改进为主）。

## 适合关注的原因
- 对真实应用中“长输入 + 工具调用”问题很贴近，尤其是安防、监控复核、法务审计、工业巡检等场景。
- 把“多模态推理”与“系统预算约束”一起处理，而非单纯追求模型规模。

## 局限性或待验证点
- 当前仍依赖合成的 tool-use trajectory 与 benchmark 评估，跨域真实场景泛化有待验证。
- 工具策略训练对超参和奖励设计敏感，可能带来迁移成本。
- 长时序偏差与数据偏移下的时域 anchor 错误仍可能放大。

## 对后续研究/应用的启发
- 可拓展到视频生成审计、长文档检索、机器人长序列决策等“先快速扫描后局部深入”的系统。
- 提供了一个可迁移的模板：统一定义低成本主干 + 高成本工具通道 + 时序对齐。

## 一句 Obsidian 快速浏览总结
一句话：OmniReasoner 的核心是让 LLM 学会“先广后精”的时间放缩决策，把长音视频推理从暴力全量读取变成可控工具调用流程。

## 标准化研究框架
- **Research question：** 在长音视频任务里，如何通过工具调用策略在保真度与成本之间实现最优平衡，并提升时序定位和回答可靠性？
- **Literature：** 基于现有长上下文 multimodal LLM 与 tool-augmented reasoning 的工作，补上了连续时序决策与时间对齐的缺口。
- **Theory：** 低成本全局扫描提供先验证据分布估计，局部放大用于降低熵高区域的不确定性，二者可提高 sample efficiency。
- **Hypotheses：** 若模型能够学习可靠的 tool-use 触发策略，并保持时间锚点一致性，推理效果在长音视频任务上可在不增加训练预算前提下显著改善。
- **Method：** 构建双分辨率推理框架（global preview + zoom-in），通过时序对齐模块和后训练（SFT+RL）联合优化。
- **Data and Analysis：** 使用 Temporal Augmented Data Engine 合成工具轨迹，评估指标围绕准确率和 temporal grounding，关注高价值片段利用率。
- **Findings：** 工具决策机制与时序对齐显著改善长视频理解中的响应质量，并提升对关键片段的定位能力。
- **Conclusion：** 方法为长音视频 + 资源受限推理提供了可工程落地的分层策略。
