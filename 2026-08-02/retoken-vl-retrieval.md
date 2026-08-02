# ReToken: One Token to Improve Vision-Language Models for Visual Retrieval

Spotlight：`ReToken` 用一个可学习的单 token 作为检索目标，在长视觉上下文中选择 query 相关的稀疏 token 子集，实现视觉检索提效：不必重训庞大骨干，也能在图片与视频检索上拿到稳定增益。

- 论文标题：ReToken: One Token to Improve Vision-Language Models for Visual Retrieval
- 作者：Yao Xiao, Reuben Tan, Zhen Zhu, Yuqun Wu, Jianfeng Gao, Derek Hoiem
- 机构（如可得）：arXiv 元信息未直接披露机构
- 发布时间：2026-07-30（v1）
- 主题标签：`#CV` `#VLM` `#VisualRetrieval` `#EfficientAI` `#Memory`
- 论文链接：[https://arxiv.org/abs/2607.28627v1](https://arxiv.org/abs/2607.28627v1)
- PDF 链接：[https://arxiv.org/pdf/2607.28627v1](https://arxiv.org/pdf/2607.28627v1)
- 项目/代码/数据链接：[@GitHub](https://github.com/avaxiao/ReToken)

## 核心问题
视觉模型在长上下文中常受干扰 token 激增影响，既推理成本高、又可能造成检索性能下降。如何用较小改动提升在长序列下的检索质量？

## 方法概要
提出 `ReToken` 作为显式可学习 embedding，训练时作为检索目标引导模型从预填充视觉 KV cache 中选择 query-relevant 的稀疏 token。该方法偏向“轻量改造”：核心模型参数基本不动，只加入可学习目标与选取机制。

## 主要贡献
- 首次系统化引入单 token 查询机制用于视觉 token 稀疏化选择。
- 兼容长图像、长视频场景下的 VLM 推理流程，降低对大规模重训的依赖。
- 在多模型、多任务上做系统比较，证明了跨模型可迁移性。

## 关键实验或结果
- Visual Haystacks 上，Qwen3VL-8B 提升 13.4 分，InternVL3.5 提升 12.4 分。
- LVBench 长视频零样本迁移中，Qwen3VL-8B 提升 8.0 分。
- 训练和长视频推理可在单卡 H100 完成，工程落地成本较低。

## 适合关注的原因
这篇工作把 attention 级别优化转化为工程友好的“可插拔模块”，适合在部署受限场景（GPU 成本、延迟约束）下先行尝试；尤其对长视频检索、视觉文档理解与多模态问答服务有直接可复用价值。

## 局限性或待验证点
- 训练集规模较小（摘要提及小规模 image-QA），跨域泛化边界尚待验证。
- 当前未完整披露不同硬件下的成本/延迟曲线。
- 复杂多模态场景下 query 多义性仍可能导致稀疏选择失效。

## 对后续研究/应用的启发
- 可与 token pruning、cache compaction 及 reranker 组成检索服务的“二层控制面”。
- 适合进一步研究对齐机制，把 ReToken 与 user-intent feedback 结合实现动态稀疏率控制。

## Obsidian 快速浏览总结
一句话：`ReToken` 通过一个 learnable token 把长视觉上下文检索从“全量吃掉”改为“关键 token 抽取”，在效果和计算成本间取得更好平衡。

## 标准化研究框架
- **Research question：** 在不显著重训主干模型的情况下，如何改善长视觉上下文中的检索性能与推理效率？
- **Literature：** 对接长期以来的视觉 token 压缩、检索增强与上下文效率优化研究。
- **Theory：** 假设 query-relevant token 可以被一个可学习目标向量显式调度并保留决策所需信息。
- **Hypotheses：** 稀疏 token 选择若保持关键证据覆盖率，则可在固定算力下同时提升指标并压缩推理开销。
- **Method：** 学习一个检索导向 embedding（ReToken），用于从 visual KV cache 中抽取子集，再在 Qwen3VL/InternVL 等模型中执行检索任务。
- **Data and Analysis：** 在 Visual Haystacks 与 LVBench 上做跨模型评测，比较单模型和 zero-shot 场景。
- **Findings：** ReToken 在公开基准上有稳定正向收益，并对长视频检索提供明显帮助。
- **Conclusion：** 这是一个工程上可迁移的高性价比方向，但需进一步验证多域鲁棒性与失败情形。
