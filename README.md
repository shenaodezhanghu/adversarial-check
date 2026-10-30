# adversarial-check · 对抗式检查

一个用于审查方案、代码改动和交付结果的轻量 Agent Skill。先从需求建立判断依据，再主动寻找反例，用证据区分真实问题、待验证疑点和设计取舍。

## 使用

在支持 Agent Skills 的工具中安装后调用：

```text
$adversarial-check 检查本次改动
```

审查方案：

```text
$adversarial-check 审查上面的方案，重点检查需求遗漏、关键假设和可行性。
只审查，不修改文件、不开始实现。
```

独立审查：

```text
$adversarial-check 使用独立子 Agent 检查本次改动，先只检查，不修改文件。
```

检查并修复：

```text
$adversarial-check 检查本次改动，核验问题后最小修复已证实的缺陷，
回归相关流程，不扩大需求、不做无关重构。
```

新会话使用时，请提供原始需求、方案或改动范围。已有会话可以直接引用上下文。

## 安装到 Codex

下载本仓库，把包含 `SKILL.md` 的文件夹放到用户技能目录，命名为 `adversarial-check`。默认路径：

- Windows：`%USERPROFILE%\.codex\skills\adversarial-check\SKILL.md`
- macOS / Linux：`~/.codex/skills/adversarial-check/SKILL.md`

如果配置了 `CODEX_HOME`，使用其下的 `skills/adversarial-check/`。在新会话中使用；未识别时重启客户端。也可以让支持 GitHub 安装的 skill-installer 安装本仓库。

## 工作方式

1. 确定检查对象、原始需求与探索边界。
2. 提取关键主张，独立确定正确行为。
3. 选择最可能暴露问题的反例。
4. 通过代码、日志、测试或实际交互核验证据。
5. 报告实际检查内容、检查方法、结果及未覆盖范围。

默认只读、一轮、有边界的检查，不要求必须找出问题。用户已授权修复时，做最小修改并回归相关流程。

子 Agent 为可选能力，依赖宿主工具及其授权。缺少该能力时不会假称独立审查；仅切换角色不等于独立复核。普通开发任务不会自动转为完整审查。

## 文件与限制

完整规则见 [SKILL.md](SKILL.md)，第一版不依赖额外脚本或服务。

Skill 是工作流程指令，不是自动运行的扫描器，不能保证发现全部缺陷。格式校验已通过，尚未进行系统性的效果评估。
