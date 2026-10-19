# Supervisor / Executor Skills

Supervisor负责固定需求、总清单、任务调度、代码审核和交付；Executor负责沿共享任务连续实现、验证与收尾。

## Supervisor硬规则

- 审代码抓实质问题，不吹毛求疵；通过直接提交推远程。
- 简单明确问题由Supervisor直接修，必要验证后提交推远程。
- 复杂问题放进唯一返工线；独立合格改动先交付。
- 按用户需求固定主线目标和总任务清单，只按既定步骤、批次及实际进度派发。
- 同时只允许主任务线、一条分支任务线、一条返工任务线；三线中有可执行项就同轮推进。
- 不允许分支再生分支、返工再生返工或无限扩展任务。
- 每次派发向用户明报三线各自总任务数、已解决数、本轮新增任务数及ID，同时列本轮派发ID。

“新增任务”是新加入总清单的任务；从已有清单选下一批只计派发，不增加总数。没有分支或返工时对应线填0，不制造任务凑数。三线是调度线，不要求新增代理或聊天。

## 文件

- [supervisor/SKILL.md](supervisor/SKILL.md)：决策、审核、三线调度及交付硬规则。
- [executor/SKILL.md](executor/SKILL.md)：读取共享任务、自主实现、验证及回执。
- [AGENTS-template.md](AGENTS-template.md)：固定目标、总清单和三线派发模板。

两个skill可分别使用。沿项目现有AGENTS.md共享任务，长细则只链接一份当前方案；不强制重排已有项目，不用报告或条件等待代替下一批任务。

## 安装

~~~bash
# Codex
cp -r supervisor executor ~/.codex/skills/

# ZCode
cp -r supervisor executor ~/.zcode/skills/

# Claude Code（项目级）
cp -r supervisor executor <你的项目>/.claude/skills/
~~~

## 使用

制定任务或复审时调用 /supervisor；实现或验证已定任务时调用 /executor。首次派发前先列总清单，之后保持稳定ID和原完成条件，三线同轮调度。

每个完整任务一次包含实现、用户操作、保存或启动、反馈/自动更新、业务结果及恢复收尾。复审只补实际差异，不移动完成线或反复回炉已通过部分；必要检查通过就交付。

已授权的合格代码提交推送后核远端ref；不强推，不捎带他人修改，文档/证据是否发布遵具体项目约定。当前技能仓库的授权发布范围不受其它项目的code-only规则限制。

## License

[MIT](LICENSE)
