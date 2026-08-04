# WorldExam: Benchmarking World Models from Apparent Appearance to Inherent Reactivity

Spotlight：WorldExam 将 video world model 评测从“画面是否好看”推进到“世界是否会按物理状态做出正确反应”，对具身模拟、交互式生成和视觉生成基准很关键。

- 论文标题：WorldExam: Benchmarking World Models from Apparent Appearance to Inherent Reactivity
- 作者/机构（如可得）：Yuxue Yang；Shuyao Shang；Jiahe Wang；Zitong Zhou；Liang Tan；Junhan Zeng；Ruizhi Li；Junyan Li；Yu Liu；Xiao Yang；Yong Li；Jun Zhu；Hongsheng Li；Tieniu Tan；Lue Fan；Zhaoxiang Zhang。作者机构在 arXiv 条目中未直接给出。
- 发布日期/版本日期：2026-08-03（v1）
- 主题标签：`#CV` `#WorldModel` `#Benchmark` `#Evaluation` `#VideoGeneration`
- 论文链接：[https://arxiv.org/abs/2608.02603](https://arxiv.org/abs/2608.02603)
- PDF 链接：[https://arxiv.org/pdf/2608.02603](https://arxiv.org/pdf/2608.02603)
- 项目/代码/数据链接：项目主页 `https://WorldExam.github.io`
- 核心问题：当前评测对 world model 大多只看外观质量和指令满足率，缺少对世界内在可反应性（inherent reactivity）的统一测度，导致模型在“看起来会动”但行为不符合场景规律时得分被高估。
- 方法概要：构建分层诊断基准，四级评估指标为 Visual Quality、Control Adherence、Spatial Consistency、World Reactivity；覆盖 1,474 个样本、8 类任务，支持 camera/action/language 三种输入范式统一评测。
- 主要贡献：
  - 将世界模型能力分解为层次化指标，明确区分“表观合成”与“内在动态一致性”。
  - 给出跨范式统一测试框架，便于比较不同控制接口的 strengths/weaknesses。
  - 引入 world reactivity 维度以检验模型对未显式约束目标的反应合理性。
- 关键实验或结果：对 20 个代表模型的评测显示明显能力分化：camera-driven 模型控镜头强但动态交互弱；action-driven 控制精度高但世界反应不足；language-driven 在交互性更好但复杂控制精度较低；无一模型同时在覆盖 breadth 与反应一致性上占优。
- 适合关注的原因：它回应了当前生成模型“看起来像电影”但难以用于决策推演的问题，对 VR、机器人模拟、数字孪生控制器都具直接参考价值。
- 局限性或待验证点：
  - 评测覆盖的物理场景与交互复杂度是否代表真实应用仍需后验确认。
  - 在真实机器人控制链路中的闭环误差传播（latency、actuation noise）未纳入。
  - 未直接给出可重复性细节与代码仓库地址（仅项目页）。
- 对后续研究/应用的启发：
  - 建议模型发布前同时报告 world reactivity 指标，而非只报视觉质量。
  - 可把 benchmark 结果用于任务/接口匹配：先选擅长 world reactivity 的模型再优化控制器。
  - 推动 world model 从“生成器”走向“可交互仿真器”评估范式。
- Obsidian 快速浏览总结：WorldExam 的关键价值是把 world model 的评价口径从“好看”升级为“能否对场景状态做正确反应”，更接近真实智能体需求。

## 标准化研究框架
- **Research question：** 如何在同一套基准下定量区分外观生成质量与世界内在反应能力，以便准确评估不同输入接口的 world model。
- **Literature：** 现有 benchmark 多集中于视觉指标和指令完成率，本研究将其拓展到动态反应层，属于评测维度重新定义的工作。
- **Theory：** 视觉世界模型应满足两类约束：一是外观一致性，二是状态转移一致性。理论上只有二者同时成立才具备可用于决策与控制的价值。
- **Hypotheses：** 加入 World Reactivity 维度后，模型排名会重排，且不同输入范式（camera/action/language）在任务覆盖与准确性之间存在稳定 trade-off。
- **Method：** 通过四层任务分解和 1,474 条样本统一打分；比较三类接口下模型在多任务指标中的差异，识别行为一致性瓶颈。
- **Data and Analysis：** 数据按任务、接口类型分组；核心分析使用指令完成率、空间一致性、反应正确率与任务覆盖率交叉统计。
- **Findings：** 摘要显示三类接口各有强项与短板：无单模型在 breadth 与 reactivity 上同时领先，说明当前 world model 仍缺少统一闭环能力。
- **Conclusion：** WorldExam 更像一个标准化诊断工具的起点，适用于指导模型选型与数据增强，而非直接给出“最优模型”答案。
