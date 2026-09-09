# FlowTask 发布仓库（FlowTask-publish）

本仓库存放 **FlowTask** Android App 的正式构建产物（APK），由源码仓库自动发布，供 App 内「检查更新」功能拉取。

> 源码仓库（私有）：[tansor/FlowTask](https://github.com/tansor/FlowTask)

## 内容

- `FlowTask_release_*.apk`：每次发布的 APK（**仅保留最近 3 个版本**，旧版本自动清理）。
- `latest.json`：始终指向最新版本，字段如下：

  ```json
  {
    "versionName": "20260909.1638",
    "versionCode": 20260909,
    "downloadUrl": "https://raw.githubusercontent.com/tansor/FlowTask-publish/main/FlowTask_release_20260909_1638.apk",
    "releaseNotes": "……",
    "publishedAt": "2026-09-09T08:38:00Z",
    "size": 12920122
  }
  ```

## 自动更新机制

- App 在「设置 → 检查更新」时，匿名读取本仓库的 `latest.json`，对比 `versionCode` 高于本机版本即自动下载 `downloadUrl` 指向的 APK 并拉起安装器。
- 发布由源码仓库的 `scripts/publish-apk.sh` 触发：构建完成后经 SSH 推送 APK 与本文件至本仓库（绕开大文件 HTTPS 上传限制），自动清理旧版本、保持最近 3 个。

## 手动安装

点击仓库中最新一个 `FlowTask_release_*.apk` 下载安装即可（安装时需允许「未知来源」应用）。
