---
spotlight: "该文提出连续化、可排序的脓毒症严重度评分，不再按小时逐点固定打分，而是学习可迁移的治疗期轨迹信号。"
---

# Learning a Continuous Sepsis Severity Score Without Hour-by-Hour Supervision: A Two-Site Retrospective Study

## 基本信息
- **论文标题**：Learning a Continuous Sepsis Severity Score Without Hour-by-Hour Supervision: A Two-Site Retrospective Study
- **作者**：Kevin Zhu, Ryan Zhang, Baraa Abed, Tilendra Choudhary, Malvern Madondo, Mehak Arora, Yixuan Yang, Alasdair Gent, Aditya Nagori, Omer T. Inan, Krista L. Haines, Patrick Georgoff, Suresh M. Agarwal, Vijay Krishnamoorthy, Tetsu Ohnuma, Mihai V. Podgoreanu, Michael R. Pinsky, Gilles Clermont, Craig M. Coopersmith, Craig S. Jabaley, Rishikesan Kamaleswaran
- **机构**：arXiv 页面未公开机构，可在正文和补充材料补齐
- **发布日期 / 版本日期**：2026-08-27（v1）
- **主题标签**：`AI4S` `Sepsis` `Healthcare AI` `Clinical Risk Score`
- **论文链接**：https://arxiv.org/abs/2608.27421
- **PDF 链接**：https://arxiv.org/pdf/2608.27421
- **项目/代码/数据链接**：未在 arXiv 页面给出公开代码或数据仓库链接

## 核心问题
现有脓毒症评分多为固定变量、固定权重、离散分层，难以覆盖当下 ICU 病历分布变化。能否构建无需逐小时监督的连续病情严重度建模方法，并在跨机构上有稳定泛化？

## 方法概要
- 使用两家医院系统的回顾性队列（Massachusetts、Georgie）进行训练与验证。
- 以 72 小时治疗窗口中的 43 项常规临床指标构建学习目标。
- 采用“以死亡率为治疗层级排序信号”替代逐时静态标签，强调时序贡献的非均匀分配。
- 在患者级和队列级分别评估相关性与跨机构一致性。

## 主要贡献
1. 将传统基于固定变量阈值的分级改为可学习、连续、时序敏感的严重度评分。
2. 在两站点大样本队列（29,116 与 7,691 例）验证可移植性。
- 以 bootstrap 置信区间支撑不确定性报告，并对比多项基线指标。

## 关键实验或结果
- 非存活组在 0-10 连续评分上持续高于存活组（0.27~1.64 区间）
- 指标在 SOFA-2 等分层内仍保持区分能力；与乳酸、MAP、肌酐变化相关性符合临床预期。
- 跨站点模型相关性为同站点相关性的 70%~77%，显示可迁移但仍有站点差异。
- 文中给出患者级别与队列级别验证（如 Spearman 相关、bootstrap 区间）支持决策支持潜力。

## 适合关注的原因
- 对 ICU 风险预警系统具有直接落地价值：可支持更动态、连续的患者状态监测。
- 跨站点验证是医疗 AI 很关键的门槛，本研究给出较规范的外部验证思路。

## 局限性或待验证点
- 现阶段仍是回顾性研究，前瞻性临床验证不足。
- 未公布公开代码/数据流程时，外部可复现性需依赖机构协议。
- 不同医院的治疗路径异质性会显著影响“治疗层级排序”设定，需更细粒度分层分析。

## 对后续研究/应用的启发
- 可扩展到 ICU 其他疾病（ARDS、败血症并发症）做“连续风险分”替代固定评分。
- 将模型输出与干预建议结合后，可形成更细粒度早期预警与转运策略。

## 一句话中文速览总结
该文用连续化脓毒症严重度重建了传统离散评分范式，展示了跨机构、跨时序的可迁移建模方向。

## 标准化研究框架
- **Research question：** 是否可在无逐小时标签监督下，从常规 ICU 变量中学习连续且可跨机构泛化的脓毒症严重度。
- **Theory：** 用死亡率作为治疗层级排序目标，可在时序中分配不同时间点权重，更符合临床决策需求。
- **Hypotheses：** 连续评分模型能比静态离散分层更好地区分患者结局并具备跨机构一致性。
- **Method：** 回顾性两站点数据建模，72 小时窗口提取 43 变量，基于排名损失与 Bootstrap 置信区间评估。
- **Data and Analysis：** 队列规模 29,116 与 7,691；比较生存/非生存组差异、Spearman 相关与跨站点相关一致性。
- **Findings：** 报告显示该评分在多个指标下与临床结局相关，跨站点相关性达到 70%~77%。
- **Conclusion：** 研究支持连续分数在 AI4S 的临床价值，但仍需前瞻验证与实现层面复现。
