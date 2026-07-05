# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个使用 Hugo 静态网站生成器构建的个人博客项目，Fork 自 [riba2534/blog](https://github.com/riba2534/blog)。上游仓库的文章内容与个人信息已移除，当前用于发布自己的文章，主题结构保持不变。

- **主站地址**: https://blog.zenlab.top
- **主题**: hugo-theme-diary (已包含在项目中，来自上游 fork)
- **评论系统**: Twikoo（当前在 `hugo.toml` 中通过 `enableTwikoo = false` 关闭，未配置 `twikooEnvId`）
- **部署平台**: Cloudflare Pages（不是 GitHub Pages）

### 重要说明
- **本项目不使用根目录的 layouts 目录**，所有布局模板都在 `themes/diary/layouts/` 中
- 如需修改模板，直接编辑主题目录下的文件即可

## 常用命令

### 使用 Makefile（推荐）
```bash
# 显示所有可用命令
make help

# 启动本地开发服务器 (localhost:1313)
make serve

# 启动局域网可访问的服务器
make serve-lan

# 构建静态网站
make build

# 清理生成的文件
make clean

# 创建新文章
make new title="文章标题"

# 构建并预览生产版本
make preview

# 推送到 main 触发自动部署（Cloudflare Pages）
make deploy
```

### 直接使用 Hugo 命令
```bash
# 启动本地开发服务器
hugo server --disableFastRender

# 构建静态网站（输出到 public 目录）
hugo --minify

# 构建用于生产环境
HUGO_ENVIRONMENT=production hugo --minify

# 创建新文章
hugo new blog/$(date +%Y)/文章标题.md
```

## 项目结构

### 核心配置
- `hugo.toml`: Hugo 配置文件，包含站点基本信息、菜单配置、评论系统配置等
- `wrangler.jsonc`: Cloudflare Pages 项目配置（构建命令、静态资源目录）
- `.github/workflows/deploy.yml`: GitHub Actions 自动部署配置，推送到 main 分支后构建并通过 wrangler 部署到 Cloudflare Pages

### 内容组织
- `content/`: 所有内容文件
  - `content/blog/`: 博客文章，按年份组织（如 `content/blog/2026/`）
  - `content/about.md`: 关于页面
  - `content/archive.md`: 归档页面

### 主题配置
- 主题直接存储在 `themes/diary/` 目录中
- 基于 hugo-theme-diary，已包含在项目中
- 主题支持数学公式（MathJax）、代码高亮、评论系统等功能

## 重要特性

1. **评论系统**: 主题支持 Twikoo，通过 hugo.toml 中的 `enableTwikoo` / `twikooEnvId` 控制，当前处于关闭状态
2. **代码高亮**: 使用 GitHub 主题，支持行号显示，带复制按钮和语言标识
3. **数学公式**: 启用了 MathJax 和 LaTeX 支持
4. **自动部署**: 推送到 main 分支后，GitHub Actions 会自动构建并通过 wrangler 部署到 Cloudflare Pages
5. **扩展版 Hugo**: 项目需要 Hugo 扩展版（extended）以支持 SASS/SCSS 编译

## 注意事项

- Hugo 版本需要使用扩展版（extended），以支持主题中的 SASS/SCSS
- 所有新文章应放在 `content/blog/` 目录下，按年份组织
- 主题文件可以直接在 `themes/diary/` 目录中修改
- 部署是通过 GitHub Actions 自动完成的，无需手动构建和推送
- **不要在根目录创建 layouts 目录**，所有模板修改都应在 `themes/diary/layouts/` 中进行

## Claude 操作规则

### Git 操作权限
- **重要**: 所有 Git 和 GitHub 相关操作（commit、push、pull、merge、创建分支等）必须得到明确授权才能执行
- 在执行这类操作前必须先询问许可

### 痕迹清理要求
每次完成修改后必须进行环境清理：
1. 删除生成的测试文件（如 `public/` 目录）
2. 删除临时文件和备份文件
3. 结束后台运行的程序（如开发服务器）
4. 确保不留下不必要的文件或进程