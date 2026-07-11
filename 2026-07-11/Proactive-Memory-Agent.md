# Remember When It Matters: Proactive Memory Agent for Long-Horizon Agents

## Spotlight（今日速读）
该文把“长程任务中的记忆衰减”具象化为可操作问题：记忆不只是检索，而是一个独立的主动决策组件。论文给出一个 plug-and-play 的 proactive memory agent，在长程任务上带来明显收益。

## 论文标题
Remember When It Matters: Proactive Memory Agent for Long-Horizon Agents

## 作者/机构
- 作者：Yifan Wu, Lizhu Zhang, Yuhang Zhou, Mingyi Wang, Bo Peng, Serena Li, Xiangjun Fan, Zhuokai Zhao
- 机构：arXiv 元数据未直接列出机构，文中提供的训练与基准设定可在后续代码/项目页核验

## 发布时间
2026-07-09（版本号：v1）

## 主题标签
#Agent #Memory #Long-horizon #RLHF #Benchmarks

## 论文链接
https://arxiv.org/abs/2607.08716v1

## PDF 链接
https://arxiv.org/pdf/2607.08716v1

## 项目/代码/数据链接
- arXiv 文本未公开给出代码仓库链接；可在后续发布页面持续跟进

## 核心问题
长时序任务中，轨迹信息、关键决策历史与反馈线索会随交互长度增长而丢失，被称为 behavioral state decay。现有 agent 多依赖上下文窗口扩展或被动检索，无法系统性决定“何时需要回忆”与“回忆何物”。

## 方法概要
- 定义一个独立的 memory agent，作为 action agent 的伴随模块并行运行。
- memory agent 会持续从最近轨迹构建结构化记忆，并学会在关键时刻插入 reminder（而非持续注入）。
- 支持插入式策略与静默策略，在 Terminal-Bench 2.0、τ²-Bench 上做对比。
- 采用 SFT + GRPO 在 SETA 上训练并验证跨基线迁移。

## 主要贡献
- 将记忆机制从“被动检索”升级为“主动记忆决策”。
- 提供可插拔方案，可叠加到已有 agent 框架。
- 在两个长程 benchmark 上显著提升 pass@1（+8.3 pp / +6.8 pp）。
- 证明选择性 intervention 优于一直注入、advisor-only、纯检索等基线。

## 关键实验或结果
- Terminal-Bench 2.0：pass@1 提升 +8.3 pp；
- τ²-Bench：pass@1 提升 +6.8 pp；
- 选择性提醒策略在多数场景优于“始终插入”与“只读检索”。

## 适合关注的原因
这为长程 AI agent 在现实工作流中的“记忆策略”提供了实操方向，不只靠上下文长度扩容，而是靠何时回忆、回忆什么来降低代价。

## 局限性或待验证点
- 目前主要在公开 benchmark 验证，真实生产环境中的噪声反馈和权限限制未覆盖；
- 代理模块可能引入额外推理延迟；
- 与不同底座模型、不同任务结构的泛化待更多实验。

## 对后续研究/应用的启发
- 记忆模块应与规划/执行解耦，变成“轻量决策器”；
- 可以引入记忆预算约束（token、延迟、隐私）用于实际系统调度；
- 在客服、运维、研发自动化中，记忆提醒策略有望显著降低重复错误与回放成本。

## 标准化研究框架
- **Research question：** 在长期任务中，主动型记忆注入是否比被动记忆检索更能稳定提升智能体绩效？
- **Literature：** 现有长期智能体方法重视上下文扩展与检索增强，较少建模“是否该记忆”的策略层。
- **Theory：** 非实验社会科学语境下，本文将理论字段定义为“行为状态衰减模型”：智能体性能是记忆更新策略与历史证据利用效率的函数。
- **Hypotheses：** (1) 插入式记忆可缓解行为状态衰减；(2) 过量提醒会带来干扰，选择性机制更优；(3) 与 baseline action agent 结合可实现迁移增益。
- **Method：** 搭建独立记忆 agent，与 Terminal-Bench 2.0 与 τ²-Bench 上的不同 action agent 做对照。
- **Data and Analysis：** 在两个 benchmark 中比较 pass@1 与失败类别（遗漏关键信息/错误分支）并做策略消融（selective vs always-on vs advisor-only）。
- **Findings：** 选择性提醒显著提升长程成功率，并优于多种替代策略。
- **Conclusion：** 长程任务的关键不只是“记更多”，而是“何时、为何、如何记”，这一策略层可系统化成可插拔组件。

一句话总结：长程智能体的记忆问题，本质是“策略化调用记忆”，而非单纯扩容上下文。
