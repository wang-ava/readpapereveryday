**Spotlight：** DELTA 将表格结构和 OCR 拆开，再让 TarQA 对紧凑结构文本进行问答，提供可定位错误的文档理解路线。关键阅读点是结构分数与端到端可用性之间的差距：OCR 仍是明显瓶颈。

# Tables Decoded: DELTA for Structure, TARQA for Understanding

## 论文信息

- 作者：Jahanvi Rajput、Dhruv Kudale、Saikiran Kasturi、Utkarsh Verma、Ganesh Ramakrishnan。
- 机构：Indian Institute of Technology Bombay、BharatGen。
- arXiv 发布日期：2026-09-15，v1；页面标注 WACV 2026 已接收，属于近期 arXiv 上线，不能称为本周首次提出的研究。正文将模型名写作 TarQA。
- 阅读范围：arXiv 摘要、正文方法与实验、第 7 节局限；未运行代码。
- 主题标签：#AI论文 #CV #文档智能 #表格理解 #多语言 #LLM
- [论文](https://arxiv.org/abs/2609.17458v1) · [PDF](https://arxiv.org/pdf/2609.17458v1) · [正文](https://arxiv.org/html/2609.17458v1)
- 项目/代码/模型/数据：[作者提供的 Tables-Decoded 仓库入口](https://github.com/Tihiitborg/Tables-Decoded)。论文称发布模型及 TORQUE；本次未验证所有下载工件是否齐全。

## 核心问题

复杂表格含有合并单元格、结构关系和不同文字系统。能否把图像中的结构与文字可靠转换成文本，再交给 LLM 推理，同时让错误来源更容易定位？

## 方法概要

DELTA 分离物理结构、逻辑结构与 OCR，输出表格后转为 OTSL；OTSL 用紧凑序列编码单元格关系和内容。TarQA 基于 LLaMA-3-8B-Instruct，以不同序列格式微调；同一问答流程可替换 OCR 与结构模块。OTSL 是已有表示，本文的贡献包含转换方法和整合评估，而非发明 OTSL。[来源：第 3–4 节](https://arxiv.org/html/2609.17458v1)

## 主要贡献

提出双重解耦的表格重建流程；比较 HTML、纯文本和 OTSL 对下游问答的影响；提供印地语 TORQUE，包含 210 张表与 422 个人工核验问答，补充低资源文字场景。

## 关键实验或结果

| 任务与指标 | 本文报告 | 应如何解读 |
| --- | --- | --- |
| WTQ，ANLS | TarQA-OTSL 56.5；TarQA-HTML 42.3 | 同系列格式差异为 14.2 分；摘要 9.3 分对应与 UDOP 47.2 的比较 |
| FinTabNetQA，relieved accuracy | DELTA + TarQA-OTSL 45.2；列出基线最高 36.0 | 对应摘要提升 9.2 个百分点；输入真实 OTSL 时为 69.2，不能作为实际端到端结果 |
| TORQUE，relieved accuracy | 本方法 27.49；Qwen-2.5-VL 47.40 | 本方法并非第一；不能据此宣称全面胜过 VLM |
| FinTabNet 表格重建 | TEDS-S 98.2；完整 TEDS 55.9 | 高结构质量不代表文字与内容同样准确 |

以上分别来自正文表 3–7，指标不可跨行直接比较。[来源：正文实验表](https://arxiv.org/html/2609.17458v1#S5)

## 适合关注的原因

适合文档问答、科研表格抽取和多语言信息处理。模块拆分让结构错误、OCR 错误和推理错误能够分别检查，对工程调试比单一最终分数更有帮助。

## 局限性或待验证点

实验语言主要是英语与印地语，TORQUE 规模有限且来源集中。OCR 造成明显误差传播；真实输入与 ground-truth 输入的差距是改进空间，不能当作已实现效果。比较涉及不同模型、预训练和输入来源，尚不足以证明模块化普遍优于端到端模型；新一代基线与复杂抽象问答仍值得重测。

## 对后续研究/应用的启发

在论文表格抽取流程中保存 OTSL 与图像单元格对应关系，低置信内容交给人工核验。建议联合报告结构、字符、数值单位和下游回答准确率；对中文科研表格的有效性需另建测试，不能直接由印地语结果推出。

## 中文快速总结

> 先把表格变成可核查的结构文本再问答很有潜力，但最终质量仍取决于 OCR 和真实输入。

## 标准化研究框架

**Research question：** 解耦结构识别、文字识别并使用紧凑表示，能否提高表格问答与跨文字系统的适用性？

**Literature：** 基于表格结构识别、OCR、OTSL、VLM 文档理解及文本表格问答；延续模块化与端到端路线的比较，见正文第 2 节。

**Theory：** 等价于工程机制：显式结构减少序列冗余，模块化使不同错误可分开优化；并非严格的性能保证定理。

**Hypotheses：** 等价于可检验设计预期：OTSL 比 HTML 更适合该微调设置，解耦支持跨文字迁移；没有社会科学式预注册假设检验。

**Method：** DELTA 重建、HTML 到 OTSL 转换、TarQA 微调、格式消融与多基准比较。

**Data and Analysis：** FinTabNet、PubTabNet、PubTables、WTQ、FinTabNetQA、TORQUE；分别用 TEDS-S/TEDS、ANLS、EM 与 relieved accuracy 衡量结构和回答。

**Findings：** OTSL 微调优于本实验 HTML 版本，但完整重建受 OCR 限制，TORQUE 上仍落后于 Qwen-2.5-VL。

**Conclusion：** 可调试的结构文本路线值得复用；多语言普适性和端到端优越性需更强对照与更广语言验证。
