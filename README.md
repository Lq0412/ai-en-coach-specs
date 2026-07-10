# AI 研发规范 Skill 工具包

把团队研发规范写成 **Claude Code Skills**——AI 在开发者主动调用时参考执行的规则，而不是让人读的文档。

10 个 Skill，分为流程 Skill（7 个）和辅助 Skill（3 个），覆盖从写 Issue 到发版的完整研发链路。

## 包含哪些 Skill

### 7 个流程 Skill

| Skill | 对应环节 | 做什么 |
|-------|---------|--------|
| `issue-standard` | 写 Issue | 四段模板、标签体系、拆分规则、关联 Milestone |
| `code-discipline` | 编码 | 决策阶梯（YAGNI→标准库→原生→依赖→最小实现）、禁止兜底和猜测性代码 |
| `pr-commit` | 提交 | Conventional Commits 格式、PR 四段描述、分支命名 |
| `branch-commit` | 提 PR | 分支生命周期、自检清单、合入后自动删分支 |
| `pr-review` | Review | 五维 Review 清单、合入条件核验、意见格式规范 |
| `release-tag` | 发版 | Tag 命名、Release Notes 模板、`gh release create` |
| `milestone-manager` | 全程 | MS 结构定义、Issue-Milestone 关联检查、进度偏差预警 |

### 3 个辅助 Skill

| Skill | 做什么 | 什么时候用 |
|-------|--------|-----------|
| `ai-design-smell` | 识别 AI 生成 UI 的"模板味"并给出修复方向 | 评审或生成界面时 |
| `product-killshot` | 竞品深度分析：读代码 → 搜竞品 → 双视角分析 → 优化报告 | 产品决策前 |
| `web-to-design-md` | 从真实网站提取设计语言，生成可复用的 DESIGN.md | 参考竞品设计时 |

## 快速开始

### Claude Code（推荐）

项目级自动加载——放在项目根目录下的 `.claude/skills/` 即自动生效：

```bash
git clone https://github.com/Lq0412/ai-en-coach-specs.git
cp -r ai-en-coach-specs/.claude/skills/ your-project/.claude/skills/
```

需要哪个 skill 就复制哪个，不一定要全装。

### 全局安装

所有项目通用：

```bash
ln -s $(pwd)/.claude/skills/milestone-manager ~/.claude/skills/milestone-manager
ln -s $(pwd)/.claude/skills/pr-commit ~/.claude/skills/pr-commit
# …选择你需要的 skill
```

### Codex (OpenAI)

```bash
cp -r .claude/skills/issue-standard ~/.codex/skills/issue-standard
cp -r .claude/skills/pr-commit ~/.codex/skills/pr-commit
# …选择你需要的 skill
```

## 操作与数据分离

Skill 文件只管操作逻辑（怎么做），项目参数（什么时间、多少人、Issue 配额）放在独立数据文件中。换项目只改数据文件，skill 原样复用。

以 `milestone-manager` 为例：

```
milestone-manager/
├── SKILL.md            ← 操作逻辑（稳定，跨项目复用）
└── data/
    └── ms-config.json  ← 项目参数（起止时间、人数、Issue 配额、预警阈值）
```

接入新项目时，只需要修改 `ms-config.json` 中的 `startDate`、`teamSize`、各 MS 的 `dueDate` 和 `issueQuota` 等参数。

## 仓库结构

```
.
├── .claude/
│   └── skills/
│       ├── ai-design-smell/
│       ├── branch-commit/
│       ├── code-discipline/
│       ├── issue-standard/
│       ├── milestone-manager/
│       │   └── data/ms-config.json  ← 项目参数
│       ├── pr-commit/
│       ├── pr-review/
│       ├── product-killshot/
│       ├── release-tag/
│       └── web-to-design-md/
├── .github/ISSUE_TEMPLATE/
│   └── proposal.md                  ← 产品提案模板
├── .githooks/
│   └── commit-msg                   ← 去除 AI 协作者签名
├── .gitignore
└── README.md
```

## 设计原则

- **操作和数据解耦**：skill 定义怎么做（how），数据文件定义做什么（what）
- **管格式不代替决策**：skill 管格式、流程提醒和常见模式检查，业务判断始终是人来做
- **触发式而非自动式**：skill 在开发者对话时触发，不是 git hooks 自动执行

## 贡献

欢迎把你团队的规范写成 Skill 一起交流。Fork → 加 Skill → 提 PR。

## 许可

MIT
