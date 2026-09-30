# Supervisor / Executor Skills

双窗口 AI Coding 工作流的两个强约束 Skill：让稀缺的高级模型只做"思考"，让额度充足的强模型做"执行"，两个窗口通过项目根目录的 `AGENTS.md` 交接。

> The skills are written in Chinese. They work with any coding agent that supports `SKILL.md` (Claude Code, Codex CLI, ZCode, etc.); feel free to translate for your own use.

## 解决什么问题

同一个项目开两个 AI 窗口时，最常见的两种浪费：

- **高级模型什么都干**：分析、拆解、实现、Review 全包，稀缺额度瞬间烧完；
- **两个模型互相踩**：执行模型自作主张改方向，或决策模型把提示词写得又薄又空，执行模型被迫自己瞎猜。

这套 Skill 的分工边界只有一条：

> **Supervisor 替 Executor 思考，Executor 只负责执行。**

## 核心原则

- **省额度 = 少参与次数 + 少轮次 + 一次到位**，不是把方案写薄。一旦参与，就把思考做全。
- **深度 ≠ 长度**：方案以"关键判断"（最大的 3–5 个风险）开头，只定分类法、判定标准与阈值（附依据）；场景枚举、组合矩阵等实例展开交给 Executor。
- **TRIAGE 先行**：杂活直接转述下放（A），少量判断后下放（B），只有架构 / 取舍 / 不可逆 / 全量性跨层工作才深度思考（C）。
- **验收分级但不跳过**：低风险只核证据，高风险对照方案深查；结论只有 PASS / REWORK / DECISION REQUIRED。
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

然后把 `AGENTS-template.md` 复制到**每个项目**的根目录并重命名为 `AGENTS.md`（每个项目独立一份，不是全局文件）。

## 使用

| 窗口 | 模型 | 启动 | 职责 |
|---|---|---|---|
| Supervisor | 高能力、额度稀缺（如 GPT-5 Astra 级） | `/supervisor` | TRIAGE → 必要时深度思考 → 写方案与 Executor Prompt 到 AGENTS.md → 验收复核 |
| Executor | 能力强、额度充足 | `/executor` | 读 AGENTS.md → 忠实执行 → 验证 → 带证据汇报；需要"思考"而非"执行"时升级 |

典型循环：

```
你 → Supervisor（TRIAGE + 方案 + Prompt 落盘）
   → Executor（读 AGENTS.md，执行 + 验证，REPORT）
   → Supervisor（验收：PASS / REWORK / DECISION REQUIRED）
   → 下一阶段
```

Executor 遇到方案未覆盖的结构性选择、方案与现状冲突、验收标准矛盾时，写入 AGENTS.md 的 `DECISION REQUIRED` 段并暂停该部分——不自行重新设计。

## 文件

- [`supervisor/SKILL.md`](supervisor/SKILL.md) — 决策与验收角色
- [`executor/SKILL.md`](executor/SKILL.md) — 执行角色
- [`AGENTS-template.md`](AGENTS-template.md) — 项目交接文件模板（六段）

## License

[MIT](LICENSE)
