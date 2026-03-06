# Vite + Vue GitHub Actions Demo

这是一个最小可运行的 `Vite + Vue` 前端项目，并且已经配置好了 `GitHub Actions + GitHub Pages` 的 CI/CD 示例。

## 本地运行

```bash
npm install
npm run dev
```

本地构建：

```bash
npm run build
```

本地执行 ESLint：

```bash
npm run lint
```

## 已包含的流程

- 推送到 `main` 分支时，自动安装依赖、执行 ESLint 并构建项目
- 构建成功后，自动发布到 `GitHub Pages`
- 提交 `Pull Request` 到 `main` 时，会先执行构建校验，但不会正式部署

## 第一次推到 GitHub

先在 GitHub 上新建一个仓库，建议先用公开仓库做测试，这样 `GitHub Pages` 更容易直接使用。

然后在本地执行：

```bash
git init
git add .
git commit -m "init vite vue cicd demo"
git branch -M main
git remote add origin <你的仓库地址>
git push -u origin main
```

## GitHub 里还要做的事

首次部署前，打开仓库的 `Settings -> Pages`，把 `Source` 设为 `GitHub Actions`。

之后每次你往 `main` 分支推送代码，GitHub 都会自动执行：

1. 安装依赖
2. 执行 ESLint
3. 构建项目
4. 发布到 Pages

部署成功后，访问地址通常是：

`https://<你的 GitHub 用户名>.github.io/<你的仓库名>/`

## 为什么这个项目可以直接部署到 Pages

`vite.config.js` 已经做了处理：

- 本地开发时，访问根路径 `/`
- 在 GitHub Actions 中构建时，会自动把 `base` 切换为 `/<仓库名>/`

这样你不需要每次换仓库名都手动改配置。
