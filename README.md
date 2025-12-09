# ECH Workers 客户端

跨平台的 ECH Workers 代理客户端，支持 Windows、macOS 和 Linux（ARM/x86）。
tg交流群 https://t.me/+ft-zI76oovgwNmRh
## 致谢

本项目的客户端和 Go 核心程序均基于 [CF_NAT](https://t.me/CF_NAT) 的原始代码开发。

- **原始项目来源**: [CF_NAT - 中转](https://t.me/CF_NAT)

## 功能特性

- ✅ **多服务器管理** - 支持多个服务器配置，快速切换
- ✅ **一键系统代理** - 自动设置系统代理，支持分流模式
- ✅ **智能分流** - 全局代理、跳过中国大陆、不改变代理三种模式
- ✅ **中国IP列表** - 自动下载并应用完整的中国IP列表（基于 [mayaxcn/china-ip-list](https://github.com/mayaxcn/china-ip-list)）
- ✅ **系统托盘** - 最小化到系统托盘，不占用任务栏
- ✅ **开机自启** - 支持 Windows 和 macOS 开机自动启动
- ✅ **高 DPI 支持** - 完美支持高分辨率显示器
- ✅ **实时日志** - 查看代理运行状态和日志
- ✅ **配置持久化** - 自动保存配置，下次启动自动加载

## 快速开始

### 方法 1: 使用预编译版本（推荐）

从 [GitHub Releases](https://github.com/your-repo/releases) 下载对应平台的压缩包：

- **Windows**: `ECHWorkers-windows-amd64.zip`
- **macOS Intel**: `ECHWorkers-darwin-amd64.zip`
- **macOS Apple Silicon**: `ECHWorkers-darwin-arm64.zip`
- **Linux x86_64**: `ECHWorkers-linux-amd64.tar.gz`
- **Linux ARM64**: `ECHWorkers-linux-arm64.tar.gz`

解压后直接运行：
- **Windows**: 双击 `ECHWorkersGUI.exe` 启动 GUI，或运行 `ech-workers.exe` 使用命令行
- **macOS**: 运行 `./ECHWorkersGUI` 启动 GUI，或运行 `./ech-workers` 使用命令行
- **Linux**: 运行 `./ECHWorkersGUI` 启动 GUI，或运行 `./ech-workers` 使用命令行

> **注意**: 预编译版本已包含所有依赖，无需安装 Python 或任何其他软件。

### 方法 2: 从源码编译

#### 编译 Go 程序

```bash
# 初始化 Go 模块
go mod init ech-workers
go mod tidy

# 编译
go build -o ech-workers ech-workers.go
```

#### 运行 Python 客户端

```bash
# 安装依赖
pip install PyQt5

# 运行
python3 gui.py
```

## 文件说明

### 核心文件
- `ech-workers.go` - Go 源码（核心代理程序，基于 [CF_NAT](https://t.me/CF_NAT) 的原始代码）
- `gui.py` - Python GUI 客户端（使用 PyQt5，基于 [CF_NAT](https://t.me/CF_NAT) 的原始 Windows 客户端）

### 配置文件
- `go.mod`, `go.sum` - Go 模块文件
- `requirements.txt` - Python 依赖列表

## 系统要求

- **Windows**: Windows 10+ (Windows 11 完全支持)
- **macOS**: macOS 10.13+
- **Linux**: Ubuntu 18.04+ / Debian 10+ / CentOS 7+ (支持 x86_64 和 ARM64)
- **Python**: 3.6+ (仅从源码运行时需要)
- **Go**: 1.23+ (仅编译时需要，ECH 功能需要此版本)

## 配置说明

配置文件保存在：
- **Windows**: `%APPDATA%\ECHWorkersClient\config.json`
- **macOS**: `~/Library/Application Support/ECHWorkersClient/config.json`
- **Linux**: `~/.config/ECHWorkersClient/config.json`

## 使用说明

### 基本使用

1. **配置服务器**
   - 点击"新增"添加服务器配置（会创建新配置，不会覆盖现有配置）
   - 填写服务地址（如：`your-worker.workers.dev:443`）和监听地址（如：`127.0.0.1:1080`）
   - 可选：填写身份令牌、优选IP、DOH服务器、ECH域名等高级选项
   - 点击"保存"保存当前配置

2. **启动代理**
   - 点击"启动代理"按钮启动代理服务
   - 查看日志区域了解运行状态
   - 点击"停止"按钮停止代理服务

3. **设置系统代理**
   - 启动代理后，点击"设置系统代理"按钮
   - 系统会自动配置代理设置
   - 停止代理或关闭程序时会自动清理系统代理

### 分流功能

程序支持三种分流模式：

- **全局代理** - 所有流量都走代理（只绕过本地和内网地址）
- **跳过中国大陆** - 中国网站直连，其他网站走代理
  - 自动下载并应用完整的中国IP列表
  - 包含常见中国域名（*.cn, *.baidu.com, *.qq.com 等）
- **不改变代理** - 不设置系统代理，手动配置

切换分流模式后，如果已设置系统代理，会自动更新绕过规则。

### 系统托盘

- **最小化到托盘** - 关闭窗口时程序会最小化到系统托盘，不会退出
- **显示窗口** - 双击托盘图标或右键菜单选择"显示窗口"
- **退出程序** - 右键托盘图标选择"退出"

### 开机自启

勾选"开机启动"复选框，程序会在系统启动时自动运行并启动代理（如果配置了自动启动参数）。

## 故障排除

### PyQt5 安装问题

如果遇到 PyQt5 安装问题：
```bash
# macOS
pip3 install --user PyQt5
# 或
pip3 install --break-system-packages PyQt5

# Windows
pip install PyQt5

# Linux
sudo apt install python3-pyqt5  # Debian/Ubuntu
# 或
pip3 install PyQt5
```

### 找不到 ech-workers

确保已编译 Go 程序：
```bash
go build -o ech-workers ech-workers.go
```

### Windows 11 系统代理问题

如果 Windows 11 系统代理设置失败：
- 确保以管理员权限运行程序
- 检查防火墙设置
- 程序会自动使用正确的代理格式（`127.0.0.1:端口`）

### Linux 系统代理设置

Linux 暂不支持自动设置系统代理，需要手动配置：
- 在系统设置中配置 SOCKS5 代理为 `127.0.0.1:端口`
- 或使用环境变量：`export ALL_PROXY=socks5://127.0.0.1:端口`

### 中国IP列表加载失败

如果中国IP列表下载失败：
- 程序会使用默认的主要IP段
- 检查网络连接
- 列表会缓存24小时，过期后自动重新下载

### 删除服务器后列表清空

已修复：删除服务器后会自动切换到其他服务器，无需重启程序。

### bad CPU type in executable (macOS)

如果遇到此错误：
- Intel Mac 请下载 `darwin-amd64` 版本
- Apple Silicon Mac 请下载 `darwin-arm64` 版本

## 开发

### 本地测试

```bash
# 编译 Go
go build -o ech-workers ech-workers.go

# 测试 Python
python3 -m py_compile gui.py
```

### GitHub Actions

推送标签会自动触发构建和发布：
```bash
git tag v1.0.0
git push origin v1.0.0
```

## 许可证

本项目基于 [CF_NAT](https://t.me/CF_NAT) 的原始代码开发。

## 技术细节

### ECH (Encrypted Client Hello)

ECH 是 TLS 1.3 的扩展功能，用于加密 TLS 握手中的 SNI（服务器名称指示），提供更强的隐私保护。这是本程序的**核心功能**，需要 Go 1.23+ 支持。

### 中国IP列表

程序会自动从 [mayaxcn/china-ip-list](https://github.com/mayaxcn/china-ip-list) 下载完整的中国IP列表，用于"跳过中国大陆"分流模式。列表会缓存24小时，过期后自动更新。

### 系统代理设置

- **Windows**: 通过注册表设置系统代理，支持 SOCKS5 代理
- **macOS**: 使用 `networksetup` 命令设置所有网络服务的 SOCKS 代理
- **Linux**: 暂不支持自动设置，需要手动配置

## 相关链接

- **原始项目**: [CF_NAT - 优选IP Telegram 频道](https://t.me/CF_NAT)
- **Telegram**: [@CF_NAT](https://t.me/CF_NAT)
- **中国IP列表**: [mayaxcn/china-ip-list](https://github.com/mayaxcn/china-ip-list)
## Star History

<a href="https://www.star-history.com/#byJoey/ech-wk&type=timeline&logscale&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=byJoey/ech-wk&type=timeline&theme=dark&logscale&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=byJoey/ech-wk&type=timeline&logscale&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=byJoey/ech-wk&type=timeline&logscale&legend=top-left" />
 </picture>
</a>
## 贡献

欢迎提交 Issue 和 Pull Request！

