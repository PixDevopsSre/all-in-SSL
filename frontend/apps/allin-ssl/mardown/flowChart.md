流程/工作流图拆封设计

- 基础节点
	- 初始化节点(不支持上传) 
	- 并行节点
	- 执行结果节点（删除整个条件判断）

- 任务节点
	- 申请节点（支持执行结果判断）
	- 上传节点（不支持执行结果判断）
	- 部署节点（支持执行结果判断）
	- 通知节点（支持执行结果判断）

- 节点操作
	- 重命名
	- 删除

- 节点下一步配置
	- 申请
	- 上传
	- 部署
	- 通知
	- 执行结果判断（上传节点不支持）
	- 并行

- 节点辅助功能
	- 拖拽
	- 放大、缩小、还原

- 节点验证
	- 验证任务节点

结构规划
- 状态存储（包含节点默认配置数据）
- 基础节点
- 任务节点（可以根据外部的机构自由的构建任务节点，主要有节点条件，节点操作方法）
- 节点渲染器
- 工具方法
- 入口文件




工作流图组件
├─ 状态存储
│   └─ 节点默认配置数据
├─ 基础节点
│   ├─ 初始化节点
│   ├─ 并行节点
│   └─ 执行结果节点
├─ 任务节点
│   ├─ 申请节点
│   ├─ 上传节点
│   ├─ 部署节点
│   └─ 通知节点
├─ 节点渲染器
│   └─ 渲染节点到界面
├─ 工具方法
│   ├─ 创建节点
│   ├─ 重命名节点
│   ├─ 删除节点
│   ├─ 配置节点下一步
│   ├─ 视图缩放
│   └─ 流程验证
└─ 入口文件
    └─ 初始化工作流图组件




