# CodeRescue: Budget-Calibrated Recovery Routing for Coding Agents

Spotlight：论文不是把 LLM coding 成功率看作二元二选，而是强调失败后的再尝试是成本可控、可学习的动态决策问题。对真实 coding agent 的稳定性优化很有工程价值。

- 论文标题：CodeRescue: Budget-Calibrated Recovery Routing for Coding Agents
- 作者：Qijia He, Jiayi Cheng, Chenqian Le, Rui Wang, Xunmei Liu, Yixian Chen, Jie Mei, Zhihao Wang, Xupeng Chen, Yuhuan Chen, Tao Wang
- 机构：arXiv 页面未在元数据页明确列出完整机构归属（建议查看正文确认）
- 发布日期（版本）：2026-07-21
- 主题标签：#CodingAgent #ToolUse #RecoveryRouting #CostControl #LLM
- 论文链接：https://arxiv.org/abs/2607.19338v1
- PDF 链接：https://arxiv.org/pdf/2607.19338v1
- 项目/代码/数据链接：代码仓库 https://github.com/Qijia-He/agent-budget-control

## 核心问题
现有成本控制常把失败修复简化为“先用廉价模型再升级到昂贵模型”的级联决策，但忽略了可执行反馈可使廉价修复再次有效，导致总成本与成功率未充分优化。

## 方法概要
- 将编码失败后的后续选择建模为一个 recovery routing 问题：在多种动作（继续便宜尝试、切换策略、升级模型）之间选择；
- 用监督路由器学习不同失败场景下的最优恢复动作；
- 引入 Conformal Risk Control（CRC）层，在不重训模型的前提下支持部署期预算参数调节；
- 同时优化“通过率”与“平均消耗成本”。

## 主要贡献
- 把 coding agent 的失败恢复问题形式化为路由器任务；
- 给出可落地的预算校准机制（CRC）而非单一固定阈值；
- 在多 benchmark 上报告了“更优解率 + 更低成本”的 frontier，展示了实际可用价值。

## 关键实验或结果
摘要提到：在 GPT-5.4-nano/GPT-5.4 场景下，CRC 校准方案可达到比“总是升级”更高的求解率，同时降低约 35% 的平均恢复成本；并且优于固定路由、提示词路由及二分类级联基线。

## 适合关注的原因
该工作把“智能代理可靠性”中的关键一环（失败后如何修复）转为可调参数的策略学习问题，能直接影响 production coding agent 的稳定性与费用控制。

## 局限性或待验证点
- 论文主要覆盖 coding benchmark 场景；
- 对超大规模工程仓库的交互式修复泛化待验证；
- CRC 的保守性在极端非平稳任务分布中可能过于保守。

## 对后续研究/应用的启发
可用于构建“分级恢复预算器”：把每次代码执行后的失败类型（报错类型/超时/静默错误）映射到不同恢复策略，减少盲目 escalation。

## 一句 Obsidian 快速浏览总结
一句话：把“失败后该做什么”做成学习得到的路由策略，能在提升解题率的同时显著降本。

## 标准化研究框架
- **Research question：** 在给定调用预算下，coding agent 面对执行失败时如何动态选择恢复动作，以最大化成功率并抑制平均开销？
- **Literature：** 结合 agentic coding、tool-augmented LLM、成本敏感推理与风险校准文献，聚焦于决策级优化。
- **Theory：** 成本约束下的分层决策可用经验风险最小化与风险控制方法（如 conformal 风格校准）建模。
- **Hypotheses：** 与二元级联相比，允许多步 cheap 恢复 + CRC 预算控制可获得更高有效成功率与更低均值成本。
- **Method：** 用监督数据训练 recovery 路由器，再通过 CRC 进行部署级预算校准；按不同预算点选择决策边界。
- **Data and Analysis：** 多个 coding benchmark 失效样本上评估正确率、拒答/失败率、开销（mean recovery cost）及其权衡。
- **Findings：** 成功点在给定成本约束下可被显著上移，出现“比总是升级更优”的 frontier；cheap 路由与升级并非互斥。
- **Conclusion：** 在非社会科学实验中，该字段可理解为“将任务成功率与成本目标统一为可约束优化，并通过验证集/部署集分离实现风险稳健。”
