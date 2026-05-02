# Sanji — 个人知识库

个人笔记、场景文章与工具箱（仓库、语言、库与服务等）的集合，用 Git 做版本管理，Markdown 书写。

**说明：** 内容为个人学习与实践记录，可能存在错误或与官方文档不一致之处；若仓库公开，读者请自行甄别。

---

## 目录导航

| 路径 | 用途 |
|------|------|
| [articles/](articles/README.md) | 个人文章：按日期 / 按场景 / 收件箱 |
| [toolbox/](toolbox/README.md) | 工具箱：仓库、语言生态、库模块、服务等 |
| [assets/images/](assets/images/) | 文章与笔记配图 |

---

## 《Sanji 知识库公约》

以下为可执行约定；不必一次做到满分，以「能持续写下去」优先。

### 目录与归属

1. **个人文章**与**工具箱**分属 `articles/` 与 `toolbox/`，不混放。
2. **按时间的文章**只放在 `articles/dated/`，建议按年分子目录 `YYYY/`，文件名为 `YYYY-MM-DD.md` 或 `YYYY-MM-DD-短标题.md`。
3. **按场景的文章**只放在 `articles/scenes/`；场景用文件夹表示（如 `work/`、`learning/`），文件名不强制带日期；需要时用文末或 YAML 标 `date`。
4. **尚未归类**的片段放在 `articles/inbox/`，并设定习惯：**每周或每月**清理到 `dated` / `scenes` / `toolbox`，避免 inbox 无限膨胀。
5. **工具箱**不限 GitHub：仓库索引在 `toolbox/repos/`，语言生态在 `toolbox/languages/`，库与模块在 `toolbox/libraries/`，线上或自托管服务在 `toolbox/services/`；一时无法归类用 `toolbox/misc/`。随手收集可先写在 **根目录 [`toolbox/inbox.md`](toolbox/inbox.md)**，再合并进对应分类。
6. **归档**：不再活跃的项目笔记或过时清单，可迁至 `articles/archive/` 或 `toolbox/_archive/`（按需创建），主索引中保留指向或删除过时链接。

### 体裁与写法（对齐常见文档分层）

7. **教程**（带新手走完一条路径）、**操作指南**（解决具体问题）、**解释**（原理与权衡）、**参考**（表格、命令、字段清单）——写作时心里区分类型；`toolbox` 内条目默认偏 **参考**：一句话用途 + 链接 + 适用场景。
8. 对**会反复回看**的主题，可采用渐进总结：**我的结论（短）→ 要点摘录 → 原文或仓库链接**。
9. **原子化**：一个文件围绕一个可独立理解的主题；过长则拆分，文首用相对路径互链：`[标题](./其它.md)`。

### 元数据与命名

10. 需要检索或日后接静态站/Obsidian 时，可在文首使用 YAML（按需，不强制每篇）：
    ```yaml
    ---
    title:
    date:
    updated:
    scene:
    type: note | howto | reference | tutorial | explanation
    status: draft | mature
    ---
    ```
11. 仓库内路径与文件名优先 **小写字母、数字、短横线**；中文可作标题写在正文 `# 标题` 中。
12. 配图统一放在 `assets/images/`，文中用相对路径引用；规模大时可细分子目录（如按年）。

### 枢纽页与维护

13. **每层 README 负责导航**：根、`articles/`、`toolbox/`、`toolbox/repos/` 等维护简短索引与跳转；大主题可增加单独的「地图页」（MOC），集中链接子文档。
14. **PARA 心智**：场景笔记可区分「具体项目（有交付）」与「长期领域（无终点）」；项目在 `scenes` 下可用 `projects/项目名/` 收纳。
15. **toolbox** 控制粒度：子目录按需要再细分（如 `libraries/python/`）；单文件过长再拆；`misc` 中的条目应定期消化到正式分类。

### 协作、隐私与自动化（可选）

16. 若仓库**公开**：禁止提交密钥、令牌、内网地址与个人隐私；截图先脱敏。
17. **协作**：他人贡献可走 Pull Request；个人独奏可不使用 `CONTRIBUTING.md`。
18. **自动化（文章量多再上）**：可对 Markdown 做 lint、对 `toolbox` 链接做死链检查（如 CI），降低维护成本。

---

## 许可证

若不特别声明，默认 **保留所有权利（All Rights Reserved）**；若你希望他人可复用内容，可自行在仓库中加入 `LICENSE` 文件。
