# From Runnable to Verifiable: An Independent Reproducibility Study of LLM/Agent-Driven Vulnerability Validation Artifacts

这篇工作并不只做“模型能力比较”，而是把 LLM/agent 生成的安全研究产物放进可验证框架，强调 artifact 的“可运行性、可复现实验性、可语义确认性”分层审计。

## 论文标题
From Runnable to Verifiable: An Independent Reproducibility Study of LLM/Agent-Driven Vulnerability Validation Artifacts

## 作者/机构
- 作者：Bo Chen
- 机构：arXiv 页面未在作者行显示机构信息。

## 发布日期/版本日期
2026-08-10（v1，提交于 13:05:02 UTC）

## 主题标签
#Agent #Security #Reproducibility #LLM #Vulnerability

## 论文链接
- https://arxiv.org/abs/2608.09567

## PDF 链接
- https://arxiv.org/pdf/2608.09567.pdf

## 项目/代码/数据链接
- 项目页/代码：未在 arXiv 页面直接披露
- 数据：以 104-paper corpus 为核心样本集合；anchor benchmark 为 arXiv:2509.24037（论文中提到）

## 核心问题
LLM/agent 驱动的漏洞验证链路常停留在“可发布 artifact”。如何区分“可下载”“可运行”“可复现实验”“语义上可验证”这四类不同可信度？

## 方法概要
- 对 2023–2026 年相关文献做系统排查，形成 104 篇共识语料（consensus corpus）。
- 定义分层验证协议（R0/R1，后续可修复流程，G1–G3 语义证据等级）。
- 使用 patched-counterfactual 和 matched negative control 进行语义确认。
- 把可重复性从“能跑起来”升级为“能被语义反证”。

## 主要贡献
1. 将 reproducibility 从单一执行状态扩展为多层证据标准。 
2. 以预注册协议给出可复用的 artifact 审计框架。 
3. 量化了 artifact 可运行性与语义有效性之间的巨大落差。

## 关键实验或结果
- 59/104（56.7%）论文有 public artifact，但 R0 可完整执行率仅 55.6%，R1 修复后 61.1%。
- 58/102（56.9%） anchor case 的 CVE 标识存在不一致问题。 
- 在 30 个有信号样本中有 20 个在 patched build 仍产生 claimed signal，表明可复现性证据可能虚假阳性。
- 7/19 matched negative control 在非恶意输入下仍触发，提示 oracle 信号存在较高假阳性。

## 适合关注的原因
它把“能否复现”定义得更严格，特别适用于自动化安全工具和 Agent-based 红蓝对抗流程。对于 LLM agent 工作流，这种审计框架可显著降低误导性漏洞宣称风险。

## 局限性或待验证点
- 研究局限于已检索到的安全文献与漏洞语料，领域外泛化待测。
- 多数结果来自 exploratory study，仍需扩大样本与时间窗口验证稳健性。 
- 文中流程较重，实际企业接入有运维成本。

## 对后续研究/应用的启发
- 对安全 Agent 工具链应加入“可验证日志+反事实测试”作为默认 Gate。
- 可复用其 protocol 作为企业安全研发的 artifact 上线前检查清单。
- 为 AI 4S/安全治理提供可审计的评价模板，避免“可运行幻觉”。

## 适合 Obsidian 快速浏览的中文总结
一句话：这篇文章提醒我们，LLM/agent 安全产物要从“可执行”走向“可验证”，否则容易产生大量伪阳性的可复现性承诺。

## 标准化研究框架
**Research question：** 在漏洞验证工作流中，如何建立可量化的标准，将 artifact 的可获取性、可运行性与语义有效性分开评估？

**Literature：** 相比传统 reproducibility 仅关注复现指标，本文补充语义层验证（语义与语义反例）与分层修复流程，在 AI security 审计中具有方法学价值。

**Theory：** 将 artifact 可信度建模为多层验收过程：可访问性、可执行性、结果稳定性与语义归因，逐层淘汰虚假阳性。

**Hypotheses：** 使用 R0/R1 与 G1–G3 级审计会显著降低“能跑但不可信”的样本比率，并区分真正高质量 artifact 与噪声 artifact。

**Method：** 通过共识语料筛选与预注册流程，对每条 artifact 执行基线复现、修复、patched-counterfactual 与 negative control，并记录失败类型。

**Data and Analysis：** 数据基于 104-paper corpus 与 anchor benchmark（arXiv:2509.24037）；分析关注可运行比例、语义确认成功率、误报率与流程修复增益。

**Findings：** “可运行但不可验证”样本占比显著，且 CVE 一致性和 oracle 特异性问题突出；R1 能修复部分样本，但并未根治语义级偏差。

**Conclusion：** 安全 AI 领域应将验证协议系统化并自动化，尤其在 LLM Agent 生产链路中，预注册+反事实验证对可信度提升至关重要。 
