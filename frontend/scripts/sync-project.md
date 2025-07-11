# 项目同步工具文档

## 功能名称
**跨平台 Turborepo 工作区编译部署自动化工具**

## 功能简述
这是一款基于纯 Shell 脚本开发的自动化工具，借助交互式命令行界面，能够对 Turborepo 项目的应用工作区进行扫描。它支持选定工作区的编译操作，还能把编译结果同步到指定的 Git 仓库，并且可以选择性地同步过滤后的项目结构。该工具最大的特点是实现了跨平台兼容，可在 Windows、macOS 和 Linux 系统上稳定运行。

## 技术规格
- **实现语言**：严格遵循 POSIX 标准的 Shell 脚本
- **跨平台方案**：
  - 在 Windows 系统中，依赖 Git Bash/MSYS2 环境运行
  - 在 macOS/Linux 系统上，直接使用原生 bash/zsh 环境
- **核心依赖工具**：
  - 需要预先安装 pnpm 包管理工具
  - 必须安装 git 版本控制工具
  - 要具备标准 Unix 工具集，像 find、grep、sed 等
  - 可选安装 yq 工具用于 YAML 配置管理

## 目录结构
所有配置和生成的文件统一放在项目根目录的 `.sync` 目录中：

- **.sync/**：工具根目录
  - `sync-config.yaml`：工作区同步配置文件
  - `history`：操作历史记录
  - `git-repos/`：Git 仓库同步目录，用于存储同步的 Git 仓库内容
  - `plugins/`：插件目录

## 配置文件格式
```yaml
# 工具配置
config:
  parallel_build: false  # 是否并行编译
  dry_run: false  # 是否干运行

# 工作区配置
workspaces:
  # 证书管理项目同步配置
  allin-ssl:
    sync_mappings: 
      - git:
          url: "http://git.bt.cn/wzz/allinssl.git"
          branch: "1.0.1"
          alias: "allinssl-gitlab"
          sync: ["/dist", "/build"]  # 要同步的目录，只支持两个字段
          source: true  # 是否同步源码
      - git:
          url: "https://github.com/allinssl/allinssl.git"
          branch: "1.0.1"
          alias: "allinssl-github"
          sync: ["/dist", "/build"]  # 要同步的目录，只支持两个字段
          source: true  # 是否同步源码
```

## 交互方式
- **菜单驱动界面**：
  - 运用上下方向键来进行选项导航
  - 通过回车键完成确认操作
  - 使用数字键1/0进行选择/取消选择
- **多步骤流程引导**：每个操作步骤都配有明确的提示信息和状态反馈
- **彩色日志输出**：对不同类型的信息，如错误、警告、成功等，使用不同颜色进行区分显示
- **步骤可视化**：直观显示当前操作进度和已完成步骤

## 优化流程
1. **初始化**：检查环境和项目结构（只执行一次）
2. **编译阶段**：先编译当前工作区的代码
3. **Git准备阶段**：检查Git目录，必要时拉取最新代码
4. **同步阶段**：将编译后的代码复制到Git目录（支持多目录同步）
5. **提交阶段**：提交并推送更改到远程仓库

## 使用方法
```bash
./sync-project.sh [选项]
```

选项:
- `--parallel, -p` - 启用并行编译
- `--dry-run, -d` - 干运行模式，不执行实际操作
- `--help, -h` - 显示帮助信息

## 兼容保证
- **路径处理**：自动处理不同操作系统的路径分隔符差异
- **命令适配**：针对不同系统提供兼容的命令实现
- **错误处理**：提供统一的错误处理和日志记录机制

## 性能优化
- 避免重复运行相同的检测逻辑
- 缓存配置文件加载结果
- 仅在必要时检查依赖工具
- 并行执行支持用于多工作区同步

## 维护与更新
- 定期检查和更新依赖工具
- 添加新功能时遵循模块化设计
- 保持脚本的跨平台兼容性
- 更新文档以反映新增功能和变更