# shadcn-zinc-ui

一套给 AI 编程助手使用的 **shadcn/ui Zinc 中性灰前端风格规范**。

统一配色、Geist 字体、间距、圆角、组件与深浅主题，适合后台、仪表盘和数据密集型界面。支持新项目搭建，也支持在保留现有业务逻辑的前提下改造界面。

**这是 AI Skill，不是 npm UI 组件库。** 安装后让 AI 读取并应用规范；安装命令本身不会修改你的页面，也不会自动安装 React、Tailwind 或 shadcn 组件。

## 快速开始：Codex 全局安装

### 方式一：Git 安装，不要求 Node.js

在 macOS / Linux 终端执行：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/Liuym911/shadcn-zinc-ui.git "$HOME/.agents/skills/shadcn-zinc-ui"
```

安装一次后，可在这台电脑的其他项目中使用。目标目录已存在时不要重复 clone，按下面的“更新”操作即可。

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME/.agents/skills" | Out-Null
git clone https://github.com/Liuym911/shadcn-zinc-ui.git "$HOME/.agents/skills/shadcn-zinc-ui"
```

安装后在目标项目中新开一个 Codex 任务，输入：

```text
使用 $shadcn-zinc-ui，将这个项目统一为 shadcn Zinc 风格，保留现有业务逻辑。
```

### 方式二：通过 Skills CLI 安装

需要 Git，以及 Node.js **22.20.0 或更新版本**和 npm。可以先用 `node --version` 检查版本；Node.js 20 用户可以直接采用上面的 Git 方式。

```bash
npx skills add Liuym911/shadcn-zinc-ui --skill shadcn-zinc-ui --agent codex --global --yes
```

`--global` 表示跨项目可用，`--agent codex` 指定 Codex，`--yes` 跳过交互选择。无须另行发布 npm 包，CLI 会从 GitHub 获取本仓库。

两种方式选一种即可，不需要重复安装。

## 只安装到当前项目

进入需要改造的项目目录，再执行：

```bash
npx skills add Liuym911/shadcn-zinc-ui --skill shadcn-zinc-ui --agent codex --yes
```

不带 `--global` 就是项目级安装。Codex 的项目级技能目录为 `.agents/skills/`。若要将技能文件随项目一起提交，可加 `--copy`：

```bash
npx skills add Liuym911/shadcn-zinc-ui --skill shadcn-zinc-ui --agent codex --copy --yes
```

## Claude Code、Cursor 等工具

Skills CLI 支持不同的目标代理；按自己使用的工具选择一条：

```bash
# Claude Code：安装到当前项目
npx skills add Liuym911/shadcn-zinc-ui --skill shadcn-zinc-ui --agent claude-code --yes

# Cursor：安装到当前项目
npx skills add Liuym911/shadcn-zinc-ui --skill shadcn-zinc-ui --agent cursor --yes
```

需要跨项目使用时，在对应命令中加 `--global`。调用语法以所用工具为准；通用提示词可以写：

```text
请读取并使用 shadcn-zinc-ui 技能，按其中的风格指南与主题变量改造界面。
```

## 常用提示词

### 改造已有项目

```text
使用 $shadcn-zinc-ui 改造这个项目的前端。
先检查现有框架、组件和主题机制，统一配色、字体、按钮、表单、卡片与表格。
保留路由、数据、业务逻辑和现有功能，支持深浅主题和手机宽度。
```

### 创建新页面

```text
使用 $shadcn-zinc-ui 实现一个后台页面。
采用中性灰、Geist 字体、细边框和小圆角，包含指标卡片、筛选区与数据表格。
```

### 只调整样式

```text
按 $shadcn-zinc-ui 统一视觉风格，不重排现有导航，不修改业务功能。
```

## 这个技能包含什么

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | AI 的入口指令与应用边界 |
| [references/style-guide.md](references/style-guide.md) | 可独立阅读的完整风格指南 |
| [assets/theme-tokens.css](assets/theme-tokens.css) | 浅色、深色语义颜色和圆角变量 |
| [assets/tailwind-theme.css](assets/tailwind-theme.css) | Tailwind CSS 4 的颜色与圆角映射 |
| [agents/openai.yaml](agents/openai.yaml) | 技能显示名称和默认提示词 |

核心风格：

- 浅色白底，深色 Zinc 黑灰底；主操作使用黑白反色。
- Geist Variable 与系统中文字体回退，字体可本地托管。
- 控件、卡片、弹窗圆角分别为 6px、10px、12px。
- 深浅主题使用独立的次要文字色，保持可读性。
- 多行菜单自动撑高，宽表在自身容器滚动。
- 渐进迁移已有组件，保留表单提交、refs、焦点与键盘操作。

这些 CSS 是可适配的源文件，不是完整样式框架。AI 应根据项目已有的 reset、主题机制和 Tailwind 版本接入，而不是直接覆盖现有样式入口。

## 更新

通过 **Git clone** 安装的版本：

```bash
git -C "$HOME/.agents/skills/shadcn-zinc-ui" pull --ff-only
```

通过 **Skills CLI** 安装的版本：

```bash
npx skills check
npx skills update shadcn-zinc-ui
```

若本机同时存在项目级和全局安装，按 CLI 提示选择需要更新的范围。

## 检查与卸载

Skills CLI 查看全局安装：

```bash
npx skills list --global --agent codex
```

Git 安装可以直接打开 `~/.agents/skills/shadcn-zinc-ui/SKILL.md` 检查文件是否存在；CLI 的更新检查不一定追踪手动 clone 的安装，手动安装请继续使用 Git 更新。

卸载通过 CLI 安装的全局版本：

```bash
npx skills remove shadcn-zinc-ui --global --agent codex --yes
```

项目级版本使用同一命令并去掉 `--global`。Git 安装的版本可在文件管理器中移出对应 `skills` 目录；如果自己修改过文件，先保留副本。

## 不支持 Skill 的 AI

直接把 [风格指南](references/style-guide.md) 提供给 AI，再按需要提供两份 CSS。无需它能识别特定的技能系统。

```text
请先读取这份风格指南，按其中的配色、字体、尺寸和组件规范实现界面。
```

## 常见问题

**安装后为什么页面没有变化？**

安装的是 AI 指令与样式参考。还需要向 AI 发出“使用这个技能改造页面”的任务，由 AI 在目标项目中实际实施。

**安装后 AI 没找到技能？**

检查是否安装给了正确的代理、是否在正确的项目目录，以及全局/项目级范围。新开一个任务后显式写出技能名，也可以直接让 AI 读取安装目录里的 `SKILL.md`。

**我已经把旧版本放在 `~/.codex/skills/` 了怎么办？**

先查看内容和是否有本地修改，再统一保留一个安装来源，避免同名技能的不同版本同时存在。不必为了采用本仓库强制移动正在使用的版本。

**必须使用 React 或 Tailwind 吗？**

React 项目可以使用 shadcn 源组件，Tailwind 4 项目可以使用配套映射。其他框架也可应用这套视觉规范，不需要仅为风格更换技术栈。

**能直接安装 shadcn 的全部组件吗？**

本技能不会自动安装组件依赖。由 AI 根据页面需求，在目标项目中按当前官方文档选择并接入所需组件。

## 参考

- [Skills CLI 安装与命令](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)
- [Skills CLI 支持的代理及安装位置](https://github.com/vercel-labs/skills/blob/main/docs/agents.md)
- [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)
- [shadcn/ui 文档](https://ui.shadcn.com/docs)

本仓库是独立的风格技能，与 shadcn/ui、Vercel 或 OpenAI 官方项目无隶属关系。
