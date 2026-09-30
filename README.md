# Seedance Director Skills

让 AI 直接担任总导演。支持剧本理解、完整执行方案、分镜、精修建议、授权修订和可独立复制的 Seedance 提示词。

这是 **Agent Skill 仓库**，`SKILL.md` 告诉 AI 何时使用、如何协作，`references/` 提供按需读取的导演方法。由宿主当前模型完成文本工作，不需要本项目的软件或 DeepSeek API Key；模型使用仍受宿主账号额度/计费影响。

## 快速开始：选择你的接入方式

| 你的工具能力 | 接入方式 |
|---|---|
| 支持 Agent Skills | 安装完整的 `skills/seedance-director` 目录，按该工具的方式启用 |
| 能读取本地文件，但没有 Skill 功能 | 指定 `SKILL.md` 的实际路径，让 AI 按任务读取参考文件 |
| 普通聊天，能上传或粘贴文字 | 提供下面列出的 7 份 Markdown，作为本次对话的导演工作指南 |

通用开场白（先安装或提供文件，再发送）：

```text
请使用 seedance-director 导演指南，读取 SKILL.md 和当前任务需要的参考文件。
如果有文件无法读取，请指出缺失，不要声称已经完整加载。
下面是我的剧本和要求，请先理解，再给我完整执行方案：
（在这里填写剧本和要求）
```

也可直接要求“检查这版分镜，先给建议不要改稿”“只改第二组”“保持设计，整理提示词”。阶段由上下文与授权决定，不必重走流程。

默认协作：讨论 → 完整方案 → 确认后分镜 → 选择精修建议/直接整理/继续修改 → 必要确认 → 最终提示词。明确授权多个步骤可连续执行；默认不会把“精修建议”当成自动改稿。

### 方式一：支持 Agent Skills 的工具

本包采用 [Agent Skills 格式](https://agentskills.io/specification)。复制完整技能目录，不要只复制 `SKILL.md`，也不要把仓库根目录误当技能目录。不同工具的安装位置、启用语法与支持程度不相同。

| 工具 | 用户级目录 | 当前项目目录 | 显式调用示例 |
|---|---|---|---|
| Codex | `~/.agents/skills/seedance-director` | `.agents/skills/seedance-director` | `$seedance-director` |
| Claude Code | `~/.claude/skills/seedance-director` | `.claude/skills/seedance-director` | `/seedance-director` |

每个工具选择用户级或项目级一种方式，避免同名重复。`~` 指运行该工具的用户目录；WSL、远程环境与 Windows 本机目录可能不同。不要覆盖已有同名技能。

上述步骤依据 [Codex 文档](https://learn.chatgpt.com/docs/build-skills) 与 [Claude Code 文档](https://code.claude.com/docs/en/skills)，不是本包在所有产品中的安装实测。其他兼容工具请按其官方说明接入，不能把 `$` 或 `/` 语法当作所有平台通用命令。

`agents/openai.yaml` 仅提供 Codex 的可选显示与调用元数据，不含独有导演规则；其他宿主不依赖它。导演规则只有一套，位于 `SKILL.md` 与 `references/`。

### 方式二：能读本地文件的 AI 助手

下载并解压仓库，告诉 AI 实际文件路径。例如本项目当前本地位置：

```text
请读取 E:/github/seedance-director-skills/skills/seedance-director/SKILL.md，
并按其中的相对路径读取本轮需要的参考文件，然后执行我的导演任务。
```

这是临时加载，不是永久安装；换电脑或目录时替换实际路径。不能读文件的工具请用方式三，不需要为了导演文本工作安装 Codex 或命令行。

### 方式三：普通 AI 聊天窗口

1. 在 GitHub 仓库点击 **Code → Download ZIP**，在电脑上解压；如果已持有本地文件，可跳过下载。
2. 上传以下 7 份文件；不需要上传 README、评测记录、AGENTS.md 或 openai.yaml：

```text
skills/seedance-director/SKILL.md
skills/seedance-director/references/workflow.md
skills/seedance-director/references/directing.md
skills/seedance-director/references/continuity.md
skills/seedance-director/references/output.md
skills/seedance-director/references/review.md
skills/seedance-director/references/project-state.md
```

3. 发送上面的通用开场白和剧本。文件平铺上传也可以，用文件名对应引用。
4. 如果平台不接受 Markdown，可逐份粘贴全文，每份标注原文件名；分批时先说“规则尚未发完，等我说发送完毕再开始”。不要只上传 ZIP 并假定 AI 已解压，也不要只给 GitHub 链接并假定它已读完。

如果附件内容不可读、被截断或超过上下文容量，先补当前阶段所需文件。AI 可处理已经可读的剧本，但必须说明缺失范围；不能假装遵循未读规则。新聊天应重新提供指南、当前稿件及简短交接信息，不假定模型记得上一会话。

此方式是对话指导，不是安装插件。文件读取、长上下文和持续遵循能力因平台与模型而异；没有读写工具时，只在聊天中交付，不声称已存档或永久记住。

## 维护与兼容性

只维护 `skills/seedance-director` 这一套规则，不另存 Codex 版、Claude 版等重复正文。更新仓库后，已复制安装的副本需要同步更新；网页编辑不会自动更新本地目录。不要将私人剧本、聊天、密钥或创作输出提交到此仓库。

“通用”指规则不绑定厂商，**不代表全部 AI 平台已经测试通过**。当前验证范围和未测项见 [VALIDATION.md](VALIDATION.md)。不支持 Skills 的平台走文档接入，不承诺自动发现、跨会话记忆、工具调用或相同创作质量。

## 内容与边界

- 一个入口技能，内含摄影节奏、动作桥、连续性、自适应全局参数、完整输出、精修与接续方法。
- 无固定JSON门禁；正文与辅助检查分开。
- 默认中文说明、台词保留原语言，无BGM/字幕，斜向机位、有效运镜；用户明确例外优先。
- 每组独立描述，视频模型不被假定记得上一组。
- 15/30秒及镜数是可覆盖的创作约定，不是已核验的Seedance官方功能上限。
- 不包含UI、余额显示、自动备份、软件项目数据库、外部API调用或视频制作；不保证实际成片的精确连续性。
- 不依赖原作者本机路径、私人Obsidian笔记、历史对话或其他Skill。

本仓库尚未指定开源许可证。技能分发形式参考 [mattpocock/skills](https://github.com/mattpocock/skills)，未复制其技能内容。
