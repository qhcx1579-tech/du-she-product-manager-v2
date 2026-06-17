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
- 如果安装包写入系统目录、创建开机启动项、安装 Windows service、修改注册表、捆绑未知 `.exe` / `.dll`、使用压缩壳/混淆/加壳二进制、静默下载或执行外部程序，必须标记为高风险并要求用户确认。
- 如果项目使用 `.iss` 打包，必须检查是否配置代码签名、是否包含不该打包的文件、是否包含 `.env` / token / cache / 日志 / 私有配置、是否存在过度权限请求、是否创建启动项/服务/注册表写入。
- 发布包不得包含 `.env`、API keys、access tokens、SSH keys、local config、private notes、chat logs、system prompts、developer prompts、internal agent prompts、cache files、database dumps、cookies、session files、用户本机绝对路径。

## Windows 发布摘要

发布 Windows 可执行文件或安装包前，必须输出检查摘要：

- installer 是否签名
- 是否预期触发 SmartScreen
- 是否检测到 Defender / antivirus 风险
- 安装包包含哪些关键文件
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
