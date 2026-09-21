> **Spotlight：** 自蒸馏训练后变强，并不自动说明教师看到的答案或解题过程提供了额外价值。本文用答案匹配的参考材料与无参考对照，把两种收益分开衡量。

# What Does Privileged Information Add to On-Policy Self-Distillation?

## 基本信息

- 作者：XiuYu Zhang、Wei Chow、Junfeng Fang、Zhenkai Liang、Tat-Seng Chua。
- 机构：National University of Singapore。
- 发布/阅读版本：2026-09-17，arXiv v1；笔记日期：2026-09-21（Asia/Shanghai）。
- 主题标签：#AI #LLM #SelfDistillation #Reasoning #ControlledExperiments
- 论文：[arXiv](https://arxiv.org/abs/2609.20612)；[PDF](https://arxiv.org/pdf/2609.20612v1)；[正文](https://arxiv.org/html/2609.20612v1)。
- 项目/代码：[opsd-reference-study](https://github.com/xiuyuz/opsd-reference-study)；数据：[AMPLE-Math](https://huggingface.co/datasets/xiuyuz/ample-math)。两页面本次可访问，未运行代码。
- 核验范围：摘要、实验协议、表 1、结果与讨论。

## 核心问题

教师拥有学生看不到的参考信息时，学生收益有多少超出了自蒸馏本身？参考材料越完整，是否就越有用？

## 方法概要

冻结模型副本作为教师，对学生生成的前缀给出监督。AMPLE-Math 为 5,319 道数学题构造六种共享答案的参考视图，并设无参考对照。主要配置是教师开启 thinking、学生训练时直接回答、评估时开启 thinking；所以无参考也仍有模式不对称。[研究设计 §2](https://arxiv.org/html/2609.20612v1#S2)

## 主要贡献

把“相对初始模型的提升”与“相对无参考蒸馏的增量”分开；数据和匹配干预也为研究参考形式、学生轨迹及训练阶段的交互提供了工具。

## 关键实验或结果

Qwen3-1.7B 在第 100 步的 Clean Solution 相对无参考增量为 1.30 个百分点，未校正区间为 [0.20, 2.41]，但未通过六种视图的 Holm 校正。SmolLM3-3B 的 Full Trace 在第 50 步增加 2 个百分点，到第 100 步各配置均低于初始模型。不能只报最有利 checkpoint。[结果 §3](https://arxiv.org/html/2609.20612v1#S3)

## 适合关注的原因

适合研究合成推理数据、蒸馏和训练归因的读者。其最大阅读价值是对照设计，能够防止将训练流程收益误记到某类数据上。

## 局限性或待验证点

证据限于两个模型家族的数学短程 LoRA 训练。长 thinking rollout 的比较同时改变推理模式、轨迹长度与受监督比例，不能单独推断“长思考有害”。主要指标 Avg@4 是四次采样正确率的平均，不是至少成功一次的 pass@4。

## 对后续研究/应用的启发

建议将无参考、错误参考和等算力训练列为基线；固定 checkpoint、输出预算和监督覆盖后再比较。可以研究随学生错误类型变化而调整参考内容，但这种自适应方案的优势尚待验证。

## 中文一句话总结

判断参考解答是否有用，要看它比无参考蒸馏多带来了什么。

## 标准化研究框架

**Research question：** privileged information 对 on-policy self-distillation 的独立增益是多少？

**Literature：** 联系 privileged information 学习、知识蒸馏与 OPSD；回应完整解题过程是否必然更利于学习的问题。

**Theory：** 等价机制解释是共享参数上的跨推理模式迁移；现有证据支持此解释，但未严格证明其为唯一机制。

**Hypotheses：** 以实验命题取代社会科学假设：更多参考推理是否增加增益、收益是否依赖学生轨迹与训练阶段？

**Method：** 答案匹配参考视图、无参考控制、跨家族比较与监督干预。

**Data and Analysis：** AMPLE-Math 和外部数学评估；配对问题级 bootstrap 区间及多重比较校正，区分不同采样指标。

**Findings：** 额外信息的增益并非单调；训练方式与 checkpoint 影响结论。

**Conclusion：** 应按学生实际增益选择参考形式，不能仅按教师获得的信息量判断价值。
