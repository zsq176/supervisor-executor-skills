# Supervisor / Executor Skills

用于制定执行任务、复审结果，以及实现和验证已定任务。每份 Skill 直接规定适用场景、输入、步骤、输出与停止条件，不包含角色定位或双方工作流设计的介绍。

> The skills are written in Chinese and can be used by coding agents that support SKILL.md.

## 文件

- [supervisor/SKILL.md](supervisor/SKILL.md) — 核依据和成果、确定取舍、生成任务、复审与交付。
- [executor/SKILL.md](executor/SKILL.md) — 读任务、核前提、自主实现、必要验证、收尾与回执。
- [AGENTS-template.md](AGENTS-template.md) — 可选的项目交接模板。

每份 Skill 可分别安装和使用，不依赖另一份 Skill。固定步骤必须有明确结果；普通小任务可以简短记录，不为每步创建文档。

## 安装

```bash
# Codex CLI
cp -r supervisor executor ~/.codex/skills/

# ZCode
cp -r supervisor executor ~/.zcode/skills/

# Claude Code（项目级）
cp -r supervisor executor <你的项目>/.claude/skills/
```

## 使用

制定任务或复审结果时使用 /supervisor；实现或验证已定任务时使用 /executor。

沿用当前项目的交接文档，默认 AGENTS.md。新项目可复制 AGENTS-template.md 到根目录并重命名；已有项目只合并必要约束，不覆盖任务或强制重排格式。

交接保存当前有效的目标、状态、已定行为、约束、待决事项和执行任务。执行任务给具体产出、对象/输入、动作/规则、前提/边界、验收/交付、停止/升级；不附完整选题论证，不预写普通实现细节。

真实业务结果决定验收，不能用编译、HTTP 200或存活代替。有效原件复用，历史失败和未知保留；同目标累计投入和停止边界不因改名、换方法或换会话清零。

会话、资源、提交、部署与外部发送权限遵用户和项目约定。有保留价值不等于有提交权限；代码交付不自动包括方案、日志、证据、交接或 Agent 配置。项目要求远程仅代码及必要配置时，其它材料只保留本地。Skill 发布到用户指定的技能仓库。

## License

[MIT](LICENSE)
