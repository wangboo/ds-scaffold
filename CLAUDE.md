# {{PROJECT_NAME}}

Data Sentinel 本地数据治理项目。

## 项目结构

- `metadata/` — 从 Data Sentinel 平台拉取的元数据（只读缓存）
  - `<project-name>/` — 每个关联项目的元数据
    - `project.json` — 项目基本信息
    - `tables/<tag0>/<tag1>/<name>.sql` — 表 DDL，按类目归类
    - `rules/<tag0>/<tag1>/<name>.csv` — 质控规则，按类目归类
    - `sqls/<tag0>/<tag1>/<name>.csv` — 质控 SQL，按类目归类
- `sql_exec/` — 质控批次得分明细（score-<batch-id>.csv）
- `skills/` — Data Sentinel 官方 skills，供 Claude Code 使用

## 配置

- `.ds-cli.yml` — 项目配置（平台连接、关联项目）
- `~/.ds-cli/credentials.yml` — 个人凭证（不提交到 git）

## 常用命令

- `ds pull` — 从平台拉取最新元数据
- `ds status` — 查看本地和平台的差异

## 数据治理工作流

1. `ds pull` 拉取平台项目的最新表结构、质控规则和 SQL
2. 在 Claude Code 中审查和分析元数据，使用 skills/ 中的 skills 辅助工作
3. 通过平台 Web 界面提交规则变更和新增
4. 在平台上触发质控批次执行，执行完成后 `ds pull` 拉取得分结果

## Skills

本项目 skills 已安装在 `skills/` 目录下。在 Claude Code 中可直接使用这些 AI 辅助技能。

## 平台关联

连接到 {{PLATFORM_URL}}，关联项目见 `.ds-cli.yml` 的 `projects` 列表。
