# SWE-Prime: Fewer Trajectories, Better Performance

> Spotlight（2句）：这篇工作把 SWE 问题中“成功轨迹都高质量吗”这件事直接提出来反驳，并提出两阶段筛选框架。结论很直接：删掉噪声并不一定损失性能，反而能明显变强，尤其适合 agent coding 的高成本数据管线。

## 基本信息
- 论文标题：SWE-Prime: Fewer Trajectories, Better Performance
- 作者：Dewu Zheng, Ruizhe Ye, Yanlin Wang, Yang Ye, Hongyu Zhang, Ensheng Shi, Xilin Liu, Yuchi Ma, Jianxing Yu, Zibin Zheng（机构未在 arXiv 摘要页完整披露）
- 发布日期（版本）：2026-08-27（v1）
- 主题标签：`#Agent` `#SWE-Bench` `#Software Engineering` `#Dataset Filtering` `#SFT` `#LLM` 
- 论文链接：[https://arxiv.org/abs/2608.27449](https://arxiv.org/abs/2608.27449)
- PDF 链接：[https://arxiv.org/pdf/2608.27449v1.pdf](https://arxiv.org/pdf/2608.27449v1.pdf)
- 项目/代码/数据链接：
  - 代码：未在摘要页公开
  - 数据：未在摘要页公开
  - 补充：论文中引用 SWE-Bench Pro / Verified 作为实验基准

## 核心问题
真实软件修复代理常把“已解决”的轨迹直接用于监督，但这些轨迹可能包含低效、冗余甚至高风险动作。问题是：能否从成功轨迹中提取更高质量片段，从而以更少数据获得更好 agent 能力？

## 方法概要
1. 在轨迹层面做第一阶段筛选：考量过程质量、结果质量、代表性。
2. 在段落/片段层面做第二阶段筛选：按贡献、可学习性与风险水平评估。
3. 训练时保留全部 segment 的上下文顺序，但仅在筛选片段上计算 loss，减少噪声监督。
4. 在不同规模子集上做对比实验，验证“更少高质量轨迹”是否更有效。

## 主要贡献
- 提出两粒度轨迹清洗框架（trajectory + segment）。
- 反驳“更多成功样本一定更好”的朴素假设。
- 给 agentic coding 提供一条可解释、可复用的数据治理路径。

## 关键实验或结果
- 在 SWE-Bench Pro 上，使用 10% 轨迹子集可较全量已解决轨迹更优，提升约 12.2%。
- 在 SWE-Bench Verified 上，10% 子集相对全量的相对提升更明显，达到约 24.2%。

## 适合关注的原因
- 将数据质量管理从“规模优先”转为“有控制的高质量样本选择”。
- 对 agent 训练/蒸馏阶段具有直接工程价值，尤其在 compute 限制下能显著省钱。
- 方法结构清晰，易于与已有 SWE pipeline 结合。

## 局限性或待验证点
- 论文未披露更多下游任务泛化结果，领域迁移未知。
- 评估聚焦 SWE 路线，未覆盖其他 agent 交互（如 web-agent、具身任务）。
- 未公开完整实现细节与开源基线，复现工作量仍需再次确认。

## 对后续研究/应用的启发
- 可拓展到通用智能体轨迹中，引入安全风险评估作为训练损失权重。
- 可与 reward model 联合形成“自动轨迹清洗 + 自适应再标注”管线。
- 数据中心化场景下，可结合时间衰减和任务难度加权实现动态筛选。

## 适合 Obsidian 快速浏览的中文总结
一句话：少量高质量轨迹比大量“成功但低质”轨迹更能训练出强 agent。

## 标准化研究框架
- **Research question：** 在 SWE Agent 训练中，如何通过数据选择显式提升有效监督信号并减少无效行为学习？
- **Literature：** 相比以往以大规模成功轨迹为主的 SFT 流派，本文提出“质量优先”的多粒度过滤，与数据效率与 curriculum 学习思想形成互补。
- **Theory：** 低质量行为会在监督中放大误导性策略；对关键 segment 加权可提升策略收敛方向性。
- **Hypotheses：** 1）轨迹筛选可提升稳定性；2）段级筛选比纯轨迹筛选更有效；3）保留上下文但缩减 loss 覆盖可抑制噪声。
- **Method：** 两阶段筛选（trajectory-level 与 segment-level）+ 局部 loss masking + SWE-Bench Pro/Verified 对照训练与测试。
- **Data and Analysis：** 以公开 SWE 数据集为评估，比较全量轨迹与按比例筛选轨迹在终端性能上的差异，并报告相对增益。
- **Findings：** 10% 轨迹子集即可超过全量样本；关键是“筛选后训练”带来更大有效信息密度。
- **Conclusion：** 数据治理在 agentic coding 中与模型规模同等关键，但方法是否跨任务泛化仍待验证。
