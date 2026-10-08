# Pure Live Zishu

**Pure Live UI 重构版 — 新架构，播放器不变**

基于 [liuchuancong/pure_live](https://github.com/liuchuancong/pure_live) 的 UI 重构项目。

---

## 目标

- **播放器及相关逻辑**：完全复用上游，零改动
- **UI 架构**：全新设计，独立开发
- **上游合并**：最小化改动，只改 `main.dart` 一个文件

---

## 架构

```
lib/
├── main.dart              # 唯一改动点（新旧 UI 选择器）
├── src/                   # 新 UI 架构（Riverpod + go_router）
│   ├── app/               # 应用壳、路由、主题
│   ├── features/          # 新页面（首页、搜索、收藏等）
│   ├── platforms/         # 平台适配
│   └── shared/            # 共享组件
├── features/              # 旧 UI（上游代码，不动）
├── domains/               # 旧业务逻辑（上游代码，不动）
├── core/                  # 旧核心层（上游代码，不动）
└── player/                # 播放器（上游代码，不动）
```

---

## 与上游的关系

| 模块 | 策略 |
|------|------|
| `lib/player/` | 完全复用，零改动 |
| `lib/src/` | 新架构，独立开发 |
| `lib/features/` | 上游代码，不动 |
| `lib/domains/` | 上游代码，不动 |
| `lib/core/` | 上游代码，不动 |
| `lib/main.dart` | 唯一改动点（加选择器） |

---

## 开发

```bash
# 克隆
git clone https://github.com/xoyofan/pure_live_zishu.git
cd pure_live_zishu

# 拉取上游更新
git fetch upstream
git merge upstream/master  # 只处理 main.dart 冲突

# 运行
flutter run
```

---

## 许可证

继承上游 [MIT License](https://github.com/liuchuancong/pure_live/blob/master/LICENSE)
