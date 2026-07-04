# PAW：从自然语言到可复用神经程序的“编译”路径

PAW 将部分 LLM 使用场景从“每次调用都推理”改为“先编译、再复用”，为日常工具类任务带来了可落地的成本-延迟折中。它对离线场景很友好，尤其适合日志告警、数据清洗这类重复高频调用的自动化工作流。

- 论文标题：Program-as-Weights: A Programming Paradigm for Fuzzy Functions
- 作者/机构（如可得）：Wentao Zhang；Liliana Hotosko；Woojeong Kim；Pengyu Nie；Stuart Shieber；Yuntian Deng
- 发布日期或版本日期：2026-07-02T17:59:50Z（arXiv v1）
- 主题标签：#LLM #ModelCompilation #Systems #Efficiency
- 论文链接：[https://arxiv.org/abs/2607.02512v1](https://arxiv.org/abs/2607.02512v1)
- PDF 链接：[https://arxiv.org/pdf/2607.02512v1](https://arxiv.org/pdf/2607.02512v1)
- 项目/代码/数据链接（如可得）：
  - 数据集：FuzzyBench（10M examples）
  - 代码/项目页：论文正文未给出公开仓库 URL
- 核心问题：在高频、规则模糊的业务函数场景中，持续调用大模型成本高、可复现性差、隐私与部署成本难以控制。
- 方法概要：提出 `fuzzy-function programming`，把任务定义从自然语言编译成紧凑的神经 artifact（parameter-efficient adapters）；冻结轻量解释器，由 4B compiler 在训练后为每个函数生成可复用的程序权重。
- 主要贡献：
  1. 给出从 prompt 到参数化小模型的工作流定义，强调“function-level caching by compilation”。
  2. 引入 FuzzyBench，并在该基准上评估可复用 artifacts 的准确性与效率。
  3. 验证 0.6B Qwen3 interpreter 搭配 PAW 可匹配 Qwen3-32B 直接 prompting 的表现。
- 关键实验或结果：
  - 性能接近 `Qwen3-32B`，但推理内存约降至 1/50；
  - 在 MacBook M3 上可达 30 tokens/s；
  - 通过离线 artifact 复用显著降低重复调用成本。
- 适合关注的原因：它把“用 LLM 写程序”变成了“先编译再运行”的工程化思路，适配企业自托管/隐私受限环境，也能减少 token 成本和抖动。
- 局限性或待验证点：
  - 对函数表达能力边界依赖于 FuzzyBench 覆盖度；
  - 复杂任务是否仍需 fallback 到 full LLM 尚不明朗；
  - 安全审计时需关注 adapter 权重是否稳定污染输入。
- 对后续研究/应用的启发：可将 PAW 与 tool-use、workflow policy 一起组成“LLM-as-compiler”服务层，在本地优先编译高频任务，只有剩余长尾任务走在线大模型。
- 一句适合 Obsidian 快速浏览的中文总结：PAW 把部分 LLM 应用从“在线智力输出”改造成“离线可复用模型插件”，更像软件工程里的编译优化。

## 标准化研究框架
**Research question：** 对于模糊但高频的函数级任务，是否存在比每次调用都调用 LLM 更高效且可靠的参数化执行路径？

**Literature：** 现有提示工程与 function calling 关注单次调用质量；本研究等价于把“任务语义 + 编译器”视为一个可训练管线，以降低重复成本。

**Theory：** 如果函数语义可被稳定压缩为轻量权重空间，则 inference cost 可由`per-token`模型转为`per-function`建模，后者在高复用场景下更优。

**Hypotheses：**
1. 编译后的神经 artifact 可以在任务准确率上保持可接受性能；
2. 在重复执行场景中总成本显著下降；
3. 复用 artifacts 后可提升隐私边界与离线可部署性。

**Method：** 构建 fuzzy-function 编程流程；训练 4B compiler；在冻结解释器上蒸馏/生成 adapters；基于 FuzzyBench 做横向比较。

**Data and Analysis：** 使用 FuzzyBench 10M 示例覆盖报警、清洗、排序等任务；比较 PAW 与直接 prompting 在性能、延迟、内存和可复用性上的差异。

**Findings：** PAW 在性能可比基础上显著降低推理内存和算力开销，并提升重复执行效率。

**Conclusion：** 对高重复、低确定度任务，LLM function compiler 路线是可行且高性价比的替代架构，可与传统 agentic pipeline 形成互补。
