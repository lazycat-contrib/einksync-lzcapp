# EinkSync - LazyCat App

[EinkSync](https://github.com/xiaokun567/EinkSync)（专为墨水屏打造的阅读伴侣）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`einksync` 镜像经 `docker.1ms.run` 加速器拉取，manifest 使用 digest 固定的引用（`latest@sha256:...`），`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 `xiaokun566/einksync:latest`（可变标签，`bump: patch`）：digest 未变化则跳过；变化则自动 patch +1、更新 manifest digest 并发布。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 结构

| 文件 | 说明 |
| --- | --- |
| `package.yml` | 包元数据（`community.lazycat.app.einksync`） |
| `manifest.yml` | 服务与路由配置（mirror 镜像 + upstream 注释） |
| `lzc-build.yml` | 构建配置 |
| `icon.png` | 图标 |
| `.github/lazycat-action.yml` | [lazycat-github-action](https://github.com/ca-x/lazycat-github-action) 配置 |
| `.github/workflows/lazycat.yml` | 构建 + 发布工作流 |

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |
