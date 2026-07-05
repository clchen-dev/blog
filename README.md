# Zenlab Blog

基于 Hugo + Diary 主题重建的个人博客。

地址计划为：https://blog.zenlab.top

主题：基于 [hugo-theme-diary](https://github.com/AmazingRise/hugo-theme-diary)，已直接包含在项目中

当前站点保留主题结构，但已移除原 fork 仓库中的文章内容与个人信息，重新用于发布自己的文章。

# 构建方法

> hugo 需要下载扩展版

```bash
# 克隆仓库
git clone https://github.com/riba2534/blog.git
cd blog

# 启动本地开发服务器
hugo server --disableFastRender

# 构建静态网站
hugo --minify
```

# 部署

当前部署目标是 Cloudflare Pages。

- Project name: `blog`
- Production branch: `main`
- Build output: `public`
- 自定义域名：`blog.zenlab.top`

仓库内置 GitHub Actions workflow，会在 `main` 推送后：

1. 安装 Hugo Extended
2. 执行 `hugo --minify`
3. 通过 `wrangler pages deploy public --project-name blog --branch main` 发布

需要的 GitHub Secrets：

- `CLOUDFLARE_ACCOUNT_ID`
- `CLOUDFLARE_API_TOKEN`
