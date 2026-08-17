# AutoDesign: Meta-Harness Optimization for Long-Horizon Agentic Design

Spotlight：本文把 agentic 设计从“单次生成-一次性打分”升级为可持续自举的 meta-harness 优化框架。它在 PosterBench 上显著提高了代码 agent 在长链路任务中的可复用性和稳定表现，值得关注任务型 agent 编排的评测与训练闭环。

## 论文信息
- 论文标题：AutoDesign: Meta-Harness Optimization for Long-Horizon Agentic Design
- 作者（机构）：Yaxin Luo; Haobin Jiang; Jialv Zou; Xu Huang; Wenhao Yan; Haodong Li; Zhengrong Yue; Jing Li; Xiaofu Chen; Xiaohan Zhao; Jiacheng Liu; Jiacheng Cui; Zhiqiang Shen; Xiaotong Li（机构未在该 arXiv 摘要页明确披露）
- 发布日期：2026-08-13（v1）
- 主题标签：`#LLM` `#Agent` `#Harness` `#Benchmark` `#ToolUse`
- 论文链接：[https://arxiv.org/abs/2608.13560v1](https://arxiv.org/abs/2608.13560v1)
- PDF 链接：[https://arxiv.org/pdf/2608.13560v1](https://arxiv.org/pdf/2608.13560v1)
- 项目/代码/数据链接：GitHub Code：<https://github.com/Yaxin9Luo/AutoDesign>
- 核心问题：如何让 agentic 文档生成系统在长时程、多轮反馈任务中持续提升能力，而不是依赖静态提示和一次性微调。
- 方法概要：论文提出 Meta-Harness 优化器，围绕 code agent 在一批 long-horizon 任务上的 rollout 反馈学习“可复用 harness 策略”；作者以学术论文海报自动生成作为任务场景，以 PosterBench 作为评价基准。
- 主要贡献：
  - 设计了与任务外部可复用的 meta-harness 架构，支持经验积累与 recursive self-improvement。
  - 在同一评测框架下同时比较不同代码 agent 配置，显式量化 harness 引入前后的增益。
- 关键实验或结果：
  - PosterBench 主赛道最高 78.32 分，较 Claude Design 高 7.45 分。
  - 七类配置中，加入学习式 harness 后平均分从 54.99 提升到 67.39（+12.4%）。
  - 长链路自动循环可执行 253 次 tool call、11 次编辑循环，约 40 分钟完成并发出 conference 级别平均质检水平结果，成本低于 $3。
- 适合关注的原因：该方向将“Agent 能力评测”从一次性 benchmark 指标拉回到“可进化系统”层面，直接影响自动化内容生产、AI coding、文档工程流水线。
- 局限性或待验证点：论文偏重公开 benchmark 与海报场景，真实生产链路中的隐私约束、代码安全审计、异构部署成本尚未充分量化；可迁移性到非学术出版任务待进一步检验。
- 对后续研究/应用的启发：可把 meta-harness 思想迁移到代码审核、合同生成、课程教学内容编排等任务，让 agent 的工具协同策略成为可学习资产，而非 prompt 的临时拼接。
- Obsidian 快速浏览一句总结：**把 harness 从静态脚本化改造为可学习闭环，是 agentic long-horizon 任务迈向稳定落地的关键。**

## 标准化研究框架
**Research question：** 在长链路 agentic 任务中，是否可以通过 meta-level 优化器学习“任务适配 harness”，持续提高工具链决策质量与可复用性？

**Literature：** 现有方法多数把 agent 性能看作单点 prompt 或模型规模的函数，缺少对执行轨迹历史进行归纳的通用 harness 学习框架；本工作补齐了长期反馈学习在 harness 层面的实践。

**Theory：** 任务执行可视作“策略改进过程”，其中 harness 充当任务级控制策略，长期 reward 来自生成与编辑后的评分信号；在此假设下，用 meta-optimization 进行快速迭代可收敛到更稳态策略。

**Hypotheses：**  
- H1：显式学习 harness 比固定 harness 在长期复杂任务中显著更优。  
- H2：学习 harness 的收益会随任务复杂度与反馈密度上升而增加。  
- H3：在多模型对比下，meta-harness 提供一致且可迁移的收益下界，不依赖单一模型偶发优势。

**Method：** 以 paper-to-poster 长链路任务构建 rollout 环境；对 baseline code agent 与学习式 meta-harness 方案做同工况对照；通过 100+ 论文主榜与 mini 子榜报告性能。

**Data and Analysis：** 使用 PosterBench（Main Track 与 mini 变体）测评；报告跨配置平均分、最高分、执行链路效率与成本。分析了 253 个工具调用、11 次编辑回合下的稳定性与质量变化。

**Findings：** 在给定预算下，meta-harness 显著拉高平均分与最优分；同时维持低成本运行，说明该方法并未把收益建立在暴涨推理成本上。

**Conclusion：** 对于长时程 agent 应用，学习型 harness 是比单次指令工程更具扩展性的主干方向；其关键在于设计可审计且可复用的反馈闭环。
