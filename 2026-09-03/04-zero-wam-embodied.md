---
spotlight: "Zero-WAM 把人类演示视频转为可与机器人策略对齐的 in-context 任务规范，实现零样本外任务泛化并在真实场景有实测成效。"
---

# Zero-WAM: In-Context World-Action Modeling from Human Videos for Open-Ended Task Generalization

## 基本信息
- **论文标题**：Zero-WAM: In-Context World-Action Modeling from Human Videos for Open-Ended Task Generalization
- **作者**：Jiaming Zhou, Qihang Zhang, Gangwei Xu, Cunxin Fan, Yujie Zhao, Ruilin Wang, Yiming Luo, Shuai Yang, Xing Zhu, Yujun Shen, Junwei Liang, Yinghao Xu
- **机构**：arXiv 页面未公开机构，建议结合正文补充
- **发布日期 / 版本日期**：2026-08-26（v2）
- **主题标签**：`Embodied AI` `Robotics` `In-Context Learning` `World-Model` `Generalization`
- **论文链接**：https://arxiv.org/abs/2608.26103
- **PDF 链接**：https://arxiv.org/pdf/2608.26103
- **项目/代码/数据链接**：arXiv 目前未给出公开代码直链；论文声明包含 HumanGen 数据集与方法细节（可在全文/补充材料继续追踪）

## 核心问题
机器人从未见任务到新任务泛化仍困难。如何用“人类视频”作为任务规范，让模型在不再微调的情况下执行新的操作任务？

## 方法概要
- 提出 Zero-WAM（World-Action Model）框架：用人类示范视频作为 context，指导机器人执行。
- 构建 HumanGen 数据管线：从任务采样轨迹自动生成 74.2K 人类-机器人配对样本（8.6K 任务）。
- 引入 IFP（In-Context Future Chunk Prediction）目标，避免模型依赖已见任务捷径。
- 强制模型在未来片段上做因果预测，提升对视频语义的真实利用。

## 主要贡献
1. 给出一个高质量跨模态任务规范表示（human video）用于 ICL 机械臂/机器人控制。
2. 通过数据构建+训练目标双重设计，显著抑制 seen-task shortcut。
3. 在 RoboTwin 2.0 的 7 个未见任务中达到明显增益。

## 关键实验或结果
- 论文报告在 7 个未见任务上，Zero-WAM 成功率 47.0%，相比最强 baseline 提升 29.5个百分点。
- 真实世界实验显示其可在未见任务配置、多物体场景、长时序操作和精细插入任务中完成迁移。

## 适合关注的原因
- 解决了从仿真到真实世界的关键“任务泛化”瓶颈，尤其是开放式任务库场景。
- 视频作为任务描述对人机交互友好，利于自然语言模型和机器人控制之间的桥接。

## 局限性或待验证点
- 真实世界评估场景规模仍有限；复杂照明、遮挡与交互力反馈可能产生更大影响。
- 数据构建依赖自动配对质量，错误配对是否会引入策略偏差有待分析。
- 方法对时长较长的视频任务是否稳定依赖更多长序列建模技巧。

## 对后续研究/应用的启发
- 可扩展到仓储、厨房、实验室等“只需给出示例视频”即可快速部署的机器人工作流。
- 与 LLM agent planner 结合，可形成“视觉任务理解 → ICL 推理 → 动作执行”的统一框架。

## 一句话中文速览总结
Zero-WAM 通过人类视频指导与因果式 IFP 目标，让机器人在未见任务上获得较强零样本泛化能力，是具身智能中低成本任务规格化的一条新路径。

## 标准化研究框架
- **Research question：** 人类演示视频是否能作为可泛化的任务上下文，提升机器人在未见任务上的 open-ended generalization？
- **Theory：** 假设视觉任务规范包含更丰富的时序与因果信息，可减少传统指令表示对模型参数更新的依赖。
- **Hypotheses：** IFP 目标可抑制模型从训练任务捷径泛化，并提高对未见任务的稳健性。
- **Method：** 构建 HumanGen，训练 Zero-WAM，通过视频 context 做 in-context 动作预测，并在 RoboTwin 2.0 与真实环境进行评测。
- **Data and Analysis：** 使用 74.2K 对样本（8.6K 任务）和 7 个 unseen tasks，比对 baseline 成功率与真实部署表现。
- **Findings：** 报告显示 Zero-WAM 在未见任务上提升约 29.5 个百分点，真实部署中展现多场景泛化。
- **Conclusion：** 人类视频上下文可有效支持具身任务的快速迁移学习，但真实世界鲁棒性与配对噪声仍需系统评估。
