# Lalaland 玩家版

这是 **Lalaland** 的玩家发行仓库，提供 Windows 和 macOS 运行包。两个版本都包含整晚 Scene 0–6 流程、BGM，以及由玩家自行填写的模型 API 配置。

## 下载与启动

### Windows

1. 打开 [Windows Release](https://github.com/192tt/Lalaland/releases/tag/windows-bgm-api-20260831)，下载 `Lalaland-Windows-bgm-api-20260831.zip`。
2. 将 ZIP **完整解压**到本地文件夹，不要直接在压缩包内运行。
3. 双击解压目录中的 `启动游戏.cmd`。
4. Windows 首次启动若显示安全提示，请核对本页 SHA-256 后再选择运行。

支持 Windows 10/11 64 位。建议使用 1280×720 或更高分辨率。

### macOS

1. 打开 [macOS Release](https://github.com/192tt/Lalaland/releases/tag/macos-bgm-api-20260831)，下载 `Lalaland-macOS-bgm-api-20260831.zip`。
2. 完整解压后，双击 `启动 Lalaland.command`，或直接打开 `Lalaland.app`。
3. 本包支持 Intel 和 Apple Silicon。请保留同目录下的 `Server` 文件夹。
4. 此交叉编译版本尚未经过 Apple Developer ID 签名和公证；首次打开时可能需要在 Finder 中按住 Control 点击 `Lalaland.app`，选择“打开”。

建议使用 macOS 13 或更高版本。包内有更完整的 `MACOS_启动说明.md`。

## 配置模型 API

进入游戏首页后，点击 **“填写模型 API”**（已有配置时显示 **“模型 API · 已配置”**），填写：

- API Base URL：兼容 OpenAI Chat Completions 的服务地址，游戏会自动追加 `/chat/completions`。
- 模型 ID：服务商提供的模型名称。
- API Key：玩家自己的模型密钥。

示例 Base URL：

- DeepSeek：`https://api.deepseek.com`
- OpenAI：`https://api.openai.com/v1`

远程地址必须使用 HTTPS；本机 `localhost`、`127.0.0.1` 或 `::1` 可以使用 HTTP。模型服务需要支持 `response_format: json_object`。没有 API Key 时仍可明确选择离线规则模式游玩。

API Key 只保存在玩家电脑的以下位置：

```text
Windows: %USERPROFILE%\.lalagame\private\model.env
macOS:   ~/.lalagame/private/model.env
```

密钥不会打进安装包、存档或日志，也不会由游戏接口返回。该本地文件未加密，建议使用有额度限制且可以随时撤销的独立密钥。

## 文件校验

```text
Windows
SHA-256  bdf4ef72223a523afda031ad72c9b8e55814e585abfc7bc98f908a59d4ee9e59
文件名   Lalaland-Windows-bgm-api-20260831.zip
大小     202,476,596 bytes

macOS
SHA-256  48deefe33294eac1edb95d354f12f1d0938f97dbecc72d822ac16f95cd226eb1
文件名   Lalaland-macOS-bgm-api-20260831.zip
大小     253,234,741 bytes
```

仓库同时提供 `.sha256` 校验文件。PowerShell 校验命令：

```powershell
Get-FileHash .\Lalaland-Windows-bgm-api-20260831.zip -Algorithm SHA256
Get-FileHash .\Lalaland-macOS-bgm-api-20260831.zip -Algorithm SHA256
```

## 本版内容

- 从电梯入场开始，串联 Scene 0–6 的酒吧整晚流程。
- 第一人称移动、观察、互动与文字交流。
- A–D 角色模型与动作系统、头顶对白气泡和面对面交谈。
- 动态社交、塔罗、走廊、断电散场和屋顶开放收尾。
- BGM 与环境音。
- 玩家自行配置在线模型 API；在线失败时可重试，不会用固定台词冒充模型回复。

## 已完成验证

- 后端测试：151/151 通过。
- 编辑器测试：28/28 通过。
- 1080p 模型 API 表单：35 项检查通过。
- 最终运行包冒烟测试：13/13 通过。
- ZIP 内 894 个文件逐项校验通过。
- macOS Universal Player 构建成功；Mac ZIP 内 906 个文件逐项校验通过，6 个启动文件保留 Unix 可执行权限。
- 发布目录已排除开发者密钥、存档、数据库、日志和调试产物。

## 已知限制

- 角色当前没有面部 BlendShape，因此本版不包含口型与面部表情；自然表现主要来自身体动作、头部注视和移动节奏。
- 独立的 Scene 2→塔罗旧测试夹具未随发布包提供；整晚主线路径由 57 项检查覆盖。
- BGM 的公开再分发权需要发布者在对外宣传或商业分发前再次确认。
- 在线对白质量和响应速度取决于玩家所选择的模型服务、网络和账户额度。
- macOS 包目前没有经过 Apple 签名、公证或真实 Mac 窗口验收；当前确认范围是交叉编译成功、双架构文件检查和归档结构校验。

## 源代码

项目源代码仓库：[LALAGAME](https://github.com/babasoumah702-rgb/LALAGAME)

本仓库仅用于分发玩家运行包。
