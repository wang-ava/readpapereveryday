# 2026-05-08 每日论文推荐索引

> 共 20 篇论文，10 篇 AI4Health，10 篇纯 AI  
> 今日重点：生物医学NLP基础、多模态医学AI、癌症预测；LLM统一框架、Agent推理、检索增强生成

---

## AI4Health 方向（10 篇）

### 📁 Biomedical-NLP（生物医学NLP）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| BioGPT | 2022 | 微软研究院 | 首个超越人类水平的生物医学生成式GPT，在PubMedQA达到78.2%（人类78.0%）| [报告](AI4Health/Biomedical-NLP/2026-05-08-BioGPT.md) |
| PubMedBERT | 2020 | 微软研究院 | 从零用PubMed文本训练BERT，证明领域预训练优于通用迁移，9个基准全面超越BioBERT | [报告](AI4Health/Biomedical-NLP/2026-05-08-PubMedBERT.md) |
| PMC-LLaMA | 2023 | 上海AI实验室 | 在LLaMA上用480万PMC全文继续预训练，开源医学LLM，MedQA达64%超越ChatGPT | [报告](AI4Health/Biomedical-NLP/2026-05-08-PMC-LLaMA.md) |
| HuatuoGPT | 2023 | 香港中文大学 | 双源数据（真实医患对话+ChatGPT蒸馏）+ 医学专用RLHF奖励模型，中文医学对话优化 | [报告](AI4Health/Biomedical-NLP/2026-05-08-HuatuoGPT.md) |

### 📁 Medical-Multimodal-AI（多模态医学AI）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| Med-PaLM M（Towards Generalist Biomedical AI） | 2023 | Google DeepMind | 首个在14个医学任务上达到专家级的多模态AI，发布MultiMedBench综合评测基准 | [报告](AI4Health/Medical-Multimodal-AI/2026-05-08-Towards-Generalist-Biomedical-AI.md) |

### 📁 Medical-Imaging-Robustness（医学影像鲁棒性）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| REMEDIS | 2022/2023 | Google Research | 两阶段预训练（互联网CLIP + 医学SimCLR），仅需1/32标注数据即可媲美全监督基线 | [报告](AI4Health/Medical-Imaging-Robustness/2026-05-08-REMEDIS.md) |

### 📁 Cancer-Survival-Analysis（癌症生存预测）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| MCAT | 2021 | 哈佛医学院 | 多模态协同注意力Transformer，融合病理WSI图像和基因组数据，6种癌症生存预测全面超越单模态 | [报告](AI4Health/Cancer-Survival-Analysis/2026-05-08-MCAT.md) |

### 📁 Cardiology-ECG-AI（心电图AI）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| ECG-FM | 2024 | 多机构合作 | 首个开源心电图基础模型，166万条ECG预训练，掩码信号建模+对比学习，房颤检测AUC 0.953 | [报告](AI4Health/Cardiology-ECG-AI/2026-05-08-ECG-FM.md) |

### 📁 Drug-Protein-Design（药物设计与蛋白质设计）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| TxGNN | 2023/2024 | 哈佛/斯坦福 | 生物医学知识图谱+GNN，零样本预测罕见病药物治疗关系，Nature Machine Intelligence | [报告](AI4Health/Drug-Protein-Design/2026-05-08-TxGNN.md) |
| ProteinMPNN | 2022 | 华盛顿大学（Baker Lab）| 消息传递神经网络设计蛋白质序列，实验成功率52%，速度比Rosetta快200倍，Science发表，2024诺贝尔化学奖相关 | [报告](AI4Health/Drug-Protein-Design/2026-05-08-ProteinMPNN.md) |

---

## 纯 AI 方向（10 篇）

### 📁 LLM-Architecture（LLM架构）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| T5 | 2019/2020 | Google Brain | 统一文本到文本框架，C4数据集，11B参数刷新GLUE/SuperGLUE/SQuAD等多项记录 | [报告](AI/LLM-Architecture/2026-05-08-T5.md) |
| FLAN | 2021/2022 | Google Research | 指令微调：62个NLP任务的指令微调让137B模型零样本超越GPT-3 175B | [报告](AI/LLM-Architecture/2026-05-08-FLAN.md) |

### 📁 Reasoning-Agents（推理与Agent）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| ReAct | 2022/2023 | 普林斯顿/Google | 思考-行动-观察交替循环，现代AI Agent的基础范式，HotpotQA提升6个点 | [报告](AI/Reasoning-Agents/2026-05-08-ReAct.md) |
| Tree of Thoughts | 2023 | 普林斯顿/DeepMind | 多分支思维树+搜索算法，24点游戏正确率从4%跃升至74%，LLM系统规划能力新标杆 | [报告](AI/Reasoning-Agents/2026-05-08-Tree-of-Thoughts.md) |
| Reflexion | 2023 | 东北大学/MIT | 语言版强化学习：失败后用自然语言反思代替参数更新，HumanEval编程91%、无需训练 | [报告](AI/Reasoning-Agents/2026-05-08-Reflexion.md) |

### 📁 Evaluation-Benchmarks（评估基准）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| MMLU | 2020/2021 | UC Berkeley | 57学科14000+题的专业知识测评，2020年GPT-3仅43.9%，现成AI能力标尺 | [报告](AI/Evaluation-Benchmarks/2026-05-08-MMLU.md) |

### 📁 Retrieval-Augmented-Generation（检索增强生成）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| RAG | 2020 | FAIR/UCL | DPR+BART端到端检索生成，知识密集任务最优，现代RAG系统的开山之作，NeurIPS 2020 | [报告](AI/Retrieval-Augmented-Generation/2026-05-08-RAG.md) |

### 📁 Self-Supervised-Vision（自监督视觉）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| MAE | 2021/2022 | Meta AI | 遮住75%图像块进行重建，ViT-H/14达ImageNet 87.8%，视觉自监督预训练新范式，CVPR 2022 | [报告](AI/Self-Supervised-Vision/2026-05-08-MAE.md) |

### 📁 Multimodal-Generation（多模态生成）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| DALL-E 3 | 2023 | OpenAI | 合成描述文字重标注训练数据，从根本上解决文字-图像对齐，ChatGPT图像生成核心引擎 | [报告](AI/Multimodal-Generation/2026-05-08-DALL-E-3.md) |
| BLIP-2 | 2023 | Salesforce | 冻结视觉+语言两端，只训练1.88亿参数Q-Former桥接，1/16计算量达到多模态SOTA，ICML 2023 | [报告](AI/Multimodal-Generation/2026-05-08-BLIP-2.md) |

---

## 今日阅读建议

### 入门路线（从基础开始）

```
MMLU → T5 → FLAN → RAG → ReAct
```
先了解AI的评测标准，再看统一语言模型架构，再看指令微调，再看如何用外部知识增强AI，最后看AI如何行动。

### 医学AI路线

```
PubMedBERT → BioGPT → PMC-LLaMA → HuatuoGPT → Med-PaLM M
```
从领域预训练的基础，到生成式医学NLP，到开源本地部署，到中文医学对话，到多模态医学通才。

### 技术深度路线

```
MAE → BLIP-2 → DALL-E 3 → MCAT → ProteinMPNN
```
从视觉自监督，到多模态桥接，到图像生成改进，到医学多模态融合，到蛋白质设计，展示深度学习在科学领域的前沿应用。

---

*报告语言：中文（面向初学者）| 涵盖背景知识、方法、结论和局限性*  
*生成日期：2026-05-08*
