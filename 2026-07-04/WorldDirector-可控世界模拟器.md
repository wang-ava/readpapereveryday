# WorldDirector：带持久记忆的可控世界模拟器

WorldDirector 的核心价值是把视频世界模型中的动作和视角控制显式解耦，并在长序列中保持对象外观与语义一致。它面向的是“可控生成”而非只会接龙式续帧，尤其适合需要可检查、可复现视频世界演化的研究。

- 论文标题：WorldDirector: Building Controllable World Simulators with Persistent Dynamic Memory
- 作者/机构（如可得）：Hanlin Wang；Hao Ouyang；Qiuyu Wang；Wen Wang；Qingyan Bai；Ka Leong Cheng；Yue Yu；Yixuan Li；Yihang Meng；Zichen Liu；Yanhong Zeng；Yujun Shen；Qifeng Chen
- 发布日期或版本日期：2026-07-02T17:59:59Z（arXiv v1）
- 主题标签：#CV #WorldModel #VideoGeneration #WorldSimulation
- 论文链接：[https://arxiv.org/abs/2607.02517v1](https://arxiv.org/abs/2607.02517v1)
- PDF 链接：[https://arxiv.org/pdf/2607.02517v1](https://arxiv.org/pdf/2607.02517v1)
- 项目/代码/数据链接（如可得）：项目页：[https://worlddirector.github.io/](https://worlddirector.github.io/)
- 核心问题：传统 world model 常把动力学与渲染强耦合，缺乏长时记忆与可控视角，导致对象身份会在遮挡后漂移、场景连贯性不足。
- 方法概要：先用 LLM 协调 3D 运动与镜头轨迹，再把轨迹作为控制信号驱动视频生成；通过持久动态记忆模块维持对象身份与状态，使离场后重入仍保持一致。
- 主要贡献：
  1. 明确提出 semantic motion orchestration 与 rendering 解耦框架；
  2. 在 world simulation 中引入持久动态记忆机制以强化跨时间一致性；
  3. 输出更可控且物理逻辑更稳的长视频生成流程。
- 关键实验或结果：
  - 能在离开视野后的延时恢复中保持对象外观一致；
  - 支持复杂、扩展时间的事件合成，提升可控性；
  - 通过项目页展示多个可控指标和场景示例。
- 适合关注的原因：生成式世界模型走向可部署应用时，用户最需要的是“可控性”和“可复现性”；该方法把两个长期痛点直接作为建模目标。
- 局限性或待验证点：
  - 模型复杂度与长时计算成本仍需在真实系统中验证；
  - 对复杂交互物理规律的泛化范围未在摘要中充分给出；
  - 与现有 3D 物理约束模型的融合仍待量化。
- 对后续研究/应用的启发：可用于强化学习模拟器、数据合成、数字孪生场景的可控回放模块，尤其适用于“先规划再渲染”的 pipeline。
- 一句适合 Obsidian 快速浏览的中文总结：WorldDirector 不仅生成画面，还把“世界怎么走”变成可编程变量。

## 标准化研究框架
**Research question：** 如何让视频世界模型在长时间生成中保持对象身份一致且支持精细动作/视角控制？

**Literature：** 传统世界模型偏重连续像素预测；本研究等价于把控制策略显式化为可编程轨迹，并用记忆模块维护状态归一。

**Theory：** 当运动语义与渲染分离时，控制变量不再完全淹没在像素级优化中，能够降低长时依赖漂移并提高可控性。

**Hypotheses：** 解耦控制与渲染可提高目标可达性与身份一致性；持久记忆可减少遮挡后重入失真。

**Method：** 用 LLM 产生高层轨迹指令，输入 world director 控制器，渲染模块按轨迹合成视频；通过遮挡重入等测试场景评估一致性。

**Data and Analysis：** 在公开合成与自建场景上测试长时事件重放，比较连续性、身份保持率、控制偏差与主观可控性。

**Findings：** 与传统一体式世界模型相比，该方法提高了对象身份和语义连续性，并改善用户对时间长度与视角的控制能力。

**Conclusion：** 论文支持“可控世界建模”应在架构层面分解为运动语义 + 渲染解码，并配合持久记忆模块实现长期一致。
