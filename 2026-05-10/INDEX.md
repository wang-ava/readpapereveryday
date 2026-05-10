# 2026-05-10 每日论文推荐索引

> 共 **20 篇**论文：10 篇 AI4Health + 10 篇纯 AI  
> 今日主题：医学视觉语言模型、开源医学LLM、DNA基础模型、计算病理学；CLIP视觉语言预训练、LLM对齐与安全、规模化定律、高效推理

---

## 🧬 AI4Health 方向（10 篇）

### 📁 Medical-VQA（医学视觉问答）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| LLaVA-Med | 2023 | Microsoft + CMU | 用 PubMed 图文+GPT-4 生成数据，一天训练出医学视觉问答AI；NeurIPS 2023 | [报告](AI4Health/Medical-VQA/2026-05-10-LLaVA-Med.md) |
| SkinGPT-4 | 2024 | Dartmouth | MiniGPT-4微调+5.3万皮肤病图像，交互式皮肤科诊断AI；npj Digital Medicine | [报告](AI4Health/Medical-VQA/2026-05-10-SkinGPT-4.md) |

### 📁 Open-Medical-LLM（开源医学LLM）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| Meditron-70B | 2023 | EPFL | Llama-2-70B + 480亿医学tokens继续预训练，超越GPT-3.5的开源医学LLM | [报告](AI4Health/Open-Medical-LLM/2026-05-10-Meditron-70B.md) |
| HuatuoGPT-II | 2024 | 香港中文大学（深圳）| 一阶段统一SFT代替两阶段RLHF，中文医学基准超越GPT-4 | [报告](AI4Health/Open-Medical-LLM/2026-05-10-HuatuoGPT-II.md) |

### 📁 Medical-Image-Segmentation（医学图像分割）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| MedSAM | 2024 | U. Toronto / MSKCC | 在157万医学图像-掩码对上微调SAM，首个通用医学图像分割基础模型；Nature Communications | [报告](AI4Health/Medical-Image-Segmentation/2026-05-10-MedSAM.md) |

### 📁 Computational-Pathology（计算病理学）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| PLIP | 2023 | Cornell / Harvard | 从Twitter病理学社区收集20万图文对做CLIP对比学习，强零样本病理分类；Nature Medicine | [报告](AI4Health/Computational-Pathology/2026-05-10-PLIP.md) |
| HIPT | 2022 | Harvard Medical School | 三层分级DINO自监督学习（256px→4096px→slide），无标注处理吉像素WSI；CVPR 2022 | [报告](AI4Health/Computational-Pathology/2026-05-10-HIPT.md) |

### 📁 Genomics（基因组学）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| Nucleotide Transformer | 2024 | InstaDeep / EMBL-EBI / BioNTech | 850物种基因组预训练DNA基础模型（500M-2.5B），18个基因组学任务SOTA；Cell Systems | [报告](AI4Health/Genomics/2026-05-10-Nucleotide-Transformer.md) |

### 📁 Radiology-AI（放射影像AI）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| RadFM | 2023 | 上海交通大学 | 同时处理2D（X光）和3D（CT/MRI）的通用放射学基础模型，构建110万图文对MedMD数据集 | [报告](AI4Health/Radiology-AI/2026-05-10-RadFM.md) |

### 📁 Biomedical-VLM（生物医学视觉语言模型）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| BiomedGPT | 2024 | UNC / Ohio State | 统一Seq2Seq架构，182M参数在9个生物医学任务上竞争性表现；Nature Medicine | [报告](AI4Health/Biomedical-VLM/2026-05-10-BiomedGPT.md) |

---

## 🤖 纯 AI 方向（10 篇）

### 📁 Vision-Language-Pretraining（视觉语言预训练）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| CLIP | 2021 | OpenAI | 4亿图文对对比学习，零样本ImageNet 76.2%，多模态AI的奠基之作；ICML 2021 | [报告](AI/Vision-Language-Pretraining/2026-05-10-CLIP.md) |

### 📁 RLHF-Alignment（RLHF与对齐）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| InstructGPT | 2022 | OpenAI | RLHF三阶段（SFT→奖励模型→PPO），1.3B模型胜175B GPT-3，ChatGPT直接前身；NeurIPS 2022 | [报告](AI/RLHF-Alignment/2026-05-10-InstructGPT.md) |
| Constitutional AI | 2022 | Anthropic | 用"宪法"原则让AI批评和修改自己，RLAIF减少人类标注需求，Claude的技术基础 | [报告](AI/RLHF-Alignment/2026-05-10-Constitutional-AI.md) |

### 📁 Scaling-Laws（规模化定律）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| Scaling Laws | 2020 | OpenAI | 幂律发现：模型越大越好，数据越多越好，GPT-3规模的理论基础 | [报告](AI/Scaling-Laws/2026-05-10-Scaling-Laws.md) |
| Chinchilla | 2022 | DeepMind | 推翻旧规模化法则：每个参数需要约20 tokens；70B Chinchilla > 280B Gopher；NeurIPS 2022 | [报告](AI/Scaling-Laws/2026-05-10-Chinchilla.md) |

### 📁 Multimodal-LLM（多模态LLM）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| Flamingo | 2022 | DeepMind | 冻结视觉+语言模型+交叉注意力桥接，交错图文少样本学习，16-shot超有监督SOTA；NeurIPS 2022 | [报告](AI/Multimodal-LLM/2026-05-10-Flamingo.md) |

### 📁 Efficient-Inference（高效推理）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| vLLM / PagedAttention | 2023 | UC Berkeley | 借鉴OS虚拟内存分页KV Cache，内存利用率96%+，2-4x推理吞吐；SOSP 2023 | [报告](AI/Efficient-Inference/2026-05-10-vLLM.md) |
| Speculative Decoding | 2023 | Google | 小模型猜测+大模型批量验证，数学保证同等输出质量，2-3x加速；ICML 2023 | [报告](AI/Efficient-Inference/2026-05-10-Speculative-Decoding.md) |

### 📁 Novel-Architecture（新型架构）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| RWKV | 2023 | 独立研究者 / 多机构 | 线性注意力兼顾Transformer并行训练+RNN O(1)推理，14B参数语言模型；EMNLP 2023 | [报告](AI/Novel-Architecture/2026-05-10-RWKV.md) |

### 📁 Open-Source-LLM（开源LLM）

| 论文 | 年份 | 机构 | 核心贡献 | 链接 |
|------|------|------|---------|------|
| LLaMA 2 | 2023 | Meta AI | 商业可用开源LLM（7B/13B/70B），2T tokens，双奖励模型RLHF，引爆开源LLM生态 | [报告](AI/Open-Source-LLM/2026-05-10-LLaMA-2.md) |

---

## 📁 文件结构

```
2026-05-10/
├── INDEX.md                                         ← 本文件
├── AI4Health/
│   ├── Medical-VQA/
│   │   ├── 2026-05-10-LLaVA-Med.md
│   │   └── 2026-05-10-SkinGPT-4.md
│   ├── Open-Medical-LLM/
│   │   ├── 2026-05-10-Meditron-70B.md
│   │   └── 2026-05-10-HuatuoGPT-II.md
│   ├── Medical-Image-Segmentation/
│   │   └── 2026-05-10-MedSAM.md
│   ├── Computational-Pathology/
│   │   ├── 2026-05-10-PLIP.md
│   │   └── 2026-05-10-HIPT.md
│   ├── Genomics/
│   │   └── 2026-05-10-Nucleotide-Transformer.md
│   ├── Radiology-AI/
│   │   └── 2026-05-10-RadFM.md
│   └── Biomedical-VLM/
│       └── 2026-05-10-BiomedGPT.md
└── AI/
    ├── Vision-Language-Pretraining/
    │   └── 2026-05-10-CLIP.md
    ├── RLHF-Alignment/
    │   ├── 2026-05-10-InstructGPT.md
    │   └── 2026-05-10-Constitutional-AI.md
    ├── Scaling-Laws/
    │   ├── 2026-05-10-Scaling-Laws.md
    │   └── 2026-05-10-Chinchilla.md
    ├── Multimodal-LLM/
    │   └── 2026-05-10-Flamingo.md
    ├── Efficient-Inference/
    │   ├── 2026-05-10-vLLM.md
    │   └── 2026-05-10-Speculative-Decoding.md
    ├── Novel-Architecture/
    │   └── 2026-05-10-RWKV.md
    └── Open-Source-LLM/
        └── 2026-05-10-LLaMA-2.md
```

---

## 📖 今日阅读建议

### 入门路线（完全新手）

```
Scaling Laws → Chinchilla → CLIP → InstructGPT → LLaMA 2
```

先理解"为什么AI需要规模"→ 再理解"最优训练策略"→ 再看"视觉+语言怎么结合"→ 再看"如何对齐AI行为"→ 最后看"开源AI生态"

### 医学AI路线

```
LLaVA-Med → Meditron-70B → HuatuoGPT-II → MedSAM → BiomedGPT
```

从"如何让通用VLM懂医学"→ 开源医学LLM的训练→ 中文医学LLM→ 医学图像分割→ 生物医学通才模型

### AI系统/工程路线

```
Speculative Decoding → vLLM → RWKV → Scaling Laws → Chinchilla
```

推理加速技术→ 内存管理优化→ 新型高效架构→ 训练规模定律

### AI安全/对齐路线

```
InstructGPT → Constitutional AI
```

从 RLHF 的基础，到 RLAIF 的进化，理解现代 AI 助手的对齐训练路线（包括 ChatGPT 和 Claude 的技术来源）

### 生物科学AI路线

```
Nucleotide Transformer → HIPT → PLIP → MedSAM → RadFM
```

DNA基础模型→ 病理图像的分层学习→ 病理图文对比学习→ 通用医学分割→ 放射学通才模型

---

## 去重说明

今日所有 20 篇论文均未在以下历史分支中出现：
- 2026-04-24：AlphaFold3, Med-Gemini, CONCH, UNI, ESM3, GigaPath, RetFound, BioMistral, MedPaLM2, CheXagent 等
- 2026-04-25：各类综述 + DeepSeek-R1 等
- 2026-04-28：BiomedCLIP, PathChat, GatorTron, CheXNet, Virchow, ClinicalBERT, MedVersa, DNABERT-2, SegVol, Med-Flamingo + ViT, SAM, SD3, Whisper, DINOv2, Toolformer, LLaVA, Self-RAG, Gemma 2, ORPO 等
- 2026-05-03：AlphaFold3, Med-Gemini, CONCH, CHIEF, EHRAgent, BioMistral, PathChat, MAIRA-2, MedImageInsight, RetFound + Mamba, KAN, Llama3, DeepSeek-V2, Mixtral, FA2, LoRA, GRPO, Gemma2, Qwen2 等
- 2026-05-04：GigaPath, UNI, ESMFold, scGPT, Evo, Med-Flamingo, BioMistral, MAIRA, BioViL-T, Uni-Mol + Mixtral8x7B, KAN, LLaVA, Whisper, QLoRA, GRPO, Phi-3, Flow-Matching, GQA, Voyager 等
- 2026-05-08：BioGPT, PubMedBERT, PMC-LLaMA, HuatuoGPT, Med-PaLM-M, REMEDIS, MCAT, ECG-FM, TxGNN, ProteinMPNN + T5, FLAN, ReAct, ToT, Reflexion, MMLU, RAG, MAE, DALL-E3, BLIP-2 等

---

*生成日期：2026-05-10 | 分支：claude/confident-turing-NUIQO*
