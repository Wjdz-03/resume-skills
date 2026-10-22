# OpenCode 安装指南

## 方法 1：自动安装（推荐）

```bash
# 克隆仓库
git clone https://github.com/Wjdz-03/resume-skills.git
cd ASu-skills

# 运行安装脚本
python .opencode-plugin/install-opencode.py
```

如果 OpenCode 使用自定义 skills 目录，或自动查找失败，可以显式指定安装位置：

```bash
# Windows
python .opencode-plugin/install-opencode.py --target "D:\OpenCode\skills"

# macOS / Linux
python .opencode-plugin/install-opencode.py --target /custom/opencode/skills
```

`--target` 优先于自动查找；指定目录不存在时，安装脚本会自动创建。路径中包含空格时请使用引号。

安装脚本除复制 `skills/` 外，还会把共享 `assets/` 与 `references/` 安装到 skills 目录的上一级，分别保存为 `assets/asu/` 与 `references/asu/`。这样 `/make-resume` 等入口能在 OpenCode 中继续定位模板与参考资料。

## 方法 2：手动安装

先 clone 并进入仓库：

```text
git clone https://github.com/Wjdz-03/resume-skills.git
cd ASu-skills
```

根据终端选择对应的复制命令。

**Windows（CMD / 命令提示符）：**

```bat
xcopy /E /I "skills\*" "%USERPROFILE%\.config\opencode\skills"
xcopy /E /I "assets\*" "%USERPROFILE%\.config\opencode\assets\asu"
xcopy /E /I "references\*" "%USERPROFILE%\.config\opencode\references\asu"
```

`/I` 会将不存在的目标视为目录并创建；路径引号用于兼容包含空格的用户名。

**macOS / Linux（Bash / Zsh）：**

```bash
mkdir -p "$HOME/.config/opencode/skills" "$HOME/.config/opencode/assets/asu" "$HOME/.config/opencode/references/asu"
cp -r skills/* "$HOME/.config/opencode/skills/"
cp -r assets/* "$HOME/.config/opencode/assets/asu/"
cp -r references/* "$HOME/.config/opencode/references/asu/"
```

复制完成后重启 OpenCode。

## 方法 3：通过 OpenCode 插件管理器（如果支持）

```bash
# 在 OpenCode 中执行
/plugin install Wjdz-03/resume-skills
```

## 使用方式

安装后，可通过以下方式触发：

| 用户意图 | 触发词 |
|---------|--------|
| 简历提升 | /great-resume、我要酥化、改写经历 |
| 简历制作 | /make-resume、做简历、同款简历、指定模板 |
| 岗位匹配 | /job-match、JD 匹配、简历差距、是否值得投递 |
| 简历投递填写 | /job-apply、自动填写招聘网站申请表 |

## 注意事项

- [OpenCode 默认全局技能目录](https://opencode.ai/docs/skills/#place-files)为 `~/.config/opencode/skills/`；Windows CMD 中使用 `%USERPROFILE%\.config\opencode\skills`。如已配置自定义目录，请替换示例中的目标路径。
- 安装后需重启 OpenCode 或执行 `/reload-plugins`
- 每个 skill 需要在 OpenCode 中配置触发词才能通过 `/` 菜单调用
