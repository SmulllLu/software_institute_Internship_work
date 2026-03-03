# 2026年2月

## 系统架构修改

### 提交： [实现了系统的配置系统的重构](https://github.com/ruyisdk/ruyi-packaging/commit/b43ce1c9cb6d9b38a29b3dac26e12331dc98f189)
  - 修复数据库初始化问题，实现表自动创建机制
  - 完善配置模板文件，补充所有缺失的配置项和环境变量
  - 保持向后兼容性，支持旧配置文件格式


### 提交： [建立 core/services/interfaces 三层架构体系](https://github.com/ruyisdk/ruyi-packaging/commit/40c829998b12688dde880e242fc9d211251d83a3)
  - 架构分层：建立核心层、服务层、接口层三层架构，从rikoriko.py、api.py 提取业务模型到 core/，将接口层 (CLI/API)与业务逻辑解耦 
  - 服务层抽取：将 CLI 命令的业务逻辑抽取为 4 个独立服务类（CheckService、ManifestService、PRService、SchedulerService），CLI 和 API共享服务层方法，避免代码重复
  - 接口层重构：CLI 移至 interfaces/cli/ 仅保留参数解析；API 拆分为 4 个路由模块，提取 Pydantic 模型到独立文件，统一使用相对导入规范化依赖关系

## Telegram Bot

### 提交：[实现TelegramBot定时发送上游更新目录](https://github.com/ruyisdk/ruyi-packaging/commit/b42e36d244dc4a34f1bbe93f0975a31e76827c7a)
  - Telegram Bot 服务新增：创建 telegramBot_service.py 实现完整的 Bot 服务层，支持消息发送
  - CLI 命令扩展：在 riko 主程序中新增 telegram-bot 子命令，将Telegram Bot 启动功能集成到 CLI 工具链，用户可通过 python3 -m riko telegram-bot 直接启动机器人

## 功能修改

### 提交：[实现自动对比上游版型与packages-index仓库版型对比并更新](https://github.com/ruyisdk/ruyi-packaging/commit/34ff64365461e0d8cb7bbf14fe395f640225985c)
  - 完成对上游版型号的整体对比，筛选出新增与删除的型号文件。通过调用manifests的版型下载和pr功能中的生成pr来协助完成version_sync功能的实现


### 提交: [修改manifests中获取size与哈希值逻辑](https://github.com/ruyisdk/ruyi-packaging/commit/72c4815e2c92d199f7c1b7cd27b40caa0eb33082)
  - 修改了manifests_r9函数的功能，在下载完成之后计算size与哈希值之后立即删除该文件，防止过多占用磁盘空间，而导致功能无法正常实施

### 提交: [将version-sync进行CLi命令扩展以及api扩展](https://github.com/ruyisdk/ruyi-packaging/commit/6d84a25de355f712f2c34c578311af8cef9d633a)
  - CLI 命令扩展：在 riko 主程序中新增 versions-sync 子命令，将 versions-sync 启动功能集成到 CLI 工具链，用户可通过 python3 -m riko  versions-sync 直接调用该功能
  - 创建 versions-sync 接口，在服务端可以直接调用接口来使用该功能
