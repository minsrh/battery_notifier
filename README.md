# 🔋 Battery Notifier for Magisk

一个适用于 Android Magisk 的电池电量通知脚本，可通过 Telegram Bot 在不同电量状态下发送提醒，支持充电进度通知、息屏判断、防止重复通知等实用功能。

---

## ✨ 功能亮点

- 📲 电量达到指定百分比自动发送通知（支持低电量/高电量）
- 🔕 避免重复通知，也会补发通知（同一个电量不会重复提醒）
- 💤 支持仅在息屏时通知（可配置是否亮屏也通知）
- 🤖 通过 Telegram Bot 实现远程推送
- 🔧 所有参数均可在配置文件中修改

---

## 📂 使用方式

### 1. 准备环境

- 需要有 **root 权限** 或 **Magisk 环境**
- 已安装并配置好 `curl` 命令（大多数 Android 已内置）

### 2. 设置配置文件

创建配置文件路径：

```bash
/sdcard/Android/conf/battery.txt
```

示例内容如下：

```properties
# Telegram Bot 的 API Token
TG_BOT_TOKEN=123456:ABC-EXAMPLE

# Telegram 聊天 ID
TG_CHAT_ID=987654321

# 设备名称（用于通知显示）
DEVICE_NAME=我的手机

# 低电量提醒阈值（多个值用逗号隔开）
TARGET_LEVELS_LOW=50,25,10

# 高电量提醒阈值
TARGET_LEVELS_HIGH=90,80,70,60

# 是否启用对应功能
ENABLE_FULL_NOTIFY=true
ENABLE_CHARGE_NOTIFY=true
ENABLE_LOW_NOTIFY=true

# 是否亮屏时也发送通知（true/false）
NOTIFY_WHEN_SCREEN_ON=false
```

### 3. 安装脚本

将主脚本 `battery_notifier.sh` 放入合适目录，如：

```bash
/data/adb/service.d/battery_notifier.sh
```

确保赋予执行权限：

```bash
chmod +x /data/adb/service.d/battery_notifier.sh
```

脚本将会每次开机后自动运行，也可手动触发运行测试。

---

## 🧪 通知示例

- 电量达到 90%，发送：

  > 💬 设备：我的手机  
  > 当前电量已充至 90%  
  > 正在充电  
  > 时间：2025-05-24 20:00  
  > 别忘了，插着充电器的手机最幸福！🔌😊

- 电量下降至 25%，发送：

  > 当前电量 25%，快点找充电器吧，不然我可要罢工了！🔋😅

- 充电保护触发时：

  > 电量已达 85%，已为您开启过充保护 🔌

---
