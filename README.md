# ProgressOfAILearning

**目标**：投入1000+小时，建立完整的LLM技术理解与应用能力，一年后能够「在LLM新技术/应用方案出现后，一周内完成原理理解、Demo复现、适用场景判断」

---

## 里程碑一：框架认知 ✅

> 目标：不求甚解地建立对 LLM 的整体印象，知道它是什么、能做什么、怎么用。

- [✅]框架性理解，不求甚解（Andrej Karpathy）
    - [✅]Deep Dive into LLMs like ChatGPT - YouTube
    - [✅]How I use LLMs - YouTube

---

## 里程碑二：动手学深度学习 ✅

> 目标：掌握模型训练的基本方法，能跑通代码，理解数据处理流程和基础数学原理。

- [✅]Practical Deep Learning for Coders Part1：https://course.fast.ai/，掌握基础的模型训练方法，了解一部分模型背后的数学原理
- [✅]Practical Deep Learning for Coders Part2：https://course.fast.ai/，理解现代深度学习架构

**学习记录**
- [✅][fastai-course-part1](https://github.com/goosmanlei/fastai-course-part1)
- [✅][fastai-course-part2](https://github.com/goosmanlei/fastai-course-part2)

---

## 里程碑三：深入理解 Transformer 与 LLM 原理✅

> 目标：从头理解 Transformer 架构，能手写 GPT，读懂相关源码。

- [✅][Stanford CS25: Introduction to Transformers with Andrej Karpathy](https://www.youtube.com/watch?v=XfpMkf4rD6E&utm_source=chatgpt.com)
- [✅][Let's build GPT: from scratch, in code, spelled out (Andrej Karpathy)](https://www.youtube.com/watch?v=kCc8FmEb1nY&utm_source=chatgpt.com)

**学习记录**
- [✅][gpt-from-karpathy](https://github.com/goosmanlei/gpt-from-karpathy)

---

## 里程碑四：对齐、微调与强化学习✅

> 目标：理解 RLHF、指令微调等让 LLM "听话" 的核心技术，掌握模型微调与部署的基本流程。

- [✅][Huggingface LLm Course](https://huggingface.co/learn/llm-course)：LLM结构、微调、推理、部署
- [✅][Illustrating Reinforcement Learning from Human Feedback (RLHF)](https://huggingface.co/blog/rlhf) 概念性理解

**学习记录**
- [✅][llm-hf](https://github.com/goosmanlei/llm-hf)

---

## 里程碑五：LLM 工程入门（进行中）

> 本小节学习目标、计划、验收项目由claude code梳理生成[2026.03.26]

> 目标：能用 API 和主流框架构建实际的 LLM 应用，具备基本的工程化能力。
> 注意：这是第一个"构建"导向的里程碑，和前四个"理解"导向的里程碑不同——遇到的主要障碍是"调不通为什么"而不是"听不懂理论"，需要主动查文档、在报错中学习。
>
> **具体子目标**：
> - 子目标1：LLM API 熟练集成（调参、roles设计、token管理、流式输出、错误重试）
> - 子目标2：Prompt Engineering 基础（zero-shot/few-shot、CoT、多步骤链、结构化输出）
> - 子目标3：RAG 系统完整构建（分块、Embedding、向量库、检索策略、带来源的生成）
> - 子目标4：简单 Agent 构建（ReAct模式、工具定义、多步骤推理、终止条件；可提前阅读里程碑六的 ReAct 原始论文）
> - 子目标5：LLM 应用框架使用（用 LangChain 作为工具实现链式组合、对话记忆、调试；框架是手段，不是目标）
> - 子目标6：基础评估能力（测试集构建、定量对比、LLM-as-judge思路）

**前置阅读**（进入本里程碑前，约30分钟）：
- [Embeddings - OpenAI Platform](https://platform.openai.com/docs/guides/embeddings) — 只读主页面的概念描述（What are embeddings、How to get embeddings、Use cases 的文字部分），理解向量化与相似度检索的原理，为 RAG 做概念铺垫。**不需要**在此阶段跑 Use cases 中的 Jupyter Notebook，相关 notebook（Question answering、Semantic text search）在子目标3 RAG 构建阶段按需参考。

**学习资源**（按顺序学习）：
1. [ChatGPT Prompt Engineering for Developers - DeepLearning.AI](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)（1小时，免费）— 建立 API 调用和 Prompt 基础，对应子目标1、2
2. [Full Stack LLM Bootcamp - University of California, Berkeley](https://www.youtube.com/playlist?list=PLoROMvodv4rN4wG6Nk6sNpTEbuOSosZdX) — 视野型课程（2023年内容，部分细节已过时），重点学安全、成本、UX、产品化思路，技术细节以后续课程为准
3. [Introduction to LangChain - Python - LangChain Academy](https://academy.langchain.com/courses/foundation-introduction-to-langchain-python) — 系统学习 LangChain（LCEL 现代语法），对应子目标3、4、5
4. [Building and Evaluating Advanced RAG - DeepLearning.AI](https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/)（1小时，免费）— 专项强化 RAG 构建与评估，对应子目标3、6
5. [Effective Context Engineering for AI Agents - Anthropic](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)（博客文章，选读）— 生产级 Agent 的上下文设计思路，内容偏进阶，了解趋势即可

**学习记录**
- [llm-engineering](https://github.com/goosmanlei/llm-engineering)

**验收项目**（按顺序完成）：

**项目一：文档问答 RAG 系统**（验收子目标1、2、3、5）

背景：有大量学习资料（笔记、论文、README）目前只能靠记忆检索。
要做什么：命令行问答系统，能基于指定文档回答问题。
实用价值：直接加载本学习仓库的笔记，后续里程碑持续往里加文档。

硬性约束（不满足不算完成）：
1. 支持 PDF + Markdown 两种格式
2. 做一次分块策略对比实验：对比 chunk_size=256 vs 512 在相同问题上的检索结果差异，写不少于100字的结论
3. 每条回答附来源引用（文档名 + 原文片段）
4. 能处理"文档中没有答案"的情况——明确告知，不允许编造
5. 实现5条问答对的最小测试集，手动评估准确率

**项目二：带工具调用的研究助手 Agent**（验收子目标1、2、4、5）

背景：技术调研需要频繁搜索+整理+记录，手动流程繁琐。
要做什么：命令行Agent，接受自然语言调研任务，自动完成多步骤推理和工具调用。
实用价值：可直接用于后续里程碑的技术调研，替代手动搜索+整理流程。

必须实现的3个工具：
- `web_search(query)` — 调用搜索API获取网页摘要
- `read_file(path)` — 读取本地文件内容
- `save_note(filename, content)` — 将内容保存为本地Markdown文件

硬性约束（不满足不算完成）：
1. 每次工具调用打印 Thought / Action / Observation，推理过程全程可见
2. 单任务工具调用上限10次，超出后主动汇报当前进展并停止
3. 必须通过端到端测试用例："调研 LangChain 和 LlamaIndex 的适用场景区别，保存为 research_note.md"，Agent能自动完成全流程
4. 能识别"不需要搜索"的问题并直接回答，不无谓调用工具
5. 完成后写一段约200字的自评：描述 Agent 在测试用例上的表现（成功/失败/出乎意料的行为），培养评估意识

**项目三（综合）：个人学习助手 Bot**（验收全部子目标）

背景：学习仓库有进度记录，但缺乏主动复习和知识检验机制，学完容易遗忘。
要做什么：交互式Bot，集成RAG（检索学习笔记）+ Agent（执行多步任务），支持三种指令：
- `/quiz [主题]` — 基于笔记内容出题，回答后给出判断和解析
- `/explain <概念>` — 解释概念，必须引用笔记中的相关内容
- `/progress` — 读取README，汇报当前哪些里程碑完成了
实用价值：每完成一个里程碑就往知识库加文档，形成长期复习工具。

推荐分阶段完成（MVP策略，避免卡死）：
- MVP：先只实现 `/explain`（纯RAG，无Agent、无记忆），跑通后再扩展
- V2：加入 `/progress`（读取README，简单文件操作）
- V3：加入 `/quiz` + 对话记忆 + 评估脚本

硬性约束（不满足不算完成）：
1. `/quiz` 出的题来源可追溯（引用哪个文件的哪段内容），不能凭空出题
2. 同一session内保持对话记忆，例如"上一题答错了，再出一道相关的"能正常工作
3. `/explain` 回答中包含笔记原文引用 + 扩展解释，两部分明确区分
4. 项目有README：运行方法、整体架构（文字描述）、一个关键设计决策及理由
5. 实现评估脚本：对 `/explain` 构建5条测试用例，能自动跑完并给出通过/未通过

所有项目验收方式：能本地跑通端到端demo；代码关键设计决策有注释；README含"遇到的问题与解决方法"。

---

## 里程碑六：复杂 Agent 系统

> 目标：掌握多步骤、多 Agent 系统的构建方法，理解 MCP 协议，能落地前沿 Agent 应用。

- [solveit course by Jeremy Howard](https://solve.it.com/)
- [ReAct 原始论文](https://arxiv.org/abs/2210.03629)（Yao et al., 2022）
- LangGraph：复杂Agent构建
    - [Introduction to LangGraph - Python](https://academy.langchain.com/courses/intro-to-langgraph)
    - [LangGraph Overview](https://docs.langchain.com/oss/python/langgraph/overview)
- MCP/Agents：多Agents系统建设，前沿应用实践
    - [Project: Deep Agents](https://academy.langchain.com/courses/deep-agents-with-langgraph)
    - [Project: Ambient Agents with LangGraph](https://academy.langchain.com/courses/ambient-agents)
    - [Project: Deep Research with LangGraph](https://academy.langchain.com/courses/deep-research-with-langgraph)

## 未来储备学习

- [Deep RL Course](https://huggingface.co/learn/deep-rl-course/unit0/introduction)


---

## 元学习（随时可读）

> 帮助建立长期有效的学习方法论，适合在任意阶段穿插阅读。

- Meta Learning: How To Learn Deep Learning And Thrive In The Digital World: 适合第二次学习AI的人, 讲哪些知识长期有效,哪些知识可以先黑箱使用

## 参考资料
- Python for Data Analysis：书籍，pandas作者写的，还没有找视频课程，可能也不需要，讲numpy、pandas等重要的基础库，学习数据处理的方法
