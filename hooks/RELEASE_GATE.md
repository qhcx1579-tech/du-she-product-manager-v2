# 发布门禁

## 发布前必须检查

- 是否存在密钥、token、账号、隐私数据
- 是否存在聊天记录、内部提示词、系统核心文件
- 是否存在本地缓存、构建产物、日志、临时文件
- 是否有 `.gitignore`
- 是否能从干净环境安装和运行
- 是否有明确的用户署名

## Windows 安装包检查

当发布对象包含 `.exe`、`setup.exe`、`installer.exe`、Inno Setup `.iss` 生成的安装包或其他 Windows 可执行发布包时，必须执行本检查。

- 是否有数字签名；如果没有签名，必须提示可能显示 Unknown Publisher、触发 Windows SmartScreen、出现 “Windows protected your PC”。
- 未签名安装包可以用于本地测试，但不应直接声称 production-ready 或适合正式公开分发。
- 新构建的未签名可执行文件通常没有 SmartScreen reputation；每次重新打包后 hash 会变化，新 hash 可能重新触发 SmartScreen 警告。
- SmartScreen 警告不一定代表程序有病毒，但属于发布风险，必须向用户说明。
- 是否可能被 Windows 11 Smart App Control 拦截；如果用户在开发测试环境中关闭 Smart App Control 后才能运行，必须标记为 Windows 安全信誉风险，而不是直接判断为代码损坏或发布通过。
- 不得把关闭 Smart App Control、SmartScreen、Defender 或防火墙作为正式发布方案；只有在开发测试环境、用户确认安装包来源可信时，才可作为临时排查选项。
- 正式发布版本不得要求用户关闭 Windows 安全功能。应优先从代码签名、发布者信息、版本信息、安装包校验、打包配置和可信分发渠道解决。
- 如果安装包写入系统目录、创建开机启动项、安装 Windows service、修改注册表、捆绑未知 `.exe` / `.dll`、使用压缩壳/混淆/加壳二进制、静默下载或执行外部程序，必须标记为高风险并要求用户确认。
- 如果项目使用 `.iss` 打包，必须先读取本地 `.iss` 文件和输出目录，再检查是否配置代码签名、是否包含不该打包的文件、是否包含 `.env` / token / cache / 日志 / 私有配置、是否存在过度权限请求、是否创建启动项/服务/注册表写入。
- `.iss` 文件应检查 `[Setup]` 中是否具备项目实际需要的 `AppName`、`AppVersion`、`AppPublisher`、`AppPublisherURL`、`AppSupportURL`、`AppUpdatesURL`、`DefaultDirName`、`DefaultGroupName`、`OutputBaseFilename`、`Compression`、`SolidCompression`、`WizardStyle`、`VersionInfoVersion`、`VersionInfoCompany`、`VersionInfoDescription`、`VersionInfoCopyright`。缺失时只能按本地项目实际名称、版本和输出目录补充，不得照搬通用模板。
- 发布包不得包含 `.env`、API keys、access tokens、SSH keys、local config、private notes、chat logs、system prompts、developer prompts、internal agent prompts、cache files、database dumps、cookies、session files、用户本机绝对路径。
- 正式发布前应使用代码签名证书签名安装包，计算并记录 SHA256 校验值，保留构建日志，并优先通过 GitHub Releases、官网或可信下载渠道分发。
- 不建议通过网盘、聊天软件直接分发未签名安装包；如果必须分发未签名测试包，必须明确说明可能触发 SmartScreen / Smart App Control 拦截。

## Windows 安装包故障诊断

当用户反馈 exe 打不开、安装包被 Windows 阻止、Windows 提示不允许安装、SmartScreen / Smart App Control 拦截、双击安装包无反应或被安全中心阻止时，不要直接判断为代码错误，也不要默认要求用户关闭安全功能。

必须先按以下顺序排查：

- Windows Smart App Control 是否拦截
- Microsoft Defender SmartScreen 是否拦截
- Microsoft Defender 是否误报
- 文件是否带有 Mark-of-the-Web 来源标记
- 安装包是否缺少代码签名
- 安装包是否缺少发布者信息
- 安装包是否缺少版本信息
- Inno Setup `.iss` 配置是否不完整
- 打包后的 exe 是否从非可信路径、网络下载目录或聊天软件缓存目录运行
- 是否存在打包器、压缩壳、混淆、过度权限请求或捆绑未知二进制导致误报

## Windows 发布摘要

发布 Windows 可执行文件或安装包前，必须输出检查摘要：

- installer 是否签名
- 是否预期触发 SmartScreen
- 是否可能被 Smart App Control 拦截
- 是否检测到 Defender / antivirus 风险
- 安装包包含哪些关键文件
- 是否已记录 SHA256 校验值
- 是否具备发布者信息和版本信息
- 是否适合 local testing
- 是否适合 public release
- 下一步建议

## GitHub 原则

- 仓库署名归用户。
- 不在提交信息、仓库说明或文件内容里把 GPT/Codex 写成作者，除非用户明确要求。
- 不上传开发者和 AI 才看的核心文件。
- 不允许在公开文档中写入用户邮箱、个人账号、具体仓库 URL 或其他可识别身份信息。
- 如需说明署名，只写“使用用户自己的本地 Git 身份”，并建议使用 GitHub no-reply 隐私邮箱。
- 提交到 GitHub 前，必须向用户确认目标仓库是否就是用户指定的仓库。
- 如果当前远程仓库不存在、不清楚或不是用户指定仓库，必须让用户提供要提交的仓库名称或 URL。
- 未经用户确认，不允许执行远程 push。
