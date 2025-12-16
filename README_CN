# Vibe Coding 终极指南 V1.2
**作者:** [Nicolas Zullo, https://x.com/NicolasZu](https://x.com/NicolasZu)  
**创建日期:** 2025年3月12日  
**最后更新:** 2025年10月6日  

---

## 入门指南
要开始 Vibe Coding（氛围编程），你只需要以下两个工具之一：  
- **Claude Sonnet 4.5**，在 Claude Code 中使用
- **gpt-5-codex (high)**，在 Codex CLI 中使用

本指南适用于 CLI 版本（在终端中使用）和 VSCode 扩展版本（Codex 和 Claude Code 都有插件，界面更新）。

*(注：虽然本指南的早期版本使用了 **Grok 3**，但我们后来过渡到了 **Gemini 2.5 Pro**。现在我们使用的是 **Claude 4.5**（或 **gpt-5-codex (high)**）)*

*(注2：如果你想使用 Cursor，请查看本指南的 [1.1 版本](https://github.com/EnzeD/vibe-coding/tree/1.1.1)，但我们认为它不如 Codex CLI 或 Claude Code 强大)*

正确设置一切是关键。如果你想认真创建一个功能齐全且视觉效果出色的游戏（或应用程序），请花时间建立坚实的基础。  

**核心原则：** *规划就是一切。* **不要**让 AI 自主规划，否则你的代码库将变成一团无法管理的混乱。

---

## 一切的准备工作

### 1. 游戏设计文档 (Game Design Document)
- 拿着你的游戏创意，要求 **GPT-5** 或 **Sonnet 4.5** 创建一个 Markdown 格式的简单**游戏设计文档**：`game-design-document.md`。  
- 审查并完善文档，确保它符合你的愿景。基础一点没关系——目的是给你的 AI 提供关于游戏结构和意图的上下文。不要过度设计，我们稍后会进行迭代。

### 2. 技术栈与 `CLAUDE.md` / `Agents.md`
- 要求 **GPT-5** 或 **Sonnet 4.5** 为你的游戏推荐最佳技术栈（例如，用于多人 3D 游戏的 ThreeJS 和 WebSocket）。将其保存为 `tech-stack.md`。
  - 挑战它提出*最简单但最健壮的技术栈*。  
- 在你的终端中，打开 **Claude Code** 或 **Codex CLI** 并使用 `/init` 命令。它将使用你目前创建的两个 .md 文件。这将创建一组规则，以便正确引导你的 LLM。 
- **至关重要的是，审查生成的规则。** 确保它们强调**模块化**（多个文件）并阻止**单体应用**（一个巨大的文件）。你可能需要手动调整或添加规则。同时确查看它们的触发时机。
  - **重要提示：** 某些规则对于保持上下文至关重要，应设置为 **"Always"（始终）** 规则。这确保 AI 在生成代码之前*始终*参考它们。考虑添加如下规则并将其标记为 "Always"：
    > ```
    > # IMPORTANT:
    > # Always read memory-bank/@architecture.md before writing any code. Include entire database schema.
    > # Always read memory-bank/@game-design-document.md before writing any code.
    > # After adding a major feature or completing a milestone, update memory-bank/@architecture.md.
    > ```
  - 示例：确保其他（非 "Always"）规则引导 AI 遵循你技术栈的最佳实践（如网络、状态管理等）。
  - *如果你想要一个尽可能优化、代码尽可能整洁的游戏，这套整体规则设置是强制性的。*

### 3. 实施计划 (Implementation Plan)
- 向 **GPT-5** 或 **Sonnet 4.5** 提供：  
  - 游戏设计文档 (`game-design-document.md`)
  - 技术栈推荐 (`tech-stack.md`)
- 要求它创建一个详细的 Markdown 格式的 **实施计划** (`.md`)，这是一套给 AI 开发者的分步指令。  
  - 步骤应小而具体。  
  - 每个步骤必须包含验证正确实施的测试。  
  - 不要写代码——只需清晰、具体的指令。  
  - 专注于*基础游戏*，而不是完整的功能集（细节稍后添加）。  

### 4. 记忆库 (Memory Bank)
- 为你的项目创建一个新文件夹，然后在 VSCode 中打开它。
- 在项目文件夹内，创建一个名为 `memory-bank` 的子文件夹。  
- 将以下文件添加到 `memory-bank` 中：  
  - `game-design-document.md`  
  - `tech-stack.md`  
  - `implementation-plan.md`  
  - `progress.md` (创建一个空文件，用于跟踪已完成的步骤)  
  - `architecture.md` (创建一个空文件，用于记录文件用途)

---

## Vibe Coding 开发基础游戏
现在乐趣开始了！

### 确保一切清晰
- 在 VSCode 扩展中打开 **Codex** 或 **Claude Code**，或在项目的终端中启动 Claude Code 或 Codex CLI。 
- 提示词 (Prompt)：Read all the documents in `/memory-bank`, is `implementation-plan.md` clear? What are your questions to make it 100% clear for you?
  *(读取 `/memory-bank` 中的所有文档，`implementation-plan.md` 清晰吗？为了让你 100% 清楚，你有什么问题？)*
- 它通常会问 9-10 个问题。回答这些问题，并提示它相应地编辑 `implementation-plan.md`，使其更加完善。

### 你的第一个实施提示词
- 在 VSCode 扩展中打开 **Codex** 或 **Claude Code**，或在项目的终端中启动 Claude Code 或 Codex CLI。  
- 提示词 (Prompt)：Read all the documents in `/memory-bank`, and proceed with Step 1 of the implementation plan. I will run the tests. Do not start Step 2 until I validate the tests. Once I validate them, open `progress.md` and document what you did for future developers. Then add any architectural insights to `architecture.md` to explain what each file does.
  *(读取 `/memory-bank` 中的所有文档，并开始实施计划的第 1 步。我来运行测试。在我验证测试之前，不要开始第 2 步。一旦我验证通过，打开 `progress.md` 并记录你所做的工作以供未来的开发者参考。然后将任何架构见解添加到 `architecture.md` 以解释每个文件的作用。)*
- **始终**以 "Ask"（询问）模式或 "Plan Mode"（计划模式，Claude Code 中按 `shift+tab`）开始，一旦你满意，允许 AI 执行该步骤。

- **极致 Vibe：** 安装 [Superwhisper](https://superwhisper.com)，可以随意地与 Claude 或 GPT-5 语音交谈，而不是打字。  

### 工作流
- 完成第 1 步后：  
- 将更改提交到 Git（如果不熟悉，请向 AI 求助）。  
- 开始一个新的聊天（`/new` 或 `/clear`）。  
- 提示词 (Prompt)：Now go through all files in the memory-bank, read progress.md to understand prior work, and proceed with Step 2. Do not start Step 3 until I validate the test.
  *(现在浏览 memory-bank 中的所有文件，阅读 progress.md 以了解之前的工作，并继续进行第 2 步。在我验证测试之前，不要开始第 3 步。)*
- 重复此过程，直到整个 `implementation-plan.md` 完成。  

---

## 添加细节
恭喜，你已经构建了基础游戏！它可能很粗糙且缺乏功能，但现在你可以进行实验和完善了。  
- 想要雾气、后期处理、特效或声音？想要更好的飞机/汽车/城堡？绚丽的天空？
- 对于每个主要功能，创建一个新的 `feature-implementation.md` 文件，包含简短的步骤和测试。  
- 增量地实施和测试。  

---

## 修复 Bug 和卡顿
- 如果提示词失败或破坏了游戏：  
- 在 Claude Code 中使用 `/rewind` 并优化你的提示词直到它工作。如果使用 GPT-5，你可以经常提交到 git 并在需要时重置。
- 对于错误：  
    - **如果是 JavaScript：** 打开控制台 (`F12`)，复制错误，并将其粘贴到 VSCode 中，如果由视觉故障请提供截图。  
    - **懒人选项：** 安装 [BrowserTools](https://browsertools.agentdesk.ai/installation) 以跳过手动复制/截图。  
- 如果卡住了：  
    - 回退到上一次 Git 提交 (`git reset`) 并使用新的提示词重试。  
- 如果*真的*卡住了：  
    - 使用 [RepoPrompt](https://repoprompt.com/) 或 [uithub](https://uithub.com/) 将整个代码库放入一个文件中，并向 **GPT-5 或 Claude** 寻求帮助。  

---

## Claude Code & Codex 技巧
- **终端中的 Codex CLI 或 Claude Code：** 在 VSCode 的终端内运行任一工具，以查看差异 (diffs) 并提供额外的上下文，而无需离开工作区。
- **Claude Code `/rewind`：** 如果一次迭代没有达到目标，使用此命令将项目回滚到较早的状态。
- **自定义 Claude Code 命令：** 创建像 `/explain $arguments` 这样的助手，触发诸如 "Do a deep-dive on the code and understand how $arguments works. Once you understand it, let me know, and I will provide the task I have for you." *(深入研究代码并理解 $arguments 是如何工作的。一旦你理解了，告诉我，我再给你布置任务)* 的提示词，这样模型在编辑之前会提取丰富的上下文。
- **清除上下文：** 如果你仍然需要以前的对话上下文，请频繁使用 `/clear` 或 `/compact` 清除上下文。
- **节省时间（风险自负）：** 使用 `claude --dangerously-skip-permissions` 或 `codex --yolo` 启动 Claude Code 或 Codex CLI，在这种模式下它永远不会要求你确认。

## 其他技巧
- **小幅修改：** 使用 GPT-5 (medium)
- **优秀的营销文案：** 使用 Opus 4.1
- **生成优秀的 Sprite（2D 图像）：** 使用 ChatGPT 和 Nano Banana
- **生成音乐：** 使用 Suno
- **生成音效：** 使用 ElevenLabs
- **生成视频：** 使用 Sora 2
- **更好的提示词输出：** - 添加 “think as long as needed to get this right, I am not in a hurry. What matters is that you follow precisely what I ask you and execute it perfectly. Ask me questions if I am not precise enough." *(思考多久都可以，只要把这件事做对，我不急。重要的是你精确地遵循我的要求并完美执行。如果我不够精确，请问我问题。)*
    - 对于 Claude Code，使用特定短语触发更深层的推理：`think` < `think hard` < `think harder` < `ultrathink`。

---

## 常见问题 (FAQ)
**问：我是在做一个应用程序，而不是游戏，这个工作流一样吗？** **答：** 工作流基本是一样的，是的！不用 GDD（游戏设计文档），你可以做一个 PRD（产品需求文档）。你也可以先使用像 v0、Lovable 或 Bolt.new 这样的优秀工具进行原型设计，然后将代码移动到 GitHub，接着克隆它以便在 VSCode 或终端中按照本指南继续开发。

**问：你在空战游戏里的飞机太棒了，但我无法用一个提示词复刻它！** **答：** 那不是一个提示词——那是大约 30 个提示词，由一个特定的 `plane-implementation.md` 文件指导。使用尖锐、具体的提示词，如“在机翼上为副翼切出空间”，而不是模糊的“做一架飞机”。

**问：为什么 Claude Code 或 Codex CLI 现在比 Cursor 更好？** **答：** 这真的取决于你的喜好。我们强调 Claude Code 在使用 Claude Sonnet 4.5 方面更好，而 Codex CLI 在使用 GPT-5 方面比 Cursor 使用它们中的任何一个都更好。让它们活在终端中解锁了更多的开发工作流：在任何 IDE 中工作，通过 SSH 跳到远程服务器等等。还有强大的自定义选项，如自定义命令、子代理 (sub-agents) 和钩子 (hooks)，随着时间的推移，这将加速开发的质量和速度。最后，如果你使用的是低层级的 Claude 或 ChatGPT 计划，这足以入门。

**问：我不知道如何为我的多人游戏设置服务器** **答：** 问你的 AI。

---
