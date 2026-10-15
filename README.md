# Kazumi · 主页改版

Kazumi 是使用 Flutter 开发的番剧浏览与在线观看应用，支持自定义规则、番剧搜索、时间表和追番管理。本地版本在原项目基础上重新设计主页，采用深蓝背景、杏橙强调色与圆角海报卡片。

## 改动与新功能

- 分类浏览：推荐、日常、奇幻、恋爱、治愈、热血；快速切换时忽略过期请求，避免混入上一分类的数据。
- 分层展示：焦点大卡、横向海报列表和「更多发现」网格，支持滚动加载与数据去重。焦点大卡展示当前列表首项。
- 快捷入口：搜索、时间表、历史记录；点击焦点卡或海报可进入番剧详情，时间表入口同步导航选中状态。
- 异常处理：封面加载失败时显示标题占位；数据加载失败时提供重试与加速设置入口。
- 屏幕适配：兼容窄屏与桌面布局，并覆盖放大字体的主页布局测试。

主要实现位于 `lib/pages/popular/` 和 `lib/pages/menu/menu.dart`，应用入口是 `lib/main.dart`。

## 本地使用

开发环境：Flutter **3.47.7**，Dart **>=3.10.0 <4.0.0**。Windows 构建还需 Visual Studio 的「使用 C++ 的桌面开发」工具。

在本目录（包含 `pubspec.yaml`）打开终端，使用已安装的 Flutter：

```powershell
flutter pub get
flutter run -d windows --no-enable-impeller
```

本机 Flutter 位于项目父目录的 `.tools/flutter`。若终端找不到 `flutter`，可在本目录直接运行：

```powershell
& '..\.tools\flutter\bin\flutter.bat' pub get
& '..\.tools\flutter\bin\flutter.bat' run -d windows --no-enable-impeller
```

VS Code：打开本目录，安装 Flutter / Dart 扩展，选择运行配置 `Kazumi (debug, Skia)`，按 **F5** 启动。

如已有 Windows 调试构建，可直接启动：

```powershell
.\build\windows\x64\runner\Debug\kazumi.exe
```

需保留可执行文件所在目录中的 DLL 与 `data` 等文件。主页数据与封面依赖网络，播放内容需配置可用的自定义规则；加载失败时可进入应用内「加速设置」，返回后重试。

## 操作示例

1. 分类找番：主页点击「奇幻」，浏览「奇幻 · 精选」，点击海报查看详情。
2. 名称搜索：点击「搜索想看的番组」，输入番组名称并查看搜索结果。
3. 查看排期：点击主页「时间表」，查看每日更新安排。
4. 继续浏览：返回「推荐」，向下滚动浏览「正在热议」「值得慢慢看」与「更多发现」。展示内容随返回数据变化。

## 本地测试

在项目根目录执行：

```powershell
flutter test
flutter analyze --no-fatal-infos --fatal-warnings
```

只运行主页回归测试：

```powershell
flutter test test/popular_page_test.dart
```

主页测试使用本地测试数据，覆盖 320 / 390 / 1280 像素宽度、1.0 / 1.5 倍字体、分类切换、首屏加载、请求乱序与错误提示。此类测试不代表在线数据源或实际播放链路验证通过。

## 上游与许可

原项目：[Predidit/Kazumi](https://github.com/Predidit/Kazumi)。完整原说明、资源授权、免责声明及致谢保留于 [README.upstream.md](README.upstream.md)，开发约定见 [贡献指引](static/doc/CONTRIBUTING.md)。

代码遵循 [GPL-3.0](LICENSE)。图标版权属于 Yuquanaaa，其原有使用授权不意味着可自由复制、修改或分发；内嵌 Mi Sans 字体版权属于 Xiaomi，资源授权详见原说明。
