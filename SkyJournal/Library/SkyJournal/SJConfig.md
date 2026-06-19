---
countdownEvent: "下一次重要航行"
countdownDate: "2026-12-31"
weatherLocation: "Nanjing"
weatherCountryCode: "CN"
weatherLatitude: ""
weatherLongitude: ""
captainAvatar: "Library/SkyJournal/avatar.jpg"
themeMode: "system"
dashboardExcludedFolders: "Library, Repositories"
dashboardTagLimit: 16
---

# Sky Journal 配置

> 配置路径：`Library/SkyJournal/SJConfig`

本页面集中保存倒数日、天气、Captain 头像和主题模式。

## 倒数日

- `countdownEvent`：事件名称
- `countdownDate`：目标日期，格式必须为 `YYYY-MM-DD`

## 天气位置

- `weatherLocation`：城市或地区名称，例如 `Shanghai`、`Tokyo`、`New York`
- `weatherCountryCode`：可选的两位国家或地区代码，例如 `CN`、`JP`、`US`
- `weatherLatitude`、`weatherLongitude`：可选固定经纬度；填写后可跳过城市地理编码请求，首次加载更快

## Captain 头像

- `captainAvatar`：图片在 Space 中的路径
- 推荐路径：`Assets/SkyJournal/captain-avatar.png`
- 留空时显示 `ST` 字母占位头像

## 主题模式

`themeMode` 支持以下三个值：

- `light`：强制使用 Sky Journal 亮色主题
- `dark`：强制使用 Sky Journal 暗色主题
- `system`：跟随 SilverBullet 当前的亮色或暗色模式

修改设置后执行一次 `System: Reload`。天气数据默认缓存 15 分钟，并会先显示缓存或加载骨架，再在后台更新。

## 标签与任务排除统计

在 SJConfig 顶部 Frontmatter 中加入：

```yaml
dashboardExcludedFolders:
  - Library
  - Repositories
```

### 排除更多目录
```yaml
dashboardExcludedFolders:
  - Library
  - Repositories
  - Templates
  - System
```
### 只排除 Library
```yaml
dashboardExcludedFolders:
  - Library
```
### 不排除任何目录
```yaml
dashboardExcludedFolders: []
```
### 单行字符串写法
```yaml
dashboardExcludedFolders: "Library, Repositories"
```