# KA Music — Windows 构建器

为 [`umr-xiaomai/kgka_Music_hl`](https://github.com/umr-xiaomai/kgka_Music_hl)（KA Music）自动构建 Windows 安装包。

上游官方 Release 只提供 `.apk`（Android）和 `.ipa`（iOS），没有 Windows 版本。
本仓库不改动任何上游代码，只通过 GitHub Actions 拉取上游源码并编译，产出可直接安装的 Windows 包。

## 产物

每次构建会生成两个文件，放在本仓库的 [Releases](../../releases) 里：

| 文件 | 说明 |
| --- | --- |
| `KA-Music-Setup-<版本>-win64.exe` | 安装版：向导式安装，创建开始菜单和桌面快捷方式，自带卸载程序 |
| `KA-Music-<版本>-portable-win64.zip` | 免安装版：解压到任意目录，双击 `kgka_music_hl.exe` 即可运行 |

> 安装包未做代码签名，首次运行 Windows SmartScreen 可能提示「未知发布者」，
> 点击「更多信息 → 仍要运行」即可。

## 自动跟随上游更新

工作流每天北京时间 03:00 自动检查一次上游仓库：

1. 读取上游 `master` 的最新 commit
2. 读取 `pubspec.yaml` 里的版本号
3. 如果对应版本的 Release 还不存在，或已存在但记录的 commit 与当前不一致 → 重新构建并更新 Release
4. 否则跳过，不浪费构建时间

## 手动触发

在 **Actions → Build KA Music for Windows → Run workflow** 中可手动运行：

- `upstream_ref`：指定要构建的上游 ref（tag / 分支 / commit）。留空用 `master`。
  例如填 `v3.2.0` 就构建官方 v3.2.0 那个稳定版本。
- `force`：勾选后无视「已构建过」的判断，强制重新构建并覆盖同名 Release。

## 说明

- 构建环境：`windows-latest` + Flutter stable 通道
- 产物架构：x64
- 本项目仅用于个人构建与学习交流，软件本身版权归原作者 [@umr-xiaomai](https://github.com/umr-xiaomai) 所有
