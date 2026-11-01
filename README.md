# AI-READONLY: 仓库总览

# personal-ai-archive — 个人跨 AI 记忆系统

本仓库是个人身份与 AI 协作的「单点档案库」：身份、工作流、偏好、技能、经验统一存放，任何 AI（豆包 / ChatGPT / Gemini / Claude 等）都可以直接读取，并在每次任务中应用、任务后沉淀。

## 目录结构

| 目录 | 内容 | AI 用途 |
| --- | --- | --- |
| `identity/` | 个人身份、职业、核心标签、人生目标 | 称呼与上下文定位 |
| `workflow/` | 工作习惯、常用工具、沟通风格、优先级规则 | 输出风格与执行规则 |
| `memory/` | 历史经验、重要决策、AI 对话沉淀偏好 | 复用经验、避免重复犯错 |
| `skills/` | 已掌握技能、学习计划、待提升能力 | 能力评估与学习规划 |
| `archive/` | 历史项目、旧文档、已完成任务归档 | 旧材料检索与复用 |

## 档案文件直读链接（raw）

> 用户或 AI 直接复制以下链接即可读取对应档案：

- 身份档案：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/identity/profile.md
- 沟通风格：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/workflow/communication.md
- 工作习惯：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/workflow/habits.md
- 优先级规则：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/workflow/priorities.md
- 个人偏好：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/memory/preferences.md
- 经验教训：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/memory/lessons.md
- 决策记录：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/memory/decisions.md
- 技能现状：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/skills/current.md
- 学习计划：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/skills/learning.md
- 待提升能力：https://raw.githubusercontent.com/heartyan/personal-ai-archive/main/skills/growth.md

## 给 AI 的读取顺序建议

1. 先读 `identity/profile.md` 建立对用户的认知；
2. 再读 `workflow/` 下三个文件，确定沟通风格、工具偏好和优先级规则；
3. 任务涉及历史经验时查 `memory/`；
4. 涉及能力评估或学习规划时查 `skills/`；
5. 任务结束后，将新产生的经验/偏好按 `ai-integration.md` 的更新规则写入对应文件。

## 使用约定

- 所有模板文件头部带 `# AI-READONLY:` 标签，AI 据此快速识别文件用途；
- 占位符格式：`{{字段名}}`，由用户本人或 AI 在确认后填写，填写后删除占位符；
- 公开仓库内只放不敏感信息，敏感内容（全名、证件号、住址、账号、密码等）永不入仓；
- 所有修改通过 Git 提交，保留完整历史，可随时回退。

## 跨 AI 接入

详细接入与自动更新规则见 [`ai-integration.md`](ai-integration.md)。