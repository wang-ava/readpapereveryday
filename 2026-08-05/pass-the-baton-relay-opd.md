# Pass the Baton: Trajectory-Relayed On-Policy Distillation

Spotlight：这篇工作把 LLM 训练中的“错误前缀陷阱”从一句提醒变成了可执行机制：让教师模型在关键时刻短暂接管学生轨迹，并让学生在接力后继续优化，既降低计算，又显著提升数学推理基准表现。

- 论文标题：Pass the Baton: Trajectory-Relayed On-Policy Distillation
- 作者/机构（如可得）：Haolei Xu；Xiaowen Xu；Haiwen Hong；Zixuan Ni；Hongxing Li；Yiwen Qiu；Weiming Lu；Yongliang Shen（作者机构在 arXiv 页面未直接披露）
- 发布日期/版本日期：2026-07-28（v1）
- 主题标签：`#LLM` `#AgenticLearning` `#Distillation` `#MathReasoning` `#Efficiency`
- 论文链接：[https://arxiv.org/abs/2607.26057](https://arxiv.org/abs/2607.26057)
- PDF 链接：[https://arxiv.org/pdf/2607.26057](https://arxiv.org/pdf/2607.26057)
- 项目/代码/数据链接（如可得）：项目页 `https://zju-real.github.io/Relay-OPD`；代码 `https://github.com/zju-real/Relay-OPD`

- 核心问题：On-policy distillation 的学生轨迹监督在学生一旦走错推理分支后会持续放大错误，后续 token 的监督信号变得低质量，导致训练效率和最终效果受损。
- 方法概要：提出 Relay-OPD（Relay On-Policy Distillation）。训练时检测“失败前缀”，当发现学生轨迹可能偏离时，由教师模型接管短程生成（teacher leg），再交还给学生继续生成；通过有限接力预算在关键位置进行干预，显著减少错误传播。
- 主要贡献：
  - 把前缀失败建模为可观测的 teacher-student 继续策略差异，并转化为无标签触发规则。
  - 用“接力式”训练替代全程教师接管，兼顾稳定性与学生策略一致性。
  - 限制接力预算，在性能和成本间建立可控折中。
- 关键实验或结果：
  - 在 8 个数学推理基准上，Qwen3-0.6B/1.7B 非思维模式学生对比标准 OPD 提升，1.7B 平均 +5.73%，较 FastOPD +1.49%。
  - 训练轨迹长度减少超过 50%，显示了明显的训练效率提升。
  - 学生可在低计算预算下获益，说明方法对蒸馏经济性有价值。
- 适合关注的原因：方法直接对应“LLM 训练长尾错误放大”常见工程痛点，具备较强可落地性，且接力机制可迁移到复杂推理工具链微调场景。
- 局限性或待验证点：
  - 主要聚焦数学推理，未明确报告代码生成、多轮对话、检索增强等任务泛化。
  - 论文摘要中未给出接力阈值、触发策略与超参敏感性细节，复现实践需查看正文。
  - 依赖高质量教师模型，接力质量下界未必始终成立。
- 对后续研究/应用的启发：可用于多阶段蒸馏和 Agent 推理模型训练：把“是否接手”和“接手长度”做成可学习策略，以减少幻觉放大与推理成本。
- Obsidian 快速浏览总结：Relay-OPD 通过“局部接力”修复 LLM 路径错误，兼顾泛化与效率，值得在长链路推理蒸馏里优先尝试。

## 标准化研究框架
- **Research question：** 在 on-policy 蒸馏中，是否可以用“有触发条件的教师短接管”替代持续教师监督，在保持学生行为一致性的同时显著抑制错误轨迹放大？
- **Literature：** 现有 OPD 与蒸馏方法大多采用学生全轨迹监督，容易受前缀失败影响；Relay-OPD 相当于在该传统链路上加入了可控的局部干预。
- **Theory：** 一旦 token 序列进入低质量决策区域，后续监督梯度会与最优方向偏离；引入接力后可在局部重置轨迹分布，减少错误条件分支对后续样本的吸附作用。
- **Hypotheses：** （1）在关键触发点接管可提升下游推理准确率；（2）接力长度与频率可调会形成精细的性能-效率前沿。
- **Method：** 1）定义失败前缀触发器；2）教师生成接力段；3）学生接续后按机器学习轨迹监督优化；4）比较不同预算下的基准成绩与训练长度。
- **Data and Analysis：** 训练与评估在 8 个数学基准上进行，对比标准 OPD 与 FastOPD；关注平均成绩、接力预算和轨迹长度。
- **Findings：** 摘要显示平均提升 +5.73%，训练轨迹缩减超 50%，表明接力机制同时对效果与效率均有帮助。
- **Conclusion：** 该方法为 agentic/LLM 蒸馏提供了可落地的“局部纠偏”框架，适合优先验证接力触发规则稳定性与跨任务泛化。
