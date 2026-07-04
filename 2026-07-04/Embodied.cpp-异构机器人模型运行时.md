# Embodied.cpp：异构机器人上的统一 VLA/WAM 推理运行时

这篇工作聚焦部署现实：当前 VLA/WAM 体系往往因框架碎片化导致难以在不同硬件闭环部署。Embodied.cpp 试图用统一 C++ runtime 把这一层整合起来。

- 论文标题：Embodied.cpp: A Portable Inference Runtime of Embodied AI Models on Heterogeneous Robots
- 作者/机构（如可得）：Ling Xu；Chuyu Han；Borui Li；Hao Wu；Shiqi Jiang；Ting Cao；Chuanyou Li；Sheng Zhong；Shuai Wang
- 发布日期或版本日期：2026-07-02T17:58:28Z（arXiv v1）
- 主题标签：#EmbodiedAI #Robotics #VLA #Runtime
- 论文链接：[https://arxiv.org/abs/2607.02501v1](https://arxiv.org/abs/2607.02501v1)
- PDF 链接：[https://arxiv.org/pdf/2607.02501v1](https://arxiv.org/pdf/2607.02501v1)
- 项目/代码/数据链接（如可得）：[https://github.com/SEU-PAISys/Embodied.cpp](https://github.com/SEU-PAISys/Embodied.cpp)
- 核心问题：现有服务化推理框架按批量请求设计，无法满足嵌入式闭环控制所需的低延迟、多速率、跨模型 I/O 一致性。
- 方法概要：抽象 VLA 与 WAM 的共享执行路径，构建五层 runtime：输入适配、序列构建、核心执行、头部插件、部署适配；在一个后端层支持多硬件和多机器人接口。
- 主要贡献：
  1. 从模型实现层给出“portable runtime”而非单模型脚本层封装；
  2. 支持多速率闭环执行与 batch-1 延迟优先策略；
  3. 为 heterogeneous edge device 提供统一接口，降低迁移成本。
- 关键实验或结果：
  - 在 HY-VLA 与 pi0.5 上实现 100.0% 与 91.0% 的任务成功率；
  - 在 WAM 测试中将 block memory 从 312.2 MiB 降到 88.1 MiB；
  - 在真实机器人与初步仿真实验中展示跨模型部署可行性。
- 适合关注的原因：具身 AI 往往卡在“模型能跑、系统跑不了”问题上；本文把系统架构问题当作研究对象，面向工程落地非常关键。
- 局限性或待验证点：
  - 评测案例规模仍偏小，任务类型覆盖有限；
  - 与更多商用机器人平台的兼容性仍需在社区生态中扩展验证；
  - 真实工业场景中的安全机制与 fail-safe 集成细节未展开。
- 对后续研究/应用的启发：适合作为构建统一 embodied-serving stack 的底座，也可与 sim2real 评估框架联合，统一比较不同硬件上的延迟-精度折中。
- 一句适合 Obsidian 快速浏览的中文总结：Embodied.cpp 体现了“具身模型价值不只在算法，而在可跨硬件稳定运行的 runtime 体系”。

## 标准化研究框架
**Research question：** 在异构机器人上，能否用一个统一运行时同时支持 VLA 与 WAM，并保持实时闭环表现？

**Literature：** 多数研究聚焦模型精度，工程部署依赖独立脚本；本研究把部署一致性视为关键科学问题之一。

**Theory：** 若将输入/序列/推理/部署分层并标准化接口，可减少重复移植成本，同时提升多模型并行扩展性与延迟可控性。

**Hypotheses：** 统一运行时可显著提高模型跨机器人迁移速度，并在典型任务上取得可比或更优的执行成功率。

**Method：** 设计 5 层 runtime 架构，在 HY-VLA、pi0.5 与 LingBot-VA Transformer block 上进行统一部署与对比评测。

**Data and Analysis：** 使用机器人控制任务与实时闭环指标（任务成功率、内存占用、控制频率）评估，多模型/多硬件下比较部署成本。

**Findings：** 统一层化运行时提高了部署成功率并显著压缩运行时内存，支持更低延迟控制。

**Conclusion：** 对工程化具身 AI 来说，模型能力需被 runtime 约束反哺，才能形成可复用生态。
