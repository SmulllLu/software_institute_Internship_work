# 2026年2月 第1周

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

