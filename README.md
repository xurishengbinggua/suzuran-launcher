# PCL 铃兰修改版（Suzuran Launcher）

> 第三方基于 [Plain Craft Launcher 2](https://github.com/Hex-Dragon/PCL2) 独立进行的二次创作，**不是 PCL 官方版本**，与原作者之间不存在隶属或授权关系。

一个以「明日方舟 · 铃兰」为主题的 PCL 界面重构版：左侧图标栏 + 悬浮白色卡片 + 冰蓝配色，启动页内置铃兰插画。

## 下载

见本仓库的 **Releases** 页面。解压后运行 `Plain Craft Launcher 2.exe` 即可，首次启动会自动创建目录，不影响已有存档。

## 功能

- 启动页铃兰主题视觉，插画可自行替换或关闭
- 下载页完整解锁：原版游戏、Mod、整合包、数据包、资源包、光影包
- 微软正版登录（OAuth 2.0 设备代码流 / 公共客户端，无客户端密码）
- 窗口默认尺寸 1000 × 600

## 微软正版登录是怎么工作的

本程序使用 Microsoft 标识平台的官方 OAuth 2.0 设备授权流：

1. 用户在启动器内点击「正版登录」；
2. 启动器向 `https://login.microsoftonline.com/consumers/oauth2/v2.0/devicecode` 申请一次性代码；
3. 用户在 `https://www.microsoft.com/link` 输入代码并在微软官方页面完成授权；
4. 启动器用返回的令牌依次换取 Xbox Live、XSTS 令牌，再调用 `api.minecraftservices.com`：
   - `/entitlements/mcstore` 校验该账号是否拥有 Minecraft: Java Edition；
   - `/minecraft/profile` 获取 Java 版档案（UUID、用户名）；
   - `/authentication/login_with_xbox` 获取启动游戏所需的凭证。

开发者不接触用户的微软账号密码；访问令牌与刷新令牌只保存在用户本机。

> 若启动器使用的 Client ID 尚未通过 Minecraft 服务审核，第 4 步会返回
> `403 Invalid app registration`（与网络、VPN 无关）。审核入口：<https://aka.ms/mce-reviewappid>

## 更换启动页插画

把图片命名为 `main.jpg`、`main.png` 或 `main.jpeg`，放进程序目录的 `PCL\Suzuran\`，覆盖原文件后重启即可生效。

删除该目录下的 `main.*` 文件，启动页会恢复为纯文字版。

## 隐私

见 [PRIVACY.md](PRIVACY.md)。简言之：不收集、不上传、不出售任何个人信息，令牌只存在本机。

## 许可与署名

- 原作者：龙腾猫跃（Hex-Dragon）· <https://github.com/Hex-Dragon/PCL2>
- 赞助原作者：<https://meloong.com/afd/a/LTCat>
- 本改版作者：guapi
- 本仓库继续沿用《PCL 分发有限许可》与《PCL 存储库合理使用指南》，全文见 [LICENSE](LICENSE)

本改版为重度使用情形，已按要求：

1. 明确标注为第三方二次创作；
2. 软件名称以 Plain Craft Launcher (PCL) 开头并带第三方修改后缀；
3. 在关于页首位署名原作者并提供赞助链接，公开源代码，继续使用原许可文件；
4. 保留 Minecraft 正版购买劝导；
5. 界面主要色相保持为蓝色，不提供类似赞助解锁的功能。

## 免责声明

请支持正版 Minecraft。本项目仅供学习与个人使用，与 Mojang Studios、Microsoft 无任何关联；Minecraft 是 Mojang Studios 的商标。

---

## For Minecraft Services reviewers

Suzuran Launcher is a free, open-source, non-commercial third-party launcher for **Minecraft: Java Edition**, built as a UI-focused derivative of the open-source **Plain Craft Launcher 2** project. It is distributed publicly at no cost and does not sell or bundle the game.

It uses the official Microsoft identity platform with the **OAuth 2.0 device authorization grant as a public client** (no client secret). After the user signs in with their own Microsoft account, tokens are exchanged through Xbox Live and XSTS, and `api.minecraftservices.com` is called only to:

1. verify that the signed-in account owns Minecraft: Java Edition (`/entitlements/mcstore`);
2. retrieve the account's Java profile (`/minecraft/profile`);
3. obtain launch credentials for the user's own account (`/authentication/login_with_xbox`).

The developer does not collect Microsoft credentials. Access and refresh tokens are stored only on the user's own device and are used only to keep the user signed in. The launcher does not bypass Microsoft authentication, does not grant Minecraft entitlements to accounts that do not own the game, and does not modify or redistribute game files.

A single public Client ID is shared by all users of the launcher, which is why one AppID approval is requested.

Contact: <!-- 填入联系邮箱 -->
