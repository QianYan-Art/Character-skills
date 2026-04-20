# Character Skills Archive

> 一个面向泛 ACG 角色扮演与智能体调用场景的 **完全开源** Skills 汇总仓库。  
> 像整理角色设定集一样，持续收录可直接使用的角色 Skills。

![Open Source](https://img.shields.io/badge/Open%20Source-Yes-5b8c7a?style=for-the-badge)
![ACG](https://img.shields.io/badge/Theme-ACG%20Character%20Skills-cb7a9f?style=for-the-badge)
![Skills](https://img.shields.io/badge/Format-Skill%20Folders-6b7fd7?style=for-the-badge)

## Archive Note

这个仓库只做一件事：  
把已经整理好的角色扮演 Skills 以清晰、可复用、可继续扩展的方式集中存档。

当前所有内容默认放在 [`skills/`](./skills) 目录下。

## Current Collection

| 角色 | 作品 | 目录 |
| --- | --- | --- |
| 唐语歌 | 《夏日花火》 | `skills/唐语歌-skill-main` |
| 满穗 | 《饿殍：明末千里行》 | `skills/满穗-skill-main` |

## Quick Pull

### 克隆整个仓库

```bash
git clone https://github.com/QianYan-Art/Character-skills.git
cd Character-skills
```

### 只取唐语歌 Skill

```bash
git clone --filter=blob:none --sparse https://github.com/QianYan-Art/Character-skills.git
cd Character-skills
git sparse-checkout set "skills/唐语歌-skill-main"
```

### 只取满穗 Skill

```bash
git clone --filter=blob:none --sparse https://github.com/QianYan-Art/Character-skills.git
cd Character-skills
git sparse-checkout set "skills/满穗-skill-main"
```

## Structure

```text
skills/
├─ 唐语歌-skill-main/
└─ 满穗-skill-main/
```

## License

本仓库内容默认以开源方式共享与整理。  
后续会继续收录更多泛 ACG 角色 Skills。
