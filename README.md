# book-maozedongxuanji

由《毛泽东选集》EPUB 提炼的 Agent Skill。定位：把原著中的战略分析方法组织成可检索的决策工具箱，同时保留全文语料，供逐字核对。

## 目录结构

```text
SKILL.md              入口：核心框架、章节索引、主题索引、文件说明
chapters/ch01–ch15    15 个主题章节，每章归并一组文章与框架
glossary.md           关键术语与定义
patterns.md           可迁移的方法与模式（含使用时机与代价）
cheatsheet.md         决策规则、权衡矩阵、识别信号
corpus.txt            完整提取文本，用于 grep 核对原文
README.md             本说明
```

## 用法

- `@skill:book-maozedongxuanji` —— 无参数加载核心框架。
- `@skill:book-maozedongxuanji 矛盾分析` —— 按主题定位；先查 `SKILL.md` 主题索引，再读对应章节。
- `@skill:book-maozedongxuanji ch06` —— 加载指定主题章节。
- 涉及原文措辞、精确计数或摘要未收录的细节时，检索 `corpus.txt`，不凭记忆作答。
- 超出本书范围的问题：明确说明「本书未涉及」，不输出与主题无关的现代建议；使用提示不等同于原文。

## 全文检索

```bash
grep -n '谁是我们的敌人' corpus.txt
grep -n '集中优势兵力' corpus.txt
```

检索时注意语料结构：

- 正文约在 **L36–L9709**；L9725 起为 `Table of Contents`，按卷列出五卷篇目，**仅有标题、非正文**。
- 同一篇名可能在正文标题、注释引用和文末篇目表中重复出现；`grep -n` 后应按行号读取上下文，勿取首个命中。
- 正文内部另有「第X章／第X节」层级标题（如《中国革命战争的战略问题》），可用于定位篇章结构。

## 数据来源与边界

- 来源：`毛泽东选集.epub`；提取元数据为 224 页、167 篇。
- `corpus.txt`：1,048,935 字符 / 9,947 行 / 约 3.1 MB，含正文与文末篇目表；原书图片未提取。
- 章节摘要与辅助文件是结构化提炼，不是原文复制；服务于分析方法论、学习研究与概念检索。
- 对历史政治论述的使用应保持语境意识与独立判断，不替代对文本的完整阅读。
- 只输出可由 `corpus.txt` 或章节文件支撑的内容；不把现代职场、民俗或个人运势类建议伪装成书中观点。
- 语料更新方式：用 `book-to-skill` 的 `scripts/extract.py` 重新提取 EPUB，并将 `full_text.txt` 复制为 `corpus.txt`。
