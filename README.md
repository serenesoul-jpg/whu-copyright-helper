# University Software Copyright Helper

面向高校软件著作权登记材料准备的 Codex Skills 项目。它把申请表填写、软件说明书撰写和材料验收中的经验整理成可复用的 AI 工作流，让 Codex 能按稳定规则生成草稿、列出缺失信息并检查常见风险。

本项目是非官方开源工具，不代表任何高校、登记机构或代理机构。仓库中的字段规则和默认值来自通用软著材料整理经验，可根据所在单位的实际要求调整。

本项目目前聚焦两个核心 Skill：

- `university-copyright-application-form`：生成并校验《计算机软件著作权登记申请表》填写草稿。
- `university-copyright-software-manual`：生成软著软件说明书、用户手册、设计说明书或操作手册正文，支持 20 页以上长文档分卷输出。

> 本项目用于材料整理和一致性检查，不提供法律意见，也不承诺登记结果。

## 功能

- 按高校软著材料场景整理申请表字段、默认值、必填项和冲突检查。
- 根据项目功能、截图、架构和申请表信息生成软件说明书正文。
- 为说明书提供 20000 字以上长文档输出协议、章节字数预算和分卷续写规则。
- 输出待补充信息、验收风险、截图清单、图注和 Word 可用正文。
- 保持 Skill 渐进式加载：核心流程在 `SKILL.md`，详细规则在 `references/`。

## 目录结构

```text
.
├── .codex/skills/
│   ├── university-copyright-application-form/
│   │   ├── SKILL.md
│   │   ├── agents/openai.yaml
│   │   └── references/
│   └── university-copyright-software-manual/
│       ├── SKILL.md
│       ├── agents/openai.yaml
│       └── references/
├── examples/
│   └── prompts.md
├── docs/
│   └── compatibility.md
├── skill-learning/
│   └── README.md
├── CONTRIBUTING.md
├── SECURITY.md
└── LICENSE
```

## 安装

本项目的 Skill 内容主要由 `SKILL.md` 和 `references/` 组成，可在 Codex、Claude Code、WorkBuddy/CodeBuddy 等支持 Skill 机制的工具中复用。不同工具的目录名称不同，详细说明见 [docs/compatibility.md](docs/compatibility.md)。

### 方式一：在本仓库中使用

把仓库作为 Codex 工作区打开即可。仓库内的 `.codex/skills` 会作为本项目的本地 Skill 使用。

### 方式二：安装到个人 Skills 目录

如果希望在其他项目中也能使用，可以复制两个 Skill 到对应工具的个人目录。

Codex：

PowerShell：

```powershell
Copy-Item -Recurse .codex\skills\university-copyright-application-form $env:USERPROFILE\.codex\skills\
Copy-Item -Recurse .codex\skills\university-copyright-software-manual $env:USERPROFILE\.codex\skills\
```

Bash：

```bash
mkdir -p ~/.codex/skills
cp -R .codex/skills/university-copyright-application-form ~/.codex/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.codex/skills/
```

Claude Code 常见目录：

```bash
mkdir -p ~/.claude/skills
cp -R .codex/skills/university-copyright-application-form ~/.claude/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.claude/skills/
```

WorkBuddy / CodeBuddy 常见目录：

```bash
mkdir -p ~/.codebuddy/skills
cp -R .codex/skills/university-copyright-application-form ~/.codebuddy/skills/
cp -R .codex/skills/university-copyright-software-manual ~/.codebuddy/skills/
```

企业定制版客户端可能使用不同目录，请以客户端实际文档为准。

## 使用示例

申请表草稿：

```text
Use $university-copyright-application-form to draft and validate a university software copyright registration application form.

软件名称：XXX系统
版本号：V1.0
开发完成日期：2026年7月1日
主要功能：...
运行环境：...
著作权人：...
```

20 页以上软件说明书：

```text
Use $university-copyright-software-manual to generate a complete university software copyright manual.

请根据以下项目信息生成完整软件说明书正文，要求复制到 Word 后不少于 20 页。可以分卷输出，但不要只给目录或样例。

软件名称：XXX系统
版本号：V1.0
核心模块：...
技术栈：...
界面截图清单：...
```

更多提示词见 [examples/prompts.md](examples/prompts.md)。

## 当前完成度

- 申请表 Skill：已具备字段草稿、默认规则、缺失项、冲突检查和验收风险输出。
- 说明书 Skill：已具备完整长文档协议，默认按 20000 中文字符以上规划，并支持分卷续写和长度自检。
- 尚未包含 `.docx` 自动排版、源代码鉴别材料整理、校内附件信息表和完整材料打包脚本。

## 开发与校验

修改 Skill 时建议检查：

- `SKILL.md` frontmatter 只包含 `name` 和 `description`。
- `description` 覆盖触发场景和排除场景。
- 长规则放在 `references/`，并从 `SKILL.md` 明确链接。
- 不把用户隐私、证件号码、真实联系人和未公开项目材料提交到仓库。

仓库内的 [skill-learning](skill-learning/README.md) 保存了 Skill 编写学习笔记、检查清单和评估模板。

## 免责声明

本项目仅用于辅助整理软件著作权登记材料，不是官方系统、官方模板或法律服务。不同学校、地区、代理流程和受理机构的要求可能变化，请以所在单位通知、中国版权保护中心和实际办理要求为准。使用者应自行核对权利归属、证件信息、日期、代码量和材料真实性。

## License

MIT License. See [LICENSE](LICENSE).
