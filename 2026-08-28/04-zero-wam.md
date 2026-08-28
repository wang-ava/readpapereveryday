# Zero-WAM: In-Context World-Action Modeling from Human Videos for Open-Ended Task Generalization

本文用“人类示例视频”作为任务条件，推动机器人从未见过的任务做到 zero-shot 长尾执行，兼顾数据构造、任务泛化和防止短视捷径的训练机制。

## 论文标题
Zero-WAM: In-Context World-Action Modeling from Human Videos for Open-Ended Task Generalization

## 作者/机构
- 作者：Jiaming Zhou, Qihang Zhang, Gangwei Xu, Cunxin Fan, Yujie Zhao, Ruilin Wang, Yiming Luo, Shuai Yang, Xing Zhu, Yujun Shen, Junwei Liang, Yinghao Xu
- 机构：arXiv 摘要页未直接在结构化字段列出机构

## 发布日期/版本日期
- 提交日期：2026-08-26（v1）
- 版本日期：2026-08-26T17:59:34Z

## 主题标签
#EmbodiedIntelligence #VLA #Generalization #RobotLearning #VisionAction

## 论文链接
- https://arxiv.org/abs/2608.26103v1

## PDF 链接
- https://arxiv.org/pdf/2608.26103v1

## 项目/代码/数据链接（如可得）
- 项目页：https://robbyant-research.github.io/Zero-WAM/
- 数据：HumanGen（文章描述为 74.2K 人体-机器人 ICL 对，覆盖 8.6K 任务；建议以仓库确认下载方式）
- 代码：摘要中未给出，可在项目页确认

## 核心问题
大多数机器人策略在已见任务下表现较好，但遇到未出现任务即失效。关键问题是如何让策略从“任务语义说明”中快速泛化，而非仅依赖固定动作分布记忆。

## 方法概要
- 使用人类视频作为任务上下文（in-context）提示，相较纯文本提供更丰富的目标动态线索。
- 提出数据构造流水线，把采样到的机器人轨迹与语义匹配的人类示范视频配对，形成大规模 HumanGen。
- 引入 in-context future chunk prediction（IFP）目标，惩罚模型只靠已见任务 shortcut，迫使模型解码任务信息。

## 主要贡献
1. 将 ICL 思路从 LLM 任务迁移到机器人动作建模，提升跨任务可解释性。
2. 构建规模级 HumanGen 数据集，覆盖大量长尾任务组合。
3. 在 RoboTwin 2.0 和真实世界上验证了跨任务泛化和复杂场景执行能力。

## 关键实验或结果
- 在 RoboTwin 2.0 七个未见任务上，零样本表现 47.0% 成功率，较最强基线提升 29.5 个百分点。
- 在真实环境中，模型能够根据人类视频完成未见配置、多目标和长时操作的泛化执行。

## 适合关注的原因
它给出一种现实可行的“任务传达协议”：把人类演示转为机器人可读上下文，使 open-ended 任务更容易被模型消费。

## 局限性或待验证点
- 人类视频与机器人动作域差异仍可能引入语义错位，IFP 抑制机制是否在极端稀疏反馈任务仍待检验。
- 数据构造和真实部署中的动作安全边界未在摘要层面展开。

## 对后续研究/应用的启发
- 可与动作层风险约束器结合，形成“演示驱动 + 安全控制”的统一 VLA 框架。
- 可尝试对齐不同机器人形态（人手/机械臂）下的任务表征投影策略，降低 embodiment 迁移成本。

## 适合 Obsidian 快速浏览的中文总结
一句话：把“人类视频示例”作为任务条件，显著提升了机器人对未见任务的跨域泛化表现。

## 标准化研究框架
**Research question：** 在机器人任务泛化场景下，视频上下文是否比传统文本提示更能支撑 zero-shot task generalization？

**Literature：** 大量机器人学习方法依赖人类标注动作序列或少量演示，任务可扩展性不足；本工作尝试借鉴 in-context 机制重构输入语义。

**Theory：** 动作策略若能从动态上下文中提取可执行任务表示，即可在未见任务下避免过拟合历史动作轨迹，形成更好的条件推断。

**Hypotheses：**
1. 视频上下文可提供更稳健的任务演化信号。
2. 大规模配对任务-人类视频数据能减少 shortcut 学习。
3. IFP 可提升 unseen 任务迁移成功率。

**Method：** 构建 HumanGen 数据并进行 zero-shot 评测；结合 IFP 目标训练 Zero-WAM，并在模拟与真实机器人上验证。

**Data and Analysis：** 用 74.2K 人机任务对进行训练与验证，评估指标包括成功率、泛化任务集合表现与真实部署可行性。

**Findings：** 视频条件与 IFP 目标的结合显著提升了未见任务成功率与实景执行稳定性。

**Conclusion：** 对具身智能而言，任务条件化方式比参数堆叠更关键，Zero-WAM 在 open-ended manipulation 方向值得作为数据-模型闭环模板。
