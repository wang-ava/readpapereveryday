# Weak-to-Strong Generalization via Direct On-Policy Distillation

该文针对“大模型后训练成本高、迁移慢”的痛点，提出把小模型 RL 后的策略偏移直接蒸馏到更强模型，避免重复在目标模型上做完整 RL。核心想法是保留“弱模型学到的更新方向”，并在强模型自身轨迹上继续施加该方向。

- 论文标题：Weak-to-Strong Generalization via Direct On-Policy Distillation
- 作者：Shiyuan Feng, Huan-ang Gao, Haohan Chi, Hanlin Wu, Zhilong Zhang
- 机构：arXiv 元信息未提供完整机构字段（建议后续核验作者主页）
- 发布日期：2026-07-06（v1）
- 主题标签：#LLM #Reinforcement Learning from Human Feedback #Distillation #Agent
- 论文链接：https://arxiv.org/abs/2607.05394v1
- PDF 链接：https://arxiv.org/pdf/2607.05394v1
- 项目/代码/数据：
  - Project page: https://bytedtsinghua-sia.github.io/Direct-OPD/
  - 代码/数据：未在 arXiv comment 中给出公开链接

## 核心问题

当直接在大模型上做 RLVR 代价高时，是否可以复用弱模型 RL 的收益？传统直观做法直接模仿弱模型最终策略，但可能混入模型容量与行为偏差。

## 方法概要

论文提出 Direct-On-Policy Distillation（Direct-OPD）：
- 对比弱模型 RL 后策略与其 pre-RL 参考模型，得到 log-ratio“策略转移信号”；
- 将该信号作为隐式奖励施加在强模型当前 on-policy 状态上，避免重新训练 reward model；
- 在强模型上完成 policy shift 迁移。

## 主要贡献

1. 将弱模型 RL 的价值放在“策略变化”而非最终参数上，降低迁移噪声。
2. 给出“直接在线蒸馏隐式奖励”的实现范式，减少强模型后训练资源。
3. 在 reasoning benchmark 上展示可稳定复用并组合多阶段 policy shift。

## 关键实验或结果

- Qwen3-1.7B 在 AIME 2024 上从 48.3% 提升到 62.4%，仅用 4 小时、8 张 A100（文内报告）。
- 对比 step-matched direct RL 有显著优势。

## 适合关注的原因

它直接降低了大模型 RL 训练的“每次都重算”的成本门槛，适合具备持续评估/迭代场景的研究与产品团队，在同一任务分布下快速刷新强模型性能。

## 局限性或待验证点

1. 当前验证任务主要集中在 reasoning 与代码风格评测，跨模态或具身任务泛化待验证。
2. 弱模型质量与 teacher-strong 差距过大时，策略偏移信号可能包含噪声。
3. 仍需验证安全/偏见约束在迁移过程中是否会被弱化。

## 对后续研究/应用的启发

可将 Direct-OPD 看作“policy-delta transfer”接口：把 RL 结果结构化为可复用信号，连接不同模型族、不同规模 checkpoint 的持续优化流程。适合在自研 agentic stack 中做 staged distillation。

一句中文总结：用弱模型 RL 的策略增量去喂强模型，给后训练带来更高性价比的升级路径。

## 标准化研究框架

- **Research question：** 弱模型上学习到的 RL 改进是否能以策略偏移形式稳定迁移到更强模型？
- **Literature：** 继承 RL 迁移学习与蒸馏范式，但将重心放在 on-policy policy delta 而非最终输出模仿。
- **Theory：** 强模型目标可近似分解为“任务能力学习 + 由弱模型提供的 policy shift regularizer”，后者能在不改动 reward model 的情况下实现迁移。
- **Hypotheses：** 在相同数据分布下，direct-OPD 比直接模仿最终模型参数更能保留 RL 收敛方向并节约预算。
- **Method：** 对弱模型与其参考模型的 log 概率差做隐式奖励，应用到强模型 on-policy rollout，量化不同任务下性能增益。
- **Data and Analysis：** 使用公开 benchmark（含 AIME、SWE-bench、Terminal-Bench）评估不同模型规模、不同组合策略的收益。
- **Findings：** 在典型评测中出现显著绝对收益增量，且显示可顺序组合多次 policy shift。
- **Conclusion：** 适配当前实践的结论是“弱强模型可通过策略偏移对齐进行高效协同”；不属于社会科学实证检验型研究，因此该字段以方法可迁移性和收敛机制作为对应。
