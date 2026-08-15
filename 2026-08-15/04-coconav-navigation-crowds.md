# CoCoNav: Conformal Control for Safe Robot Navigation in Crowds

> Spotlight：CoCoNav 通过“在线 conformal 校准 + 软约束先生成 + 事后验证”的组合，缓解人群动态预测漂移导致的控制器振荡与不可行问题。

- 论文标题：CoCoNav: Conformal Control for Safe Robot Navigation in Crowds
- 作者（机构）：Cheng Guo, Mingzhe Ni, Zheng Liang, Yihu Ling, Yuan Hu, Michele Caprio, Daniele Pucci, Wei Pan（arXiv 页面未给出机构）
- 发布日期（版本日期）：2026-08-07（arXiv v1）
- 主题标签：`#Embodied` `#RobotNavigation` `#ConformalPrediction` `#MPC` `#Safety`
- 论文链接：[https://arxiv.org/abs/2608.07751](https://arxiv.org/abs/2608.07751)
- PDF 链接：[https://arxiv.org/pdf/2608.07751v1](https://arxiv.org/pdf/2608.07751v1)
- 项目/代码/数据链接（如可得）：未公开（arXiv 页面未给出）
- 核心问题：人群导航中环境预测误差会随时间变化，如何在保持可行性的同时减少碰撞并维持效率？
- 方法概要：
  - 引入在线 conformal calibration，按时间视界动态调整轨迹误差边界。
  - 使用 horizon-specific conformal PI controller 去调节覆盖率和保守程度。
  - 采用 relax-then-verify 流程：先软约束生成名义轨迹，再对其进行硬约束认证，并保留 contingency 备选轨迹。
- 主要贡献：
  - 解决了 MPC 因硬约束 infeasible 导致的执行停滞问题。
  - 以控制器内校准替代固定保守 margin，更好处理非平稳预测误差。
  - 在仿真与四足机器人实验中展示安全性与效率兼顾的策略。
- 关键实验或结果：
  - 相比 baseline，提升了在人群场景中的碰撞规避成功率与任务达成稳定性。
  - 相对更直接的 reactive 与静态约束方法，出现更低振荡、更平滑轨迹。
- 适合关注的原因：框架可直接应用于仓储、服务机器人等真实复杂环境，且不要求完整重建环境模型。
- 局限性或待验证点：
  - 源码与超参数公开不足，工程复现门槛较高。
  - 在不同城市户外复杂动态行人流中的泛化能力需要更多闭环验证。
- 对后续研究/应用的启发：
  - 可探索把 conformal bound 与语义地图结合，形成双层安全保证。
  - 可用于多机器人协同导航中对临界风险进行资源优先级调度。
- 适合 Obsidian 快速浏览的中文总结：CoCoNav 让“安全导航”从静态保守策略转为概率校准驱动的动态可信控制。

## 标准化研究框架

**Research question：** 在动态人群环境中，是否能通过在线误差覆盖率校准，使导航控制既可行又稳定。 

**Literature：** 与传统 reactive/CBF 或确定性 MPC 相比，该文强调误差分布随时间漂移，需持续校准而非一次性硬编码。

**Theory：** 本质上将环境不确定性转化为可验证的边界约束，再通过验证器过滤不安全名义轨迹。

**Hypotheses：**
- H1：动态边界优于固定边界。
- H2：先生成后验证可显著减少 infeasible 导致的控制退化。
- H3：在密集人群中能提升成功率与轨迹平滑性。

**Method：** 计算 horizon-specific conformal interval，结合 PI controller 与 soft-MPC 规划；执行前进行硬约束验证与后备动作选择。

**Data and Analysis：** 采用仿真 + 四足实验场景，指标包含碰撞率、任务完成、路径长度/效率与验证通过率。

**Findings：** 框架在多个场景中显示更稳健的安全/效率权衡，验证了“校准驱动的验证型控制”可行。

**Conclusion：** CoCoNav 提供了可复用的 robust navigation 模式，适用于高波动环境中的具身智能部署。

**Note：** 本文属于具身控制研究，不是传统社会科学实验，字段中的 *Hypotheses/Findings* 主要指控制策略假设与执行指标检验。
