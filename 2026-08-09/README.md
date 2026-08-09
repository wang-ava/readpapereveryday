# 2026-08-09 AI 论文分享

> 今日聚焦“Agent 的结构化工具决策、具身 AI 的行为泛化、以及仿真评测可复现性”三条线：Agent/tooling、具身导航与感知、以及 safety evaluation。所有论文均为 2026-07-30 到 2026-08-01 期间发布的近期 arXiv 工作。

## 推荐顺序

1. **[HyperAgent: Planning and Acting over Tool-Schema Hypergraphs for Tool-Use LLM Agents](./hyperagent-tool-schema-hypergraph.md)**  
   **Spotlight：** HyperAgent 将工具关系显式图谱化，让 LLM Agent 从“盲猜工具链”转向“状态驱动的 schema 约束规划”，在任务完成率、调用效率上更可控。
   [论文](https://arxiv.org/abs/2608.02650) · [PDF](https://arxiv.org/pdf/2608.02650)

2. **[Embodied Passive Aeroacoustic Perception Enables Relative Sensing and Pursuit Between Aerial Robots](./embodied-passive-aeroacoustic-perception.md)**  
   **Spotlight：** SonicFly 把飞行自噪声转成观测量，实现无需外部通信与 GPS 的空中相对感知与追踪，展示了被动声学的新型协同策略。
   [论文](https://arxiv.org/abs/2608.00401) · [PDF](https://arxiv.org/pdf/2608.00401) · [项目页](http://generalroboticslab.com/SonicFly)

3. **[X-NavDP: Generalizing Navigation Diffusion Policy to Novel Behavior and Embodiments with Group Q-score Reweighted Matching](./x-navdp-group-qscore.md)**  
   **Spotlight：** GQRM 把 diffusion policy 后训练转成“组级重加权”问题，显著改善新行为与异构机器人上的导航成功率。
   [论文](https://arxiv.org/abs/2607.28560) · [PDF](https://arxiv.org/pdf/2607.28560) · [项目页](https://yty-sky.github.io/x-navdp-project-page)

4. **[WM-Cov: Test Adequacy for Interactive World-Model-Style Autonomous Driving Simulation](./wm-cov-interactive-testing-coverage.md)**  
   **Spotlight：** 本文把自动驾驶世界模型评测从“事件计数”转成“证据充分性”度量，强调预算下有效证据而非表面失败数量。
   [论文](https://arxiv.org/abs/2608.00298) · [PDF](https://arxiv.org/pdf/2608.00298)

5. **[ACE-Data-0: Human-Centric Ambient Capture as Embodied Data Engine](./ace-data-0-embodied-data-engine.md)**  
   **Spotlight：** ACE-Data-0 用同构的多模态时空采集框架构建大规模家庭交互数据，强化了具身模型在接触/遮挡/长时序场景下的验证基础。
   [论文](https://arxiv.org/abs/2607.28625) · [PDF](https://arxiv.org/pdf/2607.28625) · [项目页](https://ace-data-engine.github.io/ACE-Data-0/)

## 阅读提示

- **先看 HyperAgent / X-NavDP**：一个从工具调用、一个从导航策略，分别覆盖 Agent 与具身系统的可泛化性设计。
- **再看 SonicFly / WM-Cov**：前者看感知硬件-算法联合，后者看评测范式，适合补齐系统工程视角。
- **最后看 ACE-Data-0**：若你在做 imitation / world model，数据工程和 benchmark 设计这篇最值得借鉴。
