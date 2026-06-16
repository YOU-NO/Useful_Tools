# GitHub 原型上传工具使用说明

本工具用于把本地 HTML 原型上传到 GitHub 仓库，并生成 GitHub Pages 分享链接。工具页面为：

`docs/tools/github-prototype-uploader.html`

## 准备工作

1. 创建或选择一个 GitHub 仓库

   建议使用独立仓库存放原型，例如 `eva-prototypes`，避免将评审原型和业务代码混在一起。

2. 开启 GitHub Pages

   推荐配置：

   - Branch: `main`
   - Folder: `/docs`

   使用该配置时，仓库中的 `docs/prototypes/demo/prototype.html` 会发布为：

   `https://{owner}.github.io/{repo}/prototypes/demo/prototype.html`

3. 创建 GitHub Token

   推荐使用 Fine-grained Personal Access Token，并限制到目标仓库。权限至少需要：

   - Repository permissions: `Contents`
   - Access level: `Read and write`

   Token 只在本地上传页面中输入。页面默认不会保存 Token。

## 上传步骤

1. 在浏览器中打开 `docs/tools/github-prototype-uploader.html`。
2. 填写 GitHub 配置：
   - Owner / 组织
   - 仓库名
   - 分支，默认 `main`
   - GitHub Pages 来源，默认 `main 分支 /docs 目录`
   - GitHub Token
3. 填写发布信息：
   - 功能英文名，例如 `inventory-alert-transfer-control`
   - 入口文件，默认 `prototype.html`
   - 发布目录，默认 `prototypes/{feature-name}`
4. 选择文件：
   - 如果只有单文件原型，选择 `prototype.html`
   - 如果有 `mock-data.json`、图片、CSS、JS 等依赖，选择整个原型文件夹
5. 检查上传预览中的仓库路径和分享链接。
6. 点击“开始上传”。
7. 上传完成后复制分享链接，等待 GitHub Pages 生效后即可分享。

## 当前原型示例

如果上传当前库存预警原型，建议选择整个目录：

`docs/prototypes/inventory-alert-transfer-control/`

工具默认会去掉所选文件夹最外层目录名，并上传为：

`docs/prototypes/inventory-alert-transfer-control/prototype.html`

如果仓库 Pages 配置为 `main /docs`，最终链接格式为：

`https://{owner}.github.io/{repo}/prototypes/inventory-alert-transfer-control/prototype.html`

## 路径规则

工具会根据 GitHub Pages 来源自动计算仓库路径：

- `main /docs`：上传到 `docs/{发布目录}/{文件相对路径}`
- `main /root`：上传到 `{发布目录}/{文件相对路径}`
- `gh-pages /root`：上传到 `{发布目录}/{文件相对路径}`

如果使用自定义域名，或 GitHub Pages 根地址不是默认格式，可以填写 `Pages Base URL` 覆盖自动生成的链接。

## 常见问题

### 上传成功后链接 404

GitHub Pages 发布通常有几十秒延迟。请等待一段时间后刷新链接。如果仍然 404，检查：

- GitHub Pages 是否已开启
- Pages 来源是否和工具中的配置一致
- 上传路径中是否存在多余目录
- 入口文件名是否为 `prototype.html`

### 页面打开后样式或数据缺失

通常是因为只上传了 `prototype.html`，但原型还依赖同目录下的其他文件。请选择整个原型文件夹重新上传。

### Token 报权限错误

检查 Token 是否具备目标仓库的 `Contents: Read and write` 权限，并确认 Owner、仓库名和分支填写正确。

### 仓库是私有仓库，别人能否访问链接

取决于 GitHub 账号、组织计划和 Pages 设置。需要给外部人员查看时，建议使用公开仓库或确认组织允许公开 GitHub Pages。

## 安全建议

- 不要把 Token 写入原型文件或提交到仓库。
- 不要把带 Token 的页面截图发给他人。
- 上传完成后可以在 GitHub 设置中按需撤销或更新 Token。
- 建议为原型上传创建专用 Token，并只授权目标原型仓库。
