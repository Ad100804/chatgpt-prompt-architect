# ChatGPT Prompt Architect — 中文使用指南

[English README](../README.md)

## 项目介绍

**Prompt Architect** 是一个以 `SKILL.md` 和自定义指令构成的 ChatGPT 内置式任务规划工作流。用户可以从不完整的想法出发，与 AI 讨论需求、整理资源、比较方案并确认细节，最后生成一份**可复制到 ChatGPT Work 或 Codex 的完整执行提示词**。

这不是独立桌面软件，不是 OpenAI 官方功能，也不能自动把普通文本 `/prompt` 注册为客户端真正的斜杠菜单命令。

## 与外置提示词改写工具相比有什么优势？

1. **不必切换应用**：可在当前 ChatGPT 工作环境里规划，再把执行简报交给 Work/Codex。
2. **可以多轮确认**：不是只润色一句提示词，而是先理解任务、选方案、询问重要细节。
3. **利用实际可见上下文**：可以基于当前会话实际提供的资料规划，不用重复解释已明确的信息。但 Side Chat **不保证**看到主聊天全部内容，也不保证能直接使用所有附件和工具。
4. **资源化管理**：Sources、文件、Skills、Plugins、约束和交付物都有固定编号，方便后续改动。
5. **规划与执行分离**：先讨论，再由用户将最终执行简报交给主 Agent，减少任务准备时误操作文件。

## 推荐仓库结构

- `skills/prompt-architect/SKILL.md`：真正的提示词规划 Skill。
- `skills/prompt-start/SKILL.md`：可选的主聊天等待 Skill。
- `instructions/global-custom-instructions.md`：全局 `/prompt` 文本触发规则。
- `instructions/codex-AGENTS-snippet.md`：Codex `AGENTS.md` 规则。
- `instructions/response-modes-optional.md`：独立的 `/ui`、`/text` 回答方式约定（非必需）。
- `templates/execution-brief.md`：输出模板。
- `examples/affinity-slideshow.md`：示例。

## 安装与配置

### 1. 安装主 Skill

在支持 Skills 的 ChatGPT 桌面版中，可以使用 Skill 创建器把仓库中 `skills/prompt-architect/SKILL.md` 的内容创建/导入成 Skill。Work 可通过 `@skill-creator` 创建；Codex 可使用 `$skill-creator`。具体调用方式以当前客户端提供的 Skill 入口为准。

对于 Codex，也可以先把仓库下载到本地，再运行：

```bash
mkdir -p ~/.agents/skills/prompt-architect
cp skills/prompt-architect/SKILL.md ~/.agents/skills/prompt-architect/SKILL.md
```

上述 `cp` 假设终端当前目录是本仓库根目录。不会自动为 ChatGPT 全局 Custom Instructions 添加规则。

### 2. 可选：加入 `/prompt` 启动规则

**ChatGPT Chat / Work**：打开 **Settings → Personalization → Custom Instructions**，参考 `instructions/global-custom-instructions.md`，把指令内容追加到已有设置里。

**Codex**：把 `instructions/codex-AGENTS-snippet.md` 的指令段加入自己的 `~/.codex/AGENTS.md`。先检查旧内容，不要覆盖全部文件。

以后在新主聊天发送：

```text
/prompt
```

注意这只是模型可识别的**文字触发词**，不是系统级命令。如果客户端无法将其当作普通文字发送，改用：

```text
[PROMPT]
```

## 标准工作流程

1. **新建主聊天**：发送 `/prompt` 或 `[PROMPT]`，让它暂不执行任务。
2. **打开 Side Chat（若当前模式支持）**：或在普通 Chat 开启独立规划会话。
3. **调用 Prompt Architect**：用自然语言描述想法，如“我想完善我的 FPS 游戏多人系统，但架构还没想清楚”。
4. **核对资源清单**：确认 S01/R01 等资料是否真实可用；检查推荐的 Skill 和 Plugin 是否安装。
5. **选方案、回答问题**：例如 `O02；Q01：只修改第 3–7 页；删除 P01`。
6. **输出最终简报**：输入“生成最终执行提示词”。
7. **正式执行**：将以 `EXECUTE APPROVED BRIEF` 开头的完整提示词，连同主会话所需的文件，发送给 Work 或 Codex。

执行触发词也只是用户与模型之间的约定，不能替代真正的权限确认。

## 编号格式

| 编号 | 类型 | 示例 |
|---|---|---|
| `S01` | Sources 参考资料 | 作业要求、Rubric、官方文档 |
| `R01` | Resources 资源 | PPT、截图、项目文件夹 |
| `K01` | Skills | 某个已安装或待确认的 Skill |
| `P01` | Plugins/Tools | MCP、外部应用和插件 |
| `C01` | Constraints 限制 | 不要改动其他页面 |
| `O01` | Options 方案 | 仅精简 / 平衡优化 / 完全重设计 |
| `Q01` | Questions 问题 | 哪些文件可编辑？ |
| `D01` | Deliverables 交付物 | PPTX、报告、测试结果 |

## 实用规则

- 对直白的小任务使用 **Quick**；常规任务 **Standard**；复杂设计或编程 **Deep**。
- 所有建议的 Skills/Plugins 都要区分“已确认可用”“建议使用”“不可用”。
- 不要把 GitHub 仓库里公开的示例误当作你的真实私人附件。
- 在规划阶段不修改文件、不运行实现命令、不安装第三方工具。
- Side Chat 的消息不会默认自动同步给主任务，所以最终提示词必须独立完整。
- 上传 GitHub 前检查：不要包含私有聊天记录、真实文件路径、密码、API Key 和认证信息。

## 可选功能：`/ui` / `/text`

`instructions/response-modes-optional.md` 单独提供交互式 UI / 文字输出模式的文本指令。它是一个**独立的桌面个性化模块**，不依赖 Prompt Architect。是否显示原生交互组件由 ChatGPT 客户端实际能力决定，无法仅靠自定义指令强制开启。

## 开发状态

当前提供的是 **v0.1.0 开源模板**，供使用者验证和迭代；不宣称已经在所有 Chat/Work/Codex 客户端完成测试。欢迎反馈和改进。项目采用 MIT License。
