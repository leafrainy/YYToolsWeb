# YYToolsWeb

YYTools 产品官网与安装包发布页。

- **官网**：由 [Vercel](https://vercel.com) 部署，可绑定自定义域名
- **安装包**：GitHub Releases 源文件 + 大陆加速镜像（`ghfast.top`）分发
- **源码仓库**（私有）：[leafrainy/YYTools](https://github.com/leafrainy/YYTools)

## 目录说明

| 文件 | 说明 |
|------|------|
| `index.html` | 官网单页，下载链接从 `release.json` 动态加载 |
| `release.json` | 当前版本与下载地址，由私有仓库 CI 在发版时自动更新 |
| `vercel.json` | Vercel 静态站配置 |

## 本地预览

```bash
npx serve .
# 访问 http://localhost:3000
```

## 发版流程

在私有仓库 [YYTools](https://github.com/leafrainy/YYTools) 中打 tag 即可触发自动构建：

```bash
git tag v3.0.0
git push origin v3.0.0
```

CI 会自动：

1. 在 macOS / Windows Runner 上分别构建安装包
2. 在本仓库创建 GitHub Release 并上传 zip
3. 更新本仓库的 `release.json`，触发 Vercel 重新部署

## 修改官网文案

直接在本仓库修改 `index.html` 并 push 到 `main`，Vercel 会自动部署，无需重新打包应用。
