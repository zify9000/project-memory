<!-- project-memory:start v1 -->
## 项目记忆体系

> 本章节由 `project-memory` skill 的 sync 脚本机械写入（写死，勿手工修改，重跑脚本会覆盖回本内容）。完整方法论、模板与体检清单见该 skill，可用 `/skill:project-memory` 调用；规则要改就改 skill 目录里的 `references/agents-chapter.md`，再重跑 `scripts/sync.sh`（Windows 用 `scripts/sync.ps1`）同步本章节。

### 冷启动阅读顺序
1. `SOUL.md`（要做什么产品、边界在哪）
2. `ARCHITECTURE.md`（骨架地图）
3. `PROGRESS.md`（进行到哪一步）
4. `design/INDEX.md`（产品长什么样，按需打开具体 ADR）
5. 涉及改动时读对应的 `impl/` 条目
（`design/archive/` 是冷存储，除非翻历史否则不读）

### 文档维护规则
- 产品定位、目标用户或边界变化 → 更新 `SOUL.md`（罕见，改了就是大事）
- 对话中拍板了架构取舍 → 当场起草 ADR（状态"草稿（待核对）"）请用户核对，通过后改"已采纳"并登记 `INDEX.md`
- 新决策取代旧决策 → 旧 ADR 状态改为"已被取代"，更新索引
- 合并触发条件满足（同主题 ≥3 条取代链 / 总数 >20 / 里程碑节点）→ 执行合并归档
- 改了某模块的职责/接口/数据流 → 同步更新 `impl/<module>.md`
- 目录结构或入口变化 → 更新 `ARCHITECTURE.md`（保持一页以内）
- 每次会话结束前 → 更新 `PROGRESS.md`
- 拿不准一个特性该不该做 → 对照 `SOUL.md` 的边界，对不上就先问
- 不确定的信息不要写进文档，宁可留空
<!-- project-memory:end -->
