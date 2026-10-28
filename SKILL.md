---
name: shadcn-zinc-ui
description: Use when building or restyling dashboards, admin tools, or data-dense interfaces in the neutral Zinc style of shadcn/ui, with consistent typography, spacing, components, and light/dark themes. Do not apply when the requested visual direction is different.
---

# Shadcn Zinc UI

一套独立的前端视觉规范：中性灰、Geist 字体、细边框、小圆角、清晰留白，支持深浅主题与密集数据界面。以 shadcn/ui 为组件基础，具体色值和尺寸由配套指南定义。

## 先读取

- 每次应用先读 [风格指南](references/style-guide.md)，其中的色值、尺寸与组件规则是实现依据。
- 建立或迁移主题时读 [主题变量](assets/theme-tokens.css)，适配后导入目标项目。
- 接入 Tailwind 4 时可用 [Tailwind 映射](assets/tailwind-theme.css)，将扫描范围改为目标前端源码。

## 应用方式

1. 先看目标项目的框架、组件、reset、主题机制与页面结构。新 React 项目优先采用 shadcn 源组件；已有项目渐进迁移并保留路由、数据与业务行为。其他框架可复用设计规范，不为外观重写框架。
2. 将主题绑定到语义 token。新项目未指定时可默认浅色；已有项目沿用用户当前偏好。`.dark` 或 `data-theme` 选一种主机制，避免冲突。
3. 先统一公共控件，再处理页面专属区域。使用真正的共享组件，避免只加高优先级样式补丁就声称完成迁移。数据布局仍可保持紧凑。
4. 更新依赖或运行 CLI 时检查目标项目和当前官方文档，不将示例的版本、构建工具、导入后缀当作所有项目的要求。
5. 用目标项目的构建、行为测试与浏览器预览验证。报告实际样式改动与验证结果。

## 实现时容易遗漏的细节

- **多行按钮**：固定高度与 `whitespace-nowrap` 适合单行操作；标题加说明的菜单项、模式选项用 `h-auto whitespace-normal` 并检查点击区域。
- **现有表格**：父层已有横向滚动容器时，不再套第二层 Table 滚动包装。保留 sticky、列宽、排序、分页和展开行的 DOM 关系。
- **原生行为**：迁移时保留 `type`、`disabled`、`ref`、提交行为、事件、精度约束与可访问名称。不能批量添加 `type="button"` 改掉原有隐式提交，也不能让取消操作意外提交。checkbox/range 可按需保留原生实现。
- **文字对比度**：深色次要文字用 `#a1a1aa`，浅色用 `#66666f`。`#71717a` 不适合作为深色小号正文。检查卡片、灰色徽章、hover 背景上的实际对比度。
- **状态切换**：业务状态的前景/背景立即切换；可以保留阴影或焦点反馈，避免两种颜色同步渐变经过不可读的中间色。
- **CSS 兼容**：已有布局依赖旧 reset 时可先只接入 Tailwind theme/utilities；新项目采用标准初始化。不要对所有十六进制色值无差别替换，也不要将旧项目的 `--muted` 文字变量误改成背景色。

## 验证

检查深浅主题、桌面及约 390px 手机宽度，覆盖长中文/英文、带单位数字、空/加载/错误状态。确认菜单不截断、表格只在自身容器滚动、焦点可见、弹窗能关闭并恢复焦点。示例内容使用通用名称与占位数据。

其他 AI 不支持 skills 时，直接提供 `references/style-guide.md`；该文件可独立阅读。需要修改主题时再提供 `assets/theme-tokens.css`。
