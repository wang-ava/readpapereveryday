# LabOSBench: Benchmarking Computer Use Agents for Scientific Instrument Control

LabOSBench 针对真实科学仪器控制难以重复、风险高、成本大的问题，给出可复用的网页化模拟基准。它把“科学仪器操作代理”从难以量化的实验现场环境，迁移到可规模化、可复现实验的 benchmark 框架。

- **论文标题**：LabOSBench: Benchmarking Computer Use Agents for Scientific Instrument Control
- **作者/机构**：Anqi Zou, Han Deng, Chengyu Zhang, Junquan Hu, Yu Wang, Yuxiang Xing, Aokai Zhang, Hanling Zhang, Zhaoyang Liu, Ben Fei, Zhihui Wang, Wanli Ouyang（arXiv 页面未统一列出机构信息）
- **发布日期/版本日期**：2026-06-15（v1）
- **主题标签**：#AI4S #Agent #Benchmark #ComputerUseAgents #ScientificInstruments
- **论文链接**：<https://arxiv.org/abs/2606.16802>
- **PDF 链接**：<https://arxiv.org/pdf/2606.16802v1>
- **项目/代码/数据链接（如可得）**：主页/代码链接未在当前版本明确给出；建议关注论文更新与附录附带链接。
- **核心问题**：现有 computer-use benchmark 多集中于软件/虚拟系统任务，难以覆盖科学仪器的反馈驱动、多步操作、参数调优与安全约束。
- **方法概要**：
  1. 构建八类科学仪器 web 模拟器组成的套件，避免高风险真实硬件实验。
  2. 通过浏览器驱动方式统一评测接口，支持子任务与端到端工作流配置。
  3. 设置 96 个子任务，覆盖样品装载、对位、参数调节、数据采集到结果检查。
- **主要贡献**：
  1. 明确将 Scientific Instrument Control 引入 computer-use 评测问题。
  2. 提供规模化可复现测试场景，兼顾安全性与可控性。
  3. 对比多类 VLM/GUI agent 与 agentic 框架，形成可复用基线。
- **关键实验或结果**：
  - 在端到端与子任务层面均观察到现有模型在结构化步骤上可达一定能力，但反馈驱动操作与长链路任务表现弱。
  - 实验支持“高可控模拟 + 任务编排”能够更真实暴露科学场景中代理链路断裂点。
- **适合关注的原因**：
  1. 以低风险方式覆盖 AI4S 中最昂贵最关键的使用场景。
  2. 对实验室自动化、远程控制、科研助手工具评测具有直接迁移价值。
  3. 为“模型能否支撑复杂仪器流程”提供统一量化口径。
- **局限性或待验证点**：
  1. Web 模拟与真实硬件之间仍有操作延迟、物理扰动与故障注入差异。
  2. 缺少开源数据集规模、版本与分布细节披露。
  3. 目前未见公开代码入口，复现实验门槛较高。
- **对后续研究/应用的启发**：
  可用于构建科学设备类“任务目录化 benchmark”，并作为企业实验室数字孪生与 agent 部署前的安全回归测试。
- **Obsidian 快速浏览的一句总结**：LabOSBench 用网页化仪器模拟器把科学实验控制变成可复现实验的代理评测任务，是 AI4S 的一条低风险落地路径。

## 标准化研究框架
- **Research question：** 如何将科学仪器控制中的高风险、低可复现场景，转化为可量化且可复现的代理基准？
- **Literature：** 对齐 computer-use benchmark、工具代理评测和实验自动化任务设计文献，补齐了“仪器级任务”空白。
- **Theory：** 采用任务拆分与层级评测（子任务+整链路）的方法论，属于实验评估工程框架，不是传统统计因果模型。
- **Hypotheses：** 若提供可复现实验环境和固定交互协议，则可更客观比较不同 agent 在反馈驱动、长链路任务中的差距。
- **Method：** 构建 96 子任务与 8 类模拟器，统一通过 browser 接口采集执行日志并按分层指标评估。
- **Data and Analysis：** 按 subtask 与 end-to-end 两级对比多个模型类别，分析成功率差异和任务断裂模式。
- **Findings：** 即便模型能完成大量结构化步骤，仍在反馈驱动与长链路阶段显著掉线，说明该 benchmark 捕捉了关键瓶颈。
- **Conclusion：** 本研究框架等价于“任务化、可复现的评测设计框架”；不以社会科学假设检验为主，而是关注工程可测评性与泛化应力测试。
