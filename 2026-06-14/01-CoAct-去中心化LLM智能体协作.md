# CoAct: A Minimal Coordination Substrate for Decentralized LLM Agents

CoAct 这篇工作将“多智能体协作是否可控”这件事落到系统设计上：它不靠复杂策略搜索，而是通过最小通信与同步提交机制，让分散的 LLM 智能体在共享状态下协作得更稳定、更可审计。

- **论文标题**：CoAct: A Minimal Coordination Substrate for Decentralized LLM Agents
- **作者/机构**：Zhenting Qi, Jack Fan, Karly Hou, Daisy Xinlei Lin, Satyaki Chakraborty, Mete Kemertas, Yu Yao, Sophia Simeng Han, Han Zheng, Zihan Wang, Xiangjun Wang, Himabindu Lakkaraju, Yilun Du（论文主页未统一披露完整机构信息）
- **发布日期/版本日期**：2026-06-02（Published / Last Modified：02 Jun 2026, FAGEN@ICML 2026）
- **主题标签**：#LLM #MultiAgent #Coordination #DecentralizedSystems #Communication
- **论文链接**：<https://openreview.net/forum?id=AvxJqW1X5>
- **PDF 链接**：<https://openreview.net/pdf?id=AvxJqW1X5>
- **项目/代码/数据链接（如可得）**：未在公开摘要页披露；当前条目未给出代码、数据集或主页链接。
- **核心问题**：分散式 LLM 智能体在多智能体协作中常出现“发现不可见、动作冲突、状态不可回放”的问题，导致局部探索虽然激进却难以形成稳定的群体决策。
- **方法概要**：
  1. 提出最小化的协作原语：
     - 紧凑共享内存（compact shared-memory）用于知识与发现的跨体共享；
     - 同步状态提交（stateful commitment）用于外部副作用动作前的共识对齐。
  2. 在每个智能体本地决策与全局动作执行之间加入同步点，避免并发写入导致的状态错位。
  3. 用统一的可重放日志规范化共享状态，提升后验审计与调试能力。
  4. 在多机制设置下比较“无同步”“有同步”“不同通信粒度”条件的规模效应。
- **主要贡献**：
  1. 将多智能体协作问题形式化为“通信表达 + 提交一致性”的双重工程瓶颈；
  2. 提出最小原语替代复杂协议，给出一套可直接嵌入现有 agent pipeline 的实现路径；
  3. 在实证上验证了通讯策略并非单调有效，适用条件与收益边界可被量化。
- **关键实验或结果**：论文中给出了分布式协作场景的 scaling 实验与案例，结论为：并非更多通讯越好；不同机制对协作收益和状态正确性有明显门槛效应。
- **适合关注的原因**：
  1. 距离“agent 性能提升”更多聚焦在“协作协议安全性与稳定性”
  2. 可直接用于复杂工具调用链路，减少多智能体系统因状态不一致引发的错误传播。
  3. 在 2026 年 LLM Agent 走向工程化部署阶段，协作原语的标准化尤为关键。
- **局限性或待验证点**：
  1. 当前披露多为稿件页摘要与部分评估结果，缺少更完整的任务列表与复现实验细则；
  2. 同步提交机制可能带来吞吐开销，需评估高负载下的效率下限；
  3. 对异步长时延环境与恶意智能体行为的鲁棒性仍需补充。
- **对后续研究/应用的启发**：可将该原语视作“agent infra API”的一部分，与工具沙箱、权限系统、回滚机制结合，形成可审计、可重放、可安全部署的 multi-agent runtime。
- **Obsidian 快速浏览一句总结**：CoAct 证明了智能体规模不是问题，问题往往是“共享状态太弱 + 动作提交不一致”，并提供了可落地的最小协调设计。

## 标准化研究框架
- **Research question：** 在不增加大量模型复杂度的前提下，如何通过最小协作原语提高去中心化 LLM 智能体在多智能体任务中的一致性与可审计性？
- **Literature：** 对齐于 agent 通信机制、工具调用协作与多智能体一致性控制文献，区别在于强调“可复用最小协议”而非任务特定策略。
- **Theory：** 将协作问题拆分为共享信息熵压缩与动作提交一致性约束，通过降低共享状态不确定性来减少后验冲突。
- **Hypotheses：** 最小共享记忆与同步提交会减少冲突率并提升跨智能体协作收益，且在适当粒度下可避免过度通讯开销。
- **Method：** 对比不同通信策略与提交策略，测量任务成功率、冲突率与状态一致性指标；观察规模增长下的收益-成本关系。
- **Data and Analysis：** 采用论文提供的多智能体任务设置与评测数据，围绕四类社会博弈与工具协作任务做横向比较；关注通信开销与鲁棒性。
- **Findings：** 协作收益并不随着“更强通信”单调增长，关键在于对齐可回放的共享状态与提交边界。
- **Conclusion：** 协调协议是可移植的系统级基建，而非模型级 trick；该思想对未来企业级 agent mesh 工程具备明确指导价值。
