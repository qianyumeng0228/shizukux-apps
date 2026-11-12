# ShizukuX 应用商店索引

ShizukuX 内置「应用」页 → 右上角「应用商店」读取的就是这个仓库的 [`apps.json`](apps.json)。

- 客户端地址：`https://raw.githubusercontent.com/qianyumeng0228/shizukux-apps/main/apps.json`
- 镜像顺序：`gh-proxy.com` → `cdn.jsdelivr.net` → `raw.githubusercontent.com` → `github.com`
- 客户端会校验 `sizeBytes` 与 `sha256`，对不上直接判失败，不会装一个残缺包。

## 字段

| 字段 | 必填 | 说明 |
|---|---|---|
| `id` | 是 | 唯一标识，建议直接用包名 |
| `name` / `nameZh` | 是 | 英文名 / 中文名，中文界面优先显示 `nameZh` |
| `packageName` | 是 | Android 包名，用于判断是否已安装与升级 |
| `versionName` / `versionCode` | 是 | 版本号，`versionCode` 用于比较是否有更新 |
| `downloadUrl` | 是 | 必须是 GitHub Release 资产或可直接下载的 https 直链 |
| `fallbackUrl` | 否 | 下载失败时的备用地址（建议填 gh-proxy 镜像） |
| `sizeBytes` | 是 | APK 字节数，客户端比对 |
| `sha256` | 是 | APK 的 SHA-256（大写或小写均可），客户端比对 |
| `minSdk` | 否 | 最低系统版本 |
| `description` / `descriptionZh` | 否 | 英文 / 中文描述 |
| `tags` | 否 | 最多 6 个标签 |
| `sourceRepo` | 否 | 开源仓库，便于溯源 |

## 提交新应用

1. 先把 APK 发到你自己的 GitHub Release（不要直接把 APK 提交进本仓库，仓库只放索引）。
2. 在 App 里「应用商店 → 上传应用」填写表单，会自动生成一份符合本仓库格式的 JSON 并打开 GitHub Issue。
3. 维护者审核后把该条目合并进 `apps.json`，所有 ShizukuX 用户即可看到。

也可以在网页端直接提 Issue：选择「应用提交」模板，填完等审核。

## 审核口径

- 只收可追溯来源的 APK：必须有公开 Release 直链 + SHA-256。
- 不收录需要额外付费、带激活校验、或无法确认签名来源的包。
- 同一个包名只保留一条，新版本直接改原条目的 `versionName` / `versionCode` / `downloadUrl` / `sizeBytes` / `sha256`。
- 默认只做索引，不在本仓库托管二进制。
