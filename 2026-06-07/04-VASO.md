VASO 这类工作很值得工程和研究两边都关注，因为它没有假设“把模型训得更大就能更安全”，而是转向一个更可落地的问题：如何把 agent skill 变成可验证、可修正、可复用的外部结构。对于真实机器人部署，这是非常务实的路线。

# Automated Skill Optimization via Formal Verification for Embodied Agents

## 基本信息

- 论文标题：Automated Skill Optimization via Formal Verification for Embodied Agents
- 作者/机构：Yunhao Yang、Neel P. Bhatt、Kevin Wang、Zhangyang Wang、Ufuk Topcu；OpenReview 页面未完整列出机构
- 发布日期或版本日期：2026-05-27，最后修改 2026-06-01
- 主题标签：#EmbodiedAI #FormalVerification #Robotics #SkillAbstraction #Safety
- 论文链接：https://openreview.net/forum?id=TxGsSn4nrZ
- PDF 链接：https://openreview.net/pdf?id=TxGsSn4nrZ
- 项目链接：未见独立项目页
- 代码链接：未公开
- 数据链接：未公开

## 核心问题

foundation model 可以从自然语言生成 robot skills，但这些 skill 往往只是“看起来合理”，没有 formal guarantee。只要局部技能违反安全约束或任务时序约束，系统级行为就不可靠。本文要解决的是：能否在不更新底层模型权重的前提下，自动扩展并优化 skill library，同时维持全局安全规格？

## 方法概要

作者形式化提出 verified skill synthesis 问题。每个 skill 同时包含 formal local rule 和 natural language contract，两者都由 foundation model 产生。随后引入 VASO（Verified/Verification-Aware Skill Optimization）闭环：先用 model checking 验证局部规则是否满足全局 temporal logic specification，再利用验证反馈去修改 skill contract，提高 planner 在全局约束下的可用性与合规性。

## 主要贡献

- 把自然语言 skill abstraction 与 formal verification 连接起来。
- 提出 verified skill synthesis，强调扩展 skill library 时也要保持全局安全约束。
- 使用 contract 作为 planner-facing 接口，使 skill 可被优化而不必改动底层模型参数。
- 在真实机器人平台上展示 closed-loop verification-driven optimization 的可行性。

## 关键实验或结果

- OpenReview 摘要报告：在 Jackal ClearPath ground robot 和 PX4 quadcopter 上，优化后的 skills 可达到 97.2% 的 formal specification compliance。
- 每个 skill 的优化样本数少于 100，优化时间低于 20 分钟。
- 论文强调这一收益是在不更新模型权重的前提下得到的，说明“外部可验证 skill 层”本身就是有效杠杆。

## 适合关注的原因

这篇工作特别适合关注 agent runtime、robot planning、tool abstraction、safety-critical deployment 的读者。它给出的启发是：与其把所有可靠性问题都压给 end-to-end model，不如在 skill layer 引入一个可以被 formal tools 检查和修正的中间层。

## 局限性或待验证点

- 当前实验规模和任务复杂度仍有限，距离开放世界机器人部署还有差距。
- 能被 temporal logic 规格化的任务更适合该框架，开放式、高语义模糊任务的适配性仍需观察。
- 未公开代码与更完整的 ablation，短期内复现实验存在门槛。
- 若底层 perception 本身不稳，再强的 formal skill contract 也无法完全消除感知误差带来的风险。

## 对后续研究/应用的启发

后续可以把 formal verification 与 memory、planner、runtime monitor、uncertainty estimation 结合起来，形成更完整的 embodied safety stack。应用侧则很直接：对高风险机器人和工业 agent，与其盲目追求端到端自治，不如先构建一个可验证 skill library 作为中间安全层。

## Obsidian 快速浏览总结

让机器人 agent 更可靠，未必先靠重训大模型，更可能先靠把 skill 层做成可验证的软件对象。

## 标准化研究框架

**Research question：** 本文研究的问题是：在 foundation model 生成机器人技能的前提下，如何通过形式化验证与闭环优化，提升技能库对全局任务与安全规格的合规性。

**Literature：** 相关文献涉及 embodied planning、skill abstraction、formal methods、model checking、robot safety 与 foundation-model-based policy generation。本文的创新点在于把“自然语言技能合同”纳入 formal optimization 流程。

**Theory：** 本文并非社会科学假设检验论文；其等价理论核心是：如果把 skill 表述成可验证的局部规则与自然语言 contract，并持续接受 model-checking feedback，那么系统级安全与任务满足率可以在不改权重的情况下提升。

**Hypotheses：** 可等价表述为：闭环 verification-driven skill optimization 能显著提高 formal specification compliance；这种提升不依赖底层模型再训练；优化后的 contract 会改善 planner 的全局行为质量。

**Method：** 方法包括 skill 生成、formal local rule 与 natural language contract 配对、global temporal logic verification，以及基于验证反馈的迭代 contract 优化，统称为 VASO 流程。

**Data and Analysis：** 数据与分析主要来自机器人任务环境及其形式化规格。分析指标是 specification compliance、优化样本数、优化时间与不同平台上的执行效果。

**Findings：** 主要发现是：在 Jackal 与 PX4 平台上，VASO 能以较低样本和时间开销，把 plans guided by optimized skills 的规格合规率提升到 97.2%。

**Conclusion：** 结论是形式化验证可以成为 embodied agent skill layer 的关键增强器；相比只依赖更大模型，构建可验证、可迭代修正的技能接口是更稳健的工程方向。
