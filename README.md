<div align="center">
  <img src="bilibili-suite-hero.png" width="100%" alt="B站综合插件" />

  <p>
    <a href="https://gitee.com/carlor-official/BilibiliSuite/releases/latest"><img src="https://img.shields.io/badge/下载-Gitee%20Releases-6C5CE7?style=flat-square" alt="Gitee Releases" /></a>
    <img src="https://img.shields.io/badge/平台-Windows%20%7C%20Linux-2684FF?style=flat-square" alt="Windows 与 Linux" />
    <img src="https://img.shields.io/badge/架构-x86__64-00A884?style=flat-square" alt="x86_64" />
    <img src="https://img.shields.io/badge/消息-文字%20%2B%20图片-F59E0B?style=flat-square" alt="文字与图片消息" />
  </p>

  <p><strong>面向萌卡 NT 框架的 Bilibili 综合功能插件</strong></p>
  <p>跨平台 WebUI · 多 QQ 独立授权与数据空间 · 本地图片渲染 · 签名在线更新</p>

  <p>
    <a href="https://gitee.com/carlor-official/BilibiliSuite/releases/latest">下载最新版</a>
    · <a href="https://gitee.com/carlor-official/BilibiliSuite/releases">版本记录</a>
    · <a href="https://gitee.com/carlor-official/BilibiliSuite/issues">问题反馈</a>
    · <a href="README.en.md">English</a>
  </p>
</div>

---

## 项目简介

B站综合插件通过萌卡 NT 的正向 WebSocket 接收机器人事件，为群聊和私聊提供 Bilibili 查询、订阅、解析与通知能力。Windows 和 Linux 版本共用同一套 Web 管理界面，所有主要配置都可以在浏览器中完成。

插件遵循宿主能力，仅发送**文字与图片消息**，不依赖 Markdown。动态、视频和直播间等内容可使用本地渲染的图片卡片展示，文字模式同样会保留有用的封面或动态图片。

> 本仓库是官方版本发布与使用文档入口，不提供插件核心功能源码。运行插件功能需要有效授权。

## 核心能力

| 模块 | 能力 |
| --- | --- |
| 订阅与通知 | 动态、直播、大航海、送礼、直播事件、番剧更新、装扮与收藏集通知 |
| 信息查询 | 用户信息、直播间信息、最新动态、最新视频、装扮与粉丝勋章查询 |
| 链接解析 | 识别 B站用户主页、直播间、动态、视频及工房分享链接 |
| 消息展示 | 全局或按群切换文字/图片模式，本地渲染动态、视频和直播卡片 |
| B站登录 | 每位 QQ 用户独立扫码登录，凭据与订阅数据互不串用 |
| 特殊订阅 | 支持通过 Bark 向 iOS 设备推送动态与直播提醒 |
| 可视化管理 | 框架连接、账号授权、插件主人、群功能开关、自定义消息模板、运行日志与在线更新 |

聊天中发送 `哔哩菜单` 即可查看当前版本提供的指令入口。

<details>
<summary><strong>常用指令示例</strong></summary>

| 场景 | 示例 |
| --- | --- |
| 登录 B站 | `扫码登录账号` |
| 查询用户 | `用户信息 + uid / B站昵称` |
| 查看最新内容 | `最新动态 + uid / B站昵称`、`最新视频 + uid / B站昵称` |
| 订阅动态/直播 | `订阅动态 + uid / B站昵称`、`订阅直播 + uid / B站昵称` |
| 番剧提醒 | `订阅番剧 + 番剧名 / mid` |
| 装扮查询 | `搜索装扮 + 关键词`、`查询装扮 + 装扮ID` |
| 粉丝勋章 | `查询粉丝牌 + 房间号 / B站昵称`、`反查粉丝牌 + 粉丝牌名` |
| 消息模式 | `设置本群文字模式`、`设置本群图片模式` |

完整指令请以插件内 `哔哩菜单` 及其子菜单为准。

</details>

## 多 QQ 与授权隔离

框架中存在多个机器人 QQ 时，插件会为每个 QQ 建立独立运行空间：

- 授权状态、到期时间和心跳分别校验；
- 配置、登录凭据、订阅和群数据独立保存；
- 单个 QQ 未授权只停用该 QQ 的功能，不会关闭程序；
- 未授权账号不会影响其他已授权账号，也不会在聊天中发送授权提示；
- 授权服务短时波动不会因为单次心跳失败立即终止插件。

## 平台支持

| 平台 | 外发包 | 运行方式 | 要求 |
| --- | --- | --- | --- |
| Windows x64 | `BilibiliSuite-*-windows-x86_64.zip` | 解压后运行 `BilibiliSuite.exe` | Windows x86_64，现代浏览器 |
| Linux x86_64 | `BilibiliSuite-*-linux-x86_64.tar.gz` | 解压后执行 `sudo ./install.sh` | glibc 2.35+，推荐 Ubuntu 22.04/24.04 |

Windows 与 Linux 使用不同的二进制和更新包，请勿混用。Linux 版本不需要桌面环境，安装后由 systemd 管理并通过 WebUI 配置。

## 快速开始

### 1. 下载

前往 [Gitee Releases](https://gitee.com/carlor-official/BilibiliSuite/releases/latest)，下载与系统对应的压缩包。Release 中的同名 `.sig` 是在线更新使用的数字签名，请勿使用来源不明或签名不匹配的包。

### 2. 启动与初始化

<details open>
<summary><strong>Windows</strong></summary>

1. 完整解压 ZIP，保持 `BilibiliSuite.exe` 与其内部同名 `.sig` 位于同一目录。
2. 双击 `BilibiliSuite.exe`。
3. 首次运行设置 WebUI 监听地址、端口和管理令牌；端口默认 `18080`。
4. 浏览器打开控制台显示的地址并输入管理令牌。
5. 如需重置 WebUI 配置，关闭程序后在程序目录执行：

```powershell
.\BilibiliSuite.exe --reset-web
```

</details>

<details>
<summary><strong>Linux</strong></summary>

1. 上传并解压 tar.gz。
2. 在解压目录执行：

```bash
sudo ./install.sh
```

3. 安装向导会配置 WebUI 监听地址、端口和管理令牌；默认端口为 `18080`。
4. 浏览器访问 `http://服务器IP:18080`。
5. 常用运维命令：

```bash
systemctl status bilibili-suite --no-pager
journalctl -u bilibili-suite -f
systemctl restart bilibili-suite
```

公网使用时，建议通过宝塔或 Nginx 配置 HTTPS 反向代理，并让插件 WebUI 仅监听 `127.0.0.1`。

</details>

### 3. 对接萌卡 NT

进入 WebUI 后依次完成：

1. 在“框架连接”填写框架 IP/域名、端口和令牌；
2. 保存并启动连接，等待框架识别机器人 QQ；
3. 在“插件主人”填写主人 QQ，多个号码使用 `#` 分隔；
4. 在“账号管理”确认各 QQ 的授权状态和到期时间；
5. 按机器人 QQ 和群号进入“插件配置”设置消息模式、功能开关与自定义消息模板；
6. 需要查询、订阅或解析 B站内容时，先在聊天中发送 `扫码登录账号` 完成独立登录。

## WebUI

WebUI 同时适用于 Windows 与 Linux，主要页面包括：

- **仪表盘**：框架连接、机器人数量、授权数量和运行状态；
- **账号管理**：查看每个 QQ 的独立授权状态与有效期；
- **插件配置**：按 QQ、按群配置解析、消息模式、通知开关和自定义消息模板；
- **框架连接**：保存、启动、暂停或修改 WebSocket 配置；
- **插件主人**：支持多个主人 QQ，并可在框架离线时独立保存；
- **运行日志**：查看收到的消息、命令匹配、授权与发送结果，敏感字段自动脱敏；
- **右上角账户菜单**：查看管理员资料、刷新授权状态或安全退出 WebUI；
- **在线更新**：只提示更高版本，同版本会显示“当前已是最新版本”。

### 自定义消息模板

“插件配置 → 自定义模板”内置 18 套模板，覆盖直播开播/下播与总结、直播事件、动态与视频、番剧更新、用户与直播间查询、装扮和收藏集查询。模板支持：

- 当前机器人 QQ 的全局模板；
- 当前机器人 QQ 下的指定群覆盖；
- 点击插入 `【变量】`、变量白名单校验、恢复内置默认；
- 图片变量继续作为真实图片消息发送，不会转换为 Markdown 或图片链接；
- 配置与机器人数据空间一起加密保存，不同 QQ 之间不会串用。

## 图片消息与远程部署

当插件与萌卡 NT 框架不在同一台机器时，需要在“框架连接”配置**图片公网访问地址**。该地址应反向代理到插件 WebUI，并保留 `/media/` 路径：

- 图片链接仅供框架读取；
- 默认约 180 秒过期；
- 每张图片只能成功读取一次；
- 未配置公网地址时会立即回退到文字回复，避免长时间等待上传超时。

## 安全与隐私

- 外发包只包含签名后的程序、运行库和使用文档，不包含插件核心源码、发布私钥、用户配置或业务数据；
- 主程序和在线更新包均进行数字签名校验，文件被修改或签名缺失时拒绝运行或安装；
- WebUI 管理令牌、框架令牌与 B站登录凭据采用本机加密存储；
- Web API 对连续错误令牌进行来源限速；
- 日志会自动隐藏令牌、Cookie 与常见敏感字段；
- 在线授权以机器人 QQ 为单位校验，不能用一个 QQ 的授权代替另一个 QQ。

请勿公开分享 `config.json`、`web-admin.json`、`admin.token` 或插件数据目录。

## 在线更新

WebUI 右上角可以检查 Gitee 最新 Release：

1. 只在远端版本高于当前版本时显示更新；
2. Windows 与 Linux 自动选择各自的 x86_64 包；
3. 下载压缩包及其同名 `.sig`；
4. 验签成功后才进入安装流程；
5. 签名缺失、损坏或平台不匹配时拒绝更新。

## 常见问题

<details>
<summary><strong>框架显示已连接，但机器人收不到消息</strong></summary>

确认萌卡 NT 使用的是正向 WebSocket 服务，并检查框架 IP、端口和令牌。然后在“运行日志”确认是否出现群聊或私聊事件；如果只看到账号列表轮询，没有收到消息事件，请检查框架插件服务的事件推送配置。

</details>

<details>
<summary><strong>指令有响应，但 B站查询失败</strong></summary>

发送 `扫码登录账号`，使用自己的 B站账号扫码并确认。B站风控、登录失效或网络代理也可能导致请求失败，请先在运行日志中查看具体错误。

</details>

<details>
<summary><strong>远程部署时图片发送失败</strong></summary>

配置可被框架访问的 HTTPS 图片公网地址，确认反向代理保留 `/media/` 路径，并检查服务器防火墙、安全组和代理规则。未配置时插件会回退到文字消息。

</details>

<details>
<summary><strong>没有授权时程序是否会退出</strong></summary>

不会。程序和 WebUI 会继续运行，未授权 QQ 保持停用并定时独立重试，其他已授权 QQ 不受影响。

</details>

## 版本与反馈

- 更新记录与下载：[Gitee Releases](https://gitee.com/carlor-official/BilibiliSuite/releases)
- Bug 与建议：[提交 Issue](https://gitee.com/carlor-official/BilibiliSuite/issues)

本仓库当前不提供插件核心源码或开源许可。请仅从本仓库 Release 获取正式外发包。
