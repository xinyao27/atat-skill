# AtAt skill（`atat`）

这个仓库是 AtAt 的 skill：它教 Claude Code、Codex、Cursor、OpenCode 这类 agent 用 `atat`
命令操作这台 Mac——截图（屏幕/窗口/区域/滚动长图）、读剪贴板历史与访达选区、录一段演示视频，
或把任务交给 AtAt 自带的 agent。它同时是一个 Claude Code 插件与插件市场，所以两种装法共用
这一个仓库。

需要 macOS 15 或更高版本，以及 [AtAt 应用](https://atatapp.com/download)。应用免费，
面向 agent 的命令不需要账号。

## 安装

1. 通过 Homebrew 或官网在 macOS 上安装 AtAt：
   `brew install --cask xinyao27/tap/atat`
   或从 [https://atatapp.com/download](https://atatapp.com/download) 下载。
2. 打开 AtAt → Settings → Agent，在 **atat CLI** 处点 **Connect**（或在终端运行 `atat skill install`）。
3. 任何会读技能与插件的 agent（Claude Code、ChatGPT、Codex、Cursor、OpenCode）从此知道怎么用它。

装完可以直接验证：

```bash
atat status
```

## 装成 Claude Code 插件

本仓库 `.claude-plugin/` 里同时放着插件市场与插件清单，插件的 `source` 就是这个仓库根，
所以一条命令即可：

```bash
claude plugin marketplace add xinyao27/atat-skill
claude plugin install atat@atat
```

插件里带的就是这一个 skill。

## 这个仓库里有什么

| 文件 | 是什么 |
| --- | --- |
| `SKILL.md` | AtAt 命令 skill |
| `skills/atat/SKILL.md` | AtAt 命令 skill，按 Claude Code 插件布局放好 |
| `skills/atat-memory/SKILL.md` | AtAt Memory skill |
| `.claude-plugin/plugin.json` | 插件清单：名字、版本、作者 |
| `.claude-plugin/marketplace.json` | 插件市场清单；它的一个插件就是这个仓库根（`source: "./"`） |

这个仓库由 AtAt 仓库里的 `tools/scripts/export-public-skill.mjs` 生成，`SKILL.md` 是 app 内那一份的副本。要改 skill，改 app 里的源头：

```bash
# 在 AtAt 仓库里
pnpm publish:skill
```

## Links

- [AtAt](https://atatapp.com) · [完整手册](https://atatapp.com/manual)
- [联系方式](hi@atatapp.com)
