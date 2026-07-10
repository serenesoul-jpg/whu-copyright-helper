# 多平台兼容性说明

本项目的核心内容是标准 Markdown Skill：每个 Skill 都包含 `SKILL.md`、可选的 `references/` 和 `agents/openai.yaml`。其中 `SKILL.md` 与 `references/` 是跨平台复用的主体，`agents/openai.yaml` 主要用于 OpenAI/Codex 相关界面展示，其他工具可以忽略。

## 兼容性概览

| 平台 | 推荐目录 | 可用内容 | 备注 |
| --- | --- | --- | --- |
| Codex | `.codex/skills/` 或 `~/.codex/skills/` | `SKILL.md`、`references/`、`agents/openai.yaml` | 当前仓库原生支持 |
| Claude Code | `.claude/skills/` 或 `~/.claude/skills/` | `SKILL.md`、`references/` | 可能忽略 `agents/openai.yaml` |
| WorkBuddy / CodeBuddy | `.codebuddy/skills/` 或用户级 skills 目录 | `SKILL.md`、`references/` | 目录名以实际客户端文档为准 |
| 其他支持 Skills 的 Agent | 对应工具的 skills 目录 | `SKILL.md`、`references/` | 需确认 frontmatter 兼容性 |

## 项目级安装

项目级安装只对当前仓库生效，适合把本仓库作为软著材料工作区使用。

### Codex

仓库已经内置：

```text
.codex/skills/
├── university-copyright-application-form/
└── university-copyright-software-manual/
```

打开仓库后即可使用。

### Claude Code

将两个 Skill 复制到 `.claude/skills/`：

```bash
mkdir -p .claude/skills
cp -R .codex/skills/university-copyright-application-form .claude/skills/
cp -R .codex/skills/university-copyright-software-manual .claude/skills/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force .claude\skills
Copy-Item -Recurse .codex\skills\university-copyright-application-form .claude\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual .claude\skills\
```

### WorkBuddy / CodeBuddy

常见项目级目录为 `.codebuddy/skills/`。如果你的客户端使用其他路径，请以客户端文档为准。

```bash
mkdir -p .codebuddy/skills
cp -R .codex/skills/university-copyright-application-form .codebuddy/skills/
cp -R .codex/skills/university-copyright-software-manual .codebuddy/skills/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force .codebuddy\skills
Copy-Item -Recurse .codex\skills\university-copyright-application-form .codebuddy\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual .codebuddy\skills\
```

## 用户级安装

用户级安装可在多个项目中复用。

### Codex

```bash
mkdir -p ~/.codex/skills
cp -R .codex/skills/university-copyright-application-form ~/.codex/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.codex/skills/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.codex\skills
Copy-Item -Recurse .codex\skills\university-copyright-application-form $env:USERPROFILE\.codex\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual $env:USERPROFILE\.codex\skills\
```

### Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R .codex/skills/university-copyright-application-form ~/.claude/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.claude/skills/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.claude\skills
Copy-Item -Recurse .codex\skills\university-copyright-application-form $env:USERPROFILE\.claude\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual $env:USERPROFILE\.claude\skills\
```

### WorkBuddy / CodeBuddy

常见用户级目录可能是 `~/.codebuddy/skills/`。如果你的客户端使用企业定制路径，请以客户端或团队文档为准。

```bash
mkdir -p ~/.codebuddy/skills
cp -R .codex/skills/university-copyright-application-form ~/.codebuddy/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.codebuddy/skills/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.codebuddy\skills
Copy-Item -Recurse .codex\skills\university-copyright-application-form $env:USERPROFILE\.codebuddy\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual $env:USERPROFILE\.codebuddy\skills\
```

## 手动触发示例

如果自动触发不稳定，可以在提示词中显式指定 Skill 名称：

```text
Use $university-copyright-application-form to draft and validate the application form.
```

```text
Use $university-copyright-software-manual to generate a complete 20-page software manual.
```

部分工具不支持 `$skill-name` 语法时，可以改成自然语言：

```text
请使用 university-copyright-software-manual 这个 Skill 的规则，生成完整软件说明书正文。
```

## 跨平台注意事项

- 不同工具的自动触发策略不同。若未自动触发，请明确写出 Skill 名称和任务目标。
- 不同工具可能只识别 `SKILL.md`，不会读取 `agents/openai.yaml`；这不影响核心能力。
- 如果工具要求 YAML frontmatter 只包含 `name` 和 `description`，当前两个 Skill 已满足。
- 如果工具不支持按需读取 `references/`，请在提示词中要求它先读取相关 reference 文件。
- 长说明书生成可能受单次回复长度限制。遇到截断时，从上一卷的“下一卷起点”继续。

## 复制后的目录检查

安装后，每个 Skill 目录应至少包含：

```text
university-copyright-application-form/
├── SKILL.md
└── references/

university-copyright-software-manual/
├── SKILL.md
└── references/
```

如果缺少 `references/`，申请表字段规则和说明书长文档协议会不完整。
