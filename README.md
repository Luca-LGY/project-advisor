# 项目顾问 · Project Advisor

一个帮助你在下达 AI 指令前审查项目方向的 Agent Skill。它根据项目目标、现有进展和约束，判断当前这一步该直接做、缩小范围、先验证依赖，还是调整方向。它会给出下一条可以直接交给 AI 的指令，以及可观察的验收标准。

## 什么时候用

| 你遇到的情况 | 项目顾问会给你什么 |
| --- | --- |
| 有目标，但手头有好几件事可以做 | 最近一个可验证的里程碑，以及接下来几步的顺序 |
| 想让 AI 执行一条指令，担心遗漏前提 | 对指令的明确判断、最可能改变决定的信息差，以及最快的验证方法 |
| 做到一半发现接口、权限或环境与预期不同 | 新证据会影响哪个决定，当前能推进哪一步，以及何时重新评估 |

## 安装

### ChatGPT Work

1. 从仓库首页选择 **Code → Download ZIP**，解压后找到 `skills/project-advisor/`。
2. 在 ChatGPT 中打开 **插件 → Skills → 创建 → 从电脑上传**。把 `project-advisor` 技能文件夹打成 ZIP 后上传，保留其中 `SKILL.md`、`agents/` 和 `assets/` 的相对位置。
3. 在项目对话里输入 `@`，选择 **项目顾问**（`project-advisor`）。

[ChatGPT Skills 官方说明](https://help.openai.com/en/articles/20001066-skills-in-chatgpt)

### Codex

把 [技能文件夹](skills/project-advisor) 复制到目标项目的 `.agents/skills/project-advisor/`。希望在多个本地项目里使用时，可以把它放在 `~/.agents/skills/project-advisor/`。安装后，在 Codex 里输入 `$project-advisor`。

[Codex 技能目录官方说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

## 快速开始

在你正在做项目的对话里调用。提供项目目标、进展、限制，以及你准备给 AI 的指令。有 README、代码或运行记录时，可以指定相关路径。

> @project-advisor 我想达成【目标】，现在做到【进展】，需要遵守【约束】。我准备让 AI【拟议指令】。判断这一步值不值得现在做，指出最可能改变决定的未知信息，以及最快怎么验证。给我一条能直接发给 AI 的指令，写清范围、交付物和验收标准。

在 Codex 里，把示例开头的 `@project-advisor` 换成 `$project-advisor`。

## 使用示例

假设你下周要演示一个能从外部服务读取真实数据的应用，已有界面用模拟数据跑通，正准备让 AI 开发登录和首页。

> @project-advisor 演示要求从外部服务读取真实数据并在页面展示。现在模拟数据已跑通，我准备让 AI 先做登录和首页。审查这个顺序，告诉我今天最值得验证什么，再给我下一条指令。

如果演示环境的数据权限还没核实，顾问会建议先用一条可用于演示的真实记录跑通读取和展示。验收证据可以是一次成功的读取记录和页面上的对应字段。如果读取失败，下一条指令应要求记录具体错误和缺失的权限，由这些证据决定先申请权限还是调整演示范围。

## 文件

- [SKILL.md](skills/project-advisor/SKILL.md) 定义触发条件、判断流程和输出要求。
- [agents/openai.yaml](skills/project-advisor/agents/openai.yaml) 定义显示名称、默认提示词和图标路径。
- [assets/icon.svg](skills/project-advisor/assets/icon.svg) 提供技能图标。
