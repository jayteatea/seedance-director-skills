# Seedance Director Skills

让 Codex 直接担任总导演，而不是调用桌面软件。支持剧本理解、完整执行方案、分镜、精修建议、授权修订和可独立复制的 Seedance 提示词。

这是 **Agent Skill 仓库**，不是应用安装包、模型权重或视频生成服务。`SKILL.md` 告诉 AI 何时使用、如何协作，`references/` 提供按需读取的导演方法。由宿主当前模型完成文本工作，不需要本项目的软件或 DeepSeek API Key；模型使用仍受宿主账号额度/计费影响。

## 使用

安装后在 Codex 输入：

```text
使用 $seedance-director。下面是剧本和要求，请先理解，再给我完整执行方案：
……
```

也可直接要求“检查这版分镜，先给建议不要改稿”“只改第二组”“保持设计，整理提示词”。阶段由上下文与授权决定，不必重走流程。

默认协作：讨论 → 完整方案 → 确认后分镜 → 选择精修建议/直接整理/继续修改 → 必要确认 → 最终提示词。明确授权多个步骤可连续执行；默认不会把“精修建议”当成自动改稿。

## 本地安装（Windows）

将本仓库的 `skills/seedance-director` **整个文件夹**复制到你的用户技能目录 `~/.agents/skills/seedance-director`，不要只复制SKILL.md。或者放到某个创作项目的 `.agents/skills/seedance-director`，仅供该项目使用。两种选一种，避免同名重复。

想继续把实体文件放E盘，可手动把 `~/.agents/skills/seedance-director` 建为指向E盘技能目录的目录链接。不要覆盖已有同名技能；安装前先检查。当前交付仅打包，未自动修改你的Codex设置或安装目录。

Codex通常自动发现技能变化，未出现时重启或新开任务，再查看技能选择器。路径与发现行为依据[官方技能文档](https://learn.chatgpt.com/docs/build-skills)。仅把仓库放在E盘或GitHub上不等于已经安装；向AI提供完整SKILL.md路径也可要求它临时读取执行，但这不等于永久注册。

## 上传 GitHub 后

本仓库根目录就是上传内容；上传文件夹内的文件并保留目录结构。无需上传外层ZIP、软件源码、node_modules或私人创作项目。本次没有自动创建远程仓库或推送。

上传后可让 Codex 的 `$skill-installer` 从你真实仓库中的 `skills/seedance-director` 目录安装。也可在确认使用第三方CLI后参考这种命令（用户名/仓库名需换成实际值，尚未远程实测）：

```text
npx skills@latest add 你的GitHub用户名/你的仓库名 --skill seedance-director
```

仓库布局参考 [mattpocock/skills](https://github.com/mattpocock/skills) 的可安装技能方式，没有复制它的工程技能或要求安装它的setup。没有打包插件市场清单，不把此仓库冒称已上架插件。

## 内容与边界

- 一个入口技能，内含摄影节奏、动作桥、连续性、自适应全局参数、完整输出、精修与接续方法。
- 无固定JSON门禁；正文与辅助检查分开。
- 默认中文说明、台词保留原语言，无BGM/字幕，斜向机位、有效运镜；用户明确例外优先。
- 每组独立描述，视频模型不被假定记得上一组。
- 15/30秒及镜数是可覆盖的创作约定，不是已核验的Seedance官方功能上限。
- 不包含UI、余额显示、自动备份、软件项目数据库、外部API调用或视频制作；不保证实际成片的精确连续性。
- 不依赖原作者本机路径、私人Obsidian笔记、历史对话或其他Skill。

详细测试与限制见 [VALIDATION.md](VALIDATION.md)。发布前请确认内容与授权许可；本次未替你选择MIT等开源授权，不复制第三方素材或代码。公开GitHub不自动等于授予开源许可证。
