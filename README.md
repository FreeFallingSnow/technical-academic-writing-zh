# 中文技术与学术写作规范

`technical-academic-writing-zh` 是一个遵循 [Agent Skills](https://agentskills.io/specification) 结构的指令型 Skill，用于中文技术报告、论文、规范和分析文本的起草、修改、清理与定稿。

它处理以下问题：

- 重复叠加“可能、提示、支持”等证据强度限定；
- 在正文、表格、摘要和结论中完整复述同一信息；
- 将审阅意见、修改说明等过程痕迹写入正文；
- 使用双重否定、绕行否定或没有技术作用的孤立排除；
- 一个句子承担过多判断，或条件、动作、结果和结论相互嵌套；
- 逐词替换问题表达，却没有修复整个句群的逻辑结构。

Skill 在修改前保护事实、数字、术语、条件、适用范围、因果方向、证据强度、引用关系和必要否定。直接引文、法规条款、公式、代码、标识符及交叉引用默认保持原貌。它不补写输入中没有的事实、来源或引用，也不代替事实核查和专业判断。

## 工作模式

### 起草、改写与定稿

规范直接作用于交付文本。模型先建立语义保护记录，再起草或修改正文，交付前检查重复、范围、过程痕迹、结构和语义保持情况。用户只要求正文时，不附加“已优化”“修改如下”等说明。

### 清理与审校

用户要求清理、精简、删除冗余、去除修改痕迹或直接审校时，模型先完成不会改变语义的确定项，再输出清理清单。只有材料不足、内容矛盾或指代不清，导致技术含义无法判断时，才保留原句并列入待确认项。

涉及数据源或方法排除时，关联检索仅使用当前文档、当前文档直接引用的材料和用户明确指定的依据。模型记忆、普通对话内容和项目目录中未与当前文档直接关联的文件不能用于补建背景。完整规则见 [`references/cleanup-review.md`](references/cleanup-review.md)。

### 仅检查

用户明确要求只找问题、不修改原文时，模型按“位置—问题—依据—建议”报告，原文保持不变。

## 长文检索

处理大段文字、多章节文稿或全文时，模型先轻量扫描全部内容，再对候选句进行深查：

1. 检索证据限定词、修改痕迹、否定词和总结词的组合；
2. 筛选主语变化、连接词堆叠、相邻复述和跨层级重复；
3. 将每个段落的末句加入候选集合；
4. 读取候选句的标题、前后文和对应摘要或结论；
5. 对同一段内集中出现的问题重组句群；
6. 修改后复检相关段落和信息层级，并与语义保护记录比较。

可疑词、句长和段末位置只负责发现候选，不直接决定删除。完整检索规则见 [`references/long-document-retrieval.md`](references/long-document-retrieval.md)。

## 通用案例

[`references/writing-examples.md`](references/writing-examples.md) 收录十组完整案例：

1. 重复限定证据强度；
2. 将范围并入结果；
3. 删除修改过程；
4. 改写绕行否定；
5. 保留安全禁令等必要否定；
6. 减少正文与结论的跨层级复述；
7. 重组承担多个判断的过载句；
8. 删除没有上下文依据的孤立排除项；
9. 保护直接引文和技术标识符；
10. 对多个问题集中的句群进行整体重组。

每个案例都给出原文、处理结果和判断理由。案例只说明规则，实际修改仍以当前文本的语义和有效依据为准。

## 安装

仓库根目录就是 Skill 根目录，目录名保持为 `technical-academic-writing-zh`。

在 Codex 中调用内置的 `$skill-installer`：

```text
$skill-installer install the skill at path . from https://github.com/FreeFallingSnow/technical-academic-writing-zh and name it technical-academic-writing-zh
```

也可以克隆到 Codex、Cursor 等客户端使用的个人 Skill 目录：

```bash
git clone https://github.com/FreeFallingSnow/technical-academic-writing-zh.git ~/.agents/skills/technical-academic-writing-zh
```

Claude Code 使用以下目录：

```bash
git clone https://github.com/FreeFallingSnow/technical-academic-writing-zh.git ~/.claude/skills/technical-academic-writing-zh
```

其他支持 Agent Skills 的客户端可以将仓库放入其 Skill 搜索目录。具体安装和自动发现方式由客户端决定。

## 使用

起草正文：

```text
$technical-academic-writing-zh 根据以下材料起草正文。保持事实和证据强度，每项判断只限定一次：
……
```

清理现有文本：

```text
$technical-academic-writing-zh 清理以下内容。直接完成语义明确的修改，并列出清理清单和真正需要确认的项目：
……
```

只检查问题：

```text
$technical-academic-writing-zh 只检查以下内容，不修改原文。按位置列出问题、依据和建议：
……
```

## 目录结构

```text
.
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── cleanup-review.md
    ├── long-document-retrieval.md
    └── writing-examples.md
```

## 许可证

[MIT License](LICENSE)
