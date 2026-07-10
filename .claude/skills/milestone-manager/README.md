# Milestone Manager

GitHub Milestone 创建、Issue 关联与进度跟踪。MS 周期和参数见 `data/ms-config.json`。

## 安装

```bash
ln -s /path/to/my-skills-lab/project-method/milestone-manager ~/.claude/skills/milestone-manager
```

## 触发示例

| 用户说 | 作用 |
|--------|------|
| 「创建 MS1 的 Milestone」 | 按模板输出标题 + 描述 + 交付物清单 |
| 「MS2 过半了，帮我看看进度」 | 对比预期和实际进度，输出偏离项 |
| 「检查这周的 Issue 都挂 MS 了吗」 | 逐条 Issue 检查 Milestone 关联 |
| 「项目周期怎么拆成 MS」 | 读取 ms-config.json，输出 MS 拆解表 |
