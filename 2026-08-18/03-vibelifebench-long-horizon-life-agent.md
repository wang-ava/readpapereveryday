# VibeLifeBench: Can Your Life Agent Be Proactive and Persistent in a Living World?

Spotlight：VibeLifeBench 直接把 LLM agent 从“被动问答”改成“持续监测+计划执行+约束维护”任务，暴露了当前主流 life agent 在长期真实场景中的普遍不足。

## 论文信息
- 论文标题：VibeLifeBench: Can Your Life Agent Be Proactive and Persistent in a Living World?
- 作者（机构）：Xiaohongshu Inc（机构即公司，未见细分作者单位）
- 发布日期：2026-08-11（v1）
- 主题标签：`#LLM` `#Agent` `#LongHorizon` `#Benchmark` `#Autonomy` `#LLM-Eval`
- 论文链接：[https://arxiv.org/abs/2608.10875v1](https://arxiv.org/abs/2608.10875v1)
- PDF 链接：[https://arxiv.org/pdf/2608.10875v1](https://arxiv.org/pdf/2608.10875v1)
- 项目/代码/数据链接（如可得）：Hugging Face 数据集： [https://huggingface.co/datasets/EvolventAI/Vibelifebench](https://huggingface.co/datasets/EvolventAI/Vibelifebench)

## 论文内容
- 核心问题：现有 agent benchmark 通常短周期、静态环境，无法评估生活助手是否能持续主动、守住隐含约束并处理“世界在背后变化”。
- 方法概要：构建 200 个长期任务、10 个生活领域，任务按周时间线展开，模拟 22 个服务的动态世界。评分机制使用 1247 个原子级检查点（fine-grained），按最终状态、执行时效、隐式约束达成度加权。
- 主要贡献：
  - 第一次把“持续沉默监听/自发复检”纳入生活助理 benchmark 评估。
  - 在多模态长时程任务中统一“时间线评分”与“原子检查”标准，强调可审计性。
  - 显示当前主流模型在该设定下普遍低分，为评测指标升级提供基线。
- 关键实验或结果：
  - 在 200 个任务上测试 7 个 frontier model，普遍表现偏低，暴露长期自主性不足。
- 适合关注的原因：
  - 对构建长期 agent 产品（私人助理、任务总监、客服、运营代理）有直接标准意义。
- 局限性或待验证点：
  - 数据与环境主要围绕模拟服务，对真实异构企业系统还需接入层验证。
  - 模拟世界的噪声和冲突是否覆盖真实多代理竞争场景仍有待检验。
- 对后续研究/应用的启发：
  - Agent 研发应从“单次任务成功率”转向“跨周期目标一致性与隐式约束保持率”。
- Obsidian 快速浏览一句总结：**该 benchmark 证明：真实生活助理更重要的是“保持任务连贯”，而非“临时回答正确”。**

## 标准化研究框架
**Research question：** 长周期、自动推进世界下，LLM Agent 的 proactive 与 persistent 能力是否可被系统性量化？

**Literature：** 先前评测多聚焦短时检索/问答。VibeLifeBench 将长期任务管理、隐式约束与世界变化纳入单一框架，是从静态 benchmark 向动态 benchmark 的关键补齐。

**Theory：** 代理的任务效能不是瞬时答题准确率，而是其在时间推进下维持“目标-状态-承诺一致性”的能力；可通过事件序列的状态一致性与时效性检验表示。

**Hypotheses：**
- H1：加入“silent world mutation”机制将显著区分目前模型的长期跟踪能力；
- H2：现有高分模型在短任务上优先但在长期情境仍容易失效；
- H3：任务可验证性越高（可读后验约束越明确），跨模型差距越稳定。

**Method：** 构建 200 条任务时间线、22 种服务绑定与 1247 条自动核验规则；对 7 个主流模型运行并按同一 contract 打分。

**Data and Analysis：** 使用发布的任务包（Version 1.1.0）进行统一评估；关注阶段完成率、时序偏差、隐式限制满足度、失败回滚行为。

**Findings：** 当前 frontier model 在该设置下整体不足，说明“长期自主+被动感知”仍是 Agent 评估盲点。

**Conclusion：** 本研究等价于把 benchmark 定义扩展为“时间维度”，对 LLM Agent 的真实落地能力评测提供了新标准。 
