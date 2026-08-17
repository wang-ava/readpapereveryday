# QuoteBench: How Matched Scores Can Hide Command-Path Failures

Spotlight：论文用 56 个任务场景展示了“看上去答案匹配”与“实际命令执行正确”之间的巨大差距。它提醒 LLM Agent 评测必须显式建模 command path，不然会高估系统能力。

## 论文信息
- 论文标题：QuoteBench: How Matched Scores Can Hide Command-Path Failures
- 作者（机构）：Shangao Li；Yao Zhang；Volker Tresp；Yuanyuan Yang（机构未在该 arXiv 摘要页完整公开）
- 发布日期：2026-08-13（v1）
- 主题标签：`#LLM` `#Agent` `#CommandExecution` `#Evaluation`
- 论文链接：[https://arxiv.org/abs/2608.13547v1](https://arxiv.org/abs/2608.13547v1)
- PDF 链接：[https://arxiv.org/pdf/2608.13547v1](https://arxiv.org/pdf/2608.13547v1)
- 项目/代码/数据链接：项目页 <https://quotebench.lsamc.website/>
- 核心问题：LLM coding agent 的“matched score”并不能分辨模型生成命令错误、执行器边界和环境差异导致的失败。
- 方法概要：构造 56 个 incident 衍生任务，建立 14 个任务簇和 1 个额外 parser 路径，对同一模型回复在不同执行边界下重放，比较 matched 成功率与最终状态一致性。
- 主要贡献：
  - 将工具调用评测从“文本匹配”提升到“执行路径与最终状态”双目标。
  - 给出可复现的 benchmark 与协议细节，强调 parser、执行策略、验证器共同影响最终结果。
  - 在 8 种配置下展示结果重排现象，证明模型边界适配才是关键瓶颈。
- 关键实验或结果：
  - Replay 到带额外 parser 时，匹配成功率可下降 55.4 到 73.2 个百分点。
  - 公布 boundary 信息后可恢复 30.4 到 60.7 个百分点（不同配置差异显著）。
  - 部分配置间出现 26 个模型对比中的明显排序反转，说明“高分并不稳健”。
- 适合关注的原因：对研发团队直接有落地价值：部署 coding agent 前，必须区分“模型聪明度”与“执行一致性”。对企业内网自动化、运维辅助、数据流水线 agent 都有直接参考意义。
- 局限性或待验证点：实验聚焦 shell-style 命令环境，未覆盖多语言、异构 API tool 套件、数据库执行器等更复杂执行面；指标迁移和安全性成本仍待补强。
- 对后续研究/应用的启发：可在产品链路中加入“执行边界公开 + final-state validator + 多配置消融”三件套，让 benchmark 结果对上线行为更可解释。
- Obsidian 快速浏览一句总结：**QuoteBench 的核心是：命令链路可复现性，才是判定 coding agent 真正可靠性的底线。**

## 标准化研究框架
**Research question：** 在 LLM coding agent 中，如何消除“输出文本匹配正确但执行路径失效”的假阳性，建立可靠评测指标？

**Literature：** 传统 coding benchmark 多偏重自然语言输出匹配或单轮正确率；本工作延伸了这类 benchmark，不采用复杂模型假设，而是改从执行系统边界建模错误来源。

**Theory：** 真实任务成功事件是“生成 + 传输 + 解析 + 执行 + 最终状态”联合函数；只评估任一子事件都会导致高估能力，必须把配置变量显式纳入评价空间。

**Hypotheses：**  
- H1：加入命令路径与 parser stress 可显著放大模型在 matched score 之外的失真。  
- H2：公开执行配置（transport、validator）会改变量化结果排序。  
- H3：基于 final-state 的验证比 token-level 匹配具有更高的现实有效性。

**Method：** 设计 56 个一-shot 任务；构建“附加 parser + 报告边界公开/保密”的实验矩阵；复放同一模型回复并统计 matched 成功率、恢复幅度和模型排序变化。

**Data and Analysis：** 统计 8 配置下跨 26 个模型对的差异；对比回复匹配分与 final-state outcome 的一致性；分析 disclosure 信息带来的性能回升。

**Findings：** matched 分并非内在属性；执行链路差异可导致大幅性能波动，配置敏感性是决定真实表现的关键变量，未披露配置会系统性高估能力。

**Conclusion：** 对于代码与工具调用 LLM，评测必须标准化执行边界与验证机制；否则 benchmark 不能支撑生产级决策。
