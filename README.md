# Character Skills

面向 ACG 角色扮演场景的角色 Skill 合集。每个 Skill 都是一个独立文件夹，由入口文件 `SKILL.md` 和按主题拆分的参考文档组成，可直接放进支持 Agent Skills 的客户端（Claude Code、Codex 等）使用。

所有内容都从游戏原文语料中蒸馏而来，每条结论都能在原文里找到对应的台词或情节。

## 收录角色

| 角色 | 作品 | 目录 | 版本 | 默认扮演时间点 |
| --- | --- | --- | --- | --- |
| 唐语歌 | 《夏日花火》 | [`skills/唐语歌-skill-main`](./skills/唐语歌-skill-main) | v2 | 高二前后，何曦铭的同桌、文学社成员（是否已任社长由用户指定） |
| 满穗 | 《饿殍：明末千里行》 | [`skills/满穗-skill-main`](./skills/满穗-skill-main) | v2 | 洛阳湖边对峙之后（十四岁），可切换到其他四个阶段 |

## 目录结构

每个 Skill 结构相同：

```text
<角色>-skill-main/
├── SKILL.md                      # 入口：扮演规则、核心原则、表达速写、资源地图
├── soul.md                       # 核心驱动、价值观、情感核心、内在矛盾、成长弧
├── limit.md                      # 证据边界、内容边界、话题处理、退出条件
└── resource/
    ├── speech_patterns.md        # 语气词、句式、称呼、分情绪/分场景语体
    ├── behavior_guide.md         # 情境 → 反应规则
    ├── relationship_dynamics.md  # 与原作人物的关系动态
    ├── key_life_events.md        # 时间线与关键事件（标注分支）
    ├── world_context.md          # 作品背景、地点、相关知识
    └── quotes.md                 # 按场景分类的原文台词锚点（附出处）
```

`SKILL.md` 只放运行时必需的规则，细节放在 `resource/` 里，由模型按需读取，以节省上下文。

## 安装与使用

### 1. 获取文件

克隆整个仓库：

```bash
git clone https://github.com/QianYan-Art/Character-skills.git
```

只取某一个角色：

```bash
git clone --filter=blob:none --sparse https://github.com/QianYan-Art/Character-skills.git
cd Character-skills
git sparse-checkout set "skills/唐语歌-skill-main"   # 或 "skills/满穗-skill-main"
```

### 2. 放入 Skill 目录

把角色文件夹复制到客户端的 Skill 目录，例如：

| 客户端 | 用户级目录 | 项目级目录 |
| --- | --- | --- |
| Claude Code | `~/.claude/skills/` | `<项目>/.claude/skills/` |
| Codex | `~/.codex/skills/` | — |

其他兼容 Agent Skills 格式的客户端，请按各自文档放置。

### 3. 激活

| 角色 | Skill 名 | 激活方式 |
| --- | --- | --- |
| 唐语歌 | `tangyuge-perspective` | `/tangyuge-perspective [问题]`，或在对话中要求“以唐语歌的身份回答” |
| 满穗 | `mansui-perspective` | `/mansui-perspective [问题]`，或在对话中要求“以满穗的身份回答” |

说“退出”“停止扮演”“切回正常模式”即可结束扮演。

## 制作方法

v2 版本按 [GalgameCharacterSkills](https://github.com/JodieRuth/GalgameCharacterSkills) 的蒸馏流程制作，但**没有调用该项目的 LLM 接口**，每个步骤都由人工审阅原文完成：

1. **语料**：使用从游戏中提取并清洗后的角色高相关剧情文本。唐语歌另外核对了全部 702 条本人台词，补查了未进入主语料的其他路线台词。
2. **切片**：用上游项目的 `FileProcessor.slice_multiple_files`（50k token / 片，`cl100k_base`）切分。唐语歌 2 片，满穗 3 片。
3. **逐片分析**：每一片都按上游的 PART A（客观事实）/ PART B（四层人格：身份锚点、表达风格、情绪与决策、行为规则）格式写成摘要，并附原文引用。
4. **汇总与校正**：合并各片摘要，用后文揭示的真相修正前文的说法（例如满穗对外谎报的年龄、籍贯和身世）。
5. **生成 Skill**：按上游的七文件结构写成，另外加了 `world_context.md` 和 `quotes.md` 两份参考文档。

### 与 v1 的主要差异

| 项目 | v1 | v2 |
| --- | --- | --- |
| 篇幅 | 每个文件约 1–2 KB | 每个角色约 40 KB，按主题拆分 |
| 证据 | 以概括为主，几乎没有原文 | 结论附原文台词与出处，另有台词锚点文件 |
| 事实准确性 | 满穗的年龄与身世沿用了她对外的说法 | 区分“她说的”与“真实的”，并标注分支与互斥结局 |
| 可操作性 | 偏抽象的性格描述 | “情境 → 反应”规则、分场景语体、阶段切换表 |
| 边界 | 只有证据边界 | 增加了内容边界、话题处理与安全提示 |

## 内容边界

两位角色在原作的主要时期都是未成年人。为此，两个 Skill 都明确规定：

- 不演绎任何恋爱、调情、亲密或性相关的互动。即使用户把时间设定改到成年以后，这条规定也不变。
- 不复现原作中儿童遭受伤害的情节，不渲染血腥与食人细节（《饿殍》）。
- 用户提到自伤、轻生时，以安全为先，并给出现实中的求助建议。

原作中的感情线只作为背景事实记录，不作为可扮演的场景。

## 声明

- 本仓库是非商业的同人整理。《夏日花火》《饿殍：明末千里行》及其中角色、剧情和台词的版权，归各自的原作权利人所有。
- `quotes.md` 只收录用于校准口吻的短句，不提供剧本全文。
- 蒸馏流程参考了 [GalgameCharacterSkills](https://github.com/JodieRuth/GalgameCharacterSkills)（MIT License）。
- 如果权利人认为某些内容不宜公开，请提交 Issue，我们会及时处理。

## 贡献

欢迎通过 Issue 或 Pull Request 指出与原作不符的地方，或补充新角色。提交时请注明依据（章节或脚本文件名）。
