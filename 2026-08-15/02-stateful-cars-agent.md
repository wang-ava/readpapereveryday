# Stateful CARS: Exact Cross-History Reuse for Policy-Constrained LLM Agents

> Spotlight：把状态相关 agent 的动作采样定义为严格条件采样问题，在可复用历史的前提下仍保证分布准确性，直接回应“Agent 工程里可验证性不足”的痛点。

- 论文标题：Stateful CARS: Exact Cross-History Reuse for Policy-Constrained LLM Agents
- 作者（机构）：Ibne Farabi Shihab, Md Najmus Swaqeeb, Abu Sa-Adat Mohamed Moon-Im Al Ahsan（arXiv 页面未给出机构）
- 发布日期（版本日期）：2026-08-08（arXiv v1）
- 主题标签：`#Agent` `#LLM` `#Sampling` `#ToolUse` `#Safety`
- 论文链接：[https://arxiv.org/abs/2608.08282](https://arxiv.org/abs/2608.08282)
- PDF 链接：[https://arxiv.org/pdf/2608.08282v1](https://arxiv.org/pdf/2608.08282v1)
- 项目/代码/数据链接（如可得）：未公开（arXiv 页面未给出）
- 核心问题：agent 在历史相关约束下是否能复用跨轨迹信息而仍从“有效动作条件分布”中采样？
- 方法概要：
  - 在每次尝试中冻结状态-续接 schema（sound schema）缓存。
  - 删除匹配抽象状态下含无效后续的轨迹候选，进行精简搜索。
  - 使用 residual Doob transform 进行采样并给出可检验的正确性条件。
- 主要贡献：
  - 提出 Stateful CARS 的 exact 采样形式主义。
  - 给出 schema soundness、adaptive exactness、i.i.d. 输出、几乎必然终止等理论性质。
  - 明确提出历史状态路径数可指数增长，且不做泛化的多项式扩展承诺。
- 关键实验或结果：
  - 可枚举工作流中，满足有效条件分布误差达到约 $10^{-16}$（valid probability $6\times10^{-8}$）。
  - 对比 state-aware local decoding 时可偏差约 $0.97$，差距显著。
  - 采样步数比值 root/Stateful 为 $0.942$（95% CI: $[0.934, 0.951]$），Qwen 对照约为 $0.99$（$[0.90,1.08]$）。
  - Cross-history transfer 在内部对照提升约 $1.27\times$。
- 适合关注的原因：在安全、合规、流程约束强的工具调用场景中，正确性比单纯速度更关键，本文提供了更可审计的生成机制。
- 局限性或待验证点：
  - 现有理论未证明高复杂度现实任务下可线性可扩展。
  - 系统效率优势在某些基线比较中不突出。
- 对后续研究/应用的启发：
  - 可用于流程型 agent、金融和企业自动化里的策略约束采样。
  - 后续可研究近似状态归并以平衡可验证性与时延。
- 适合 Obsidian 快速浏览的中文总结：Stateful CARS 强调“先正确，再快”，把 LLM Agent 采样从启发式修修补补推到理论可核验。

## 标准化研究框架

**Research question：** 在状态依赖策略约束下，是否可在保留跨历史复用的同时，仍保证从目标有效条件分布采样？

**Literature：** 多数 Agent 采样方法难给出严格偏差边界；该文将问题形式化为带状态约束的条件随机过程采样问题。

**Theory：** 通过定义 state-continuation schema 与可验证 bisimulation，建立可复用状态空间的精确采样约束。

**Hypotheses：**
- H1：复用无效性证书可减少重复无效采样。
- H2：在可验证条件下可得到准确分布采样。
- H3：状态空间增长会限制方法在超大规模场景的即席部署。

**Method：** 使用可复用 schema 的 stateful 验证机制，在采样前做轨迹剔除并用 residual Doob 转换重参数化采样分布，再作与 baseline 的误差对比。

**Data and Analysis：** 以可枚举 workflow 为主，比较采样误差、步数效率与迁移收益；并记录跨历史复用比值与近似一致性。

**Findings：** 方法在目标分布逼近上显著优于比较 baseline，但系统规模扩展性与通用速度优势尚未完全成立。

**Conclusion：** 本文适合作为高可靠性 Agent 的基线框架：先确保采样正确，再通过后续工程技巧优化资源消耗。
