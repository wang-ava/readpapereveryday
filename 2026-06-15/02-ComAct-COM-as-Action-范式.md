# ComAct: Reframing Professional Software Manipulation via COM-as-Action Paradigm

ComAct 的核心贡献不是再做“更强 GUI 视觉识别”，而是把专业软件操控的交互机制改写成可程序合成的 COM 动作语义，避免 GUI 自动化链条中的视觉脆弱性。对于工业 CAD、设计软件等高价值工具场景，这一思路能显著减少长链路误操作。

- **论文标题**：ComAct: Reframing Professional Software Manipulation via COM-as-Action Paradigm
- **作者/机构**：Jiaxin Ai, Tao Hu, Xuemeng Yang, Shu Zou, Hairong Zhang, Daocheng Fu, Yu Yang, Hongbin Zhou, Nianchen Deng, Pinlong Cai, Zhongyuan Wang, Botian Shi, Kaipeng Zhang, Licheng Wen（未在论文页完整展开机构清单；属于软件工程 + AI 交叉方向）
- **发布日期/版本日期**：2026-06-11（`v1`）
- **主题标签**：#LLM #Agent #SoftwareEngineering #COM #Tools #Benchmark
- **论文链接**：<https://arxiv.org/abs/2606.13239>
- **PDF 链接**：<https://arxiv.org/pdf/2606.13239v1>
- **项目/代码/数据链接（如可得）**：该条目当前公开页未给出项目页或代码仓库链接；暂缺 `Code/Data`。
- **核心问题**：GUI-based 软件代理在长流程任务中易出现定位漂移和执行失效，而 API 方式又受制于异构协议和不可访问接口，导致专业软件自动化长期不稳定。
- **方法概要**：
  1. 提出 COM-as-Action：将界面操作重述为对 Component Object Model 的程序化动作生成问题。
  2. 设计 ComCADBench：作为工业 CAD 软件代理评测基准，检验跨长时程软件操控的成功率和准确率。
  3. 构建 ComActor：三阶段自我纠错学习框架，专门弥补语法正确但几何精度不足的执行缺口。
  4. 给出 ComForge：用于 Windows 容器内大规模训练的软件工具链（按论文描述）。
- **主要贡献**：
  1. 提出了一个可执行且可工程化的“确定性程序式软件交互”范式。
  2. 给出了 ComCADBench 这一面向真实工业软件的长程基准。
  3. 实验证明 COM 化执行可显著优于纯 GUI 管道，尤其在长链路任务中鲁棒性提升明显。
- **关键实验或结果**：
  - 论文报告 frontier 模型在 GUI 路径下几乎失效，但在 COM-as-Action 管线下显著提升。
  - ComActor 在 ComCADBench 上取得 SOTA，并在外部 CAD 基准上展现一定泛化能力。
- **适合关注的原因**：
  1. 与“LLM agent 调工具”最常见痛点高度吻合。
  2. 从问题定义上绕开了传统 GUI 代理最脆弱的视觉环节，工程收益明确。
  3. 对企业软件自动化、运维脚本生成、数字孪生工作流具有明确迁移空间。
- **局限性或待验证点**：
  1. 公开页面缺少代码与数据细节，复现门槛较高。
  2. 方案对 Windows COM 生态友好，对其他平台兼容性需要补充。
  3. 专业软件的授权、版本差异会影响 benchmark 结果稳定性。
- **对后续研究/应用的启发**：可以把“GUI 自动化”问题系统性迁移到“接口动作编译”问题：在企业 IT 场景里，agent 的动作空间先语义化，再绑定真实执行器。
- **Obsidian 快速浏览的一句总结**：ComAct 的价值在于把软件 agent 的交互重构为“可编程动作”，把长流程软件操作从视觉噪声里解耦出来。

## 标准化研究框架
- **Research question：** 在商业化专业软件中，能否通过统一动作抽象替代视觉 GUI 步骤，让 LLM Agent 更稳定地完成长链路任务？
- **Literature：** 对标软件代理工具使用、GUI-agent 与自动化基准（如 SWE/SWE-bench 类任务）路线，但转向 COM 过程化编排，属于“交互表示学习”新分支。
- **Theory：** 不以经典统计模型为主，等价于系统架构假设：把操作定义为可组合原语（action primitives）可提高可复现性与确定性。
- **Hypotheses：** COM 级动作表示能减少视觉噪声导致的失败，并提高长时程任务成功率；三阶段自纠错训练可进一步提升几何与执行精度。
- **Method：** 设计 ComCADBench 基准，比较 GUI 与 COM 两条执行路径，训练 ComActor 并在不同任务长度和软件场景下做基准对比。
- **Data and Analysis：** 以 ComCADBench 与外部 CAD benchmark 的任务轨迹为主要分析对象，关注成功率、稳定性、几何正确性与长链路失效率。
- **Findings：** COM-as-Action 在该类任务上明显优于 GUI 传统范式，且错误修复能力（自我纠错）对高难度任务有实效性。
- **Conclusion：** 对于高价值软件工具链，问题并不只是“让模型会问”，而是“定义可执行、可验证的动作空间”；该工作提供了可迁移思路。
