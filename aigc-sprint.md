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

学习目标：
- 搞清楚你之后会接触的图像/视频生成问题空间
- 能画出“短剧视频生成 POC”的高层链路

学习内容：
- 回看你自己的 [README.md](./README.md) 里工程导向的学习方式
- 阅读 Diffusers 文档总览
- 快速浏览 HunyuanVideo 论文摘要、引言、架构图

实践输出：
- 写一页笔记：`图像生成 vs 视频生成` 的关键差异
- 画出短剧 POC 链路草图：`script -> storyboard -> keyframe -> video clip -> edit -> subtitle -> review`

完成标准：
- 能用自己的话解释为什么视频生成比图像生成难

### Day 2：图像生成模型的工程认知

学习目标：
- 建立 text-to-image 的接入和调参认知

学习内容：
- Diffusers 基础 pipeline 概念
- 理解 prompt、negative prompt、steps、guidance scale、seed

实践输出：
- 跑通一个最小图像生成例子
- 记录 3 组参数变化对结果的影响

完成标准：
- 能解释哪些参数主要影响风格，哪些主要影响成本/速度

### Day 3：视频生成模型的工程认知

学习目标：
- 认识 text-to-video 与 image-to-video 的接入方式和差异

学习内容：
- `Text-to-video`
- `Text or image-to-video`

实践输出：
- 跑通一个最小视频生成例子，哪怕是低分辨率、短时长
- 记录一次失败案例：显存不足、速度太慢、画面抖动、时序差都算

完成标准：
- 能说出为什么很多生产链路会先做关键帧，再做视频

### Day 4：视频生成的成本与推理约束

学习目标：
- 把“能生成”升级成“知道代价”

学习内容：
- Diffusers memory optimization 文档
- 理解 offload、precision、frame 数、分辨率、时长之间的关系

实践输出：
- 写一页表格：不同参数对 `显存 / 延迟 / 质量` 的影响
- 形成你自己的“POC 阶段推荐参数默认值”

完成标准：
- 能解释为什么 POC 阶段不应一上来就追求长视频和高分辨率

### Day 5：视频生成的安全、合规和上线风险

学习目标：
- 对“合规”形成产品和工程双视角

学习内容：
- Sora System Card
- NIST AI RMF 结构

实践输出：
- 写一页风险清单：人物肖像、未成年人、版权、误导性内容、审查与追溯
- 产出一个最小 checklist：模型接入前要问的 10 个问题

完成标准：
- 能把合规问题前置到模型选型和产品能力设计，而不是上线前补丁

---

## Day 6-10：补齐模型接入、视频链路和原子能力

### Day 6：ComfyUI 和工作流视角

学习目标：
- 理解图像/视频生成为什么常用 workflow 方式组织

学习内容：
- ComfyUI 官方文档中的 workflow / API 概念

实践输出：
- 画一个 workflow：`prompt -> image model -> upscale / refine -> export`
- 记录你认为它适合作为哪些场景的内部工具

完成标准：
- 能解释 ComfyUI 适合什么，不适合什么

### Day 7：FFmpeg 基本功

学习目标：
- 具备最基本的视频后处理能力

学习内容：
- FFmpeg 文档中最常见的命令模式

实践输出：
- 完成这些命令：
  - 视频转码
  - 多段视频拼接
  - 抽帧
  - 加字幕
  - 调整分辨率和码率

完成标准：
- 以后和视频链路同学讨论时，不会停留在概念层

### Day 8：设计一个统一模型接入抽象

学习目标：
- 把“调模型”变成“设计接口”

学习内容：
- 回看 Diffusers / ComfyUI / 现有代码的接口组织方式

实践输出：
- 设计一个统一接口草案，例如：
  - `generate_image(prompt, config)`
  - `generate_video(prompt, config)`
  - `image_to_video(image, prompt, config)`
  - `post_process(asset, config)`
- 定义入参、出参、错误结构、trace id

完成标准：
- 输出一份 1-2 页的接口草案文档

### Day 9：做一个轻量生成 harness

学习目标：
- 从单次 demo 升级为批量实验能力

学习内容：
- 参考 `lm-evaluation-harness` 的“统一配置 + 统一执行 + 统一结果”思路

实践输出：
- 做一个最简 harness MVP：
  - 支持读取一组 prompts
  - 支持切换两个模型或两组参数
  - 支持输出结果目录和 metadata

完成标准：
- 能重复跑同一批 case，并保留可比较结果

### Day 10：为短剧方向定义 case set

学习目标：
- 建立“业务导向评测”意识

学习内容：
- 参考 `lmms-eval` 的任务组织方式

实践输出：
- 设计一个 20 条以内的短剧视频 case set，覆盖：
  - 人物一致性
  - 镜头稳定性
  - 场景切换
  - 文生视频
  - 图生视频
  - 中文 prompt 理解

完成标准：
- 每条 case 都有目的、输入、预期观察点、评分维度

---

## Day 11-15：补齐评测 harness 与负责人视角的判断力

### Day 11：读懂 `lm-evaluation-harness`

学习目标：
- 学会“评测框架的脑子”

学习内容：
- README
- task / config / result 的基本组织方式

实践输出：
- 跑通一个最小任务
- 总结 5 条“这个框架的设计理念”

完成标准：
- 你能把这些理念迁移到视频模型评测上

### Day 12：读懂 `lmms-eval`

学习目标：
- 理解多模态评测框架和纯文本评测框架的核心差异

学习内容：
- README
- 任务配置方式

实践输出：
- 总结 `lmms-eval` 相比 `lm-eval` 多了哪些工程复杂度

完成标准：
- 能清楚说出图片/视频任务为什么更难做统一评测

### Day 13：建立你自己的视频评测表

学习目标：
- 补齐“没有标准 benchmark 时，负责人怎么决策”

学习内容：
- 结合前几天输出，自建一份评测 rubric

实践输出：
- 制作一个评分表，至少包含：
  - 指令遵循
  - 人物一致性
  - 时序稳定性
  - 镜头自然度
  - 画质
  - 成本
  - 延迟
  - 合规风险

完成标准：
- 任何两个模型都能用这张表做第一轮比较

### Day 14：做一次模型/参数对比实验

学习目标：
- 用实验代替直觉

学习内容：
- 选 2 个模型、或 1 个模型 2 组配置

实践输出：
- 对你的 case set 跑一轮对比
- 写一份实验记录，说明：
  - 哪些维度谁更好
  - 哪些问题属于模型本身
  - 哪些问题属于 prompt / 参数 / 后处理

完成标准：
- 输出一份像团队内部技术选型 memo 的结论

### Day 15：形成短剧 POC 的技术选型建议

学习目标：
- 从学习者切到负责人口径

学习内容：
- 整理 Day 1-14 的结果

实践输出：
- 写一页结论：
  - POC 第一阶段推荐路线
  - 暂不推荐路线
  - 原因：质量、时延、成本、可控性、合规

完成标准：
- 这页内容可以直接拿去和团队同学聊

---

## Day 16-20：补齐 AI coding 推进能力

### Day 16：建立 AI coding 的正确预期

学习目标：
- 把 AI coding 从“工具体验”拉回“组织能力”

学习内容：
- `Introducing Codex`
- 仓库中 `06-deep-agents/`、`10-context-engineering/`

实践输出：
- 写一页笔记：哪些研发任务适合 agent，哪些不适合

完成标准：
- 能给团队定出第一版适用场景边界

### Day 17：理解 AI coding 的评测方式

学习目标：
- 具备最小的 benchmark 思维

学习内容：
- SWE-bench README
- 理解 task -> environment -> patch -> verification 的结构

实践输出：
- 基于你未来团队场景，列出 10 个内部任务类型：
  - 小需求实现
  - 单测补齐
  - 重构
  - 文档生成
  - 代码解释
  - 排查 bug

完成标准：
- 能区分哪些任务适合做硬指标，哪些适合做辅助指标

### Day 18：设计团队的 AI coding 最小推进方案

学习目标：
- 输出可执行方案，而不是观点

学习内容：
- 参考 agent 与评测材料，结合你过往工程经验

实践输出：
- 形成一版推进方案，至少包括：
  - 试点范围
  - 工具选择
  - 适用任务
  - 代码 review 要求
  - 验收标准
  - 风险控制
  - 周度指标

完成标准：
- 这份方案能在团队里先跑 2 周而不至于失控

### Day 19：做一个 AI coding harness 草案

学习目标：
- 把“推进方案”变成“能测的东西”

学习内容：
- 参考 SWE-bench 的结构，但做轻量化

实践输出：
- 设计一个内部最小 harness：
  - 输入：任务描述、代码仓库、验收方式
  - 输出：patch、测试结果、人工 review 结论
  - 指标：接受率、返工率、节省时间、失败类型

完成标准：
- 你能说清团队为什么需要这个 harness，而不是只靠主观反馈

### Day 20：总复盘与交付包

学习目标：
- 形成真正可带入新工作的资产

实践输出：
- 完成一个交付包，至少包含：
  1. `短剧 POC 技术路线图`
  2. `视频模型接入抽象草案`
  3. `视频生成 case set + rubric`
  4. `AI coding 推进方案`
  5. `未来 30 天行动建议`

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
