---
spotlight: "通过双视角协同建模和潜变量预测，DUET-DINO 让机器人在三维抓取-放置等任务上实现更完整的 7-DoF 规划表现。"
---

# DUET-DINO: Simultaneous Cross-View World Modeling for Latent Planning in Robot Manipulation

## 基本信息
- **论文标题**：DUET-DINO: Simultaneous Cross-View World Modeling for Latent Planning in Robot Manipulation
- **作者**：Nisarga Nilavadi, Ralf Römer, Moritz Reuss, Michael Krawez, Tobias Jülg, Angela P. Schoellig, Rudolf Lioutikov, Wolfram Burgard
- **机构**：arXiv 元数据中未公开。
- **发布日期 / 版本日期**：2026-09-09（v1）
- **主题标签**：`Embodied AI` `Robot Manipulation` `World Model` `Latent Planning` `Cross-View`
- **论文链接**：https://arxiv.org/abs/2609.10506
- **PDF 链接**：https://arxiv.org/pdf/2609.10506
- **项目/代码/数据链接**：项目页 https://utn-air.github.io/DUET-DINO；论文声明代码与模型即将开源（建议以官方发布为准）。

## 核心问题
单视角世界模型在处理细粒度抓取（角度、姿态）时常有预测偏差；全自由度 7-DoF 规划缺乏跨视角一致建模。论文核心是：能否通过同一模型同步利用静态侧视与腕部视角，提升动作条件下的潜变量规划能力。

## 方法概要
提出 DUET-DINO：在静态侧视和手腕视角之间做联合条件建模，通过 cross-view coupling 将场景大局与末端执行器细节结合，进行动作条件的未来潜状态预测。该潜空间预测再用于 latent planning，支持连续 7-DoF 控制。

## 主要贡献
- 首次在单模型中同时融合侧视与腕部视角实现动作条件 latent 预测。
- 从表示学习角度解释 DINO 在细粒度动作下更能捕捉场景动力学。
- 在单视图基线、独立双视图基线之外提供统一改进路径。

## 关键实验或结果
在 reach、angled-reach、multi-goal grasp-and-lift 三类任务上，DUET-DINO 分别达到 92%、72.5%、60.0% 的成功率，且在 DROID 与 RoboArena 数据集的分布外场景中保持更稳健；在跨时序可视化预测质量上优于 V-JEPA2 wrist-view 基线。

## 适合关注的原因
这是把“视角不一致”转化为可学习互补信息的实证例子，尤其适合真实操作任务中 7-DoF 控制误差经常来自单视角盲区的问题。

## 局限性或待验证点
- 论文摘要仅给出少量数据集与任务；多样工业抓取与长时序动作链尚未覆盖。
- 代码是否完全开源、复现实验细节尚需项目页后续确认。
- 依赖视觉质量的场景仍对重反光/遮挡更敏感。

## 对后续研究/应用的启发
- 可将 cross-view latent planning 与触觉信息继续融合，减少姿态误差。
- 对实际机器人系统，可用该框架替代单视图世界模型作为规划前端。
- 适合验证在远程协作机器人中的样本效率提升能力。

## 一句话中文速览总结
DUET-DINO 通过双视角潜在世界建模，把全自由度抓取的动作预测和规划能力显著抬升。

## 标准化研究框架
- **Research question：** 同时建模侧视与腕部视角，是否能显著提高动作条件世界模型对精细操作任务的可规划性？
- **Literature：** 多数世界模型要么单视角、要么独立双视图，难以统一利用全局语义与抓取端细节。
- **Theory：** 融合不同视角可减小动作条件下信息缺失，使潜变量预测对姿态变化更敏感，降低规划误差。
- **Hypotheses：**（1）交叉视角联合预测在多任务中优于单视角；（2）可显著提升角度敏感任务；（3）对分布外场景的泛化更强。
- **Method：** 训练联合潜变量世界模型，以 7-DoF 动作为条件输入，在 DROID 与 RoboArena 进行训练并用下游规划验证。
- **Data and Analysis：** 对比单视图、独立双视图和本方法的成功率，并分析不同任务场景下的行为偏差。
- **Findings：** DUET-DINO 在关键任务上取得 92%/72.5%/60.0% 成功率，并显示对分布外场景更稳。
- **Conclusion：** cross-view 世界建模为具身操作提供了更稳健的 latent planning 路径，但真实工业场景仍需补齐更广泛任务和感知条件评估。
