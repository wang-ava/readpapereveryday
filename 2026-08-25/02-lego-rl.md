# LEGO-RL: Harness-Native Reinforcement Learning for Coding Agents

该文聚焦 coding agent 训练中的“环境噪声+工具链不透明”问题，给出一个兼顾真实 harness 行为与强化学习优化的一体化方案。它的价值在于把训练过程中的 token-level 对齐和执行稳定性从工程修补提升为可优化对象。

如果你在做代码 agent 的持续学习，这篇论文可以直接借鉴其“原生 harness + 训练闭环”思路，尤其是对 rollout 与训练分布不一致问题的处理方式。

## 论文标题
LEGO-RL: Harness-Native Reinforcement Learning for Coding Agents

## 作者/机构
- 作者：Yiming Du, Yuxin Jiang, Tao Yuan, Jianbo Dai, Shaowei Wang, Jierun Chen, Chaofan Tao, Xianzhi Yu, Lifeng Shang, Kam-Fai Wong, Xiaohui Li, Haoli Bai
- 机构：arXiv 页面未直接展示机构信息，按作者名单记录

## 发布日期/版本日期
- 版本发布日期：2026-08-18（v1，`2026-08-18T05:34:35Z`，对应 Asia/Shanghai 2026-08-18）

## 主题标签
#AI-Agents #ReinforcementLearning #LLM #CodeAgent #SWEbench

## 论文链接
- https://arxiv.org/abs/2608.17393v1

## PDF 链接
- https://arxiv.org/pdf/2608.17393v1

## 项目/代码/数据链接
- 项目页：https://lego-rl.pages.dev
- 代码：网页未直接给出仓库链接，待公开后补充
- 数据：训练与评测基准为公开 SWE-bench Verified（文内指标引用）

## 核心问题
现有 coding agent 强化学习训练常被 harness 行为差异拖累：模型在训练时看到的是代理化抽样，部署时却落到复杂执行流程，导致信号错配、奖励污染和 reward hacking。论文核心问题是如何在不改动 harness 内部控制流的情况下，稳定进行策略梯度训练。

## 方法概要
- 提出三层设计：
  1) In-process LLM proxying：在 harness 原生环境内捕获 token 级生成流，支持训练侧概率重计算。
  2) 可扩展 sandbox orchestration：加入 image caching 与分阶段防御，降低环境崩溃与奖励投机。
  3) 可观测插件与 Live UI：把验证、监控与轨迹诊断并入训练过程。
- 采用 GSPO 在三类原生 coding harness 上训练 Qwen3.5-35B-A3B。

## 主要贡献
1. 将 coding agent 训练“与其执行平台解耦”改为“与 harness 原生流程同构”，减少训练-推理偏移。
2. 提供了可复用的日志与策略评估接口设计，便于跨平台调试。
3. 在 SWE-bench Verified 上显著提升多个基线平台性能，验证框架级收益，而非单模型技巧收益。

## 关键实验或结果
- OpenHands SDK：64.0% 9 70.4%
- Claude Code：62.4% 9 68.2%
- OpenCode：57.2% 9 66.6%
- 训练与 rollout 的 probability 相关性维持在 0.99 以上（文内声称），表明优化行为与执行轨迹一致性较高。

## 适合关注的原因
研究聚焦了生产级 coding agent 最难的问题：不是更强模型，而是更可信的训练闭环。对需要稳定迭代 agent 的研发团队，这类方法可直接减少“训练好了但线上退化”的典型痛点。

## 局限性或待验证点
- 论文目前主要在代码 agent 任务族验证，跨任务泛化尚待更广泛验证。
- 对奖励定义仍依赖具体评测基准与 harness 设定，指标可迁移性需要注意。
- 公开的实现细节（如默认超参、失败恢复策略边界）在摘要中不完整。

## 对后续研究/应用的启发
- 适合将“环境稳定性优化”与“策略学习”共同建模，避免单独优化模型而忽视执行系统。
- 可探索同构思想到数据分析、运维自动化等其他 agent 场景。
- Live UI 与监控链路可为 agent 生命周期治理（失败复盘、合规审计）提供模板。

## 适合 Obsidian 快速浏览的中文总结
一句话：LEGO-RL 把 coding agent 的训练目标从“模型输出更好”扩展为“训练轨迹与 harness 行为一致”，对真实工程可用性提升更直接。

## 标准化研究框架
**Research question：** 本文不是传统社会科学假设检验，而是工程科学问题：在原生 harness 上如何建立可复现、稳定且可解释的 RL 训练闭环。

**Literature：** 相关工作多处理 agent 基准或奖励设计，较少系统化处理 harness 与训练的接口一致性；本工作强调“原生环境约束下的 RL 可行性”。

**Theory：** 在本文中可等价为控制变量框架：通过 token 级概率重建与沙箱防护，减少训练损失与执行回报之间的偏差。

**Hypotheses：** 如果 token 记录与奖励生成在训练和部署都共享可追踪路径，则训练收益可更稳定地转化为线上性能，并降低 reward hacking。

**Method：** 对三类 harness 做统一实验设置：同基座模型、同任务集合下比较原始训练与 LEGO-RL 的 GSPO 路径，并记录成功率、验证通过率及行为相关性。

**Data and Analysis：** 数据/任务以 SWE-bench Verified 等公开 benchmark 为主，分析指标为成功率提升、跨平台差异、轨迹相关性与策略稳定性。

**Findings：** 三平台均出现显著提升，并观察到较高的 rollout-training 概率相关性，说明训练过程更贴近实际推理环境。

**Conclusion：** 如果你要推进代码 agent 的持续学习，首要优化对象往往不是模型参数本身，而是训练闭环的一致性与可观测性。
