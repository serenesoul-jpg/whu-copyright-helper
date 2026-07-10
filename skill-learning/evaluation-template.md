# Skill 评估模板

评估主要回答两个问题：

1. Skill 是否在正确的时候触发？
2. 触发后，结果是否比没有 Skill 更稳定、更准确？

## 触发评估

准备混合用例。正例应该触发，反例不应该触发，边界例用于澄清模糊表达。

| ID | 类型 | 用户请求 | 期望 | 备注 |
| --- | --- | --- | --- | --- |
| T01 | 正例 | 帮我把这个 Go 项目从 old-http-client 迁移到 unified-httpclient。 | 触发 | 直接匹配 |
| T02 | 正例 | 替换 `pkg/request` 里的旧请求客户端导入。 | 触发 | “迁移”的同义表达 |
| T03 | 反例 | 帮我审查这个 Go 函数的可读性。 | 不触发 | 一般代码审查 |
| T04 | 反例 | 调试一下 HTTP 接口为什么返回 500。 | 不触发 | 运行时调试，不是迁移 |
| T05 | 边界 | 检查这个项目是否还在用旧 HTTP 客户端。 | 视情况触发 | 如果 Skill 包含发现/预检查流程，则可以触发 |

建议指标：

- Precision：触发的用例里，有多少本来就应该触发。
- Recall：应该触发的用例里，有多少真的触发了。
- 可用目标：85% 以上；优秀目标：95% 以上。

## 效果评估

每个效果用例都应包含输入、期望行为和评分标准。

### 用例 Q01：典型迁移

输入：

```go
package request

import oldhttp "github.com/example/old-http-client"

func Do(req *oldhttp.Request) (*oldhttp.Response, error) {
    return oldhttp.Do(req)
}
```

期望行为：

- 更新 import 到新包。
- 如果 API 映射要求，更新请求和响应类型。
- 保留 package 名、函数名和无关格式。
- 运行或建议正确验证命令。

评分标准：

- [ ] import 替换正确。
- [ ] 类型和调用适配正确。
- [ ] 没有无关重写。
- [ ] 包含验证步骤。
- [ ] 对模糊 API 差异标注人工确认。

### 用例 Q02：边界场景

输入：

```go
const help = "old-http-client appears in documentation only"
```

期望行为：

- 不要盲目替换纯文档字符串，除非 Skill 明确要求更新文档。
- 说明代码导入和文字引用为什么不同。

评分标准：

- [ ] 区分代码和说明文字。
- [ ] 避免不安全的全局替换。
- [ ] 清楚报告剩余引用。

## 评估报告格式

```text
Skill: <skill-name>
版本/日期: <version or date>

触发评估：
- 用例数: <count>
- Precision: <percent>
- Recall: <percent>
- 漏触发: <ID 和原因>
- 误触发: <ID 和原因>

效果评估：
- 用例数: <count>
- 平均分: <score>
- 表现好的方面: <summary>
- 薄弱环节: <summary>
- 已做修订: <description 变更、示例补充、脚本补充等>
```

