# Scene2Demo: Self-Evolving Embodied Data Generation via Object-Action Graph

Scene2Demo 提供“输入图像 + 任务意图”即生成可执行仿真任务与训练数据的闭环方案，用反馈代理不断修正失败轨迹，提高 embodied 数据自举效率。

## 基本信息

- 论文标题：Scene2Demo: Self-Evolving Embodied Data Generation via Object-Action Graph
- 作者/机构（如可得）：Xiang Liu、Sen Cui、Guocai Yao、Zhong Cao、Jingheng Ma、Min Zhang、Miao Liu、Changshui Zhang（机构信息未在页面完整列出）
- 发布日期或版本日期：2026-05-27（发布），6-day 内修订：2026-06-01
- 主题标签：#EmbodiedAI #EmbodiedData #ObjectActionGraph #ImitationLearning #DataGeneration
- 论文链接：https://openreview.net/forum?id=88IawleLNi
- PDF 链接：https://openreview.net/pdf?id=88IawleLNi
- 项目/代码/数据链接（如可得）：页面未给出可直接点击的仓库链接；需待后续版本公开。

## 核心问题

真实世界可执行数据昂贵且难扩展。该研究关注如何从少量输入（RGB 场景+查询）高效生成可验证、可执行且有标注价值的 embodied 数据。

## 方法概要

方法将任务构建拆成 object-action graph 流程：先从输入图像与用户查询构建对象级状态与动作拓扑，再生成可执行场景配置和多视角视频，再形成离线学习数据集。若执行失败，反馈代理读取可视化 rollouts，自动修改动作序列或参数并重采样。

## 主要贡献

- 提出自进化（self-evolving）数据生成闭环，而非一次性合成。
- 引入对象-动作图作为任务语义抽象，适配任务规划与行为克隆。
- 用反馈代理替代纯人工重写，提高数据可复用性。

## 关键实验或结果

论文给出 102 个原始任务对的生成结果：基线 primitive execution 成功率到 self-evolution 后提升到 71.6%。在 4 个长时任务上，局部执行质量和整体成功率均有提升，并在 RoboGen、GenSim2 等对照上有优势。

## 适合关注的原因

如果你在做机器人模拟数据、行为克隆、任务规划预训练，这类“可进化数据工厂”很适合减少人工标注与真实采集成本，并可能形成稳定的数据增长曲线。

## 局限性或待验证点

- 页面并未公开完整对照设置（动作基线、硬件/环境细节）。
- 是否能跨域泛化到非人造物体场景与真实机械臂部署尚待验证。
- 代码与数据发布状态不透明，工程复现路径需继续跟进。

## 对后续研究/应用的启发

可先将其作为“任务数据供给层”试点：把对象关系图和反馈智能体内置到仿真训练流水线，逐步减少真人样本构建成本，并形成失败闭环。

## Obsidian 快速浏览总结

Scene2Demo 的价值在于把“数据生成”与“自我纠错”合在一个 loop 里，适合解决长时任务数据稀缺问题。

## 标准化研究框架

**Research question：** object-action 图驱动的 self-evolving 闭环能否在降低人工成本的同时提升 long-horizon embodied 任务的数据有效性？

**Literature：** 与现有 embodied data generation 工作不同，该文强调结构化动作图与失败反馈重生长；与行为克隆任务相比减少了固定模板依赖。

**Theory：** 框架理论重点在于“反馈优化数据生成分布”，不是传统因果假设检验范式。

**Hypotheses：** 假设反馈代理可持续降低执行失败，并提高任务执行率；非社会科学语境下可理解为“系统级收敛/改进假设”。

**Method：** 从输入查询生成场景与动作图，生成任务配置与视频，收集失败样本，反馈代理修订后重采样，最终形成可用于行为克隆的数据。

**Data and Analysis：** 评估对象为 102 个任务对及多个 long-horizon benchmark，核心指标为 execution success 与子任务质量对比。

**Findings：** 自进化后成功率达 71.6%，并在子任务层面相对 primitive baseline 有明显提升。

**Conclusion：** 该方法在模拟闭环数据场景很有潜力，但需更多公开细节与跨域实验确认其真实部署价值。
