# Pass the Baton: Trajectory-Relayed On-Policy Distillation

Spotlight：把 on-policy distillation 的“错误前缀连锁崩塌”显式化为可控交接点，并在 teacher 的少量介入下提升长链推理稳定性。

- 论文标题：Pass the Baton: Trajectory-Relayed On-Policy Distillation
- 作者：Haolei Xu, Xiaowen Xu, Haiwen Hong, Zixuan Ni, Hongxing Li, Yiwen Qiu, Weiming Lu, Yongliang Shen
- 机构（如可得）：页面未公开
- 发布日期或版本日期：2026-07-28（v1）
- 主题标签：#LLM #Reasoning #Distillation #LLM-Agent #RLHF-style
- 论文链接：[https://arxiv.org/abs/2607.26057v1](https://arxiv.org/abs/2607.26057v1)
- PDF 链接：[https://arxiv.org/pdf/2607.26057v1](https://arxiv.org/pdf/2607.26057v1)
- 项目/代码/数据链接（如可得）：Project: [https://zju-real.github.io/Relay-OPD](https://zju-real.github.io/Relay-OPD)；Code: [https://github.com/zju-real/Relay-OPD](https://github.com/zju-real/Relay-OPD)

## 核心问题
- on-policy distillation（OPD）在学生模型自举时容易出现前缀错误：一旦思路偏离，后续监督会继续沿错误路径放大偏差。
- 传统修正方法常要么标注代价高，要么重跑大规模生成，导致推理成本高且不可控。
- 如何用更低代价在关键时刻“接管-纠偏-交还”，提高数学与长链 reasoning 的稳定性，是这篇工作聚焦的问题。

## 方法概要
- 文中提出 Relay-OPD：对学生轨迹中的失败前缀检测触发点，短时引入 teacher 进行接管，生成 teacher leg 后交还给学生。
- 引入“label-free handoff trigger”，不依赖外部逐 token 的额外人工标签。
- 采用可控的 relay budget：仅在关键时段有限次替换，既保留学生主体能力又避免轨迹偏移过大。
- 以 OPD 框架下训练流程为基础，比较标准 OPD 与 FastOPD，并加入 teacher 轮换机制。

## 主要贡献
- 把前缀错误问题上升为训练层可观测事件，提出可操作的 teacher-student 交接策略。
- 给出在数学推理任务上可复用的“最小干预”范式：不是全流程替换，而是在必要时段点对点纠偏。
- 在同样架构下给出显著更省算力的轨迹优化方向，减少了训练路径中的冗余偏差探索。

## 关键实验或结果
- 以 Qwen3-4B-Instruct-2507 为 teacher，Qwen3-0.6B/1.7B-Non-Thinking 为 student，在 8 个数学推理基准评估。
- Relay-OPD 在 1.7B 上平均超越标准 OPD +5.73%，超越 FastOPD +1.49%。
- 多组设置均显示训练轨迹长度下降超过 50%，说明效率提升是该方法的重要收益。

## 适合关注的原因
- 这类“有限教师干预”策略，直接对应现实 Agent 中的长链修复问题：LLM 一旦进入错误链条，如何快速回到正确分支。
- 方法比单纯扩大模型更贴近工程控制，能显著降低重试与失败恢复成本。

## 局限性或待验证点
- 评价主要集中于数学推理，尚缺与多模态工具调用或复杂 planning 的系统级泛化检验。
- 触发阈值与 teacher 介入时机可能依赖任务分布，是否可迁移到超长开放域对话/工具调用尚不确定。
- 并未直接解决“教师失误”本身的风险，交接策略仍依赖 teacher 质量。

## 对后续研究/应用的启发
- 可以将该机制迁移到 tool-using 或 agent workflow 中，作为“runtime recovery policy”的核心模块。
- 与 verifier 或 reward-model 结合可形成“触发-纠偏-审计”闭环，提高自动化系统的可靠性。
- 可在推理服务中做预算分配实验：用更低 compute 保证高置信度链路。

## 一句 Obsidian 快速浏览总结
一句话：Relay-OPD 通过有界 teacher 接管，把“错误前缀传播”变成可控修复，兼顾推理准确率与算力效率。

## 标准化研究框架
- **Research question：** 在 on-policy distillation 中，能否通过少量、可解释的教师接管机制，在不依赖额外标注的情况下显著抑制 student 错误前缀的累积失真？
- **Literature：** 延续 OPD 与 teacher-student 蒸馏方向，但与传统全流程蒸馏不同，强调“时点选择”与“最小干预”原则。
- **Theory：** 从路径依赖角度看，单次早期偏差会放大为后续全局偏差；有限教师重置可降低马尔可夫链式误差传播。
- **Hypotheses：** 
  - 限定触发点数量的 teacher relay 可以显著提升 benchmark 得分；
  - 更低比例的干预可兼顾性能与训练轨迹长度；
  - 机制主要在长推理链和高步骤任务上收益更明显。
- **Method：** 在公开数学推理 benchmark 上比较 OPD/FastOPD 与 Relay-OPD：定义交接规则、relay budget 并执行统一训练与评测。
- **Data and Analysis：** 以 8 个数学基准为主，关注平均分提升、失败前缀恢复能力及训练 trajectory length，进行统计对比与显著性讨论。
- **Findings：** 在论文报告中，Relay-OPD 在 1.7B 条件下显著优于 OPD 与 FastOPD，且在相同任务中显著缩短训练轨迹。
- **Conclusion：** 对应“有成本预算的 reasoning safety”场景，Relay-OPD 提供了可落地的纠偏架构，比单纯扩大模型参数更高效。
