# ArchWiki（miyu-scripts-archwiki-query）

给 Miyu 的脚本工具 `archwiki`：搜 ArchWiki、读页面。

- 给搜索词就找最匹配的页面并打开，其余结果列在末尾；只想看结果用 `action=search`。
- 长页面先给导言和放得下的小节，放不下的列出编号、标题和字数（三级以下的并进上一级），再用 `section` 取。
- 代码块、注意/提示框、表格保留；编辑链接、目录、相关文章栏去掉。
- `lang=zh` 查 Arch Linux 中文维基（wiki.archlinuxcn.org，社区翻译，可能比英文版旧）。

## 参数

| 参数 | 说明 |
|---|---|
| `query` | 搜索词 |
| `title` | 准确的页面标题，写了就直接打开（重定向会跟过去） |
| `action` | `auto`（默认）、`search`（只列结果）、`page`（按标题打开） |
| `section` | 只取一个小节：编号（如 `2.1`）或标题（如 `Troubleshooting`），连同子小节 |
| `lang` | `en`（默认）或 `zh` |
| `limit` | 搜索结果几条，1–20，默认 8 |
| `max_chars` | 正文最多几个字，1000–40000，默认 8000 |
| `format` | `md`（默认）或 `json` |

## 依赖与注意

- 只用 Python 标准库，走 MediaWiki 的 `api.php`。
- ArchWiki 自带的全文搜索排序很差（搜「nvidia suspend」前四十条都是笔记本型号页），所以多词搜索时每个词再单独搜一遍标题，标题里命中词多的排前面。
- 英文模式下滤掉译文页（标题带「(Deutsch)」这类后缀或非拉丁文字的子页面）。
