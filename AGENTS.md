# AGENTS.md

## 项目红线

**以下模块严禁修改：**

| 模块 | 路径 | 说明 |
|------|------|------|
| 播放器 | `lib/player/` | 播放器内核、渲染、控制 |
| 平台解析 | `lib/core/site/` | 各平台直播解析逻辑 |
| 弹幕协议 | `lib/core/danmaku/` | 弹幕协议解析 |
| IPTV 解析 | `lib/core/iptv/` | IPTV 播放列表解析 |
| 网络层 | `lib/core/network/` | HTTP 客户端、代理 |
| 数据模型 | `lib/core/models/` | 核心数据模型 |
| 录制逻辑 | `lib/domains/recorder/` | 录制核心逻辑 |

**只允许修改 UI 相关：**

| 模块 | 路径 | 说明 |
|------|------|------|
| 新 UI 架构 | `lib/src/` | 新 UI 开发（唯一改动区域） |
| 旧 UI | `lib/features/` | 不动（上游代码） |
| 业务逻辑 | `lib/domains/` | 不动（上游代码） |
| 核心层 | `lib/core/` | 不动（上游代码） |
| 启动入口 | `lib/main.dart` | 唯一改动点（新旧 UI 选择器） |

---

## 架构原则

1. **播放器共享**：新旧 UI 共用 `lib/player/`
2. **解析不变**：所有平台解析逻辑完全复用上游
3. **UI 独立**：新 UI 在 `lib/src/` 下独立开发
4. **上游合并**：只改 `main.dart`，其他文件零改动

---

## 上游合并流程

```bash
# 1. 拉取上游
git fetch upstream

# 2. 合并（只处理 main.dart 冲突）
git merge upstream/master

# 3. 解决 main.dart 冲突
# 4. 提交
git add main.dart
git commit -m "merge: 上游更新"
```

---

## 开发规范

- 新 UI 代码放在 `lib/src/`
- 引用上游代码用 `import 'package:pure_live/core/...'`
- 不复制上游代码
- 不修改上游文件路径
