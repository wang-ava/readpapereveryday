# OmegaUse-OfficeVal: Benchmarking LLM Agents on Long-Horizon Office-Suite Tasks with Economic Grounding

Spotlight：这是把“LLM Agent 能否完成长期任务”从主观印象改造为“成本—产出—质量”的量化题目。它把任务时长、人力成本与任务价格引入评测闭环，直接回答企业应用中的真实价值问题。

- 论文标题：OmegaUse-OfficeVal: Benchmarking LLM Agents on Long-Horizon Office-Suite Tasks with Economic Grounding
- 作者：Jingbo Zhou, Yusai Zhao, Qi Bao, Jingjia Cao, Zhenghai Chen, Chang Gao, Kaiqi Guo, Muxin Guo, Mingxuan Li, Xinjiang Lu, Yanru Ma, Yixiong Xiao, Zenghui Zhang, Le Zhang, Hua Wu
- 机构（如可得）：未在 arXiv 页面直接给出机构字段
- 发布日期或版本日期：2026-07-29T17:33:47Z（UTC），折合 Asia/Shanghai 为 2026-07-30 01:33:47
- 主题标签：#LLM #Agent #OfficeAutomation #Evaluation #AgentBenchmark
- 论文链接：[https://arxiv.org/abs/2607.27155v1](https://arxiv.org/abs/2607.27155v1)
- PDF 链接：[https://arxiv.org/pdf/2607.27155v1](https://arxiv.org/pdf/2607.27155v1)
- 项目/代码/数据链接（如可得）：[https://omegause-officeval.github.io](https://omegause-officeval.github.io)

## 核心问题
- 常见 Agent benchmark 看重任务是否完成，但企业更关心单位时间/金钱下的收益与可复用性。
- Office 套件任务时长长、步骤多，很多 benchmark 无法反映真实生产效率。
- 缺少能统一比较“模型成本”和“人工替代成本”的评测设计。

## 方法概要
- 构建 OmegaUse-OfficeVal：100 个来源于企业实践的 office-suite 任务。
- 每项任务标注两类经济信号：
  - 人类完成该任务的劳动时长
  - 任务价格代理值（price proxy）
- 采用代码化验证器，对输出结果进行细粒度打分。
- 同步报告模型与人类基线在质量、速度与成本比上的差距。

## 主要贡献
- 将长时序 office 任务作为独立 benchmark 领域系统化建模。
- 引入经济指标（time/cost）实现更贴近落地需求的价值评估。
- 开放代码与数据，便于可复现和横向对比。

## 关键实验或结果
- 任务平均人工完成成本对应约 2.32 小时人力。
- 各 LLM agent 在成本上远低于人工（更快更便宜），但输出质量仍明显落后于人类基线。
- 通过价值加权机制，能够把“只看正确率”替换为“正确率-成本”双目标评估。

## 适合关注的原因
- 如果你在评估 AI 助理在真实业务文档和协同流程中的投入产出，这个 benchmark 提供了可直接复用的范式。
- 对自动化效率治理（预算控制 + 质量门控）特别有价值。

## 局限性或待验证点
- 任务仍偏 office 场景，跨行业泛化（法律、研发、客服）需扩展验证。
- 目前指标是否能覆盖非量化质量（创造性、语气、沟通效果）仍需讨论。
- 不同语言和区域的办公规范会影响评分器一致性，需进一步鲁棒性实验。

## 对后续研究/应用的启发
- 评测框架可迁移到客服、客服工单、销售支持等长链任务。
- 可与自动路由系统结合做模型选型策略（小模型处理低价值任务，大模型处理关键任务）。
- 有助于形成“AI 代理 ROI”指标体系，而非单指标 benchmark 竞赛思维。

## 一句 Obsidian 快速浏览总结
一句话：OmegaUse-OfficeVal 把 LLM Agent 的真实价值问题从“会不会做”转换为“以多大代价做到什么程度”。

## 标准化研究框架
- **Research question：** 对长时序 office 任务，LLM agent 在质量、时间与成本维度上的综合价值如何定位？
- **Literature：** 继承了 LLM-Agent benchmark 的趋势，加入经济学式评估以对齐企业落地场景。
- **Theory：** 任务价值应以效用函数（质量与人力替代成本）而非单任务正确率刻画，才能支持投资决策。
- **Hypotheses：** 同等任务难度下，即使质量不足，agent 的成本优势仍能显著带来实用价值；但达到人类质量仍需策略增强。
- **Method：** 建立 100 项任务集+双经济标签+代码审计器，比较多个 agent 与人类基线。
- **Data and Analysis：** 分析维度包括任务完成质量、时间消耗、推理成本与价值加权分数。
- **Findings：** 现有 agent 显著更廉价且更快，但在 deliverable 质量上仍未追平人工。
- **Conclusion：** 长时序办公任务评测应加入经济约束，未来可据此设计“任务价值最优”的模型路由策略。
