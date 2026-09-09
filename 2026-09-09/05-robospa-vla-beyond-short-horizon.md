---
spotlight: "把 VLA 评测从单次成功率扩展到空间推理和长程规划，暴露了当前模型在复杂操控中的真实短板。"
---

# RoboSPA: Can VLA Models Go Beyond Simple Scenes and Short-Horizon Tasks?

## 基本信息
- **论文标题**：RoboSPA: Can VLA Models Go Beyond Simple Scenes and Short-Horizon Tasks?
- **作者**：Zhenxuan Fan, Bo Zhang, Yutong Lin, Yuqian Yuan, Juekai Lin, Liang Liang, Zhuoyi Huang, Wenqiao Zhang, Juncheng Li, Siliang Tang, Jun Xiao, Yueting Zhuang
- **机构**：arXiv 元数据中未公开
- **发布日期 / 版本日期**：2026-09-04（v1）
- **主题标签**：`Embodied` `VLA` `Robotics` `Benchmark` `长程推理`
- **论文链接**：https://arxiv.org/abs/2609.05324
- **PDF 链接**：https://arxiv.org/pdf/2609.05324
- **项目/代码/数据链接**：https://github.com/fanzhenxuan/RoboSPA

## 核心问题
现有 Vision-Language-Action 基准往往偏重短时、固定场景评估，难以揭示真实任务中的空间关系推理和长程规划能力。本文要回答：模型能否在更复杂场景与程序流程下仍保持行为稳定性？

## 方法概要
- 构建 RoboSPA 数据集与评测协议：
  - 两大维度：
    - Fine-Grained Spatial Reasoning（细粒度空间推理）
    - Long-Horizon Procedural Planning（长程过程规划）
  - 10 类任务，56 个基任务，5 个难度层次，共 280 组变体。
- 收集 527K 轨迹，覆盖多种机器人 embodiment 与多场景分布。
- 除二元成功率外引入更细粒度诊断指标。

## 主要贡献
- 给出了一个面向 embodied benchmark 的高覆盖任务矩阵。
- 将 VLA 评测从“能否完成单目标”扩展到“如何在复杂过程内保持准确执行”。
- 提供大规模公开轨迹，支持对模型泛化、失败模式的可解释比较。

## 关键实验或结果
- 在代表性 VLA 模型上的实验发现：
  - 复杂空间关系处理仍是瓶颈；
  - 精细执行（低级动作）错误率高；
  - 长程记忆/规划仍显薄弱。
- 数据表明新 benchmark 可以显著区分模型在“短期任务”和“复杂场景任务”上的性能差异。

## 适合关注的原因
该数据集把“会不会把一个任务做完”升级为“能否在多约束场景中持续正确执行”，非常适合检验企业实际机器人部署前的模型能力。

## 局限性或待验证点
- 当前主要聚焦操控任务范式，路径导航、行走操作等其他具身技能的覆盖仍有限。
- 多 embodiment 采集虽充分，但不同硬件平台的泛化边界尚需跨域验证。

## 对后续研究/应用的启发
- 可用于训练阶段的难度 curriculum：先低难度再逐步引入复杂空间-程序维度。
- 对安全边界设计有帮助：可将失败类型（空间偏差、程序中断、记忆失配）转为可控触发条件。

## 一句话中文速览总结
RoboSPA 把 VLA 的短平快任务评测拉回真实难题，暴露了长程空间-过程推理仍是当前模型关键短板。

## 标准化研究框架
- **Research question：** VLA 模型在高空间复杂度与长程任务下是否仍保持稳定策略？
- **Literature：** 既有 benchmark 通常以 success rate 为主，缺少对空间关系、跨步骤依赖和程序记忆的细粒度刻画。
- **Theory：** 具身智能需要同时优化局部控制和全局程序一致性，两者失衡会导致高成功率掩盖脆弱性。
- **Hypotheses：**（1）在复杂场景下成功率下降更明显；（2）空间关系和过程记忆错误是主要失效源；（3）诊断型指标可比单成功率更敏感地区分模型。
- **Method：** 设计双维度任务矩阵与多难度变体，采集大规模轨迹并定义任务成功以外的行为诊断指标。
- **Data and Analysis：** 280 变体（10 类×56 基任务×5 难度）与 527K 轨迹；对比多个代表性 VLA 在各维度成功率和诊断指标。
- **Findings：** 长程规划与精细执行仍是明显瓶颈，表明现有模型在现实操作复杂度下有较大改进空间。
- **Conclusion：** RoboSPA 将具身评测推向更复杂任务空间，为 VLA 的模型改造和安全部署提供了更贴近真实的检验标准。

