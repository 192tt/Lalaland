# Lalaland 玩家版

## 最新 Windows：Unreal 测试版 · 2026-10-16

[下载新版 Windows 游戏](https://github.com/192tt/Lalaland/releases/tag/windows-ue5-20261016)

下载发布页的 **Lalaland-Windows-UE5-20261016.zip**，完整解压到可写目录（建议 D 盘），按以下顺序启动：

1. 双击 **配置API.cmd**，在记事本打开的 `Config/model.env` 中填写自己的配置。
2. `LALALAND_DEEPSEEK_API_KEY=` 后填写自己的 DeepSeek Key；默认模型为 `deepseek-flash`，可改成账号支持的 DeepSeek 模型。
3. `TYPESAFE_API_KEY=` 后填写自己的 TypeSafe / Jev Key，以启用模型自主行动调度；留空时该调度不可用。
4. 保存并关闭记事本，双击 **Lalaland.exe**。不要从 ZIP 内部启动，不要只复制 exe。

无需 Unity、Unreal Editor 或单独安装 Node.js。**公开包不含任何项目方 API 密钥，不提供免费托管模型**。当前 Unreal 版使用外部配置文件，没有旧 Unity 版的游戏内 API 表单，也不会自动切换离线回复。模型调用消耗玩家自己的服务商额度。填入密钥后不要再公开分享配置文件。

DeepSeek 用于角色、主控和 A2A；Jev 用于行动意图，实际移动、到达、关系由游戏验证。需要联网和可用账号额度。存档、日志、缓存及临时数据写在解压目录 `UserData`，请自行备份。

### 新版内容与测试范围

- 当前实现的入场、酒吧社交/文字对话、调酒、弹球、露台流星与首夜总结；包含本轮二楼承重/灯光、开局节奏、调酒确认和赠饮规则修复。
- 338 项后端测试通过。独立包内服务检查 6 项通过；公开空配置能明确报错，不伪装成在线就绪。本次封包未发送付费模型请求。
- 同一 Shipping 构建此前二楼 cooked 支撑检测 27/27、2 块地板/3 盏灯；自动场景 105 项通过。编辑器 37 通过、1 项旧音效资源检查失败，Night 25 通过。不是本次重新完整人工验收。
- 基础公共音乐已有验证；全部英韩文本、角色专属好感 BGM、配音/口型和道具接触精修未全部完成。正常速度完整首夜真人体验、投球手感和跨电脑兼容仍待反馈。
- 本次仅发布 Windows Unreal 测试版，**没有同步更新 macOS**，也不表示旧计划全部 Scene 0–6 已完整迁移。

按 E 与目标交谈、Enter 发送文字、Esc 返回；WASD 移动，F8 问主控。更多操作和限制见包内 `README.md`、`TEST_RESULTS.md`。

发布页附 `.zip.sha256`，包内附逐文件 `SHA256SUMS.txt`。PowerShell 校验：

```powershell
Get-FileHash .\Lalaland-Windows-UE5-20261016.zip -Algorithm SHA256
```

本版保留现有场景与角色，不包含开发者密钥、API Excel 库、个人存档、日志、调试符号或编辑器。请勿将填好密钥的本地配置提交 GitHub。

---

## 历史发行说明 · 2026-08-31（旧 Unity 版，不适用于新版 Unreal）

以下启动文件、API 表单、Scene 0–6、测试数字与 macOS 描述均只属于旧版；旧资产和下载保留，不作为新版完成证据。

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
