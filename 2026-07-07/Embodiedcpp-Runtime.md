# Embodied.cpp: A Portable Inference Runtime of Embodied AI Models on Heterogeneous Robots

**Spotlight：**
相比大量实验室级示例代码，本工作更像“工程级运行时”设计，聚焦可落地的异构机器人部署问题。对于已有 VLA / WAM 的团队，这是把研发验证成本压低到更接近生产的尝试。

- 论文标题：Embodied.cpp: A Portable Inference Runtime of Embodied AI Models on Heterogeneous Robots
- 作者/机构（如可得）：Ling Xu, Chuyu Han, Borui Li, Hao Wu, Shiqi Jiang, Ting Cao, Chuanyou Li, Sheng Zhong, Shuai Wang；arXiv 元数据未直接给出机构（可从 PDF 补充）
- 发布日期或版本日期：2026-07-02（v1）
- 主题标签：`#EmbodiedAI` `#Robotics` `#InferenceRuntime` `#Systems`
- 论文链接：[https://arxiv.org/abs/2607.02501](https://arxiv.org/abs/2607.02501)
- PDF 链接：[https://arxiv.org/pdf/2607.02501](https://arxiv.org/pdf/2607.02501)
- 项目/代码/数据链接：项目仓库：[https://github.com/SEU-PAISys/Embodied.cpp](https://github.com/SEU-PAISys/Embodied.cpp)
- 核心问题：现有 embodiment 推理栈过于模型碎片化，无法在异构边缘设备/机器人上统一满足多速率闭环控制、batch-1 低延迟和统一 I/O 抽象。  
- 方法概要：提出一个 C++ portable runtime，围绕 input adapters、sequence builders、backbone execution、head plugins、deployment adapters 5 层结构，兼容 VLA 与 WAM 的运行约定并支持多速率执行。  
- 主要贡献：
  - 给出可跨不同底层模型的统一执行路径；
  - 明确面向闭环控制的推理约束（而非纯服务推理）；
  - 给出轻量部署优化指标：任务成功率与内存峰值。
- 关键实验或结果：在 VLA 模型上验证闭环任务执行成功率：HY-VLA 为 100%，pi0.5 为 91%；WAM 基准块内存从 312.2 MiB 降至 88.1 MiB。  
- 适合关注的原因：当前 embodied stack 往往瓶颈在部署而非算法，本文直接切中该层问题；兼容异构硬件有利于从实验室扩展到真实设备。  
- 局限性或待验证点：当前公开结果主要集中在初步 WAM benchmark，任务复杂度、长时稳定性与安全边界仍需更大规模验证。  
- 对后续研究/应用的启发：可用于统一企业内的机器人模型服务层，搭建“统一调度+设备感知优化”架构；对端到端学习模型上层部署有明显工程迁移价值。  
- 适合 Obsidian 快速浏览的一句话总结：通过统一 C++ runtime 抽象，Embodied.cpp 让不同机器人/芯片上部署多种 Embodied AI 成为更低成本路径。

## 标准化研究框架

- **Research question：** 能否构建一个与模型无关、面向闭环控制的 Embodied AI 推理运行时，并兼顾异构硬件效率？  
- **Literature：** 关联 VLA/WAM 部署、嵌入式推理优化、机器人控制栈标准化；与传统服务端推理框架相比，多了一层 real-time 与 I/O 一致性要求。  
- **Theory：** 若将推理过程分层抽象并显式绑定控制节拍与接口约束，可减少重复适配工作并提高跨设备可移植性。  
- **Hypotheses：** 统一 runtime 可在不牺牲准确率的前提下显著提升成功率稳定性与资源效率。  
- **Method：** 提出五层运行时抽象并在 VLA 与 WAM 上做统一部署实验（含闭环测试），比较任务成功率与内存占用。  
- **Data and Analysis：** 采用公开论文内的两类 VLA（HY-VLA、pi0.5）与 1 个 WAM 预览基准，分析执行成功率和内存压缩比。  
- **Findings：** 在所测任务上，运行时带来高成功率与显著内存下降，支持“统一运行时可优于逐模型定制”假设。  
- **Conclusion：** 本文的标准化框架字段可等同为系统工程验证框架；对于社会科学式假设检验并不直接适用，关键在于跨系统复现与工程量化指标。

