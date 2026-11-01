# AI-READONLY: 跨AI适配配置

# ai-integration — 跨 AI 平台接入配置

本文件说明如何将 `personal-ai-archive` 接入主流 AI 平台，实现「一次搭建、全平台复用」。

## 一、目录读取指引（AI 通用）

| 目录 | 文件 | 内容 | 什么时候读 |
| --- | --- | --- | --- |
| identity/ | profile.md | 身份、职业、标签、目标 | 每次任务开始时 |
| workflow/ | habits.md | 工作习惯、常用工具 | 涉及工具与方法时 |
| workflow/ | communication.md | 沟通风格、称呼、输出偏好 | 每次回复前 |
| workflow/ | priorities.md | 任务优先级与处理规则 | 多任务、冲突时 |
| memory/ | lessons.md | 历史经验与教训 | 同类任务、决策前 |
| memory/ | decisions.md | 重要决策记录 | 需要对齐历史口径时 |
| memory/ | preferences.md | AI 对话沉淀的偏好 | 每次任务结束时核对 |
| skills/ | current.md | 已掌握技能 | 能力评估时 |
| skills/ | learning.md | 学习计划 | 学习规划时 |
| skills/ | growth.md | 待提升能力 | 提升建议时 |
| archive/ | README.md | 历史项目归档索引 | 旧材料检索时 |

## 二、主流平台接入方式

### 方式一：提示词直连（ChatGPT / Gemini / Claude 等对话模型）

通过 GitHub raw 链接让模型直接拉取档案，无需下载：

```
https://raw.githubusercontent.com/{{你的GitHub用户名}}/personal-ai-archive/main/identity/profile.md
```

建议提示词模板：

```
请先读取我的个人档案仓库：https://github.com/{{你的GitHub用户名}}/personal-ai-archive
规则：
1. 读取 identity/profile.md，按其中信息称呼我并定位我的背景；
2. 读取 workflow/ 三个文件，按我的沟通风格和优先级规则输出；
3. 涉及历史问题时查 memory/ 目录；
4. 任务结束后，把新产生的经验/偏好追加到 memory/preferences.md 并提交。
```

### 方式二：Agent 自动同步（Meta Muse / OpenAI Dots / 豆包等 Agent 型 AI）

1. 克隆仓库到本地或 Agent 工作区：
   ```
   git clone https://github.com/{{你的GitHub用户名}}/personal-ai-archive.git
   ```
2. 在 Agent 配置中声明档案路径，任务开始前自动读取 `identity/` 与 `workflow/`；
3. 配置任务结束钩子，按下方「自动更新规则」写回新偏好并提交。

### 方式三：GitHub API（供开发者/自建 Agent）

```bash
# 读取档案
curl -H "Authorization: Bearer {{TOKEN}}" \
  https://api.github.com/repos/{{你的GitHub用户名}}/personal-ai-archive/contents/identity/profile.md

# 更新档案（写入新偏好）
curl -X PUT -H "Authorization: Bearer {{TOKEN}}" \
  -H "Accept: application/vnd.github+json" \
  https://api.github.com/repos/{{你的GitHub用户名}}/personal-ai-archive/contents/memory/preferences.md \
  -d '{"message":"feat(preferences): 新增偏好","content":"BASE64内容","branch":"main"}'
```

## 三、自动更新规则

AI 在每次任务完成后，按以下规则沉淀内容：

1. **新经验** → 追加到 `memory/lessons.md`（一行一条：`- 时间 | 场景 | 经验/教训`）；
2. **新决策** → 追加到 `memory/decisions.md`（含时间、背景、决策、理由）；
3. **新偏好**（用户纠正、明确要求）→ 追加到 `memory/preferences.md`，删除已失效条目；
4. **工作习惯/工具变化** → 更新 `workflow/habits.md`；
5. **技能变化** → 更新 `skills/current.md` 或 `skills/growth.md`。

提交信息规范：

```
feat(preferences): 一句话描述本次沉淀
docs(workflow): 更新沟通风格
```

规则：**不删除用户已确认的内容**；修改前先读当前文件；每次修改走一次 Git 提交，保留可回退历史。

## 四、版本与安全

- **版本控制**：所有变更自动生成 Git 提交记录，可一键回退（`git log` 查看历史，`git revert <commit>` 回退）；
- **公开仓库边界**：本仓库为公开仓库，只存放模板与占位符；真实身份、财务、医疗等敏感信息**禁止**写入公开仓库；
- **敏感信息方案**：真实档案建议放入同名私有仓库，公开仓库通过占位符/环境变量引用；
- **定期备份**：建议每月将仓库导出一次本地备份。
