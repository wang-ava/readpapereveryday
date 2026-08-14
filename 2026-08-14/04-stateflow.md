# StateFlow: Building, Evolving, and Accessing 3D World States for Previsualization

> Spotlight：StateFlow 将“提示一次性生成”改为“持久世界状态编辑”，把预可视化任务中的迭代建模与摄像机规划拆开处理，更符合复杂创意流程。

- 论文标题：StateFlow: Building, Evolving, and Accessing 3D World States for Previsualization
- 作者（机构）：Yuyang Yin, Zixiang Li, Longxuan Deng, Hongkai Li, Shifang Zhao, Junnan Liu, Weirong Huang, Mengyu Wang, Tianxiao Fu, Yikai Wang, Peng-Shuai Wang, Xiaojie Jin, Yao Zhao, Yunchao Wei；机构未在 arXiv 页面直接给出（可通过作者主页/机构主页进一步确认）
- 发布日期（版本日期）：2026-08-12（arXiv v1）
- 主题标签：`#CV` `#3DWorldState` `#Previsualization` `#GenerativeModel`
- 论文链接：[https://arxiv.org/abs/2608.12314](https://arxiv.org/abs/2608.12314)
- PDF 链接：[https://arxiv.org/pdf/2608.12314v1](https://arxiv.org/pdf/2608.12314v1)
- 项目/代码/数据链接（如可得）：Project Page [https://yuyangyin.github.io/StateFlow](https://yuyangyin.github.io/StateFlow)；目前未公开额外代码/数据仓库链接
- 核心问题：现有预可视化多依赖一次性 2D/3D 生成，难以支持持续迭代、局部编辑与跨帧一致性控制，导致创作流程效率低。
- 方法概要：提出 state-centric 的 StateFlow 框架，用可持久 3D 世界状态承载场景几何、外观、相机等元素。框架分三阶段：state construction（先验引导+双视角初始化重建场景）、state evolution（用户意图驱动的局部状态转移并保留记忆）、state access（基于 render-feedback 的摄像机轨迹反思优化）。
- 主要贡献：
  - 用“世界状态”替代每帧重生成作为预可视化核心表示。
  - 在状态演化中保留历史记忆，减少重复计算与重建成本。
  - 引入 render-feedback feedback loop 提升摄像机路径可行性与视觉稳定性。
- 关键实验或结果：论文报告该框架可生成高质量 3D world 用于视频制作与游戏式原型搭建，体现了高保真与交互可编辑性的综合优势。
- 适合关注的原因：适配电影、游戏、建筑、城市设计等行业流程，尤其对“可迭代编辑+快速预演”场景有方法论价值。
- 局限性或待验证点：公开细节里缺少统一定量对比（如时延、参数规模、跨场景泛化率）；对工业级超大场景性能仍需继续验证。
- 对后续研究/应用的启发：可结合交互策略搜索（camera + scene graph planner）与可解释状态编辑，可扩展到可控内容生成和自动动画分镜 pipelines。
- 适合 Obsidian 快速浏览的中文总结：StateFlow 把预可视化从“画一次”改成“持续编辑世界状态”，对创意生产工具的迭代效率和稳定控制很关键。

## 标准化研究框架

**Research question：** 是否能通过持久化 3D 世界状态替代一次性视频生成，实现更高可控性和可迭代编辑性能？

**Literature：** 现有 previsualization 工作多偏向 prompt-to-video 或 static scene generation。StateFlow 与其不同之处在于显式建模场景与摄像机状态，使后续编辑在同一世界语义中连续进行。

**Theory：** 场景生成可拆成“结构状态”与“视图渲染”两层；复用共享状态可降低优化空间，减少每次编辑带来的漂移与重生成误差。

**Hypotheses：** 持久世界状态可提升编辑一致性并减少迭代成本；render-feedback 可提高相机轨迹可行性与最终视觉自然度。

**Method：** 构建三阶段框架：先用双视角先验初始化 3D scene state，再通过用户命令执行状态变更并保持历史约束，最后反向优化相机控制以满足可行性与美学目标。

**Data and Analysis：** 使用论文公开的视频/场景样例进行对比验证，重点观察可编辑性、几何一致性与相机轨迹有效性；评测指标从摘要中以定性结果为主。

**Findings：** 该框架能在预可视化任务中产生高质量 3D 世界并支持反复修改，但缺少更细粒度 quantitative baseline（未来可补充）。其核心价值在于过程可控性而非一次性生成分数。

**Conclusion：** 对需要持续交互的创意 AI 工具，StateFlow 给出“状态优先”范式；后续可补齐大规模 benchmark 与性能指标，检验其在复杂管线中的工程收益。
