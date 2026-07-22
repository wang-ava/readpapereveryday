# Copy Less, Ground More: Overcoming Repetitive Copying in Long-Context Reasoning via Evidence-Aware Reinforcement Learning

Spotlight：这篇论文把 LLM 长上下文推理里一个被忽视但高发的「复写」失败点抽象为可量化问题，并给出可验证的缓解策略。对关注长文档复杂推理可靠性的读者很值得优先看。

- 论文标题：Copy Less, Ground More: Overcoming Repetitive Copying in Long-Context Reasoning via Evidence-Aware Reinforcement Learning
- 作者：Lizhe Fang, Weizhou Shen, Tianyi Tang, Yisen Wang
- 机构：arXiv 页面未显式给出机构归属（论文文本/作者主页可继续补充）
- 发布日期（版本）：2026-07-21
- 主题标签：#LLM #长上下文 #Reasoning #ReinforcementLearning #Evaluation
- 论文链接：https://arxiv.org/abs/2607.19345v1
- PDF 链接：https://arxiv.org/pdf/2607.19345v1
- 项目/代码/数据链接：未在 arXiv 页面公开（arXiv 及相关抓取页面未稳定给出代码仓库）；后续可关注作者主页与 CatalystX/项目页是否补充。

## 核心问题
当前长上下文推理模型在生成链式思考时，常把原文段落大量原样重复进思维过程，导致“看起来在用证据”但实质上缺失真正推理，答案正确率下降。

## 方法概要
将输入按“任务相关证据”和“无关上下文”划分，建立证据感知奖励 GEAR：
1. 增加“重叠关键证据”激励项，提升模型对关键依据的使用；
2. 对无关文本重复设置惩罚；
3. 构造证据标注数据流水线，在任意长文档上自动生成监督样本；
4. 在 RL 训练中联合准确性与 grounding 奖励。

## 主要贡献
- 首次系统性定义并量化了长上下文 reasoning 的 repetitive copying 失效模式；
- 提出 GEAR 奖励框架兼顾任务正确性与证据定位质量；
- 给出可复用的证据抽取与标注管道，降低依赖昂贵人工标注成本；
- 验证表明在多尺度模型和数据上均可提升长上下文任务表现。

## 关键实验或结果
论文摘要中给出的核心结果包括平均性能提升最高可达约 +4.6（与标准基线相比）；同时在更长上下文下，repetitive copying 现象下降、推理长度更合理。未给出全部 benchmark 细表，建议后续直接下载正文核对每个 benchmark 的对照组。

## 适合关注的原因
它把“可解释性”问题和“性能”问题耦合起来：不是只追求分数，而是限制模型被噪声上下文误导的 tendency，和很多长文档 AI 应用（法务、代码审查、科学文献问答）直接相关。

## 局限性或待验证点
- 目前主要验证围绕 arXiv 上线前公开实验，行业级真实任务还需迁移验证；
- reward 定义依赖证据匹配近似，和人类对“关键证据”的主观判定可能有偏差；
- 是否适用于 multimodal/工具调用流程仍待测试。

## 对后续研究/应用的启发
适合拿到内部长上下文任务上做“安全阈值策略”：当上下文长度变长、决策风险增加时，优先约束模型证据使用路径，而不是一味扩展最大上下文。

## 一句 Obsidian 快速浏览总结
一句话：把“少写复制、少抄原文、多做 grounded reasoning”变成可训练目标，尤其适合把 long-context 生成系统从“会说”推成“会用据据”。

## 标准化研究框架
- **Research question：** 长上下文下，是否可以通过奖励函数显式约束“证据使用”来系统抑制模型复写行为并提升推理质量？
- **Literature：** 继承了 chain-of-thought、reward model 与长上下文鲁棒性相关工作，属于可解释与可控推理路线的延展。
- **Theory：** 强化学习中的奖励成分设计可以偏置策略为“依据可验证证据”而非盲目复制上下文 token。
- **Hypotheses：** 加入证据重叠奖励与噪声上下文惩罚后，模型可减少 copy 并提高正确率，且随上下文长度增长优势更明显。
- **Method：** 利用证据标注器构建训练数据，用 RL 优化准确率与 grounding 两类奖励的组合目标。
- **Data and Analysis：** 文章以多种长上下文 benchmark 的对照设置评估 RL 后的正确率、copying 率与解题长度。
- **Findings：** 观测到重复抄写显著下降，部分设置下性能平均提升约 4.6 分；更长上下文场景受益更明显。
- **Conclusion：** 该字段可等价理解为“在非社会科学实验里，把 research question/假设映射到“推理行为约束”的可验证机制上，并用基准任务检验可迁移性”。
