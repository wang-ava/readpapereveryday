# KForge: LLM-Driven Cross-Platform Kernel Generation for AI Accelerators

KForge 将“多后端 kernel 生成”从单模型生成问题改造为双角色 LLM 代理闭环，直接对齐真实编译与 profiling 流程，这使它对 AI 基础设施（AI4S）有更直接的工程价值。

- **论文标题**：KForge: LLM-Driven Cross-Platform Kernel Generation for AI Accelerators
- **作者/机构**：Taras Sereda，Burak Bartan，Ankita Nayak，Tom St.John，Natalie Serrino，Zain Asgar；机构：Gimlet Labs Inc.
- **发布日期/版本日期**：2026-06-01（arXiv:2606.02963）
- **主题标签**：#AI4S #KernelGeneration #Systems #LLMAgent #CUDA #Profiling
- **论文链接**：[https://arxiv.org/abs/2606.02963](https://arxiv.org/abs/2606.02963)
- **PDF 链接**：[https://arxiv.org/pdf/2606.02963.pdf](https://arxiv.org/pdf/2606.02963.pdf)
- **项目/代码/数据链接（如可得）**：摘要页显示源代码/项目入口可在 arXiv Source 中获取，但当前未在可直接抓取内容中得到可点击 URL；可先以 arXiv 页面为主线跟踪版本。
- **核心问题**：跨异构加速器（不同架构、不同编程模型）反复迭代 kernel 的成本极高，当前人工规则难以快速满足性能与正确性双目标。
- **方法概要**：KForge 提出双代理协同框架：
  1. Generation Agent 在反馈驱动下迭代生成/修订 kernel；
  2. Performance-analysis Agent 解析编译与 profiling 信号，输出下一轮优化建议；
  3. 两者闭环运行，在生产推理中动态调整策略。
- **主要贡献**：
  1. 把 LLM-agent 机制落地到编译-调优全链路；
  2. 明确了“性能分析 agent”在自动化 kernel 改进中的可行信息流；
  3. 为异构硬件生态提供可扩展的跨平台思路，不再把问题限制在单 backend。
- **关键实验或结果**：论文核心论据为在异构加速器场景下，通过协同迭代可减少依赖手工经验的反复尝试，提升优化效率（具体数值在公开摘要中未展开）。
- **适合关注的原因**：
  1. 与模型推理、编译器优化、算子调优高度贴合；
  2. 强调 agent 的工程闭环特性而非单次检索式生成；
  3. 对企业内部 AI 平台建设中的 kernel 维护成本具有直接启发。
- **局限性或待验证点**：
  1. 公开版本对关键指标（吞吐、时间、稳定性）披露不足；
  2. 多硬件平台的统一泛化能力仍依赖持续版本更新；
  3. 安全和正确性边界（错误 kernel 的误伤风险）未在当前摘要中充分展开。
- **对后续研究/应用的启发**：可将该思路扩展为“性能分析模型 + 工具调用代理”标准化框架，把 profiling 观测与代价建模内嵌到持续集成流程。
- **Obsidian 快速浏览一句总结**：KForge 是把 LLM 变成跨平台 kernel 团队的工程实践，目标是把手工微调 kernel 的工作流自动化。

## 标准化研究框架
- **Research question：** 如何将 LLM 代理系统用于跨硬件平台 kernel 生成，实现在正确性与性能之间高效权衡？
- **Literature：** 与 compiler-in-the-loop、代码生成 agent、AI4S 工作负载优化相关；与传统静态模板优化不同，更强调交互式优化迭代。
- **Theory：** 用反馈闭环替代单次优化假设，基于编译/profiling 信号的策略修正提升在异构环境中的鲁棒性。
- **Hypotheses：** 通过双代理分工（生成+分析），比单模型一次性优化更容易在多平台上稳定提升效率。
- **Method：** 构建 iteration loop：生成代理产出 kernel，分析代理执行 profiling、抽取瓶颈、反馈修订，再继续迭代。
- **Data and Analysis：** 以真实硬件编译与 runtime profiling 为驱动信号进行连续优化；使用对比基线验证代理化迭代收益。
- **Findings：** 摘要期证据显示该闭环能显著减少人工优化路径，提升优化过程可复用性和平台切换适应性。
- **Conclusion：** 该框架为 AI4S 里的 kernel 工程问题提供可执行方向，但需要更完整公开指标以验证规模化收益与边界安全。
