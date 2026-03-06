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

自动修复大部分 ESLint 问题：

```bash
npm run lint:fix
```

一键执行正式 CI 校验：

```bash
npm run check
```

本地提交前自动检查已启用：

- `git commit` 时会通过 `husky + lint-staged` 自动检查已暂存的 `js/vue` 文件
- 检查命令会对这些文件执行 `eslint --fix`
- 如果还有无法自动修复的错误，提交会被阻止

## 已包含的流程

- `Frontend CI`：在 `push main`、`Pull Request`、手动触发时执行 `ESLint + build`
- `Deploy Vite app to GitHub Pages`：在 `push main` 或手动触发时发布到 `GitHub Pages`
- 部署工作流里也会先执行校验，确保不会把未通过检查的代码发到线上
- `pre-commit`：在本地提交前优先拦截明显的 ESLint 问题

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

1. `Frontend CI` 先跑 ESLint 和构建校验
2. `Deploy Vite app to GitHub Pages` 再执行检查并发布到 Pages

部署成功后，访问地址通常是：

`https://<你的 GitHub 用户名>.github.io/<你的仓库名>/`

## 为什么这个项目可以直接部署到 Pages

`vite.config.js` 已经做了处理：

- 本地开发时，访问根路径 `/`
- 在 GitHub Actions 中构建时，会自动把 `base` 切换为 `/<仓库名>/`

这样你不需要每次换仓库名都手动改配置。

## 推荐你继续练的真实团队用法

- 改完代码先 `git add`，再 `git commit`，让 `pre-commit` 自动先检查本次暂存内容
- 提交代码前先在本地执行 `npm run check`
- 发起 `Pull Request` 时观察 `Frontend CI` 是否通过
- 在仓库的 `Settings -> Branches` 里给 `main` 开启保护规则，并要求 `Frontend CI` 必须通过后才能合并
