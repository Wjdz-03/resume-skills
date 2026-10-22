# resume-skills

<div align="center">
  <img src="assets/asu-avatar-circle.png" width="180" height="180" alt="ASu-skills 图标">
  <h3>中文简历求职技能包</h3>
  <p>用四个独立入口完成简历提升、简历制作、岗位匹配分析和简历投递填写。</p>
</div>

<div align="left">
  <a href="README_en.md">English</a> | <a href="README.md">中文</a> | <a href="https://github.com/Wjdz-03/resume-skills">仓库</a>
</div>

<br>

<div align="center">
  <a href="LICENSE"><img src="https://img.shields.io/github/license/Wjdz-03/resume-skills?logo=github" alt="License: MIT"></a>
</div>

<p align="center">
  <img src="assets/asu-skills-overview-landscape-v2.png" alt="ASu-skills 部分技能工作流示意" width="1100">
</p>

> **致谢/许可**：本项目基于 [Hisn00w/ASu-skills](https://github.com/Hisn00w/ASu-skills)（MIT）二次开发，感谢原作者 Hisn00w；MIT 许可证文本保留于 [LICENSE](LICENSE)。

## 目录

- [安装](#安装)
- [第一次使用：从哪个入口开始](#第一次使用从哪个入口开始)
- [四个 Skill](#四个入口如何配合)
  - [`/great-resume`：简历提升](#great-resume简历提升)
  - [`/make-resume`：制作简历](#make-resume制作简历)
  - [`/job-match`：岗位匹配分析](#job-match岗位匹配分析)
  - [`/job-apply`：简历投递填写](#job-apply简历投递填写)
- [四个入口如何配合](#四个入口如何配合)
- [事实边界](#事实边界)
- [文件结构](#文件结构)
- [参与贡献](#参与贡献)
- [特别感谢](#特别感谢)
- [致谢](#致谢)
- [Contributors](#contributors)
- [开源协议](#开源协议)
- [Star History](#star-history)

<!-- catalog:readme.zh.intro:begin -->
ASu-skills 现在是一个插件包。安装后会提供四个可单独调用的入口：

| 入口 | 用途 | 主要交付 |
| --- | --- | --- |
| `/great-resume` | 简历提升 | 岗位定位、项目改写、成果证据、HR 开场白 |
| `/make-resume` | 简历制作 | 按 ASu 或指定模板生成可编辑 HTML 简历，支持 PDF 导出与可选的 LaTeX 源文件 |
| `/job-match` | 岗位匹配 | 对照 JD 与真实经历，输出证据矩阵、硬性门槛和投递建议 |
| `/job-apply` | 简历投递填写 | 连接浏览器自动填写求职申请，核对后停在提交前 |
<!-- catalog:readme.zh.intro:end -->

## 安装

resume-skills 同时支持 Codex、Claude Code、DeepSeek Harness Desktop、TraeWork 和 Qoder，另有 Cursor、OpenCode 与 WorkBuddy 的轻量桥接入口。所有入口共用同一套 `skills/`、`assets/` 和 `references/`；入口清单以根目录 `skills.registry.json` 为单一事实源，由 `npm run sync:skills` 生成并对账（CI 以 `--check` 校验）。

| 平台        | 安装入口                                                                                 | 安装后操作                              | 卸载方式                                      |
| ----------- | ---------------------------------------------------------------------------------------- | --------------------------------------- | --------------------------------------------- |
| Codex       | 将 GitHub 仓库链接发给 Codex，并说明安装                                                 | 新建对话，从`/` 菜单选择入口             | 在 Codex 的插件管理中移除 resume-skills       |
| Claude Code | 执行`/plugin marketplace add Wjdz-03/resume-skills` 和 `/plugin install resume-skills@asu` | 按提示执行`/reload-plugins`              | 执行`/plugin uninstall resume-skills`         |
| DeepSeek Harness Desktop | 在插件面板选择“添加插件”，粘贴 `https://github.com/Wjdz-03/resume-skills.git` 并安装 | 在插件面板启用 resume-skills，新建会话后从`/` 菜单选择入口 | 在插件面板卸载 resume-skills                  |
| Cursor      | [查看 Skill bridge 安装说明](.cursor-skills/install.md)                                    | 新建 Agent 对话，输入 `/` 或 `/great-resume` 等 | 删除项目 `.cursor/skills/` 或用户 `~/.cursor/skills/` 下对应目录 |
| TraeWork    | 复制仓库到`~/.trae-cn/plugins/<publisher>/resume-skills/<version>/`                     | 重启 TraeWork，从`/` 菜单选择入口        | 删除对应的 TraeWork 插件目录                  |
| OpenCode    | [查看安装指南](.opencode-plugin/installation-guide.md)                                    | 重启 OpenCode 或执行`/reload-plugins`    | 按安装方式删除对应的技能与资源目录            |
| WorkBuddy   | [查看桥接安装说明](.workbuddy-plugin/install.md)                                          | 重启 WorkBuddy 或刷新技能列表            | 删除`~/.workbuddy/skills/`下对应目录或软链    |
| Qoder       | [查看安装说明](.qoder-plugin/install.md)                                                  | 重启 Qoder 或新建对话，从`/` 菜单选择入口 | 按安装方式执行`qodercli plugin uninstall`或删除插件目录 |

开发者请参阅 [贡献指南](.github/CONTRIBUTING.md)，其中包含本地校验、测试命令和 PR 提交流程。

## 第一次使用：从哪个入口开始

先根据当前最需要解决的问题选择第一个入口：

| 当前情况                                       | 建议先使用                   |
| ---------------------------------------------- | ---------------------------- |
| 已有经历，但不知道如何匹配目标岗位             | `/great-resume`            |
| 简历内容已确定，需要制作常规可编辑简历         | `/make-resume`             |
| 想复刻 ASu 同款高密度技术简历                  | `/make-resume`（默认模板） |
| 已有 JD 和简历，需要判断匹配与证据缺口         | `/job-match`               |
| 已有职位链接，需要填写招聘网站申请表           | `/job-apply`               |

也可以组合多个入口：

- **已有项目、准备开始投递**：先用 `/great-resume` 对齐目标岗位、整理经历表述，再用 `/make-resume` 生成简历；默认使用 ASu 模板，也可以指定其他模板；
- **已有简历和具体 JD、需要决定是否投递**：先用 `/job-match` 区分已匹配、表达缺口和真实缺口，需要改写时再交给 `/great-resume`；
- **准备填写招聘网站申请表**：先用 `/job-apply` 连接已登录的浏览器，填写并核对一个具体职位，简历需要更新时再回到 `/great-resume` 和 `/make-resume`。

## `/great-resume`：简历提升

适合以下任务：

- 根据目标岗位重新定位个人经历；
- 把页面、接口、数据绑定等底层工作翻译成招聘语言；
- 改写项目要点、简历摘要和个人介绍；
- 生成 Boss 直聘或微信发给 HR 的中文开场白；
- 整理面试追问、证据补强清单和事实边界。

建议提供目标岗位、岗位描述、现有简历、项目说明、真实职责和成果数据。信息不足时，skill 会先给出可用初稿，并标记 `【待补】`，不会自行编造 title、公司、技术栈或数据。

典型用法：

```text
/great-resume

目标岗位：AI 应用工程师
请根据我下面的实习和项目经历，给出稳妥版和进取版定位，改写简历要点，并生成一段发给 HR 的开场白。
```

### HR 开场示例

<img src="assets/hr-intro-example.jpg" width="360" alt="HR 开场示例">

## `/make-resume`：制作简历

`/make-resume` 专门负责全部简历文件交付。未指定模板时默认使用 ASu 单栏高密度技术简历模板；用户可以指定仓库内其他模板、本地 HTML 或上传参考截图。它最终生成真正可编辑的 HTML，而不是把截图嵌入页面。

支持：

- 18 个中文 HTML 模板；
- A4 单页或双页排版；
- 浏览器内编辑文字、照片、字体、颜色和加粗；
- 将当前编辑内容保存为本地 HTML；
- 「本地字体」读取系统中已安装的字体（Chrome 103+，需浏览器授权），「导入字体」加载本地字体文件（TTF/OTF/WOFF/WOFF2）作为补充；
- 打印导出 PDF；
- 可选导出 LaTeX `.tex` 源文件，提供默认 ASu、紧凑单栏、学术风三套版式，用于在 Overleaf 等环境继续编辑（需用户主动要求）；
- 根据截图分析栏位、间距、字号、颜色和分页结构；
- 使用虚构示例照片作为占位，生成真实简历时由用户主动替换。

默认 ASu 模板以只读文件 `assets/asu-resume-template.html` 为母版，生成简历时只复制到用户副本，不修改模板源文件。“我想要阿酥同款简历”也统一由 `/make-resume` 处理；如果用户指定其他模板，则以用户指定内容为准。

典型用法：

```text
/make-resume

请根据我提供的教育、实习和项目经历，选择一份适合后端开发岗位的模板，生成可编辑 HTML 简历，并告诉我如何导出 PDF。
```

### 模板预览

![简历模板预览](assets/template-overview.jpg)

### LaTeX 输出预览

用户明确要求提供 LaTeX 或适用于 Overleaf 的简历版本时，可在 HTML 之外附加导出 `.tex` 源文件，在 Overleaf 中编译即可继续调整排版。目前提供三套版式：默认 ASu、紧凑单栏（适合经历较多）和学术风（黑白打印友好）。三套都无需上传额外宏包或配置字体。

推荐用 [Overleaf](https://www.overleaf.com/) 编译，无需在本地安装 TeX 环境，三步完成：

1. New Project → Blank Project，填写 Project name → Create；
2. 上传生成的 .tex 文件；若简历使用证件照，把图片一并上传到同一项目（与 .tex 同级，文件名保持一致）；
3. 左上角 File → Settings：Main document 选择上传的文件，Compiler 选 XeLaTeX，然后 Recompile。

下图为一份示例数据在三套版式下的编译结果。

![LaTeX 简历预览](assets/latex-resume-overview.png)

## `/job-match`：岗位匹配分析

`/job-match` 把目标 JD 拆成硬性条件、核心能力和加分项，再与用户已经确认的简历、经历或主张—证据账本逐项对照。它区分“已经匹配”“做过但没写清”“证据不足”“真实缺口”和“待确认”，不会用关键词重合伪造一个精确匹配分数。

默认交付包括要求—证据矩阵、硬性门槛、最多 5 个优先补强项，以及“建议投递 / 补充材料后投递 / 谨慎投递 / 暂不建议投递”的可解释结论。分析本身不会修改简历、填写网页或提交申请。

典型用法：

```text
/job-match

请对照这份 JD 和我的简历，列出每项要求的真实证据、表达缺口和能力缺口，并告诉我是否值得投递。先不要改简历。
```

## `/job-apply`：简历投递填写

**重要提醒：本项目禁止滥用技能批量投递、骚扰 HR，或发送千篇一律、夸大包装的开场白。请只基于真实经历，针对具体岗位进行适度、个性化沟通；堆砌 GitHub Star、过度包装经历并直接发送的文案，容易引起 HR 反感，也可能损害求职者和项目的信誉。`/job-apply` 只用于用户明确确认的单个职位申请，技能不会绕过确认、批量提交，也不会代替用户发送未经审核的消息。**

<div align="center">
  <img src="assets/hr-opening-warning.jpg" alt="HR 反感模板化求职开场白示例" width="420">
  <p><em>反面示例：模板化、夸大式开场白容易引起反感，请勿照搬。</em></p>
</div>

`/job-apply` 用已确认的简历资料填写一个具体招聘网站的申请表，支持页面读取、字段映射、文本填写、下拉选择、简历/作品附件上传和提交前核对。默认停在最终提交按钮前，不会因为“帮我填简历”就替用户投递。

<img src="assets/job-apply-form-example.png" alt="校招申请表填写示例" width="900" />

### 使用 Kimi WebBridge 连接浏览器

**使用前请先安装并启用浏览器控制扩展，并确认扩展已连接对应的浏览器控制服务。** 未完成扩展安装和连接检查前，ASu 不会读取或填写招聘页面。

如果希望操作自己已经登录的 Chrome 或 Edge，可以安装并启用官方 [Kimi WebBridge](https://www.kimi.com/products/kimi-webbridge)。它通过浏览器扩展、本机 daemon 和 Chrome DevTools Protocol 连接浏览器，登录会话和页面内容保留在本机。

如果使用 ChatGPT/Codex 的浏览器控制能力，也可以安装并启用 [ChatGPT 浏览器扩展（Microsoft Edge Add-ons）](https://microsoftedge.microsoft.com/addons/detail/chatgpt/odlomjlbamekndcpllcnffbgeohgkmjh)（Chrome 扩展商店已下架，目前使用 Edge 扩展商店），再按照宿主应用中的浏览器控制页面完成连接。两种方式任选其一即可，不需要同时安装。

### 典型用法

```text
/job-apply

请使用我确认的简历，打开这个职位申请页面，填写可确认的字段和简历附件；遇到缺失信息先问我，最后停在提交前让我核对。
```

登录、密码、短信验证码、邮箱验证码、MFA、通行密钥和 CAPTCHA 必须由用户完成。涉及个人资料输入、文件上传和最终提交时，ASu 会分别确认；不会读取 Cookie、令牌或密码，也不会绕过反爬和访问控制。

## 四个入口如何配合

推荐按照下面的顺序使用：

1. 用 `/great-resume` 根据已有经历明确目标岗位，整理简历表述和 HR 话术；
2. 用 `/make-resume` 把确认后的文字放入可编辑简历并导出 PDF；
3. 用 `/job-match` 对照具体 JD 判断证据匹配、硬性门槛和投递优先级；
4. 用 `/job-apply` 连接浏览器填写具体职位申请，并在提交前核对。

也可以在同一条需求里说明组合目标，例如：“先用 `/great-resume` 提升经历，再用 `/make-resume` 生成 HTML 简历，最后用 `/job-match` 对照 JD 检查证据缺口”。

组合使用多个入口、材料存在冲突或简历包含强主张时，可以复制 [`assets/career-claim-ledger-template.json`](assets/career-claim-ledger-template.json) 建立主张—证据账本。它让经历提升和简历文件共享同一份事实、确认状态与个人边界；详细规则见 [`skills/great-resume/references/claim-evidence-ledger.md`](skills/great-resume/references/claim-evidence-ledger.md)。

## 事实边界

ASu-skills 的“简历提升”是强定位、强证据和清晰表达，不是伪造经历。使用时请遵守：

- 保留真实职位、公司、时间和教育背景；
- 区分团队成果和个人贡献；
- 只有有证据时才使用“主导”“负责人”“Owner”等强表述；
- 没有可靠数据时使用可核验的定性结果；
- 不把计划做的事情写成已经完成；
- 不把 AI 生成的代码成果冒领为未经验证的个人能力；
- 不在公开 skill 文件中写入真实姓名、电话、邮箱、密码、验证码或招聘隐私。

## 文件结构

```text
resume-skills/
├── .claude-plugin/
│   ├── plugin.json              # Claude Code 插件清单
│   └── marketplace.json         # Claude Code 插件市场清单
├── .codex-plugin/
│   └── plugin.json              # Codex 插件清单
├── .trae-plugin/
│   └── plugin.json              # TraeWork 插件清单
├── .opencode-plugin/
│   ├── plugin.json              # OpenCode 插件清单（skills.entries 由 registry 生成）
│   ├── install-opencode.py      # OpenCode 安装脚本（技能名单由 registry 生成）
│   └── installation-guide.md    # OpenCode 手动安装指南
├── .workbuddy-plugin/
│   ├── install.md               # WorkBuddy 桥接说明（清单区由 registry 生成）
│   ├── install.sh               # macOS / Linux 桥接脚本
│   └── install.ps1              # Windows 桥接脚本
├── .qoder-plugin/
│   ├── install.md               # Qoder 安装说明（CLI / Agent 两种安装方式）
│   └── plugin.json              # Qoder 插件清单（interface 等附加元数据）
├── skills.registry.json        # ★ 入口目录单一事实源：新增/删除入口先改这里，再 npm run sync:skills
├── package.json                # DSH 插件包清单（bundle patch 入口）
├── cordis.patch.yml            # 注册 DSH filesystem skill 提供方
├── lib/
│   └── index.js                # DSH 插件入口模块
├── skills/                     # 全部入口目录（与 skills.registry.json 一一对应）
│   ├── great-resume/           # /great-resume 简历提升
│   ├── job-apply/              # /job-apply 简历投递填写（依赖浏览器桥接）
│   ├── job-match/              # /job-match 岗位匹配分析
│   └── make-resume/            # /make-resume 简历制作
├── scripts/
│   ├── sync-skill-catalog.mjs  # ★ 从 registry 生成/对账各入口清单（npm run sync:skills）
│   ├── build-asu-resume.mjs    # ASu 简历模板构建（内联共享样式与编辑器）
│   ├── inline-template.mjs     # 其余模板壳构建
│   ├── build-latex-resume.mjs  # LaTeX 简历源文件生成
│   ├── export-resume-pdf.mjs   # 简历 PDF 导出
│   └── kimi-webbridge.mjs      # Kimi WebBridge 本机 HTTP 客户端
├── assets/                     # 模板、图片和示例资源
│   ├── asu-resume-template.html # ASu 同款可编辑简历起点
│   ├── icons/                   # 个人信息与通用信息 SVG 图标
│   └── logos/                   # LobeHub Icons 静态 SVG Logo
├── references/                  # 招聘邮箱整理参考
├── .github/
│   ├── CONTRIBUTING.md          # 贡献指南
│   ├── CONTRIBUTING_en.md       # English contribution guide
│   └── PULL_REQUEST_TEMPLATE.md # PR 模板
└── README.md
```

## 参与贡献

欢迎提 Issue 和 PR，详见[贡献指南](.github/CONTRIBUTING.md)。也可以直接查看 [Pull Requests](https://github.com/Wjdz-03/resume-skills/pulls)。

新增、删除或重命名入口时，先更新 [`skills.registry.json`](skills.registry.json)，再运行 `npm run sync:skills` 同步全部插件清单、安装脚本、Issue 模板与 README 总览；可用 `npm run sync:skills -- --check` 校验一致性。

## 特别感谢

原项目（ASu-skills）特别感谢 [L7WD3-Xiao](https://github.com/L7WD3-Xiao) 的维护与支持。

## 致谢

感谢以下小红书博主的公开分享与启发：

- [**阿酥在coding**](https://xhslink.cn/m/2LHuLJZ30b2)：关于 Coding 面试经验的分享；
- [**Hi Mr Lonely**](https://xhslink.cn/m/3kVQDyUJ6of)：关于简历包装与求职表达的分享。

本插件对相关内容进行了整理、结构化和合规化改写，用于形成可复用的求职工作流。

感谢 [LobeHub/lobe-icons](https://github.com/lobehub/lobe-icons) 提供开源品牌图标资源；本插件按其技能说明优先使用 `@lobehub/icons` 及静态 SVG/CDN 资源。

感谢 [Kimi WebBridge](https://www.kimi.com/products/kimi-webbridge) 提供本机浏览器连接能力，让 `/job-apply` 可以通过 Chrome DevTools Protocol 操作用户已登录的浏览器，登录会话与页面内容始终保留在本机。

## Contributors

感谢所有为 resume-skills 做出贡献的人。

<a href="https://github.com/Wjdz-03/resume-skills/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Wjdz-03/resume-skills" alt="Contributors" />
</a>

## 开源协议

本项目基于 [MIT License](LICENSE) 发布，可自由使用、修改与分发，欢迎 fork 与 PR。开源治理体系由社区 Owner 主导建设，已实现全链路 License 覆盖率 100%。

## Star History

<a href="https://www.star-history.com/?repos=Wjdz-03%2Fresume-skills&type=timeline&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=Wjdz-03/resume-skills&type=timeline&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=Wjdz-03/resume-skills&type=timeline&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=Wjdz-03/resume-skills&type=timeline&legend=top-left" />
 </picture>
</a>
