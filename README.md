# Engineering Workflow Skill

一个面向 Codex 的中文工程化 skill：从用户明确提供的工程规则中提炼需求澄清、复杂度判定、计划审查、测试先行和分步 Git 交付流程。

修改至少三个文件、引入新依赖或跨模块重构时，先输出可审阅的计划，等待用户回复“同意”后实施。普通小变更按项目规则和实际风险验证，不额外套用复杂项目审批。

## 安装

将仓库克隆到 Codex 的用户级 skills 目录。若目标目录已存在，先检查其中内容，避免覆盖。

PowerShell：

```powershell
$skillsDirectory = Join-Path $env:USERPROFILE '.agents\skills'
New-Item -ItemType Directory -Force -Path $skillsDirectory | Out-Null
git clone https://github.com/320MUYU/engineering-workflow-skill.git (Join-Path $skillsDirectory 'engineering-workflow-skill')
```

macOS / Linux：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/320MUYU/engineering-workflow-skill.git ~/.agents/skills/engineering-workflow-skill
```

仓库根目录就是 skill 目录，不需要额外移动子文件夹。Codex 支持自动发现 skill；如果安装后未显示，重启 Codex 后再检查。
位置和格式遵循 [Codex 官方 skills 文档](https://developers.openai.com/codex/skills/)。

## 使用

显式调用：

```text
使用 $engineering-workflow-skill 为这个项目添加输入校验。
先读取项目规则，澄清需求并判断复杂度，再按工作流推进。
```

也允许根据任务自动选择。技能适用于功能开发、缺陷修复和重构等工程变更，不用于纯知识问答或非工程内容创作。

已有的计划批准和上传授权持续有效，不反复确认同一事项。需要改变批准计划时重新审查；未经用户明确授权，不推送或发布。
本 skill 不扩大工具权限，也不自动替用户选择仓库或公开属性。

## 内容

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | 触发范围、核心规则及按需阅读入口 |
| [agents/openai.yaml](agents/openai.yaml) | 中文界面信息、调用示例与自动发现策略 |
| [references/engineering-workflow.md](references/engineering-workflow.md) | 计划、Git、测试、重试和发布的详细处理 |
| [tests/scenarios.md](tests/scenarios.md) | 14 条可观察验收场景及审阅方法 |

这是指令型 skill，无执行脚本或新增运行依赖。详细流程仅在需要时读取，避免每次加载全部说明。

## 验证与维护

先建立验收场景，再修改指令。维护时应：

1. 使用 skill-creator 自带的 `scripts/quick_validate.py` 检查本目录中的 skill 格式；使用 UTF-8 读取中文文件。
2. 检查界面 YAML、默认调用名称、相对链接和实际发布文件。
3. 按验收场景审阅审批、授权、Git、验证与重试的决策边界。
4. 若需要实际行为评测，在获准的临时项目中记录代理动作和证据；不得把静态审阅描述为已完成独立代理实测。

原始记忆、聊天记录、私人路径、凭据和调试日志不属于发布内容。`.gitignore` 仅帮助排除常见临时文件，不能代替发布前的内容与提交历史审阅。

工程规则的来源是用户明确提供的工作流要求；本仓库不分发原始长期记忆，也不将缺失的历史记录补写为经验。
