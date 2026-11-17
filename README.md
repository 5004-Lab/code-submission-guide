# 5004-Lab 代码上传规范

本规范适用于向 5004-Lab 下的项目仓库提交代码。提交前先确认目标仓库和目标分支，并遵守项目仓库 README 中的具体约定。

## 提交哪些文件

- 提交本次改动需要的源代码、测试、依赖清单和示例配置。新增或修改项目时，在项目 README 中同步说明环境、安装方式和运行命令。
- 用 `.gitignore` 排除虚拟环境、依赖安装目录、缓存、日志、本地 IDE 配置和可重新生成的构建产物。提交前用 `git status` 和 `git diff --cached` 检查暂存内容。
- 密码、访问令牌、私钥、真实的 `.env` 文件及受限数据禁止提交。示例配置使用占位值。如果凭据误入提交，应立即吊销或轮换，并联系仓库维护者处理 Git 历史。
- 大型数据集、模型权重和二进制文件优先存放在项目约定的位置。确需纳入版本管理时，先与维护者确认是否使用 Git LFS。

## 分支、提交和评审

1. 从最新的默认分支创建工作分支。分支名写明用途，例如 `feat/data-loader` 或 `fix/startup-error`。
2. 每个提交聚焦一项改动，提交信息说明改了什么，例如 `fix: 修复设备初始化超时`。推送前运行受影响的测试，或至少验证相关功能能正常运行。
3. 将工作分支推送到 GitHub，再向目标分支发起 Pull Request（PR）。在 PR 中写清改动目的、主要变更和验证方法及结果。涉及配置变更或使用方式变化时一并说明。
4. 等相关检查通过、评审意见处理完毕后再合并。请勿直接向默认分支推送，也不要强制推送共享分支。

## 命令示例

以下以默认分支为 `main`、修改文件为 `src/data_loader.py` 的项目为例。在本地工作区没有未提交改动时开始操作。

```bash
git switch main
git pull --ff-only origin main
git switch -c feat/data-loader

# 完成修改并运行相关测试后
git add src/data_loader.py
git diff --cached
git commit -m "feat: 添加数据加载功能"
git push -u origin feat/data-loader
```

推送后，在 GitHub 上从 `feat/data-loader` 向 `main` 发起 PR。
