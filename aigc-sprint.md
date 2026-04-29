# AIGC Sprint

> 目标：用 20 天 * 5 小时，完成一轮面向新问题的前置学习与实战储备。
>
> 适用背景：
> - 核心职责：短剧方向技术 POC
> - 同时负责：视频基建和链路工具、成本优化、合规、模型接入、视频原子能力
> - 协同要求：服务端偏重，前端强协同
> - 明确要求：补齐 `harness / 视频图像生成模型 / AI coding 推进` 相关能力

---

## 先说明一个假设

`harness` 语义略宽。这里按你下一步工作最有价值的方式理解为三类：

1. **模型评测 harness**：统一跑 prompt、数据集、指标、结果对比的框架
2. **模型接入 harness**：统一接不同图像/视频模型、参数、后处理链路的工程骨架
3. **AI coding harness**：用于衡量和推进 AI 编码效果的任务集、流程和评估标准

如果后续你和团队内部对 `harness` 有更具体定义，这份计划也仍然基本成立，只需要替换第 9-16 天的实践主题。

---

## 为什么这样安排

这份计划不是“系统学习 AIGC 全家桶”，而是按问题优先级排序：

1. **先补视频/图像生成模型的工作认知**
   目标不是训练 SOTA，而是做到“知道主流模型如何分层、优缺点是什么、接入时要看哪些参数和代价”。
2. **再补模型接入和视频链路能力**
   你的职责里有视频基建、成本、合规、原子能力，这比纯研究更重要。
3. **再补 harness 和评测**
   你作为技术负责人，需要能组织团队用统一方法比较模型，而不是靠主观感觉选型。
4. **最后补 AI coding 推进**
   这不是“学会用工具”就结束，而是要形成一套可落地的推进方案、指标和最小治理机制。

---

## 总学习目标

### 目标 1：建立图像/视频生成模型的工程认知

达到程度：
- **理解层**，不是训练层
- 能说清 text-to-image、image-to-video、text-to-video 的常见路线
- 能看懂模型介绍、论文摘要、官方推理文档
- 能和业务讨论“该用哪类模型，不该用哪类模型”

重点掌握：
- Diffusion / DiT 基本思路
- 图像生成与视频生成的差异：时序一致性、镜头控制、人物一致性、运动质量
- 开源与闭源模型的差异：质量、成本、可控性、可私有化程度

### 目标 2：建立视频生成链路与基建认知

达到程度：
- **可落地设计层**
- 能拆出一个短剧生成 POC 的链路
- 能识别成本、耗时、失败率、审核风险、后处理复杂度

重点掌握：
- 模型接入抽象
- prompt / storyboard / shot / asset / render / post-process 链路
- FFmpeg 常见后处理能力
- 推理显存、速度、分辨率、时长、并发的权衡

### 目标 3：具备最小可用的 harness 能力

达到程度：
- **能自己搭一个轻量版 harness**
- 能批量跑 case，对比不同模型或参数
- 能输出结构化结果，而不是停留在 demo

重点掌握：
- 用 `lm-evaluation-harness` 建立评测思路
- 用 `lmms-eval` 理解多模态评测框架
- 为图像/视频生成任务设计自己的 case set 和评分表

### 目标 4：为 AI coding 推进准备一套可执行方案

达到程度：
- **负责人推进层**
- 不只是“自己会用”，而是能推动团队形成最小规范和指标

重点掌握：
- AI coding 的任务边界
- 适合 AI 代理的任务类型
- 如何做任务拆分、验收、代码 review、效果衡量
- 如何避免“看起来很快，实际返工变多”

---

## 资源清单

下面只列与你这 20 天目标强相关、且尽量具体的资源。

### 一、图像/视频生成模型

1. [Diffusers Documentation - Text-to-video](https://huggingface.co/docs/diffusers/en/api/pipelines/text_to_video)
   - 学到什么：text-to-video pipeline 的基本调用方式、关键参数、开源视频模型接入方式
   - 学习深度：**必须通读并跑一个最小例子**

2. [Diffusers Documentation - Text or image-to-video](https://huggingface.co/docs/diffusers/v0.30.2/using-diffusers/text-img2vid)
   - 学到什么：image-to-video / text-to-video 两类入口和典型使用姿势
   - 学习深度：**理解为主，至少跑通一个方向**

3. [Diffusers Documentation - Reduce memory usage](https://huggingface.co/docs/diffusers/en/optimization/memory)
   - 学到什么：显存优化、offload、吞吐与速度权衡
   - 学习深度：**必须理解，这是视频基建和成本优化的直接知识**

4. [HunyuanVideo: A Systematic Framework For Large Video Generative Models](https://arxiv.org/abs/2412.03603)
   - 学到什么：开源大视频生成模型整体框架、训练和推理设计、视频质量关注点
   - 学习深度：**读摘要、引言、架构图、实验结论即可**

5. [Sora System Card](https://openai.com/index/sora-system-card/)
   - 学到什么：高能力视频生成系统在安全、滥用、部署上的真实问题
   - 学习深度：**重点读风险与缓解，不必深究产品细节**

6. [ComfyUI Official Documentation](https://docs.comfy.org/)
   - 学到什么：工作流式模型编排、节点图、作为模型接入/实验平台的思路
   - 学习深度：**理解 workflow + API 即可，不要求深度插件开发**

### 二、评测 harness 与实验框架

1. [EleutherAI / lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)
   - 学到什么：统一 benchmark、任务配置、批量跑评测的工程抽象
   - 学习深度：**理解 README、task/config 思路，跑通一个最小任务**

2. [EvolvingLMMs-Lab / lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval)
   - 学到什么：多模态评测如何组织 image / video / audio / text 任务
   - 学习深度：**理解框架设计和任务组织方式，不要求完整跑大型 benchmark**

3. [SWE-bench](https://github.com/SWE-bench/SWE-bench)
   - 学到什么：AI coding 能力如何被 benchmark 化
   - 学习深度：**读 README 和 harness 入口，理解评估思路**

### 三、视频链路、合规与工程

1. [FFmpeg Documentation](https://ffmpeg.org/documentation.html)
   - 学到什么：拼接、转码、抽帧、加字幕、分辨率处理、音视频封装
   - 学习深度：**必须会查，会写最常见命令**

2. [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
   - 学到什么：合规和风险治理该怎么结构化思考
   - 学习深度：**理解框架，不要求全文精读**

3. [Full Stack LLM Bootcamp - LLMOps](https://fullstackdeeplearning.com/llm-bootcamp/spring-2023/llmops/)
   - 学到什么：成本、监控、评估、上线流程的工程视角
   - 学习深度：**选学，与现有仓库 `02-fullstack-llm-bootcamp/lesson-07-llmops.ipynb` 联动**

### 四、AI coding 推进

1. [Introducing Codex](https://openai.com/index/introducing-codex/)
   - 学到什么：软件工程 agent 的任务边界与能力定位
   - 学习深度：**通读，形成“哪些任务值得 agent 化”的判断**

2. [Building Effective AI Agents](https://resources.anthropic.com/hubfs/Building%20Effective%20AI%20Agents-%20Architecture%20Patterns%20and%20Implementation%20Frameworks.pdf)
   - 学到什么：agent workflow 设计、任务拆分、评估与控制
   - 学习深度：**选读核心章节，重点吸收任务设计和失败控制**

3. 当前仓库既有内容
   - `04-intro-langgraph/`
   - `05-intro-langsmith/`
   - `06-deep-agents/`
   - `10-context-engineering/`
   - 学到什么：如何把 AI coding 从“聊天”推进到“可观测、可验收、可调试”的 agent workflow
   - 学习深度：**优先复用你已经学过/正在学的材料，减少切换成本**

---

## 20 天时间规划

总预算：**100 小时左右**

建议每天固定结构：
- 2 小时：主线学习
- 2 小时：动手实践
- 1 小时：做笔记、沉淀结论、整理明日问题

---

## Day 1-5：补齐视频/图像生成模型的工作认知

### Day 1：建立地图

今日资料：
- [README.md](./README.md)
- [Diffusers Documentation - Text-to-video](https://huggingface.co/docs/diffusers/en/api/pipelines/text_to_video)
- [HunyuanVideo](https://arxiv.org/abs/2412.03603) 的摘要、引言、架构图

执行脚本：
1. 回看 [README.md](./README.md)，只抓两件事：你的职责边界是什么、这 20 天最终要交付什么。
2. 通读 Diffusers `Text-to-video` 页面，不抄代码，先建立“输入是什么、输出是什么、核心参数有哪些”的脑图。
3. 快速读 HunyuanVideo 的摘要、引言、架构图，只回答一个问题：视频生成相比图像生成多了哪些难点。
4. 画一张高层链路图：`script -> storyboard -> keyframe -> video clip -> edit -> subtitle -> review`。

今日输出：
- 一页笔记：`图像生成 vs 视频生成` 的关键差异
- 一张短剧 POC 高层链路图

完成标准：
- 能用自己的话解释为什么视频生成比图像生成难

### Day 2：图像生成模型的工程认知

今日资料：
- [Diffusers Documentation - Text-to-video](https://huggingface.co/docs/diffusers/en/api/pipelines/text_to_video)
- [Diffusers Documentation - Text or image-to-video](https://huggingface.co/docs/diffusers/v0.30.2/using-diffusers/text-img2vid)

执行脚本：
1. 从文档里抽出共通参数：`prompt`、`negative prompt`、`num_inference_steps`、`guidance scale`、`seed`。
2. 选一个最小可跑的图像生成例子，先跑通默认参数。
3. 只改 3 组参数做对比，每次只改一个主变量。
4. 把结果按“风格变化 / 速度变化 / 稳定性变化”记录下来。

今日输出：
- 一个最小图像生成样例
- 3 组参数实验记录

完成标准：
- 能解释哪些参数主要影响风格，哪些主要影响成本和速度

### Day 3：视频生成模型的工程认知

今日资料：
- [Diffusers Documentation - Text-to-video](https://huggingface.co/docs/diffusers/en/api/pipelines/text_to_video)
- [Diffusers Documentation - Text or image-to-video](https://huggingface.co/docs/diffusers/v0.30.2/using-diffusers/text-img2vid)
- [HunyuanVideo](https://arxiv.org/abs/2412.03603) 中和时序、一致性相关的描述

执行脚本：
1. 对照 `text-to-video` 和 `image-to-video` 两种入口，整理它们的典型适用场景。
2. 选一个方向跑通最小视频生成例子，要求低分辨率、短时长、可接受低质量。
3. 主动记录一次失败案例，不要跳过。
4. 回头对照 HunyuanVideo，解释失败更可能来自模型、参数还是硬件限制。

今日输出：
- 一个最小视频生成样例
- 一份失败案例记录
- 一段“为什么生产链路常先做关键帧再做视频”的说明

完成标准：
- 能说出 text-to-video 和 image-to-video 在生产上各适合什么

### Day 4：视频生成的成本与推理约束

今日资料：
- [Diffusers Documentation - Reduce memory usage](https://huggingface.co/docs/diffusers/en/optimization/memory)
- Day 2-3 的实验记录

执行脚本：
1. 精读 `Reduce memory usage`，重点看 `offload`、`dtype`、显存优化、吞吐权衡。
2. 用你前一天的视频例子，至少改 2 组配置，观察 frame 数、分辨率、时长对资源占用的影响。
3. 做一张对照表：`参数 -> 显存 -> 延迟 -> 质量 -> 适用阶段`。
4. 写出一版你自己的 POC 默认配置，不要求最优，只要求可稳定复现。

今日输出：
- 一页参数影响表
- 一版 `POC 默认参数建议`

完成标准：
- 能解释为什么 POC 阶段不应一开始就追求长视频和高分辨率

### Day 5：视频生成的安全、合规和上线风险

今日资料：
- [Sora System Card](https://openai.com/index/sora-system-card/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

执行脚本：
1. 读 Sora System Card，只抓风险类型、滥用方式、缓解手段。
2. 读 NIST AI RMF，只抓框架结构，不做细节背诵。
3. 把两者映射成你的短剧场景风险清单。
4. 写一个“模型接入前必须问的 10 个问题” checklist。

今日输出：
- 一页风险清单：人物肖像、未成年人、版权、误导性内容、审查与追溯
- 一个最小 checklist

完成标准：
- 能把合规问题前置到模型选型和产品能力设计里

---

## Day 6-10：补齐模型接入、视频链路和原子能力

### Day 6：ComfyUI 和工作流视角

今日资料：
- [ComfyUI Official Documentation](https://docs.comfy.org/)
- Day 1 的 POC 链路图

执行脚本：
1. 阅读 ComfyUI 文档中 workflow、node、API 相关部分。
2. 把 Day 1 的链路草图改写成 workflow 视角：哪些步骤是节点，哪些步骤是可替换模块。
3. 画一个最小 workflow：`prompt -> image model -> refine/upscale -> export`。
4. 写 3 条判断：它适合什么，不适合什么，什么时候该回到普通服务端接口。

今日输出：
- 一张 workflow 图
- 一段 ComfyUI 适用边界说明

完成标准：
- 能解释为什么图像/视频生成链路经常天然长成 workflow

### Day 7：FFmpeg 基本功

今日资料：
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)

执行脚本：
1. 先查官方文档，再自己写命令，不先找别人博客抄答案。
2. 至少完成 5 类操作：转码、拼接、抽帧、加字幕、改分辨率和码率。
3. 每做完一类，顺手记一条“这在短剧 POC 里有什么用”。
4. 把常用命令沉淀成一个你自己的速查表。

今日输出：
- 一份 FFmpeg 常用命令清单
- 一个包含 5 类操作的最小实验目录

完成标准：
- 以后和视频链路同学讨论时，不会停留在概念层

### Day 8：设计一个统一模型接入抽象

今日资料：
- [Diffusers Documentation - Text-to-video](https://huggingface.co/docs/diffusers/en/api/pipelines/text_to_video)
- [Diffusers Documentation - Text or image-to-video](https://huggingface.co/docs/diffusers/v0.30.2/using-diffusers/text-img2vid)
- [ComfyUI Official Documentation](https://docs.comfy.org/)

执行脚本：
1. 回看 Day 2-7 的笔记，只抽共性，不纠结某个具体模型。
2. 先列能力，再列接口，不要一上来写类图。
3. 至少定义 4 个接口：
   - `generate_image(prompt, config)`
   - `generate_video(prompt, config)`
   - `image_to_video(image, prompt, config)`
   - `post_process(asset, config)`
4. 为每个接口补齐入参、出参、错误结构、trace id、artifact 存储约定。

今日输出：
- 一份 1-2 页的模型接入抽象草案

完成标准：
- 输出的是“团队可以讨论的接口文档”，不是一堆零散想法

### Day 9：做一个轻量生成 harness

今日资料：
- [EleutherAI / lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)
- Day 8 的接口草案

执行脚本：
1. 先读 `lm-evaluation-harness` README，只抓 `统一配置 + 统一执行 + 统一结果`。
2. 不试图复刻它，直接做自己的轻量 MVP。
3. MVP 至少支持：
   - 读取一批 prompts
   - 切换两组模型或参数
   - 输出结果目录和 metadata
4. 输出目录提前设计好，避免后面实验结果不可比。

今日输出：
- 一个最小 harness MVP
- 一份结果目录结构说明

完成标准：
- 能重复跑同一批 case，并保留可比较结果

### Day 10：为短剧方向定义 case set

今日资料：
- [EvolvingLMMs-Lab / lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval)
- Day 9 的 harness MVP

执行脚本：
1. 阅读 `lmms-eval` 的任务组织方式，只看它怎么定义任务，不追求跑完整 benchmark。
2. 从业务角度列你最关心的失败类型，而不是先列模型能力名词。
3. 设计一个 20 条以内的 case set，覆盖人物一致性、镜头稳定性、场景切换、文生视频、图生视频、中文 prompt 理解。
4. 每条 case 必须写清楚：目的、输入、预期观察点、评分维度。

今日输出：
- 一份短剧方向 case set

完成标准：
- 每条 case 都能直接喂给 harness 执行或人工评估

---

## Day 11-15：补齐评测 harness 与负责人视角的判断力

### Day 11：读懂 `lm-evaluation-harness`

今日资料：
- [EleutherAI / lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)

执行脚本：
1. 读 README 和一个最小 task/config 示例。
2. 画出它的最小抽象：任务定义、运行入口、结果产出。
3. 尝试跑通一个最小任务，哪怕只到命令层面和配置层面。
4. 总结 5 条设计理念，并逐条写“如何迁移到视频评测”。

今日输出：
- 一页 `lm-eval` 设计理念总结

完成标准：
- 你能把它的思想翻译成你自己的生成评测框架语言

### Day 12：读懂 `lmms-eval`

今日资料：
- [EvolvingLMMs-Lab / lmms-eval](https://github.com/EvolvingLMMs-Lab/lmms-eval)

执行脚本：
1. 读 README 和任务配置示例。
2. 对比 Day 11，专门找多模态多出来的复杂度。
3. 从输入格式、资产管理、指标设计、人工评审依赖四个角度写差异。
4. 顺手修正你的 harness 和 case set 结构，如果你发现前面定义太理想化。

今日输出：
- 一页 `lmms-eval vs lm-eval` 差异总结
- 一次对 case set 或 harness 的修订

完成标准：
- 能清楚说出图片/视频任务为什么更难做统一评测

### Day 13：建立你自己的视频评测表

今日资料：
- Day 10 的 case set
- Day 11-12 的框架笔记
- Day 5 的风险清单

执行脚本：
1. 把“评测表”当成负责人决策工具，而不是学术 benchmark。
2. 至少包含这些维度：指令遵循、人物一致性、时序稳定性、镜头自然度、画质、成本、延迟、合规风险。
3. 为每一项定义 1-5 分的判分标准，避免只写名词。
4. 补充一列“失败是否可通过 prompt/参数/后处理修复”。

今日输出：
- 一张可直接用于评审的 rubric 表

完成标准：
- 任意两个模型或两组参数都能用这张表做第一轮比较

### Day 14：做一次模型/参数对比实验

今日资料：
- Day 9 的 harness MVP
- Day 10 的 case set
- Day 13 的 rubric

执行脚本：
1. 选 2 个模型，或 1 个模型的 2 组配置。
2. 不求 case 全跑完，先选一小批高价值 case 跑出第一轮结果。
3. 用 rubric 做评分，同时单独记录失败类型。
4. 写结论时强制拆成三类：模型本身问题、prompt/参数问题、后处理问题。

今日输出：
- 一份实验记录
- 一份简短对比结论

完成标准：
- 输出看起来像一份团队内部技术选型 memo，而不是学习笔记

### Day 15：形成短剧 POC 的技术选型建议

今日资料：
- Day 1-14 的全部产出
- [Full Stack LLM Bootcamp - LLMOps](https://fullstackdeeplearning.com/llm-bootcamp/spring-2023/llmops/)
- 仓库里你已有的 LLMOps 学习材料

执行脚本：
1. 回看前面所有结论，只保留会影响业务推进的判断。
2. 用质量、时延、成本、可控性、合规五个维度做最终归纳。
3. 写三段结论：
   - POC 第一阶段推荐路线
   - 暂不推荐路线
   - 需要继续验证的问题
4. 把措辞改成负责人视角，不写“我感觉”，只写“建议/原因/风险”。

今日输出：
- 一页短剧 POC 技术选型建议

完成标准：
- 这页可以直接拿去和团队同学讨论

---

## Day 16-20：补齐 AI coding 推进能力

### Day 16：建立 AI coding 的正确预期

今日资料：
- [Introducing Codex](https://openai.com/index/introducing-codex/)
- 仓库中的 `06-deep-agents/`
- 仓库中的 `10-context-engineering/`

执行脚本：
1. 读 `Introducing Codex`，只抓任务边界、能力形态、适用场景。
2. 回看你已经学过的 `06-deep-agents/` 和 `10-context-engineering/`，把“AI coding agent”理解成 workflow，而不是聊天窗口。
3. 写一页边界判断：哪些研发任务适合 agent，哪些不适合。
4. 每类任务至少给一个真实团队例子。

今日输出：
- 一页 AI coding 任务边界笔记

完成标准：
- 能给团队定出第一版适用场景边界

### Day 17：理解 AI coding 的评测方式

今日资料：
- [SWE-bench](https://github.com/SWE-bench/SWE-bench)

执行脚本：
1. 读 SWE-bench README，重点理解 `task -> environment -> patch -> verification`。
2. 把这个结构翻译成你未来团队的语言。
3. 列 10 个内部任务类型，如小需求实现、单测补齐、重构、文档生成、代码解释、排查 bug。
4. 给每类任务标记：更适合硬指标，还是更适合辅助指标。

今日输出：
- 一份内部任务类型清单
- 一份指标分类表

完成标准：
- 能区分哪些任务适合做 benchmark，哪些更适合人工抽检

### Day 18：设计团队的 AI coding 最小推进方案

今日资料：
- Day 16-17 的输出
- [Building Effective AI Agents](https://resources.anthropic.com/hubfs/Building%20Effective%20AI%20Agents-%20Architecture%20Patterns%20and%20Implementation%20Frameworks.pdf)

执行脚本：
1. 读 `Building Effective AI Agents` 中和任务拆分、失败控制、评估相关的章节。
2. 基于你自己的工程经验，设计一版 2 周可试运行方案。
3. 方案至少包括：试点范围、工具选择、适用任务、代码 review 要求、验收标准、风险控制、周度指标。
4. 删掉空泛口号，只保留能执行、能检查的条目。

今日输出：
- 一版 AI coding 推进方案

完成标准：
- 这份方案能在团队里先跑 2 周而不至于失控

### Day 19：做一个 AI coding harness 草案

今日资料：
- [SWE-bench](https://github.com/SWE-bench/SWE-bench)
- Day 18 的推进方案

执行脚本：
1. 回看 SWE-bench 的结构，但只抽最小骨架。
2. 设计你的内部最小 harness，先定义输入输出，再谈实现。
3. 至少写清楚：
   - 输入：任务描述、代码仓库、验收方式
   - 输出：patch、测试结果、人工 review 结论
   - 指标：接受率、返工率、节省时间、失败类型
4. 明确哪些步骤自动化，哪些步骤保留人工把关。

今日输出：
- 一份 AI coding harness 草案

完成标准：
- 你能说清团队为什么需要这个 harness，而不是只靠主观反馈

### Day 20：总复盘与交付包

今日资料：
- Day 1-19 的全部输出

执行脚本：
1. 回收所有零散笔记，只保留真正能带去新工作的资产。
2. 整理成一个交付包，至少包含：
   1. `短剧 POC 技术路线图`
   2. `视频模型接入抽象草案`
   3. `视频生成 case set + rubric`
   4. `AI coding 推进方案`
   5. `未来 30 天行动建议`
3. 补一页总复盘：哪些判断已经足够，哪些仍需实验验证。
4. 最后检查一遍，每个结论是否都能追溯到前面某天的资料或实验。

今日输出：
- 完整交付包
- 一页总复盘

完成标准：
- 不是“学过了”，而是“拿得出去”

---

## 建议的 3 个实践产出

为了让这 20 天不是只看资料，建议你至少交付下面 3 个东西。

### 实践 1：轻量多模型生成 harness

目标：
- 支持一批 prompts 跑多个模型/参数
- 统一保存结果和 metadata

做到什么程度：
- **MVP 即可**
- 不追求漂亮 UI
- 能重复跑、能对比、能留痕就够

### 实践 2：短剧 POC 方案草图

目标：
- 不是把整条链路全部做出来，而是拆清楚

至少包含：
- 剧本拆镜
- 角色设定
- 关键帧生成
- 图生视频 / 文生视频
- 片段拼接
- 字幕/配音预留位
- 审核与追溯点

做到什么程度：
- **方案级**
- 能指导第一阶段 POC 即可

### 实践 3：AI coding 推进包

目标：
- 为硬性指标提前准备方法论

至少包含：
- 试点任务类型
- 评估指标
- review 规则
- 失败案例分类
- 周报模板

做到什么程度：
- **负责人可直接拿来试运行**

---

## 每个主题的学习深度建议

有些东西要学深，有些只要建立判断力，不要平均用力。

### 要学深的

- Diffusers 的推理与显存优化
- 视频生成链路中的 FFmpeg 基本能力
- 模型接入抽象
- 业务 case set 与评测 rubric 设计
- AI coding 推进方案和指标设计

### 只需理解到“能判断”的

- 大模型/视频模型训练细节
- 长篇学术 benchmark
- ComfyUI 高级插件生态
- 复杂分布式训练框架

### 暂时不用投入太多的

- 自己训练视频基础模型
- 追最新 SOTA 论文细节
- 过早做前端重交互工具

---

## 和你现有学习计划的衔接关系

你之前的学习计划已经把 LLM 工程基础、Agent、LangGraph、LangSmith 打下来了，这次不应该重学一遍，而应该“迁移”：

- 之前学的 `LangGraph / Agent / Context Engineering`
  现在用于理解 AI coding 和 workflow 编排
- 之前学的 `LangSmith / 评估`
  现在用于理解 harness、结果对比和可观测性
- 之前学的 `Full Stack LLM / LLMOps`
  现在用于思考视频模型服务的成本、监控、上线约束

换句话说，这 20 天不是重新起步，而是把你已有的 LLM 工程能力，转成 **多模态生成 + 视频链路 + 负责人视角**。

---

## 最终验收标准

20 天结束时，至少达到下面 6 条中的 5 条：

1. 能清楚解释图像生成、图生视频、文生视频三类能力的差异和适用场景
2. 能画出一版短剧视频 POC 的端到端链路
3. 能设计统一的模型接入抽象，而不是每接一个模型写一套
4. 能做一个最小可用的生成 harness 或实验框架
5. 能拿出一套带 case set 和 rubric 的模型评测方案
6. 能写出一版 AI coding 推进方案，并说明指标如何定义

如果你能做到这一步，第一阶段就不是“边学边摸”，而是可以较快进入“能判断、能设计、能推进”的状态。
