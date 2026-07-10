# Skill 编写学习笔记

这个目录用于沉淀“如何写好 Skill”的学习材料。内容结合了本地 `skill-creator` 官方指导，以及本次对话中提供的中文实战手册，整理成后续可以直接复用的笔记、模板、检查清单和评估框架。

## 核心理解

Skill 是给 AI 编程助手使用的能力包。它把某个领域、项目或重复流程中的经验，整理成一个可被按需加载的文件夹，让另一个 AI Agent 不必重新摸索，就能按稳定流程完成任务。

一个常见结构如下：

```text
skill-name/
├── SKILL.md              # 必需：元数据 + 核心指令
├── agents/               # 推荐：Skill 列表和 UI 展示元数据
│   └── openai.yaml
├── scripts/              # 可选：确定性脚本，适合重复或脆弱操作
├── references/           # 可选：按需读取的详细参考资料
└── assets/               # 可选：输出中会用到的模板、图片、字体等资源
```

## 渐进式加载

写 Skill 的关键不是“把所有知识都塞进去”，而是把信息放在合适的加载层级，尽量节省上下文窗口。

| 层级 | 加载时机 | 内容 | 设计原则 |
| --- | --- | --- | --- |
| Level 1 | 始终可见 | `name` 和 `description` | 触发描述要精准、完整 |
| Level 2 | Skill 被选中后 | `SKILL.md` 正文 | 只放核心流程，建议控制在 500 行以内 |
| Level 3 | 执行时按需读取 | scripts、references、assets | 详细示例、规格、长文档放这里 |

## 好 Skill 的要点

1. 只解决一件明确的事。复杂流程可以拆成主 Skill、子 Skill 或 reference 文件。
2. 写好 `description`。它必须说明 Skill 做什么、什么时候用、适用哪些技术和任务、哪些相邻任务不该触发。
3. 使用直接的指令语气。告诉 Agent 做什么、检查什么、何时停止。
4. 对脆弱规则解释原因。Agent 理解“为什么”后，遇到变体更容易做对。
5. 为关键转换提供 Before/After 示例。具体例子通常比长段解释更可靠。
6. 在关键步骤之间加入检查点。不要等所有步骤完成后才发现第一步已经错了。
7. 把重复、脆弱、需要确定性的逻辑写成脚本。
8. 把背景、详细规范、长表格放进 `references/`，不要把 `SKILL.md` 写成 Wiki。
9. 避免秘密泄露和危险自动化。脚本要校验输入和路径，危险操作要确认或备份。
10. 用触发评估和效果评估验证 Skill，而不是只凭感觉判断好坏。

## 推荐创建流程

1. 收集具体使用场景、反例场景和边界场景。
2. 判断是否需要 `scripts/`、`references/` 或 `assets/`。
3. 创建标准 Skill 目录。
4. 编写 `SKILL.md`，frontmatter 只保留 `name` 和 `description`。
5. 先补充可复用资源，再在 `SKILL.md` 中清楚说明何时读取它们。
6. 校验目录结构、YAML frontmatter 和命名规则。
7. 运行触发评估和效果评估，根据结果迭代。

## 本目录文件

- [skill-template.md](skill-template.md)：可直接改写的 `SKILL.md` 模板。
- [checklist.md](checklist.md)：发布或使用前的质量、结构、安全、评估检查清单。
- [evaluation-template.md](evaluation-template.md)：触发评估和效果评估模板。
- [anti-patterns.md](anti-patterns.md)：常见反模式和修正方式。

