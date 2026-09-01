# Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses

> Spotlight（2 句）：Recuris 把 long-horizon agent 的“记忆管理”升级为可递归演化的控制变量，而不是只依赖静态上下文。它将失败定位到具体 memory 组件并通过闭环更新技能库，在延展任务上显著减少长链错误。

## 基本信息
- 论文标题：Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses
- 作者：赵晨 Yu, Yingcheng Wu, Zhenfei Yin, Kaiyuan Chen, Zhe Zhao, Mengdi Wang, Shuicheng Yan, Ling Yang（机构未在 arXiv 页面完整披露）
- 发布日期（版本）：2026-08-25（v1）
- 主题标签：`#Agent` `#LongHorizon` `#Memory` `#ToolUse` `#RLA`
- 论文链接：[https://arxiv.org/abs/2608.24876v1](https://arxiv.org/abs/2608.24876v1)
- PDF 链接：[https://arxiv.org/pdf/2608.24876v1.pdf](https://arxiv.org/pdf/2608.24876v1.pdf)
- 项目/代码/数据链接：
  - Code：[https://github.com/Gen-Verse/Recuris](https://github.com/Gen-Verse/Recuris)
  - 数据：论文中未说明公开 benchmark 脚本细节

## 核心问题
长任务中，agent 的任务状态会随交互轨迹膨胀，固定上下文与静态技能调用常常导致错误放大。论文问的是：能否通过可递归更新的工作记忆机制，让 agent 在执行中持续自我修正并提高长程任务成功率？

## 方法概要
1. 引入 Working Memory 跟踪任务进度，用于驱动 Skill Memory 的检索。
2. Meta-Agent 在每轮执行后解析失败证据，将其映射到 memory 组件。
3. 在验证门控下，对 Skill Memory 发起局部更新，实现 bounded 的 recursive memory evolution loop。
4. 将“证据定位 + 记忆更新 + 重新执行”嵌入统一 harness。

## 主要贡献
- 提出 Recuris，首次将递归记忆演化机制系统化用于 agent long-horizon harness。
- 给出可解释的 failure localization：失败不是黑盒，而是定位到 memory slot 与 skill 组合。
- 在四个 long-horizon benchmark 和 10 个模型上实现更稳健的任务推进与可扩展的性能提升。

## 关键实验或结果
- 在 4 个长程基准和 10 个模型上完成 37 个模型-任务对，35 对明显受益。
- 在 tau-bench 中，GPT-5.6 系列提升 +17.8 点，Opus 5 提升 +15.6 点，SkillFlow 上 Qwen3.6-27B / 35B 分别提升 +16.6 与 +13.5。
- 长任务段收益更明显：最长任务上平均增益 +32.2 点。
- 常见长程失败项下降高达 80%。

## 适合关注的原因
- 直接回答了 agent 落地里最痛的稳定性问题：复杂流程中错误传播。
- 与现有多模型路由方案兼容度高，可作为 harness 层增强模块。
- 在“可解释 + 可调优”上给 agent 部署提供了新抓手。

## 局限性或待验证点
- 没有给出非常细的算力消耗与延迟开销基准，真实部署成本仍需估算。
- 论文侧重 benchmark，真实世界生产数据分布下是否同样稳定尚待验证。
- 递归更新策略可能引入策略迭代振荡，长时间运行安全性需额外监控。

## 后续研究/应用启发
- 可在 RAG 或工具调用 Agent 中复用“failure-localization + memory rewrite”范式。
- 可与 verification module 联合，做更安全的 bounded-self-update。
- 适合作为自动化工作流（客服、运维、代码开发）中的 agent supervisor。

## 适合 Obsidian 快速浏览的中文总结
一句话：Recuris 用递归记忆演化把长链错误变成可更新的结构性证据，显著提升了长程 agent 的成功率。

## 标准化研究框架
- **Research question：** 长程任务中能否通过经验工作记忆的递归更新，系统提高 agent harness 的鲁棒性和任务成功率？
- **Literature：** 相比静态 memory/context 与纯监督微调，本文把 memory 更新与执行闭环绑定，强调在线可解释失败修正。
- **Theory：** 假设任务失败与 skill 执行之间存在可结构化对应关系，可在局部记忆上进行验证门控更新以减少误差扩散。
- **Hypotheses：** ①递归更新可提升长任务成功率；②对越长 horizon 的任务增益越高；③失败检索可减少重复错误循环。
- **Method：** 构建 Recuris 架构并在长程基准上与多模型 baseline 逐项对比。
- **Data and Analysis：** 使用 4 个 benchmark + 10 个模型，采用成功率、失败类型归因与收益幅度作为核心指标。
- **Findings：** 多项任务显著受益，文中报告的 success 和失败下降结果支持递归记忆假设。
- **Conclusion：** 论文在工程可部署性与方法解释性之间取得平衡，但真实闭环环境中的安全边界仍需补充。
