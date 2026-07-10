# 示例提示词

这些示例用于演示如何触发两个核心 Skill。使用真实材料时请先脱敏，不要把证件号、手机号、邮箱、真实截图和未公开源码提交到公开仓库。

## 生成申请表草稿

```text
Use $university-copyright-application-form to draft and validate a university software copyright registration application form.

请根据以下信息生成《计算机软件著作权登记申请表》填写草稿，并列出缺失项和风险点。

软件全称：示例智能文档管理系统
软件简称：文档管理系统
版本号：V1.0
开发完成日期：2026年7月1日
软件分类：应用软件
发表状态：未发表
开发方式：独立开发
编程语言：Python、JavaScript
主要功能：用户登录、文档上传、文档分类、全文检索、权限管理、操作日志、报表导出
开发目的：提升文档归档、检索和权限管理效率
面向领域：高校科研项目文档管理
运行环境：Windows 11 / Ubuntu 22.04，Chrome 浏览器
开发工具：VS Code、Git、PostgreSQL、FastAPI、Vue
源程序量：待统计
著作权人：待确认
联系人：待确认
```

## 生成 20 页以上软件说明书

```text
Use $university-copyright-software-manual to generate a complete university software copyright manual.

请生成完整软件说明书正文，复制到 Word 后不少于 20 页。可以按第 1 卷、第 2 卷、第 3 卷分批输出，但不要只给目录或前两章样例。每卷末尾请给出累计字数估算和下一卷起点。

软件全称：示例智能文档管理系统
版本号：V1.0
开发完成日期：2026年7月1日
目标用户：高校科研团队、项目管理员、普通成员
软件用途：用于科研项目文档的上传、分类、检索、权限控制和归档管理
核心模块：
1. 用户登录与权限管理
2. 文档上传与元数据录入
3. 文档分类与标签管理
4. 全文检索与筛选
5. 操作日志与审计
6. 报表统计与导出
技术栈：FastAPI、Vue、PostgreSQL、Redis、Nginx
运行环境：Windows 11 或 Ubuntu 22.04，Chrome/Edge 浏览器
截图情况：暂未提供真实截图，请使用图位占位、图题和图注说明
测试情况：请设计功能测试、异常测试和权限测试场景
```

## 根据申请表摘要续写说明书

```text
Use $university-copyright-software-manual to draft a long software manual based on the application-form facts below.

下面是申请表 Skill 输出的项目事实摘要。请基于这些事实生成完整说明书正文，目标不少于 20000 中文字符。缺少截图时使用图位占位，不要虚构真实截图。

项目事实摘要：
- 软件全称：示例智能文档管理系统
- 版本号：V1.0
- 主要功能：用户登录、文档上传、分类标签、全文检索、权限管理、日志审计、报表导出
- 技术特点：信息安全软件、人工智能软件、智慧城市软件
- 运行环境：Windows 11 / Ubuntu 22.04，Chrome 浏览器
- 开发工具：VS Code、Git、PostgreSQL、FastAPI、Vue
- 鉴别材料：多种文档：平台原型、说明文档
```

## 校验说明书完整度

```text
Use $university-copyright-software-manual to validate this software manual against university software copyright documentation expectations.

请检查下面的软件说明书草稿是否适合软著文档鉴别材料，重点看章节覆盖、图表说明、功能模块具体性、长度是否足够 20 页、是否存在模板化或虚构内容。

【粘贴说明书草稿】
```
