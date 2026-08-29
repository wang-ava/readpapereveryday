# Personalized Privacy Control in LLMs via Attention Head Intervention

通过在推理阶段直接干预注意力头，P3Bench 以“可个性化隐私策略”框架把模型的隐私泄露控制从统一上下文规则改造为用户特定偏好控制。

## 论文标题
Personalized Privacy Control in LLMs via Attention Head Intervention

## 作者/机构
- 作者：Junseok Kim；Nakyeong Yang；Kyomin Jung
- 机构：arXiv 摘要页未披露。

## 发布日期/版本日期
- 提交日期：2026-08-21 15:22:20 UTC
- 版本：v1

## 主题标签
#LLM #Privacy #AttentionHead #Inference-TimeControl #PromptAlignment

## 论文链接
- https://arxiv.org/abs/2608.21209v1

## PDF 链接
- https://arxiv.org/pdf/2608.21209v1.pdf

## 项目/代码/数据链接（如可得）
- 代码：未公开（页面未给出）
- 数据/Benchmark：文中提出 P3Bench（个性化隐私保护基准），但摘要页未给出公开仓库链接

## 核心问题
LLM 在上下文隐私控制上只能做到“上下文统一规则”约束，难以处理同一上下文下不同用户差异化的隐私偏好。现有 prompt 级策略容易违反用户个性化要求，导致大量用户偏好失守。

## 方法概要
- 提出 personalized privacy 的定义：将隐私边界显式建模为“用户特定偏好”。
- 构建 P3Bench，用于扩展传统上下文隐私基准。
- 提出 `Repair` 推理期注意力头干预策略：在解码阶段利用注意力头进行行为约束，把不符合个性化策略的输出概率偏离拉回。

## 主要贡献
1. 将“隐私控制”问题从上下文通用化约束提升到用户个人化偏好约束。
2. 系统性指出 prompt 级方法在 personalized privacy 上的失效率高的问题。
3. 给出一类可直接嵌入推理阶段的 head-level 干预机制，替代全模型再训练方案。

## 关键实验或结果
- Qwen2.5-7B 与 Gemma3-4B 在基线 prompt 策略下出现显著偏离，policy ignorance ratio 分别为 **51.25%** 与 **74.28%**。
- `Repair` 方法显著降低模型未遵循用户偏好的失败案例（文中称“显著改善”）。
- 实验显示方法对 personalized privacy 约束更稳定，且不依赖于重训。

## 适合关注的原因
- 该工作直接面向“模型对真实用户可控性不足”这一真实产品痛点，比静态对齐策略更贴近企业落地中的个性化合规需求。

## 局限性或待验证点
- 摘要内未给出跨语言、多任务、长会话上下文的泛化指标。
- 偏好表达假设较结构化，若用户偏好语义模糊或冲突，干预机制的稳定性待验证。
- 缺少对机构/部署方规模化评估（如不同安全策略下的吞吐影响）。

## 对后续研究/应用的启发
- 可把 personalized privacy 作为“policy-aware decoding layer”的标准化模块，并与检索、工具调用策略结合。
- 后续可在客户端/企业策略引擎侧引入偏好模板推理，形成可审计的“隐私合规回放”链。

## 适合 Obsidian 快速浏览的中文总结
将隐私对齐从“同一上下文统一规范”升级为“按用户偏好约束”的推理期控制，提示：可在不重训的情况下降低隐私策略违规。

## 标准化研究框架
**Research question：** 在不重训或低成本改造的条件下，能否通过注意力头级推理干预，实现 LLM 输出对用户个体化隐私规则的稳定遵循？

**Literature：** 先前工作主要聚焦 context-aware 隐私与 prompt 级规则控制，但对“同场景不同用户偏好”的细粒度约束支持不足。该文通过个体化定义弥补这一空缺。

**Theory：** 个体化偏好可看作对输出行为的隐式约束分布。若推理阶段可动态调节关注源，模型对隐私违规行为的采样概率可被系统性压低。

**Hypotheses：** 1）仅依赖 prompt 难以满足高差异化偏好约束；2）头级干预可在保持原有模型能力的同时显著降低 policy ignorance；3）个性化约束可跨模型复用。

**Method：** 构造个性化隐私基准 P3Bench；定义偏好执行度指标；设计 Repair 的注意力头干预策略并在推理时注入；比较 prompt 基线与 Repair 在多模型上的偏离率。

**Data and Analysis：** 采用 P3Bench 任务与多模型（文中至少 Qwen2.5-7B、Gemma3-4B）进行对比，基于 policy ignorance ratio 和输出一致性指标做量化。

**Findings：** personalized context 条件下，基线 prompt 失败率高，而 Repair 能显著提高偏好遵循率；该机制在所测模型上均出现显著改善。

**Conclusion：** 在隐私控制强场景中，inference-time 的头部干预是可复用、低改造成本的一条实用路径。
