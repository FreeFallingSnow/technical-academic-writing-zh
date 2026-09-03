# 中文技术与学术写作规范

`technical-academic-writing-zh` 是一个指令型 Codex skill，用于在中文技术与学术文稿的起草、修改和定稿过程中持续执行同一套表达规范。

它集中处理五类问题：

- 重复叠加“可能、提示、支持”等证据强度限定；
- 在正文、表格、摘要和结论中重复展开同一信息；
- 将审阅意见、修改说明等写作过程痕迹带入正文；
- 使用双重否定、绕行否定和无技术价值的重复排除；
- 句子承担过多判断、主语不清或条件与结果相互嵌套。

所有规则都受语义保护约束。skill 要求保持事实、数字、术语、条件、因果方向和证据强度，不承担事实核查、文献检索或专业结论判断。

## 安装

在 Codex 中调用内置的 `$skill-installer`：

```text
$skill-installer install the skill from https://github.com/FreeFallingSnow/technical-academic-writing-zh/tree/main/skills/technical-academic-writing-zh
```

也可以手动将 [`skills/technical-academic-writing-zh`](skills/technical-academic-writing-zh) 复制到：

```text
~/.agents/skills/technical-academic-writing-zh
```

如果 Codex 没有检测到新 skill，请重启 Codex。

## 使用

在起草阶段执行规范：

```text
$technical-academic-writing-zh 根据以下材料起草正文。每项证据强度只限定一次，避免跨段重复和过程性说明：
……
```

修改现有文本：

```text
$technical-academic-writing-zh 在保持数字、术语、条件和结论强度不变的前提下修改以下内容：
……
```

定稿检查：

```text
$technical-academic-writing-zh 检查全文的重复限定、跨层级复述、修改痕迹、否定性冗余和难读句。
```

## 通用示例

原文：

> 现有数据提示因素 A 可能影响结果。受证据范围限制，这些数据仅支持存在影响的可能性，不能确定影响程度。

规范写法：

> 现有数据提示因素 A 可能影响结果，但不能据此确定影响程度。

改写删除了重复的不确定性说明，同时保留了不能确定影响程度这一独立边界。

## 验证范围

`SKILL.md` 使用 Codex `skill-creator` 附带的 `quick_validate.py` 检查格式、名称和 frontmatter。该检查只验证 skill 结构，不代表模型在所有文本上的写作效果。

[`evals/cases.yaml`](evals/cases.yaml) 记录了通用测试输入、预期行为和必须保持的语义，可用于后续回归评估；仓库不会在未实际运行评估时声明这些案例已经通过。

## 目录结构

```text
.
├── README.md
├── LICENSE
├── evals/
│   └── cases.yaml
└── skills/
    └── technical-academic-writing-zh/
        ├── SKILL.md
        └── agents/
            └── openai.yaml
```

## 许可证

[MIT License](LICENSE)
