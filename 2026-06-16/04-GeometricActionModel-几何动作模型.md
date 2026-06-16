# Geometric Action Model for Robot Policy Learning

Geometric Action Model（GAM）将“几何基础模型”直接放进动作决策主干，试图解决 VLA/WAM 在接触操作里忽视三维几何连续性的不足。通过共享 backbone 的方式，它在 perception、时序预测与动作解码之间建立统一通路。

- **论文标题**：Geometric Action Model for Robot Policy Learning
- **作者/机构**：Jisang Han, Seonghu Jeon, Jaewoo Jung, René Zurbrügg, Honggyu An, Tifanny Portela, Marco Hutter, Marc Pollefeys, Seungryong Kim, Sunghwan Hong（arXiv 页面未统一列出机构信息）
- **发布日期/版本日期**：2026-06-15（v1）
- **主题标签**：#EmbodiedAI #Robotics #VLA #GeometricAI #PolicyLearning
- **论文链接**：<https://arxiv.org/abs/2606.17046>
- **PDF 链接**：<https://arxiv.org/pdf/2606.17046v1>
- **项目/代码/数据链接（如可得）**：项目页：<https://cvlab-kaist.github.io/Geometric-Action-Model/>
- **核心问题**：很多机器人策略模型虽借助多模态 foundation model，但仍基于 2D/2D-衍生潜变量，难以精细刻画接触-rich 操作中的三维几何关系。
- **方法概要**：
  1. 以预训练几何基础模型（GFM）为主干。
  2. 在中间层断点分离编码与预测路径：浅层负责观测编码，后续插入因果式未来预测模块。
  3. 未来 latent token 在语言、Proprioception、动作历史条件下预测后再回传后续 GFM block，统一生成几何与动作输出。
- **主要贡献**：
  1. 提出“几何动作模型”在同一 backbone 内实现动作与几何协同建模。
  2. 相比重建式复杂模型，保持架构轻量化。
  3. 在仿真和真实机器人 manipulation suite 上展示更高准确率、鲁棒性与速度。
- **关键实验或结果**：
  - 相比现有 foundation-model-scale baseline，文章报告在模拟与真实操作任务中均更优，且运行更快更轻。
  - 证明将语言条件和几何预测融合可显著改善接触操作执行。
- **适合关注的原因**：
  1. 具备较高工程迁移性，适合从研究原型向机器人 pipeline 过渡。
  2. 提供“3D-aware 语言-动作映射”的实证方向，值得关注下一代 VLA 结构。
  3. 与高成本硬件环境中的快速迭代需求契合。
- **局限性或待验证点**：
  1. 任务覆盖范围和场景分布仍需持续扩展。
  2. 未披露大规模跨域迁移和硬件差异泛化细节。
  3. 对实时部署中的传感噪声鲁棒性仍需更细粒度测试。
- **对后续研究/应用的启发**：
  可以与手眼标定误差建模、接触物理约束损失结合，构建更稳健的“语言控制机器人操作”系统。
- **Obsidian 快速浏览的一句总结**：GAM 用几何基础模型承接语言条件动作，强调接触操作里 3D 几何先验的重要性，值得用于下一代具身策略模型原型。

## 标准化研究框架
- **Research question：** 如何在保持模型轻量化的前提下，让 robot policy 同时获得语言语义理解与三维几何一致性？
- **Literature：** 对齐 VLA / WAM / GFM 思路，进一步强调 geometry-aware policy 的统一建模。
- **Theory：** 用共享表示与中间层任务分工代替传统多模型串接，属于结构重参数化工程范式，不是统计假设检验。
- **Hypotheses：** 若语言、动作与未来几何预测共享同一几何主干，则可提升决策稳定性并降低模型复杂度。
- **Method：** 将 GFM 切分为两段，在中间插入预测器并将语言+状态条件注入未来 token；回传后续层进行动作解码。
- **Data and Analysis：** 在仿真与真实机器人操作任务上做准确率、鲁棒性、速度/参数量对比。
- **Findings：** 报告显示该拆分机制对性能和效率兼顾更优，说明几何先验可作为动作策略共享骨干的关键资源。
- **Conclusion：** 该框架可理解为“结构共享+时序几何约束”的工程模型，适合直接作为具身智能策略的 baseline 进行再开发。
