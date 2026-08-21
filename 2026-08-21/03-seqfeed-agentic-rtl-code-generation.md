# SeqFeed: Improving Agentic RTL Code Generation with Sequential Behavior Feedback

Spotlight：论文把“LLM 不能稳定理解时序硬件行为”转化为结构化反馈问题：把波形观察做成可检索事件+依赖图。它更像给 Agentic coding 增加一套可观测性协议，提升闭环修正效率。

## 论文信息
- 论文标题：SeqFeed: Improving Agentic RTL Code Generation with Sequential Behavior Feedback
- 作者（机构）：Yuxin Du, Juxin Niu, Tao Hu, Xi Wang, Zhe Jiang, Nan Guan（论文页未公开机构）
- 发布日期：2026-08-09（v2）
- 主题标签：`#Agent` `#LLM` `#RTL` `#Hardware` `#ToolUse`
- 论文链接：[https://arxiv.org/abs/2608.16934v2](https://arxiv.org/abs/2608.16934v2)
- PDF 链接：[https://arxiv.org/pdf/2608.16934v2](https://arxiv.org/pdf/2608.16934v2)
- 项目/代码/数据链接（如可得）：未在 arXiv 页面公开给出。

## 论文内容
- 核心问题：LLM Agent 在写 RTL 时难以稳定理解时序行为，传统全文波形过于冗长、RTL 源码又缺乏逐周期语义证据。
- 方法概要：先研究工程师调试习惯并提出三类反馈需求（事件可寻址、依赖可追踪、可反复查询）；再提出 SeQuery（类 SQL 的波形查询语言）和 SeGraph（跨时钟周期信号传播依赖图），为 Agent 提供可编程、可复用的时序反馈通道。 
- 主要贡献：
  - 定义了时序行为反馈在 agentic coding 中可执行的表示与交互接口。  
  - 将 SeQuery 与 SeGraph 设计为解耦组件，可单独或联合使用。  
  - 用多模型实验验证反馈机制对 pass rate 的实际提升。
- 关键实验或结果：
  - 实验显示 SeQuery 与 SeGraph 均能独立提升结果，多模型联合使用时表现互补。
- 适合关注的原因：
  - 该方向直接影响硬件/低延迟系统中“可执行 AI”落地，尤其适合复杂协议代码、时序约束强的工程链路。 
- 局限性或待验证点：
  - 文内未给出所有 benchmark 的统一指标与标准偏差，复现实验细节仍需补充。  
  - SeQuery 的查询语言是否可迁移到不同模拟环境（如芯片级、FPGA 工具链差异）仍待验证。
- 对后续研究/应用的启发：
  - 可将“事件化反馈”扩展到数据库、编译器错误日志、测试覆盖率报告，实现跨域 agent 统一调试通道。 
  - 工程上建议把反馈语义内化到工具定义（tools schema）中，减少手工 prompt 工程成本。
- Obsidian 快速浏览一句总结：**对 Agentic RTL 生成而言，信息不在于更多日志，而在于能否把时序问题转成可检索的事件语义。**

## 标准化研究框架
**Research question：** 通过结构化事件/依赖反馈，是否能在缺乏完备波形可读性的条件下稳定提升 agentic RTL 代码生成质量？

**Literature：** 现有代码生成研究多依赖执行/编译反馈，但对硬件时序语义支持薄弱。本文通过可查询反馈语言把传统“事后调试”提升为“过程中的闭环引导”。

**Theory：** 若行为证据能够被映射为可复用的事件元数据，Agent 的决策搜索空间会被显著约束，可减少无效迭代。

**Hypotheses：**  
- H1：事件化查询（SeQuery）可提升对故障信号定位速度。  
- H2：依赖图（SeGraph）可提高跨周期错误传播理解。  
- H3：两者联合提供互补增益，优于单一反馈通道。 

**Method：** 定义三类反馈需求，分别设计 query 与 dependency graph 接口，并在多模型 RTL generation setting 下做消融。

**Data and Analysis：** 以多模型生成结果与多轮修正回合进行对比，分析 pass rate 的提升幅度与反馈组件的单独/联合贡献。

**Findings：** 实验支持“双模块互补”结论，说明时序反馈不仅可提高通过率，也可使 agent 行为更具可解释性。

**Conclusion：** 对硬件 AI Agent 场景，反馈表示层比单纯参数规模更关键，标准化时序反馈可作为可复用工具原语。
