# Supervisor / Executor Skills

双窗口 AI Coding 工作流的两个 Skill：Supervisor 决定目标、设计和验收口径，Executor 完成实现、诊断、连续修复与回归。两个窗口通过项目根目录的 `AGENTS.md` 交接。

> The skills are written in Chinese. They work with any coding agent that supports `SKILL.md` (Claude Code, Codex CLI, ZCode, etc.); feel free to translate for your own use.

## 解决什么问题

同一个项目开两个 AI 窗口时，最常见的两种浪费：

- **高级模型什么都干**：分析、拆解、实现、Review 全包，稀缺额度瞬间烧完；
- **两个模型互相踩**：执行模型自作主张改方向，或决策模型把提示词写得又薄又空，执行模型被迫自己瞎猜。

这套 Skill 的分工边界只有一条：

> **Supervisor 决定做什么与如何验收；Executor 自主处理实现与调试。明确缺陷连续修复，真正需要改变产品决策或无法收敛时才升级。**

## 核心原则

- **省额度 = 少参与次数 + 少轮次 + 一次到位**，不是把方案写薄。一旦参与，就把思考做全。
- **深度 ≠ 长度**：方案以"关键判断"（最大的 3–5 个风险）开头，只定分类法、判定标准与阈值（附依据）；场景枚举、组合矩阵等实例展开交给 Executor。
- **TRIAGE 先行**：杂活直接转述下放（A），少量判断后下放（B），只有架构 / 取舍 / 不可逆 / 全量性跨层工作才深度思考（C）。
- **验收标准保持**：所有等级均读完整 diff、新文件和对应原始结果；风险控制调用链调查及验证深度，不缩减改动审查覆盖。结论为 PASS / PASS + 自修 / REWORK / DECISION REQUIRED。
- **明确 bug 连续修复**：当前授权目标内、根因明确、恢复既定行为的缺陷及必要回归在同一任务处理；多文件或新增测试不单独触发决策，不改变用户明确 Scope、业务语义、owner 或公共契约。
- **局部阻塞、独立推进**：产品失败、工具失败、缺证据分别处理。必要证据不齐的能力仍不能通过；只暂停真实依赖它的步骤，其它独立且已授权单元继续，不自动开启未授权阶段。
- **累计收敛**：两轮无区分事实、两次实质修正仍同失败/关联回归，或同一单元两次返工仍不满足原完成条件，必须重新判断方向、取证或拆分。新增关联子缺陷、换脚本或名称不清零；原门槛与失败证据不变。
- **减少重复验证**：昂贵采集先验证一个真实代表样本的方法与收尾；按变更影响增量补证/回归，保留原失败，复用未受影响的有效原件。实际候选提交组合仍须单独验证依赖与必要检查。
- **交接全走文件**：决策、方案、执行提示词全部落盘到项目根目录 `AGENTS.md`（六段固定结构，约 100 行硬上限），聊天不做交接载体，不需要跨窗口复制粘贴。

## 安装

兼容所有支持 `SKILL.md` 的 Coding Agent：

```bash
# Codex CLI
cp -r supervisor executor ~/.codex/skills/

# ZCode
cp -r supervisor executor ~/.zcode/skills/

# Claude Code（项目级）
cp -r supervisor executor <你的项目>/.claude/skills/
```

新项目可把 `AGENTS-template.md` 复制到项目根目录并重命名为 `AGENTS.md`。已有项目只合并必要结构和规则，保留现有约束与任务，不能直接覆盖。每个项目独立一份，不是全局文件。

## 使用

| 窗口 | 模型 | 启动 | 职责 |
|---|---|---|---|
| Supervisor | 高能力、额度稀缺 | `/supervisor` | TRIAGE → 必要决策与任务说明 → 全面复审 → 按授权交付合格单元 |
| Executor | 能力强、额度充足 | `/executor` | 读 AGENTS.md → 实现/诊断/连续修复回归 → 分单元报告；真实决策或累计停滞时局部升级 |

典型循环：

```
你 → Supervisor（TRIAGE + 方案 + Prompt 落盘）
   → Executor（读 AGENTS.md，实现 → 修复 → 回归，独立单元持续推进）
   → Supervisor（完整审查与证据核验，交付合格单元）
      ├ 普通明确缺陷/必要补证 → 同一 Executor 继续当前任务
      └ 真正决策/累计停滞 → 修订方向，只暂停受影响步骤
```

Executor 遇到业务语义、所有者、公共契约、兼容性、显式 Scope 或验收条件冲突时，写入 `DECISION REQUIRED` 并暂停相关步骤，其它已授权独立工作继续。角色分工不授权新会话、提交推送或部署；这些动作遵用户与项目权限。缺证据或总体未通过不能外推为 PASS，也不能自动冻结全部工作。

## 文件

- [`supervisor/SKILL.md`](supervisor/SKILL.md) — 决策与验收角色
- [`executor/SKILL.md`](executor/SKILL.md) — 执行角色
- [`AGENTS-template.md`](AGENTS-template.md) — 项目交接文件模板（六段）

## License

[MIT](LICENSE)
