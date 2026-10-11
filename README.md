# iland Releases

本仓库**只存放** Windows 安装包与自动更新清单，**不包含源代码**。

源码仓库为私有；用户与其他设备通过本仓库获取更新。

## 版本基线

发版按 **大版本基线 → 小版本基线 → 修订号** 排布（例如 `0` → `0.1` → `0.1.10`），避免修订过密时难找归属：

| 查看方式 | 说明 |
|----------|------|
| [Releases](../../releases) 标题 `基线 0.1 · v0.1.x` | 单次修订 |
| 标签 `baseline-0.1` | 该小版本基线下的**当前**安装包（滚动更新） |
| `latest` | 全仓库最新正式版（自动更新用） |

## 当前版本

**0.1.40.10**：优化设置搜索动效与 Dock 快捷键对齐，完善三维知识星河，修复工作流空资源策略和移动互联聊天额度误占用。完整变更及验证边界见对应 Release。

## 下载

打开右侧 [Releases](../../releases)，下载最新的：

- `iland_*_x64-setup.exe` — Windows 安装程序（推荐）

也可直接使用最新版直链（版本号随发版变化）：

```
https://github.com/tonylzm/iland-releases/releases/latest
```

## 自动更新说明

已安装的 iland 会在启动时**静默检查**本仓库的 `latest.json`：

```
https://github.com/tonylzm/iland-releases/releases/latest/download/latest.json
```

- 有新版本时在后台下载安装包，下载完成后由你确认何时安装体验
- 暂不安装时可继续使用当前版本，稍后从设置页进入更新
- 设置页可查看当前版本并手动「检查更新」

安装包经 Tauri 签名校验，篡改将无法安装。

## 维护者发版（私有源码仓）

在私有源码仓库执行：

```powershell
# 1) 本地构建（需 src-tauri/keys/iland.key）
powershell -ExecutionPolicy Bypass -File scripts\build-tauri.ps1

# 2) 发布到本公开仓库（需 RELEASES_GITHUB_TOKEN）
$env:RELEASES_GITHUB_TOKEN = "<PAT>"
powershell -ExecutionPolicy Bypass -File scripts\publish-github-release.ps1 -Notes "更新说明…" -CreateRepoIfMissing
```

每个版本会创建 GitHub Release 标签 `vX.Y.Z`，并上传：

| 文件 | 用途 |
|------|------|
| `iland_*_x64-setup.exe` | 安装包 |
| `iland_*_x64-setup.exe.sig` | 签名 |
| `latest.json` | 客户端更新发现 |
