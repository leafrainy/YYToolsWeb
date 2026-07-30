# YYToolsWeb

YYTools 产品官网与安装包发布页。

- **官网**：由 [Vercel](https://vercel.com) 部署，可绑定自定义域名
- **安装包**：提交到本仓库 `downloads/`，经 [jsDelivr](https://www.jsdelivr.com/) CDN 加速分发（GitHub Releases 仍作备份）
- **源码仓库**（私有）：[leafrainy/YYTools](https://github.com/leafrainy/YYTools)

## 目录说明

| 文件 | 说明 |
|------|------|
| `index.html` | 官网单页，下载链接从 `release.json` 动态加载 |
| `release.json` | 当前版本与 jsDelivr 下载地址，由私有仓库 CI 在发版时自动更新 |
| `downloads/` | 当前版本的 `YYTools-mac.zip` / `YYTools-win.zip`（写入 git，供 jsDelivr 加速） |
| `vercel.json` | Vercel 静态站配置 |

## 本地预览

```bash
npx serve .
# 访问 http://localhost:3000
```

## 发版流程

在私有仓库 [YYTools](https://github.com/leafrainy/YYTools) 中打 tag 即可触发自动构建：

```bash
git tag v0.9.4
git push origin v0.9.4
```

CI 会自动：

1. 在 macOS / Windows Runner 上分别构建安装包
2. 将 zip 写入本仓库 `downloads/`，更新 `release.json` 为 jsDelivr 地址
3. 推送 `main` 并打同名 tag（供 `cdn.jsdelivr.net/gh/...@vX.Y.Z/...`）
4. 创建 GitHub Release 并上传 zip 作为备份
5. 触发 Vercel 重新部署

下载地址示例：

```text
https://cdn.jsdelivr.net/gh/leafrainy/YYToolsWeb@v0.9.4/downloads/YYTools-mac.zip
https://cdn.jsdelivr.net/gh/leafrainy/YYToolsWeb@v0.9.4/downloads/YYTools-win.zip
```

## 修改官网文案

直接在本仓库修改 `index.html` 并 push 到 `main`，Vercel 会自动部署，无需重新打包应用。
