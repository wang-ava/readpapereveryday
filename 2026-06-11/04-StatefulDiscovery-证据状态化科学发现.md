# StatefulDiscovery: Evidence-Calibrated Claim Formation in Open-Ended Scientific Discovery

从“让模型回答问题”到“让代理判断何时下结论”，本研究的关键是状态化证据链。它更关注发现过程中的 claim 质量控制，而不是单次任务准确率提升，适合想把 AI 引入研究流程的人参考。

- **论文标题**：StatefulDiscovery: Evidence-Calibrated Claim Formation in Open-Ended Scientific Discovery
- **作者/机构**：Jiayao Chen, Shi Liu, Linyi Yang；机构信息未在公开摘要页给出
- **发布日期/版本日期**：2026-06-10（UTC）
- **主题标签**：#AI4S #Scientific-Discovery #Agent #Evidence-Ranking #Reasoning
- **论文链接**：[https://arxiv.org/abs/2606.11851](https://arxiv.org/abs/2606.11851)
- **PDF 链接**：[https://arxiv.org/pdf/2606.11851.pdf](https://arxiv.org/pdf/2606.11851.pdf)
- **项目/代码/数据链接（如可得）**：未见公开代码与数据链接
- **核心问题**：开端式科学发现不仅是执行已有分析，更是持续决策“接下来该研究什么”；模型容易在证据不足时过度解释、过早下结论。
- **方法概要**：提出 StatefulDiscovery 框架：
  1. 引入显式“state”记录探索轨迹；
  2. 状态内关联 frontier 选择、证据收集、claim 处理；
  3. 使用结构化假设与局部裁决机制约束 claim 形成；
  4. 在多轮探索中动态平衡探索收益与证据可靠性。
- **主要贡献**：
  1. 将科学探索流程形式化为“证据-假设-主张”的闭环状态机；
  2. 强调 claim 可证性而非仅关注单步精度；
  3. 提出可复用的 frontier 控制与 adjudication 机制。
- **关键实验或结果**：在 40 个真实数据发现任务中，StatefulDiscovery 相比若干基线，产生了更多“既有较好支持又高价值”的 claim；消融表明结构化假设、局部裁决、frontier 控制均有贡献。
- **适合关注的原因**：
  1. 回应 AI4S 中“结论可靠性”痛点；
  2. 可以减少科学研究自动化中的幻觉式推断；
  3. 提供了可解释的状态管理模板，便于和实验台账系统结合。
- **局限性或待验证点**：
  1. “高价值 claim”的评判仍依赖任务定义与评审者偏好；
  2. 大规模跨学科任务中状态结构可能膨胀；
  3. 公开复现实验包与详细超参尚未充分展开。
- **对后续研究/应用的启发**：可与实验数据平台联动，把“证据可信度”作为调度信号加入 agent workflow；对科研自动化流程中可复用、可追踪的发现链路建设有直接启示。
- **Obsidian 快速浏览一句总结**：把“科学发现代理”从答题器转向研究流程管理器，核心是让每个 claim 都有可追踪证据等级。

## 标准化研究框架
- **Research question：** 在开放式科学探索任务中，如何使代理在多轮决策下产出更可信、可复核的研究主张（claim）？
- **Literature：** 该工作位于 AI for Science 与 open-ended reasoning 交界，补齐了“多步探索 + 证据校准”维度的缺口。
- **Theory：** 可视为决策过程建模：用显式状态替代一次性提示，实现证据驱动的 claim 形成机制。
- **Hypotheses：** 引入显式状态和 frontier 调度可减少过早泛化与虚高主张，提升 claim 与证据的一致性。
- **Method：** 设计 stateful 工作流（frontier 选择→证据获取→主张裁决），并通过 ablation 分析各模块贡献。
- **Data and Analysis：** 使用 40 个数据驱动发现任务评估 claim 数量、支持充分度和高价值比例；对比基线并做组件消融。
- **Findings：** 显著提升了高价值且证据充分 claim 的产出；状态化机制是主要增益来源之一。
- **Conclusion：** 面向 AI4S，状态化证据治理是缓解“伪深度发现”与过度推断风险的有效方向，但需进一步扩展到大规模跨学科场景验证。
