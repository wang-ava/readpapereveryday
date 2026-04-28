# 2026-04-28 每日论文推荐

今日共推荐 20 篇论文：10 篇 AI4Health + 10 篇 纯AI。所有论文均为首次收录，无历史重复。

---

## AI4Health 论文（10篇）

| # | 论文名称 | 主题 | 年份 | 论文链接 |
|---|---------|------|------|---------|
| 1 | BiomedCLIP | 医学视觉语言模型 | 2023 | https://arxiv.org/abs/2303.00915 |
| 2 | PathChat | 病理图像AI助手 | 2024 | https://arxiv.org/abs/2312.08816 |
| 3 | GatorTron | 临床大语言模型 | 2022 | https://arxiv.org/abs/2203.03540 |
| 4 | CheXNet | 胸部X光深度学习 | 2017 | https://arxiv.org/abs/1711.05225 |
| 5 | Virchow | 病理图像基础模型 | 2024 | https://arxiv.org/abs/2309.07778 |
| 6 | ClinicalBERT | 临床NLP/再入院预测 | 2019 | https://arxiv.org/abs/1904.05342 |
| 7 | MedVersa | 多任务医学影像AI | 2024 | https://arxiv.org/abs/2405.07988 |
| 8 | DNABERT-2 | 基因组语言模型 | 2023 | https://arxiv.org/abs/2306.15006 |
| 9 | SegVol | 3D医学图像分割 | 2023 | https://arxiv.org/abs/2311.13385 |
| 10 | Med-Flamingo | 少样本医学多模态 | 2023 | https://arxiv.org/abs/2307.15189 |

### AI4Health 分类

**医学影像诊断**
- CheXNet（2017）——胸部X光14种疾病检测，AI首超放射科医生
- MedVersa（2024）——单一模型处理所有医学影像任务

**病理图像分析**
- PathChat（2024）——病理学多模态对话AI，Nature发表
- Virchow（2024）——150万病理切片预训练，Nature Medicine发表

**医学视觉语言模型**
- BiomedCLIP（2023）——1500万对医学图文，医学领域CLIP

**临床大语言模型**
- GatorTron（2022）——8.9亿参数，90亿词临床文本预训练
- ClinicalBERT（2019）——BERT适配临床笔记，再入院预测

**医学多模态（少样本）**
- Med-Flamingo（2023）——交错图文输入的少样本医学VLM

**医学图像分割**
- SegVol（2023）——文字+空间双提示的3D CT分割基础模型

**基因组学**
- DNABERT-2（2023）——136个物种，BPE分词的多物种DNA语言模型

---

## 纯AI 论文（10篇）

| # | 论文名称 | 主题 | 年份 | 论文链接 |
|---|---------|------|------|---------|
| 1 | Vision Transformer (ViT) | 视觉基础模型 | 2020 | https://arxiv.org/abs/2010.11929 |
| 2 | Segment Anything (SAM) | 可提示图像分割 | 2023 | https://arxiv.org/abs/2304.02643 |
| 3 | Stable Diffusion 3 | 文字生成图像 | 2024 | https://arxiv.org/abs/2403.03206 |
| 4 | Whisper | 鲁棒语音识别 | 2022 | https://arxiv.org/abs/2212.04356 |
| 5 | DINOv2 | 自监督视觉特征 | 2023 | https://arxiv.org/abs/2304.07193 |
| 6 | Toolformer | LLM工具调用 | 2023 | https://arxiv.org/abs/2302.04761 |
| 7 | LLaVA | 视觉指令微调 | 2023 | https://arxiv.org/abs/2304.08485 |
| 8 | Self-RAG | 自反思检索生成 | 2023 | https://arxiv.org/abs/2310.11511 |
| 9 | Gemma 2 | 知识蒸馏开源LLM | 2024 | https://arxiv.org/abs/2408.00118 |
| 10 | ORPO | 无参考模型偏好优化 | 2024 | https://arxiv.org/abs/2403.07691 |

### 纯AI 分类

**视觉基础模型**
- ViT（2020）——把图像当词序列处理，Transformer统治计算机视觉的起点
- SAM（2023）——可提示零样本分割，视觉AI的"GPT时刻"
- DINOv2（2023）——自监督学出超越有监督的通用视觉特征

**生成模型**
- Stable Diffusion 3（2024）——MMDiT + 整流流，文字渲染重大突破
- Whisper（2022）——68万小时弱监督，99语言鲁棒语音识别

**多模态学习**
- LLaVA（2023）——GPT-4生成数据，第一个开源视觉指令跟随模型

**工具调用与智能体**
- Toolformer（2023）——AI自学使用5种外部API工具，自我监督训练

**检索增强生成**
- Self-RAG（2023）——自主决定何时检索、自我审核输出可信度

**高效训练与对齐**
- Gemma 2（2024）——知识蒸馏让9B模型超越70B，Google开源
- ORPO（2024）——无需参考模型的一阶段偏好优化，简化对齐流程
