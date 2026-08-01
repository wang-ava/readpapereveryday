# OSReward: Instituting Standardized Evaluation for Cross-Platform Computer-Use Reward Models

Spotlight：这篇论文把 CUA 评测核心矛盾讲透了——把 VLM 当裁判时很容易“过度宽容”；它提出统一评测与低成本可复用 reward 模型，直接面对 agent 训练中的 reward 漏洞。

- 论文标题：OSReward: Instituting Standardized Evaluation for Cross-Platform Computer-Use Reward Models
- 作者：Qiushi Sun, Kanzhi Cheng, Yian Wang, Bowen Yang, Hang Yan, Liheng Chen, Fangzhi Xu, Zichen Ding, Nuo Chen, Jialin Cao, Xingdong Gong, Zehao Li, Kaiming Jin, Xinfeng Yuan, Zhoumianze Liu, Jingyang Gong, Zhangyue Yin, Jiahui Gao, Zhiyong Wu, Tianbao Xie, Jianbing Zhang, Ben Kao, Lingpeng Kong
- 机构（如可得）：arXiv 元信息未直接展示完整机构信息
- 发布时间：2026-07-30（v1）
- 主题标签：`#Agent` `#ComputerUse` `#RewardModel` `#Benchmark` `#VLM-Judges` `#Evaluation`
- 论文链接：[https://arxiv.org/abs/2607.28609v1](https://arxiv.org/abs/2607.28609v1)
- PDF 链接：[https://arxiv.org/pdf/2607.28609v1](https://arxiv.org/pdf/2607.28609v1)
- 项目/代码/数据链接：论文摘要给出主页与公开资源入口（暂不含单独独立 release 码流区分）：[https://os-copilot.github.io/OSReward-Home/](https://os-copilot.github.io/OSReward-Home/)

## 核心问题
在跨平台 computer-use agent 中，如何用可扩展且可信的自动化评估机制替代昂贵且不一致的人类判定？

## 方法概要
论文构建 OSReward 评测基准：收集多平台 agent 在人工任务上的轨迹，经过多阶段人类注释形成高质量 verdict；再定义 OSReward-Hard 与 OSReward-Multi 两类挑战集，并基于轨迹判定任务训练/验证 reward model。核心不是只追求更强 judge，而是强调 judge 的可解释偏差诊断与成本效率。

## 主要贡献
- 建立高质量 computer-use trajectory 评价基准，形成统一可复用的标准化 pipeline。
- 系统发现并量化 `VLM judge` 的 leniency bias（倾向过于宽松）。
- 发布 OS-Shepherd-100K，补齐 open reward 与数据不足之间的缺口。
- 在开源/商业可比条件下，训练 9B 和 35B 模型形成较优成本-可靠性平衡。

## 关键实验或结果
- 结果显示当前 SOTA VLM judge 仍显著偏离“理想裁判”，尤其在失败样例识别上存在一致性偏差。
- 该工作训练的 OS-Shepherd-100K 与 OS-Shepherd 系列在成本上可低于商业 frontier 30%–60%，同时保持更稳定可靠信号。
- OSReward-Hard 与 OSReward-Multi 暴露了不同任务维度下的误判模式，支持后续对齐预算优化。

## 适合关注的原因
如果你在做 agentic workflow、RPA、测试自动化或长程工具调用系统，这篇工作提供了“如何不被虚假成功率误导”的实证起点，尤其适用于 reward model 快速迭代和 benchmark 演进。

## 局限性或待验证点
- 论文摘要标记为 Work in progress，意味着官方 pipeline 与训练细节可能仍在持续更新。
- 评测是否完整覆盖行业真实平台组合尚需后续实测。
- 成本收益比与偏差修正策略在高安全等级生产环境（受限 UI、低错误容忍）尚待复核。

## 对后续研究/应用的启发
可把 OSReward 思路推广到领域化 agent：将“单模型裁决”升级为多任务、多平台校准的 judge 面板机制，从而将 `reward hacking` 与错误正反馈抑制在训练早期。

## Obsidian 快速浏览总结
一句话速看：OSReward 用统一基准 + 公开轨迹语料，暴露并纠正 CUA judge 的系统性松弛偏差，支持低成本可复用的 reward 学习闭环。

## 标准化研究框架
- **Research question：** 在 cross-platform computer-use 场景下，如何建立可复用的评估标准，使 reward signal 的准确性与可扩展性同时达到实用水平？
- **Literature：** 工作位于 agent 评测、VLM judge 对齐、reward model 学习三条线交叉点上，重点不是模型架构创新，而是评测与训练闭环规范化。
- **Theory：** 基于“高质量监督信号决定 reward 稳定性”的原则，强调多来源证据（轨迹 + 人工标签）可抑制 judge 偏差。
- **Hypotheses：** 非经典假设检验范式；可改写为“若评测集覆盖真实困难样例且分层难度明确，则能显著提升 reward 的可靠性并降低幻觉式高估。”
- **Method：** 构建 OSReward 及其子集，提取多平台轨迹，建立 ground-truth verdict，训练 OS-Shepherd 系列并对比 open/closed judge 成本与准确性。
- **Data and Analysis：** 以轨迹数据 + 多层标注为核心数据资产，结合 OSReward-Hard、OSReward-Multi 进行分层误差分析并对齐不同规模模型。
- **Findings：** 可扩展 judge 体系下仍存在 leniency bias；开源 reward（OS-Shepherd）可在更低成本下接近商业水平。
- **Conclusion：** 对 agent 系统而言，评测闭环比单点模型提升更关键，下一步应扩平台覆盖与域外场景验证以提高部署稳健性。
