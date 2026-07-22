# project-memory

面向 AI agent 的项目记忆文档结构（Kimi Code CLI Skill）：为项目搭建一套对抗上下文重置的长期记忆体系，初始化时拉出框架，开发过程中由 agent 伴随维护。

## 解决的问题

AI agent 的上下文会被压缩和重置，磁盘文档是它唯一的长期记忆。本 skill 在项目中建立六个各司其职的文件，构成一条完整的追问链：

**要做什么产品（SOUL）→ 产品长什么样（design）→ 产品的内部细节（impl）→ 骨架是什么（ARCHITECTURE）→ 现在进行到哪（PROGRESS）→ 怎么维护这套体系（AGENTS）**

```
SOUL.md          # 要做什么产品（最稳定，人写，项目的定位与初心）
design/          # 产品长什么样（ADR 决策记录，agent 起草、人核对）
  INDEX.md       # 决策索引，冷启动先读它
  archive/       # 被合并取代的旧 ADR（冷存储）
impl/            # 产品的内部细节（模块级实现说明）
ARCHITECTURE.md  # 骨架（一页地图）
PROGRESS.md      # 进行到哪一步（每次会话收尾更新）
AGENTS.md        # "项目记忆体系"章节，由 sync 脚本机械写入
```

核心原则：**稳定的、代码推不出来的信息才值得写成文档；代码能回答的问题，让 agent 去问代码。**

## 安装

把整个目录克隆为 Kimi Code CLI 的用户级 skill：

```bash
git clone https://github.com/zify9000/project-memory.git ~/.kimi-code/skills/project-memory
```

新开一个会话后生效。

## 使用

- 手动调用：`/skill:project-memory`
- 自动触发：初始化新项目、为存量项目补建文档结构、开发中出现架构决策需要沉淀、要求更新或体检项目记忆文档时

## 仓库结构

```
SKILL.md                        # 完整方法论（模板、流程、体检清单、反模式）
references/agents-chapter.md    # AGENTS.md 章节的标准副本（唯一事实源，含版本号）
scripts/sync.sh                 # 章节安装/同步/校验脚本（Linux / macOS）
scripts/sync.ps1                # 同上，Windows PowerShell 版
```

### sync 脚本

AGENTS.md 的"项目记忆体系"章节是写死的标准件，不手工复制，由脚本机械执行：

```bash
# Linux / macOS
bash scripts/sync.sh <项目根目录>          # 安装或同步（幂等）
bash scripts/sync.sh --check <项目根目录>  # 仅校验；缺失/被篡改/过期时退出码 1

# Windows PowerShell
powershell -File scripts/sync.ps1 <项目根目录>
powershell -File scripts/sync.ps1 -Check <项目根目录>
```

修改规则 = 改 `references/agents-chapter.md` 并升级版本号，然后对各个项目重跑 sync 脚本。
