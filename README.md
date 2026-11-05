# Human Body · 人体图谱

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/liuxing5/human-body)

一个可交互的 3D 人体解剖探索器：把 BodyParts3D 成年男性参考模型拆成 **2,234 个可单独选中的网格**，支持 **15 个解剖系统** 的显隐、**3,432 个命名概念** 的检索与检视。前端使用 React 19 + Three.js + Vite + shadcn/ui。

- 在线示例（Vercel）：<https://human-atlas-seven.vercel.app>
- 渲染部署（Render）：见下方 [部署到 Render](#部署到-render)

## 仓库结构

| 路径 | 说明 |
| --- | --- |
| `human-atlas/` | 子模块（<https://github.com/liuxing5/human-atlas>）：应用源码、模型数据与构建配置 |
| `gh-pages-deploy/` | 子模块（同一仓库的 `gh-pages` 分支）：已构建好的静态站点，用于 GitHub Pages |
| `human-atlas.zip` | 应用源码快照备份 |
| `render.yaml` | Render Blueprint：把本仓库部署为静态站点 |

## 本地运行

需要 Node.js 22.13 或更高版本。

```sh
git clone --recurse-submodules https://github.com/liuxing5/human-body.git
cd human-atlas
npm ci
npm run dev      # http://localhost:3016
```

构建静态站点：

```sh
npm run build    # 产物在 human-atlas/dist（约 34 MB，含 3D 模型数据）
```

## 部署到 Render

`render.yaml` 已把部署配置写好：静态站点、`main` 分支、构建命令 `cd human-atlas && npm ci && npm run build`、发布目录 `human-atlas/dist`，并为 `/assets/*`、`/models/*` 设置长缓存头、为单页应用设置回退到 `index.html` 的 rewrite 规则。

一键部署（需要登录 Render 并授权 GitHub）：

<https://render.com/deploy?repo=https://github.com/liuxing5/human-body>

手动方式：

1. Render Dashboard → **New → Static Site**，选择 `liuxing5/human-body`，分支 `main`。
2. Build Command：`cd human-atlas && npm ci && npm run build`
3. Publish Directory：`human-atlas/dist`
4. 添加环境变量 `SKIP_INSTALL_DEPS=true`（依赖装在子模块里，避免 Render 在仓库根目录自动安装）。
5. Create Static Site，首次构建约 2–4 分钟；之后每次推送 `main` 会自动重新部署。

> Render 会读取 `.gitmodules` 并克隆子模块，因此其中的地址必须使用 HTTPS（SSH 地址无法用 Render 的 Git 凭据克隆）。

## 数据与许可

解剖数据来自 **BodyParts3D 4.0**（CC BY 4.0），应用代码以 MIT 许可发布。完整署名与改编说明见 [`human-atlas/public/ATTRIBUTION.md`](human-atlas/public/ATTRIBUTION.md)。本项目用于教学演示，不能用于诊断或手术规划。
