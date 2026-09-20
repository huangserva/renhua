# 人话 (renhua)

中文 AI/技术写作的去 AI 味编辑器，做成 Claude Code skill。

把一段中文 AI 技术稿改成作者本人的口吻：保住事实、数字、模型名、技术术语和作者的判断，删掉 AI 写作特有的结构壳子和表演性词汇。

适用题材：推特长文、技术拆解、模型测评、产品笔记、公开发布的草稿。

## 它管什么

这个 skill 不做通用的「润色」，它只干一件事——把稿子里能被一眼认出是 AI 代笔的地方揪出来改掉，同时不把作者的声音一起抹平。

规则分两层：

- **Hard Bans**：一条条列出禁用的句式和词，每条都带 Bad / Better 对照示例。
- **Before Returning**：交稿前的机器检查清单，逐条比对字符串和句式。

## 安装

```bash
git clone git@github.com:huangserva/renhua.git ~/.claude/skills/renhua
```

装好之后在 Claude Code 里直接说「用 renhua 改一下这段」，或者让它自己按 description 触发。

## 用法

默认只返回改好的正文，不带诊断、不带修改说明。

想知道某句为什么像 AI 写的，明说要诊断，它会返回 3 到 6 条具体触发点，每条引用原句并指出是哪种模式。

## 文件

- `SKILL.md` — 全部规则
- `agents/openai.yaml` — OpenAI agent 接口配置

## 许可

个人使用。规则来自真实改稿积累，对着别人的文风不一定适用。
