# ✦ SJ WIDGETS · README EDITION ✦

> **版本：v1.4**  
> Configuration · Widgets · Section Pages · Dynamic Tag Fit

```text
        .            ✦             .
   ┌──────────────────────────────────┐
   │        S J   W I D G E T S       │
   │      RELINK FLIGHT SYSTEM        │
   ├──────────────────────────────────┤
   │  HERO      CALENDAR    WEATHER   │
   │  TAGS      TASKS       PARA      │
   │  CONFIG    FILTERS     PAGES     │
   └──────────────────────────────────┘
          \        |        /
       ----        ✦        ----
          /        |        \
```

`SJ Widgets` 是 Sky Journal Dashboard 的 Space Lua 组件库。

---

## 🧩 加载顺序

| 优先级 | 模块 | 作用 |
|---:|---|---|
| 100 | Core | 全局配置、缓存、基础函数 |
| 95–85 | Visual | Hero、Captain、活动日历 |
| 80–65 | Services | 倒数、过滤、天气、导航、标签 |
| 60–40 | Lists / Pages | 最近笔记、任务、PARA、完整板块页 |
| 20 | Footer | 页脚 |
| 10 | Initialization | 图片组件与标签适配初始化 |

> [!warning]
> 不建议随意改变优先级。核心必须先加载，初始化必须最后执行。

---

## ⚙️ SJConfig 配置

配置页名称：

```text
Library/SkyJournal/SJConfig
```

推荐 Frontmatter：

```yaml
---
countdownEvent: 下一次重要航行
countdownDate: 2026-12-31

captainAvatar: Library/SkyJournal/Assets/avatar.png

weatherLocation: Shanghai
weatherCountryCode: CN
weatherLatitude:
weatherLongitude:

themeMode: system

dashboardExcludedFolders:
  - Library
  - Repositories
---
```

| 字段 | 作用 |
|---|---|
| `countdownEvent` | 倒数事件名称 |
| `countdownDate` | 日期，格式 `YYYY-MM-DD` |
| `captainAvatar` | 本地 Space 图片或远程 URL |
| `weatherLocation` | 城市或地点 |
| `weatherCountryCode` | 两位国家代码 |
| `weatherLatitude` / `weatherLongitude` | 精确坐标 |
| `themeMode` | `system`、`light`、`dark` |
| `dashboardExcludedFolders` | Tags 与 Tasks 排除目录 |

### 排除目录

```yaml
dashboardExcludedFolders:
  - Library
  - Repositories
```

会同时过滤：

- Dashboard Tag Constellation；
- Dashboard Active Missions；
- Tags 板块页；
- Tasks 板块页。

`Library` 会匹配 `Library/...`，但不会误匹配 `LibraryNotes`。

关闭过滤：

```yaml
dashboardExcludedFolders: []
```

---

## 🛰️ 函数速查

| 分类 | 函数 |
|---|---|
| 主视觉 | `sj.hero()`、`sj.captain()` |
| 日历 | `sj.calendarActivity()`、`sj.heatmap()`、`sj.clock()` |
| 倒数 / 天气 | `sj.countdown()`、`sj.weather()` |
| 导航 | `sj.quickNav()` |
| 标签 | `sj.tagsCard()`、`sj.status()`、`sj.tagsPage()` |
| 列表 | `sj.recentNotes()`、`sj.openTasks()` |
| PARA 卡片 | `sj.journalList()`、`sj.projectList()`、`sj.areaList()`、`sj.archiveList()` |
| 完整板块页 | `sj.journalPage()`、`sj.projectPage()`、`sj.areaPage()`、`sj.archivePage()` |
| Tasks 页面 | `sj.tasksPage()` |
| 其他 | `sj.footer()`、`sj.art(url)` |

兼容别名：

```text
sj.heatmap() → sj.calendarActivity()
sj.clock()   → sj.calendarActivity()
sj.status()  → sj.tagsCard()
```

---

## 🎨 自定义指南

### Hero

搜索：

```lua
function sj.hero()
```

修改主标题与副标题。

### Captain

搜索：

```lua
function sj.captain()
```

可修改姓名、身份和状态文字。头像建议在 `SJConfig` 中设置：

```yaml
captainAvatar: Library/SkyJournal/Assets/avatar.png
```

### 快捷导航

在 `sj.quickNav()` 中增删：

```lua
dom.a { href = "页面名", "图标 显示名称" }
```

### 最近笔记数量

修改 `sj.recentNotes()` 查询中的：

```lua
limit 8
```

### 首页任务数量

同时修改：

```lua
if #tasks >= 8 then
```

以及：

```lua
"最多显示 8 项未完成任务"
```

### 天气缓存

文件核心模块中：

```lua
sj.weatherCacheMinutes = sj.weatherCacheMinutes or 15
sj.weatherErrorCacheMinutes = sj.weatherErrorCacheMinutes or 3
```

单位为分钟。

### 标签排序

`sj.collectTags()` 默认：

1. 引用次数由高到低；
2. 次数相同按名称排序。

调整其中的 `table.sort` 即可改变顺序。

### 动态标签适配

`sj.installDashboardTagFit()` 会根据标签卡剩余高度：

- 保留完整标签行；
- 隐藏第一个放不下的标签及后续内容；
- 在窗口尺寸变化后重新计算。

不要删除文件末尾的：

```lua
sj.installDashboardTagFit()
```

### PARA 目录

默认：

```text
Journal
Project
Area
Archive
```

重命名时必须同步修改：

- 对应 `sj.*List()`；
- 对应 `sj.*Page()`；
- Dashboard 导航；
- 实际目录结构。

---

## 🧯 故障排查

### 函数未定义

- 确认本页已加载；
- 停用旧 Widgets 页面；
- 执行 `System: Reload`。

### 有内容但没有主题样式

确认当前 `SJTheme` 已启用。本文件不包含 CSS。

### 配置不生效

确认大小写完全一致：

```text
Library/SkyJournal/SJConfig
```

### 标签或任务没有被过滤

检查：

```yaml
dashboardExcludedFolders:
  - Library
  - Repositories
```

保存后等待 Object Index 更新，再执行 `System: Reload`。

### 天气长期加载

检查地点或坐标、网络代理和 Open-Meteo 可用性；必要时清理站点缓存后重载。

---

# PROGRAM MODULES

## 🧠 00｜运行时核心、配置与通用工具

初始化 `sj` 命名空间、配置页、排除目录、天气缓存和通用 DOM 工具。

> **自定义提示：** 常用修改：`sj.configPage`、`sj.defaultDashboardExcludedFolders`、天气缓存分钟数。

```space-lua
-- priority: 100

-- SJ Widgets v1.4
-- Configuration page: Library/SkyJournal/SJConfig
-- dashboardExcludedFolders applies to:
--   1. Dashboard Tag Constellation
--   2. Dashboard Active Missions
--   3. Tags detail page
--   4. Tasks detail page

sj = sj or {}

-- Sky Journal 共用配置页：倒数日、天气位置等设置均保存在这里。
sj.configPage = "Library/SkyJournal/SJConfig"

-- 兼容旧调用名，但实际统一指向 Library/SkyJournal/SJConfig。
sj.countdownPage = sj.configPage

-- 标签与任务索引默认忽略目录。
-- 用户可在 Library/SkyJournal/SJConfig 的 Frontmatter 中通过
-- dashboardExcludedFolders 字段覆盖此列表。
-- 为兼容既有配置，字段名继续保留；该规则现在同时作用于
-- Dashboard、Tags 详情页与 Tasks 详情页。
sj.defaultDashboardExcludedFolders = {
  "Library",
  "Repositories"
}

-- 天气数据内存缓存；默认 15 分钟内不重复请求。
sj.weatherCacheMinutes = sj.weatherCacheMinutes or 15
sj.weatherErrorCacheMinutes = sj.weatherErrorCacheMinutes or 3
sj._weatherCache = sj._weatherCache or {}
sj._weatherLoading = sj._weatherLoading or {}

-- ================= BASIC HELPERS =================
function sj.countRows(rows)
  local count = 0
  for _, row in ipairs(rows) do
    count = count + 1
  end
  return count
end

function sj.shortDate(value)
  if value == nil then
    return ""
  end
  return string.sub(tostring(value), 1, 10)
end

function sj.relativePageName(pageName, folder)
  local prefix = folder .. "/"
  if pageName:startsWith(prefix) then
    return string.sub(pageName, string.len(prefix) + 1)
  end
  return pageName
end

function sj.newNoteButton(folder)
  return dom.button {
    type = "button",
    class = "sky-create-btn sky-new-note-btn",
    title = "在 " .. folder .. " 中新建笔记",
    onclick = function()
      local defaultTitle = os.date("%Y-%m-%d %H-%M")
      if folder == "Journal" then
        defaultTitle = os.date("%Y-%m-%d")
      end
      local pageName = editor.prompt(
        "请输入新笔记路径",
        folder .. "/" .. defaultTitle
      )
      if pageName == nil then
        return
      end
      pageName = string.trim(pageName)
      if pageName == "" then
        return
      end
      editor.navigate(pageName)
    end,
    dom.span {
      class = "sky-create-btn-label",
      "新建笔记"
    }
  }
end

function sj.pageActionLink(pageName, label, title)
  return dom.a {
    href = pageName,
    class = "sky-create-btn sky-action-link",
    title = title or label,
    label
  }
end

function sj.listHeader(icon, title, subtitle, folder, showCreateButton)
  local header = {
    class = "sky-list-header",
    dom.div {
      class = "sky-list-heading",
      dom.div {
        class = "sky-list-title",
        icon .. " " .. title
      },
      dom.div {
        class = "sky-list-subtitle",
        subtitle
      }
    }
  }
  if showCreateButton ~= false then
    table.insert(header, sj.newNoteButton(folder))
  end
  return dom.div(header)
end

function sj.emptyRow(text)
  return dom.div {
    class = "sky-list-empty",
    text
  }
end

function sj.pageRow(page, folder)
  local displayName = page.name
  if folder ~= nil then
    displayName = sj.relativePageName(page.name, folder)
  end
  return dom.a {
    href = page.ref or page.name,
    class = "sky-list-row sky-page-row",
    dom.span {
      class = "sky-list-row-main",
      "◇ " .. displayName
    },
    dom.span {
      class = "sky-list-meta",
      sj.shortDate(page.lastModified)
    }
  }
end

function sj.taskRow(task)
  local target = task.ref or task.page
  local taskName = task.name or "Untitled task"
  local sourcePage = task.page or ""
  return dom.a {
    href = target,
    class = "sky-list-row sky-task-row",
    dom.span {
      class = "sky-list-row-main",
      "☐ " .. taskName
    },
    dom.span {
      class = "sky-list-meta",
      sourcePage
    }
  }
end
```

## 🌌 01｜Hero 主视觉

生成 Dashboard 顶部主标题与副标题。

> **自定义提示：** 修改 `sj.hero()` 中的两段文字。

```space-lua
-- priority: 95

-- ================= HERO =================
function sj.hero()
  return widget.htmlBlock(
    dom.div {
      class = "sky-hero",
      dom.div { class = "sky-hero-title", "SKY JOURNAL" },
      dom.div {
        class = "sky-hero-subtitle",
        "Journey Beyond The Blue Sky"
      }
    }
  )
end
```

## 🐺 02｜Captain HUD 与头像

提供 Captain 身份卡、文字头像、本地 Space 图片和远程图片兼容。

> **自定义提示：** 姓名和身份在 `sj.captain()`；头像在 `SJConfig` 的 `captainAvatar`。

```space-lua
-- priority: 90

-- ================= CAPTAIN HUD =================
function sj.captainTextAvatar()
  return dom.div {
    class = "sky-captain-avatar-mask",
    dom.div {
      class = "sky-captain-avatar-placeholder",
      "ST"
    }
  }
end

function sj.isRemoteAssetPath(path)
  local value = tostring(path or "")
  return string.sub(value, 1, 7) == "http://"
    or string.sub(value, 1, 8) == "https://"
    or string.sub(value, 1, 5) == "data:"
    or string.sub(value, 1, 5) == "blob:"
end

function sj.spaceAssetPath(path)
  local value = string.trim(tostring(path or ""))

  if string.sub(value, 1, 5) == "/.fs/" then
    return string.sub(value, 6)
  end

  value = string.gsub(value, "^/+", "")
  return value
end

function sj.assetUrl(path)
  local value = string.trim(tostring(path or ""))

  if value == "" then
    return ""
  end

  if sj.isRemoteAssetPath(value)
    or string.sub(value, 1, 5) == "/.fs/"
  then
    return value
  end

  value = sj.spaceAssetPath(value)

  -- Browser URLs need escaped spaces, while space.fileExists uses
  -- the original Space path.
  value = string.gsub(value, " ", "%%20")

  return "/.fs/" .. value
end

function sj.captainAvatarNode()
  local config = sj.configData()
  local avatarPath = string.trim(
    tostring(config.captainAvatar or "")
  )

  if avatarPath == "" then
    return sj.captainTextAvatar()
  end

  -- Remote URLs can be used directly. Local Space files must be checked
  -- using their Space path, but rendered through the /.fs/ HTTP endpoint.
  if not sj.isRemoteAssetPath(avatarPath) then
    local spacePath = sj.spaceAssetPath(avatarPath)

    if spacePath == "" or not space.fileExists(spacePath) then
      return sj.captainTextAvatar()
    end
  end

  return dom.div {
    class = "sky-captain-avatar-mask",
    dom.img {
      class = "sky-captain-avatar",
      src = sj.assetUrl(avatarPath),
      alt = "Captain avatar"
    }
  }
end

function sj.captain()
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-captain-card",
      dom.div {
        class = "sky-captain-copy",
        dom.div {
          class = "sky-captain-kicker",
          "✦ CAPTAIN STATUS ✦"
        },
        dom.div {
          class = "sky-captain-name",
          "空野汰輝"
        },
        dom.div {
          class = "sky-captain-role",
          "Skyfarer • Wolf-Blooded"
        },
        dom.div {
          class = "sky-captain-state",
          dom.span {
            class = "sky-captain-state-dot"
          },
          "FLIGHT SYSTEM ACTIVE"
        }
      },
      dom.div {
        class = "sky-captain-avatar-frame",
        sj.captainAvatarNode()
      }
    }
  )
end
```

## 📅 03｜月度活动日历

统计页面修改日期，生成可切换年月并跳转 Journal 日期页的活动月历。

> **自定义提示：** 修改统计范围时调整 `sj.calendarActivity()` 查询条件。

```space-lua
-- priority: 85

-- ================= MONTHLY ACTIVITY CALENDAR =================
function sj.activityLevel(count, maxCount)
  if count <= 0 then
    return 0
  end
  if maxCount <= 1 then
    return 4
  end
  local ratio = count / maxCount
  if ratio <= 0.25 then
    return 1
  elseif ratio <= 0.50 then
    return 2
  elseif ratio <= 0.75 then
    return 3
  end
  return 4
end

function sj.monthName(month)
  local names = {
    "JANUARY", "FEBRUARY", "MARCH", "APRIL",
    "MAY", "JUNE", "JULY", "AUGUST",
    "SEPTEMBER", "OCTOBER", "NOVEMBER", "DECEMBER"
  }
  return names[month] or ""
end

function sj.calendarView()
  local now = os.time()
  local fallbackYear = tonumber(os.date("%Y", now))
  local fallbackMonth = tonumber(os.date("%m", now))

  local year = tonumber(clientStore.get("sj.calendar.year")) or fallbackYear
  local month = tonumber(clientStore.get("sj.calendar.month")) or fallbackMonth

  if month < 1 or month > 12 then
    month = fallbackMonth
  end
  if year < 1900 or year > 2200 then
    year = fallbackYear
  end

  return year, month
end

function sj.setCalendarView(year, month)
  year = tonumber(year)
  month = tonumber(month)
  if year == nil or month == nil then
    return
  end

  while month < 1 do
    month = month + 12
    year = year - 1
  end
  while month > 12 do
    month = month - 12
    year = year + 1
  end

  clientStore.set("sj.calendar.year", year)
  clientStore.set("sj.calendar.month", month)

  -- 当前 Dashboard 是由 ${sj.dashboard()} 渲染的代码 Widget。
  -- 直接刷新代码 Widget，才能立即重新计算 clientStore 中的年月。
  codeWidget.refreshAll()
end

function sj.shiftCalendarMonth(delta)
  local year, month = sj.calendarView()
  sj.setCalendarView(year, month + delta)
end

function sj.chooseCalendarMonth()
  local year, month = sj.calendarView()
  local value = editor.prompt(
    "选择月份（1-12）",
    tostring(month)
  )
  if value == nil then
    return
  end

  local selected = tonumber(string.trim(value))
  if selected == nil or selected < 1 or selected > 12 then
    editor.flashNotification(
      "月份必须是 1 到 12 之间的数字。",
      "warning"
    )
    return
  end

  sj.setCalendarView(year, selected)
end

function sj.chooseCalendarYear()
  local year, month = sj.calendarView()
  local value = editor.prompt(
    "选择年份",
    tostring(year)
  )
  if value == nil then
    return
  end

  local selected = tonumber(string.trim(value))
  if selected == nil or selected < 1900 or selected > 2200 then
    editor.flashNotification(
      "年份必须在 1900 到 2200 之间。",
      "warning"
    )
    return
  end

  sj.setCalendarView(selected, month)
end

function sj.resetCalendarToday()
  clientStore.del("sj.calendar.year")
  clientStore.del("sj.calendar.month")

  -- 重新执行 Dashboard 表达式，立即返回当前月份。
  codeWidget.refreshAll()
end

function sj.calendarActivity()
  local pages = query[[
    from p = index.contentPages()
    where p.lastModified ~= nil
      and p.name ~= "Index"
      and p.name ~= "index"
      and not p.name:startsWith("Library/")
    select p
  ]]

  local activity = {}
  for _, page in ipairs(pages) do
    local dayKey = string.sub(tostring(page.lastModified), 1, 10)
    activity[dayKey] = (activity[dayKey] or 0) + 1
  end

  local now = os.time()
  local currentYear = tonumber(os.date("%Y", now))
  local currentMonth = tonumber(os.date("%m", now))
  local currentDay = tonumber(os.date("%d", now))
  local year, month = sj.calendarView()

  local firstTime = os.time {
    year = year,
    month = month,
    day = 1,
    hour = 12
  }

  local nextYear = year
  local nextMonth = month + 1
  if nextMonth == 13 then
    nextMonth = 1
    nextYear = year + 1
  end

  local nextMonthTime = os.time {
    year = nextYear,
    month = nextMonth,
    day = 1,
    hour = 12
  }

  local lastDayTime = nextMonthTime - 86400
  local daysInMonth = tonumber(os.date("%d", lastDayTime))
  local firstWeekday = tonumber(os.date("%w", firstTime)) or 0
  local mondayOffset = (firstWeekday + 6) % 7

  local maxCount = 0
  local totalCount = 0
  for day = 1, daysInMonth do
    local dayKey = string.format("%04d-%02d-%02d", year, month, day)
    local count = activity[dayKey] or 0
    totalCount = totalCount + count
    if count > maxCount then
      maxCount = count
    end
  end

  local cells = {
    class = "sky-calendar-grid"
  }

  for _ = 1, mondayOffset do
    table.insert(
      cells,
      dom.div {
        class = "sky-calendar-day sky-calendar-empty"
      }
    )
  end

  for day = 1, daysInMonth do
    local timestamp = os.time {
      year = year,
      month = month,
      day = day,
      hour = 12
    }
    local dayKey = string.format("%04d-%02d-%02d", year, month, day)
    local count = activity[dayKey] or 0
    local level = sj.activityLevel(count, maxCount)
    local position = mondayOffset + day - 1
    local weekday = position % 7
    local cellClass =
      "sky-calendar-day sky-calendar-level-" .. tostring(level)

    if year == currentYear
      and month == currentMonth
      and day == currentDay
    then
      cellClass = cellClass .. " sky-calendar-today"
    end
    if weekday == 5 or weekday == 6 then
      cellClass = cellClass .. " sky-calendar-weekend"
    end
    if timestamp > now then
      cellClass = cellClass .. " sky-calendar-future"
    end

    local cell = {
      href = "Journal/" .. dayKey,
      class = cellClass,
      title = dayKey
        .. " · "
        .. tostring(count)
        .. " 篇笔记更新 · 打开 Journal/"
        .. dayKey,
      dom.span {
        class = "sky-calendar-date-number",
        tostring(day)
      }
    }

    if count > 0 then
      table.insert(
        cell,
        dom.span {
          class = "sky-calendar-activity-count",
          tostring(count)
        }
      )
    end

    table.insert(cells, dom.a(cell))
  end

  local usedCells = mondayOffset + daysInMonth
  local trailingCells = (7 - (usedCells % 7)) % 7
  for _ = 1, trailingCells do
    table.insert(
      cells,
      dom.div {
        class = "sky-calendar-day sky-calendar-empty"
      }
    )
  end

  local isCurrentMonth =
    year == currentYear and month == currentMonth
  local headerMetric = tostring(totalCount)
  local headerLabel = " NOTES"

  if isCurrentMonth then
    local todayKey = string.format(
      "%04d-%02d-%02d",
      currentYear,
      currentMonth,
      currentDay
    )
    headerMetric = tostring(activity[todayKey] or 0)
    headerLabel = " TODAY"
  end

  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-calendar-card",
      dom.div {
        class = "sky-calendar-header",
        dom.div {
          dom.div {
            class = "sky-calendar-title",
            "✦ NAVIGATION ACTIVITY ✦"
          },
          dom.div {
            class = "sky-calendar-controls",
            dom.button {
              class = "sky-calendar-nav-btn",
              title = "上一个月",
              onclick = function()
                sj.shiftCalendarMonth(-1)
              end,
              "‹"
            },
            dom.button {
              class = "sky-calendar-picker-btn",
              title = "选择月份",
              onclick = function()
                sj.chooseCalendarMonth()
              end,
              sj.monthName(month)
            },
            dom.button {
              class = "sky-calendar-picker-btn sky-calendar-year-btn",
              title = "选择年份",
              onclick = function()
                sj.chooseCalendarYear()
              end,
              tostring(year)
            },
            dom.button {
              class = "sky-calendar-nav-btn",
              title = "下一个月",
              onclick = function()
                sj.shiftCalendarMonth(1)
              end,
              "›"
            },
            dom.button {
              class = "sky-calendar-today-btn",
              title = "返回当前月份",
              onclick = function()
                sj.resetCalendarToday()
              end,
              dom.span {
                class = "sky-calendar-today-icon",
                "📅"
              }
            }
          }
        },
        dom.div {
          class = "sky-calendar-today-count",
          dom.span { headerMetric },
          headerLabel
        }
      },
      dom.div {
        class = "sky-calendar-weekdays",
        dom.span { "MON" },
        dom.span { "TUE" },
        dom.span { "WED" },
        dom.span { "THU" },
        dom.span { "FRI" },
        dom.span { "SAT" },
        dom.span { "SUN" }
      },
      dom.div(cells),
      dom.div {
        class = "sky-calendar-footer",
        dom.span {
          "本月共 " .. tostring(totalCount) .. " 次页面更新"
        },
        dom.span {
          "点击日期打开 Journal/" ..
          string.format("%04d-%02d-DD", year, month)
        }
      }
    }
  )
end

-- 保留旧名称，避免其他页面仍调用 sj.heatmap() 或 sj.clock() 时失效
function sj.heatmap()
  return sj.calendarActivity()
end

function sj.clock()
  return sj.calendarActivity()
end
```

## 🧭 04｜倒数日、配置读取、目录过滤与标签适配

读取 `SJConfig`，处理倒数日、Tags/Tasks 排除目录和 Dashboard 标签动态裁切。

> **自定义提示：** 使用 `countdownEvent`、`countdownDate`、`dashboardExcludedFolders`。

```space-lua
-- priority: 80

-- ================= COUNTDOWN =================
function sj.normalizedDate(value)
  if value == nil then
    return nil
  end
  local text = string.sub(tostring(value), 1, 10)
  local year, month, day = string.match(
    text,
    "^(%d%d%d%d)%-(%d%d)%-(%d%d)$"
  )
  if year == nil then
    return nil
  end
  return text, tonumber(year), tonumber(month), tonumber(day)
end

function sj.daysUntil(value)
  local text, year, month, day = sj.normalizedDate(value)
  if text == nil then
    return nil
  end
  local targetTime = os.time {
    year = year,
    month = month,
    day = day,
    hour = 12
  }
  local todayText = os.date("%Y-%m-%d")
  local _, todayYear, todayMonth, todayDay = sj.normalizedDate(todayText)
  local todayTime = os.time {
    year = todayYear,
    month = todayMonth,
    day = todayDay,
    hour = 12
  }
  return math.floor(((targetTime - todayTime) / 86400) + 0.5)
end

function sj.configData()
  local rows = query[[
    from p = index.pages()
    where p.name == sj.configPage
    limit 1
    select p
  ]]
  return rows[1] or {}
end

-- ================= TAG / TASK INDEX FILTERS =================

-- 统一目录写法：
--   "/Library/"  -> "Library"
--   "Library/"   -> "Library"
function sj.normalizeDashboardFolder(value)
  local folder = string.trim(tostring(value or ""))
  folder = string.gsub(folder, "^/+", "")
  folder = string.gsub(folder, "/+$", "")
  return folder
end

-- 从 SJCONFIG 读取标签与任务索引的排除目录。
--
-- 推荐 Frontmatter 写法：
-- dashboardExcludedFolders:
--   - Library
--   - Repositories
--
-- 也兼容逗号、分号或换行分隔的字符串。
-- 当字段不存在时，使用 sj.defaultDashboardExcludedFolders。
-- 当字段明确设置为空数组 [] 时，不排除任何目录。
function sj.dashboardExcludedFolders()
  local config = sj.configData()
  local raw = config.dashboardExcludedFolders

  if raw == nil then
    raw = sj.defaultDashboardExcludedFolders
  end

  local folders = {}
  local seen = {}

  local function addFolder(value)
    local folder = sj.normalizeDashboardFolder(value)
    if folder ~= "" and not seen[folder] then
      seen[folder] = true
      table.insert(folders, folder)
    end
  end

  if type(raw) == "table" then
    for _, value in ipairs(raw) do
      addFolder(value)
    end
  elseif type(raw) == "string" then
    for value in string.gmatch(raw, "[^,;\n]+") do
      addFolder(value)
    end
  end

  return folders
end

-- 获取索引对象所属页面。
-- task/tag 对象通常直接提供 page；ref 作为兼容回退。
function sj.indexObjectPage(object)
  if object == nil then
    return ""
  end

  local page = object.page
  if page ~= nil and tostring(page) ~= "" then
    return tostring(page)
  end

  local ref = tostring(object.ref or "")
  if ref == "" then
    return ""
  end

  local refPage = string.match(ref, "^(.-)@%d+")
  return refPage or ref
end

-- 精确匹配目录根本身及其所有子页面。
-- 例如 Library 会排除：
--   Library
--   Library/Std
--   Library/SkyJournal/SJConfig
-- 但不会误伤 LibraryNotes。
function sj.isDashboardPageExcluded(pageName)
  local page = tostring(pageName or "")

  for _, folder in ipairs(sj.dashboardExcludedFolders()) do
    if page == folder or page:startsWith(folder .. "/") then
      return true
    end
  end

  return false
end

function sj.dashboardObjectAllowed(object)
  return not sj.isDashboardPageExcluded(
    sj.indexObjectPage(object)
  )
end


-- =========================================================
-- DASHBOARD TAG ROW FIT CONTROLLER
--
-- All filtered tags are rendered. The browser then keeps every complete
-- row that fits between the card header and statistics footer.
--
-- This controller only toggles [hidden] on rendered Widget buttons.
-- It never changes CodeMirror lines, editor text or decorations.
-- =========================================================

function sj.installDashboardTagFit()
  if js == nil or js.window == nil then
    return
  end

  js.window.eval([[
(function () {
  const controllerKey = "__sjDashboardTagFitController";
  const controllerVersion = "1.4";
  const existing = window[controllerKey];

  if (
    existing &&
    existing.version === controllerVersion &&
    typeof existing.scan === "function"
  ) {
    existing.scan();
    return;
  }

  if (
    existing &&
    typeof existing.destroy === "function"
  ) {
    existing.destroy();
  }

  let frame = 0;
  const pendingCards = new Set();
  const observedCards = new WeakSet();

  function tagChips(cloud) {
    return Array.from(cloud.children).filter(function (node) {
      return (
        node instanceof HTMLElement &&
        node.classList.contains("sky-tag-chip")
      );
    });
  }

  function fitCard(card) {
    if (!(card instanceof HTMLElement)) {
      return;
    }

    const cloud = card.querySelector(".sky-tag-cloud");

    if (!(cloud instanceof HTMLElement)) {
      return;
    }

    const chips = tagChips(cloud);

    chips.forEach(function (chip) {
      chip.hidden = false;
    });

    if (chips.length === 0) {
      return;
    }

    /*
    Read all positions before hiding anything. If the first chip of a row
    crosses the cloud boundary, that complete row and every later row are
    hidden together.
    */
    const cloudBottom =
      cloud.getBoundingClientRect().bottom + 0.5;

    const rectangles = chips.map(function (chip) {
      return chip.getBoundingClientRect();
    });

    let firstOverflowIndex = chips.length;

    for (
      let index = 0;
      index < rectangles.length;
      index += 1
    ) {
      if (rectangles[index].bottom > cloudBottom) {
        firstOverflowIndex = index;
        break;
      }
    }

    for (
      let index = firstOverflowIndex;
      index < chips.length;
      index += 1
    ) {
      chips[index].hidden = true;
    }
  }

  function flush() {
    frame = 0;

    pendingCards.forEach(function (card) {
      fitCard(card);
    });

    pendingCards.clear();
  }

  function queueCard(card) {
    if (!(card instanceof HTMLElement)) {
      return;
    }

    pendingCards.add(card);

    if (frame === 0) {
      frame = window.requestAnimationFrame(flush);
    }
  }

  const resizeObserver =
    typeof ResizeObserver === "function"
      ? new ResizeObserver(function (entries) {
          entries.forEach(function (entry) {
            queueCard(entry.target);
          });
        })
      : null;

  function scan() {
    document
      .querySelectorAll(".sky-tags-card")
      .forEach(function (card) {
        if (!observedCards.has(card)) {
          observedCards.add(card);

          if (resizeObserver) {
            resizeObserver.observe(card);
          }
        }

        queueCard(card);
      });
  }

  const mutationObserver = new MutationObserver(scan);

  function start() {
    if (!document.body) {
      window.setTimeout(start, 50);
      return;
    }

    mutationObserver.observe(document.body, {
      subtree: true,
      childList: true
    });

    scan();
  }

  window.addEventListener("resize", scan);
  window.addEventListener("pageshow", scan);

  window[controllerKey] = {
    version: controllerVersion,
    scan: scan,
    destroy: function () {
      mutationObserver.disconnect();

      if (resizeObserver) {
        resizeObserver.disconnect();
      }

      if (frame !== 0) {
        window.cancelAnimationFrame(frame);
      }

      window.removeEventListener("resize", scan);
      window.removeEventListener("pageshow", scan);
    }
  };

  start();
})();
  ]])
end


function sj.countdownData()
  local page = sj.configData()
  local eventName = page.countdownEvent or "尚未设置倒数事件"
  local dateText = page.countdownDate
  local normalizedDate = sj.normalizedDate(dateText)
  return {
    event = tostring(eventName),
    date = normalizedDate,
    days = sj.daysUntil(dateText)
  }
end

function sj.countdown()
  local data = sj.countdownData()
  local numberText = "—"
  local labelText = "WAITING FOR ROUTE"
  local stateClass = " sky-countdown-unset"
  if data.days ~= nil then
    if data.days > 0 then
      numberText = tostring(data.days)
      labelText = "DAYS REMAINING"
      stateClass = ""
    elseif data.days == 0 then
      numberText = "TODAY"
      labelText = "THE DAY HAS ARRIVED"
      stateClass = " sky-countdown-today"
    else
      numberText = tostring(math.abs(data.days))
      labelText = "DAYS SINCE"
      stateClass = " sky-countdown-past"
    end
  end
  local dateText = data.date or "请在 Library/SkyJournal/SJConfig 页面设置日期"
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-countdown-card" .. stateClass,
      dom.div {
        class = "sky-countdown-header",
        dom.div {
          dom.div {
            class = "sky-countdown-title",
            "✦ COUNTDOWN ROUTE ✦"
          },
          dom.div {
            class = "sky-countdown-subtitle",
            "下一处重要航标"
          }
        },
        sj.pageActionLink(
          sj.configPage,
          "设置",
          "打开 Sky Journal 配置页面"
        )
      },
      dom.div {
        class = "sky-countdown-body",
        dom.div {
          class = "sky-countdown-event",
          data.event
        },
        dom.div {
          class = "sky-countdown-main",
          dom.strong {
            class = "sky-countdown-number",
            numberText
          },
          dom.span {
            class = "sky-countdown-label",
            labelText
          }
        }
      },
      dom.div {
        class = "sky-countdown-footer",
        dom.span {
          class = "sky-countdown-date",
          "TARGET DATE · " .. dateText
        },
        dom.span {
          class = "sky-countdown-status",
          "ROUTE LOCKED"
        }
      }
    }
  )
end
```

## 🌦️ 05｜天气预报与缓存

通过 Open-Meteo 获取天气，包含地点解析、缓存、骨架屏和延迟刷新。

> **自定义提示：** 在 `SJConfig` 设置地点、国家代码或经纬度。

```space-lua
-- priority: 75

-- ================= WEATHER FORECAST =================
function sj.urlEncode(value)
  local text = tostring(value or "")
  text = string.gsub(text, "\n", "\r\n")
  text = string.gsub(
    text,
    "([^%w%-_%.~])",
    function(char)
      return string.format("%%%02X", string.byte(char))
    end
  )
  return text
end

function sj.weatherIcon(code, isDay)
  code = tonumber(code) or -1
  if code == 0 then
    if tonumber(isDay) == 0 then
      return "🌙"
    end
    return "☀️"
  elseif code == 1 then
    if tonumber(isDay) == 0 then
      return "🌙"
    end
    return "🌤️"
  elseif code == 2 then
    return "⛅"
  elseif code == 3 then
    return "☁️"
  elseif code == 45 or code == 48 then
    return "🌫️"
  elseif code >= 51 and code <= 57 then
    return "🌦️"
  elseif code >= 61 and code <= 67 then
    return "🌧️"
  elseif code >= 71 and code <= 77 then
    return "❄️"
  elseif code >= 80 and code <= 82 then
    return "🌦️"
  elseif code == 85 or code == 86 then
    return "🌨️"
  elseif code >= 95 and code <= 99 then
    return "⛈️"
  end
  return "🌡️"
end

function sj.weatherDescription(code)
  code = tonumber(code) or -1
  if code == 0 then
    return "晴朗"
  elseif code == 1 then
    return "晴间多云"
  elseif code == 2 then
    return "多云"
  elseif code == 3 then
    return "阴天"
  elseif code == 45 or code == 48 then
    return "雾"
  elseif code >= 51 and code <= 57 then
    return "毛毛雨"
  elseif code >= 61 and code <= 67 then
    return "降雨"
  elseif code >= 71 and code <= 77 then
    return "降雪"
  elseif code >= 80 and code <= 82 then
    return "阵雨"
  elseif code == 85 or code == 86 then
    return "阵雪"
  elseif code >= 95 and code <= 99 then
    return "雷雨"
  end
  return "天气变化中"
end

function sj.roundTemperature(value)
  local number = tonumber(value)
  if number == nil then
    return "—"
  end
  return string.format("%.0f", number)
end

function sj.weatherConfig()
  local config = sj.configData()
  local location = string.trim(
    tostring(config.weatherLocation or "")
  )
  local countryCode = string.trim(
    tostring(config.weatherCountryCode or "")
  )
  local latitude = tonumber(config.weatherLatitude)
  local longitude = tonumber(config.weatherLongitude)

  return {
    location = location,
    countryCode = countryCode,
    latitude = latitude,
    longitude = longitude
  }
end

function sj.weatherConfigKey()
  local config = sj.weatherConfig()
  local rawKey =
    config.location
    .. "|"
    .. config.countryCode
    .. "|"
    .. tostring(config.latitude or "")
    .. "|"
    .. tostring(config.longitude or "")

  return sj.urlEncode(rawKey), config
end

function sj.weatherGeoStoreKey(key)
  return "sj.weather.geo." .. key
end

function sj.weatherForecastStoreKey(key)
  return "sj.weather.forecast." .. key
end

function sj.weatherLocation()
  local key, config = sj.weatherConfigKey()

  if config.location == ""
    and (config.latitude == nil or config.longitude == nil)
  then
    return nil, nil, "请在 Library/SkyJournal/SJConfig 中设置天气位置"
  end

  -- When coordinates are configured, skip geocoding entirely.
  if config.latitude ~= nil and config.longitude ~= nil then
    local displayName = config.location
    if displayName == "" then
      displayName =
        string.format(
          "%.4f, %.4f",
          config.latitude,
          config.longitude
        )
    end
    return config.latitude, config.longitude, displayName
  end

  local memoryKey = "geo|" .. key
  local memoryRecord = sj._weatherCache[memoryKey]
  if memoryRecord ~= nil then
    return
      memoryRecord.latitude,
      memoryRecord.longitude,
      memoryRecord.displayName
  end

  -- Geocoding rarely changes, so persist it between browser reloads.
  local stored = clientStore.get(sj.weatherGeoStoreKey(key))
  if stored ~= nil
    and stored.latitude ~= nil
    and stored.longitude ~= nil
  then
    sj._weatherCache[memoryKey] = stored
    return stored.latitude, stored.longitude, stored.displayName
  end

  local geoUrl =
    "https://geocoding-api.open-meteo.com/v1/search"
    .. "?name=" .. sj.urlEncode(config.location)
    .. "&count=1&language=zh&format=json"

  if config.countryCode ~= "" then
    geoUrl =
      geoUrl
      .. "&countryCode="
      .. sj.urlEncode(config.countryCode)
  end

  local response = net.proxyFetch(
    geoUrl,
    {
      method = "GET",
      headers = {
        Accept = "application/json"
      }
    }
  )

  if response == nil or not response.ok or response.body == nil then
    return nil, nil, "无法获取地点坐标"
  end

  local result = nil
  if response.body.results ~= nil then
    result = response.body.results[1]
  end
  if result == nil then
    return nil, nil, "没有找到地点：" .. config.location
  end

  local displayName = tostring(result.name or config.location)
  if result.admin1 ~= nil and tostring(result.admin1) ~= "" then
    displayName =
      displayName .. " · " .. tostring(result.admin1)
  elseif result.country_code ~= nil
    and tostring(result.country_code) ~= ""
  then
    displayName =
      displayName .. " · " .. tostring(result.country_code)
  end

  local record = {
    latitude = result.latitude,
    longitude = result.longitude,
    displayName = displayName
  }

  sj._weatherCache[memoryKey] = record
  clientStore.set(sj.weatherGeoStoreKey(key), record)

  return record.latitude, record.longitude, record.displayName
end

function sj.fetchWeatherData()
  local latitude, longitude, displayName = sj.weatherLocation()
  if latitude == nil or longitude == nil then
    return {
      error = displayName or "天气位置配置无效"
    }
  end

  local url =
    "https://api.open-meteo.com/v1/forecast"
    .. "?latitude=" .. tostring(latitude)
    .. "&longitude=" .. tostring(longitude)
    .. "&current=temperature_2m,weather_code,is_day"
    .. "&hourly=precipitation_probability"
    .. "&daily=weather_code,temperature_2m_max,temperature_2m_min"
    .. "&temperature_unit=celsius"
    .. "&timezone=auto"
    .. "&forecast_days=4"
    .. "&forecast_hours=12"

  local response = net.proxyFetch(
    url,
    {
      method = "GET",
      headers = {
        Accept = "application/json"
      }
    }
  )

  if response == nil or not response.ok or response.body == nil then
    return {
      error = "天气服务暂时不可用",
      location = displayName
    }
  end

  local body = response.body
  if body.current == nil or body.daily == nil then
    return {
      error = "天气数据不完整",
      location = displayName
    }
  end

  local maxRain = 0
  if body.hourly ~= nil
    and body.hourly.precipitation_probability ~= nil
  then
    for _, probability in ipairs(
      body.hourly.precipitation_probability
    ) do
      local value = tonumber(probability) or 0
      if value > maxRain then
        maxRain = value
      end
    end
  end

  local rainText = "降雨可能较低"
  local rainClass = " sky-weather-rain-low"
  if maxRain >= 60 then
    rainText = "很可能下雨"
    rainClass = " sky-weather-rain-high"
  elseif maxRain >= 30 then
    rainText = "可能下雨"
    rainClass = " sky-weather-rain-medium"
  end

  local daily = body.daily
  local forecast = {
    {
      label = "明天",
      code = daily.weather_code and daily.weather_code[2],
      high = daily.temperature_2m_max
        and daily.temperature_2m_max[2],
      low = daily.temperature_2m_min
        and daily.temperature_2m_min[2]
    },
    {
      label = "后天",
      code = daily.weather_code and daily.weather_code[3],
      high = daily.temperature_2m_max
        and daily.temperature_2m_max[3],
      low = daily.temperature_2m_min
        and daily.temperature_2m_min[3]
    },
    {
      label = "大后天",
      code = daily.weather_code and daily.weather_code[4],
      high = daily.temperature_2m_max
        and daily.temperature_2m_max[4],
      low = daily.temperature_2m_min
        and daily.temperature_2m_min[4]
    }
  }

  return {
    location = displayName,
    currentTemperature = body.current.temperature_2m,
    currentCode = body.current.weather_code,
    isDay = body.current.is_day,
    maxRain = math.floor(maxRain + 0.5),
    rainText = rainText,
    rainClass = rainClass,
    forecast = forecast
  }
end

function sj.weatherCacheRecord()
  local key, config = sj.weatherConfigKey()

  if config.location == ""
    and (config.latitude == nil or config.longitude == nil)
  then
    return {
      data = {
        error = "请在 Library/SkyJournal/SJConfig 中设置天气位置"
      },
      fetchedAt = os.time()
    }, key, config
  end

  local memoryKey = "render|" .. key
  local memoryRecord = sj._weatherCache[memoryKey]
  if memoryRecord ~= nil then
    return memoryRecord, key, config
  end

  local stored =
    clientStore.get(sj.weatherForecastStoreKey(key))
  if stored ~= nil and stored.data ~= nil then
    sj._weatherCache[memoryKey] = stored
    return stored, key, config
  end

  return nil, key, config
end

function sj.weatherRecordFresh(record)
  if record == nil or record.fetchedAt == nil then
    return false
  end

  local ttlMinutes = tonumber(sj.weatherCacheMinutes) or 15
  if record.data ~= nil and record.data.error ~= nil then
    ttlMinutes =
      tonumber(sj.weatherErrorCacheMinutes) or 3
  end

  return
    os.time() - tonumber(record.fetchedAt)
    < ttlMinutes * 60
end

function sj.weatherLazyTrigger(key)
  return dom.img {
    class = "sky-weather-lazy-trigger",
    alt = "",
    src =
      "data:image/gif;base64,"
      .. "R0lGODlhAQABAIAAAAAAAP///ywAAAAAAQABAAACAUwAOw==",
    onload = function()
      sj.refreshWeatherInBackground(key)
    end
  }
end

function sj.refreshWeatherInBackground(expectedKey)
  local key = sj.weatherConfigKey()
  if expectedKey ~= nil and key ~= expectedKey then
    return
  end

  if sj._weatherLoading[key] then
    return
  end

  sj._weatherLoading[key] = true

  -- This network work runs from a DOM event after the rest of the
  -- Dashboard has already rendered.
  local data = sj.fetchWeatherData()
  local record = {
    data = data,
    fetchedAt = os.time()
  }

  sj._weatherCache["render|" .. key] = record
  clientStore.set(sj.weatherForecastStoreKey(key), record)

  sj._weatherLoading[key] = false
  codeWidget.refreshAll()
end

function sj.weatherForecastDay(day)
  return dom.div {
    class = "sky-weather-forecast-day",
    dom.div {
      class = "sky-weather-forecast-label",
      day.label
    },
    dom.div {
      class = "sky-weather-forecast-icon",
      sj.weatherIcon(day.code, 1)
    },
    dom.div {
      class = "sky-weather-forecast-temp",
      dom.strong {
        sj.roundTemperature(day.high) .. "°"
      },
      dom.span {
        sj.roundTemperature(day.low) .. "°"
      }
    }
  }
end

function sj.weatherSkeletonDay(label)
  return dom.div {
    class =
      "sky-weather-forecast-day sky-weather-skeleton-day",
    dom.div {
      class = "sky-weather-forecast-label",
      label
    },
    dom.div {
      class =
        "sky-weather-skeleton "
        .. "sky-weather-skeleton-icon"
    },
    dom.div {
      class =
        "sky-weather-skeleton "
        .. "sky-weather-skeleton-line"
    }
  }
end

function sj.weatherLoadingCard(config, key)
  local location = config.location
  if location == "" then
    location = "正在定位航线"
  end

  return widget.htmlBlock(
    dom.div {
      class =
        "sky-card sky-weather-card "
        .. "sky-weather-loading-card",
      dom.div {
        class = "sky-weather-header",
        dom.div {
          dom.div {
            class = "sky-weather-title",
            "✦ WEATHER ROUTE ✦"
          },
          dom.div {
            class = "sky-weather-location",
            location
          }
        },
        sj.pageActionLink(
          sj.configPage,
          "设置",
          "打开 Sky Journal 配置页面"
        )
      },
      dom.div {
        class = "sky-weather-current",
        dom.div {
          class =
            "sky-weather-skeleton "
            .. "sky-weather-skeleton-current-icon"
        },
        dom.div {
          class = "sky-weather-current-copy",
          dom.div {
            class =
              "sky-weather-skeleton "
              .. "sky-weather-skeleton-temp"
          },
          dom.div {
            class =
              "sky-weather-skeleton "
              .. "sky-weather-skeleton-desc"
          }
        }
      },
      dom.div {
        class =
          "sky-weather-rain "
          .. "sky-weather-skeleton-rain",
        dom.div {
          class =
            "sky-weather-skeleton "
            .. "sky-weather-skeleton-rain-icon"
        },
        dom.div {
          class =
            "sky-weather-skeleton "
            .. "sky-weather-skeleton-rain-copy"
        }
      },
      dom.div {
        class = "sky-weather-forecast-grid",
        sj.weatherSkeletonDay("明天"),
        sj.weatherSkeletonDay("后天"),
        sj.weatherSkeletonDay("大后天")
      },
      dom.div {
        class = "sky-weather-attribution",
        "FETCHING · OPEN-METEO"
      },
      sj.weatherLazyTrigger(key)
    }
  )
end

function sj.weatherErrorCard(data, trigger)
  local card = {
    class =
      "sky-card sky-weather-card sky-weather-error-card",
    dom.div {
      class = "sky-weather-header",
      dom.div {
        dom.div {
          class = "sky-weather-title",
          "✦ WEATHER ROUTE ✦"
        },
        dom.div {
          class = "sky-weather-location",
          data.location or "天气航线"
        }
      },
      sj.pageActionLink(
        sj.configPage,
        "设置",
        "打开 Sky Journal 配置页面"
      )
    },
    dom.div {
      class = "sky-weather-error-body",
      dom.div {
        class = "sky-weather-error-icon",
        "☁️"
      },
      dom.div {
        class = "sky-weather-error-title",
        "无法载入天气"
      },
      dom.div {
        class = "sky-weather-error-message",
        data.error or "请检查位置和网络设置"
      }
    },
    dom.div {
      class = "sky-weather-attribution",
      "DATA · OPEN-METEO"
    }
  }

  if trigger ~= nil then
    table.insert(card, trigger)
  end

  return widget.htmlBlock(dom.div(card))
end

function sj.weatherDataCard(data, stale, trigger)
  local forecastNodes = {
    class = "sky-weather-forecast-grid"
  }
  for _, day in ipairs(data.forecast or {}) do
    table.insert(
      forecastNodes,
      sj.weatherForecastDay(day)
    )
  end

  local cardClass = "sky-card sky-weather-card"
  if stale then
    cardClass = cardClass .. " sky-weather-stale"
  end

  local card = {
    class = cardClass,
    dom.div {
      class = "sky-weather-header",
      dom.div {
        dom.div {
          class = "sky-weather-title",
          "✦ WEATHER ROUTE ✦"
        },
        dom.div {
          class = "sky-weather-location",
          data.location or "天气航线"
        }
      },
      sj.pageActionLink(
        sj.configPage,
        "设置",
        "打开 Sky Journal 配置页面"
      )
    },
    dom.div {
      class = "sky-weather-current",
      dom.div {
        class = "sky-weather-current-icon",
        sj.weatherIcon(data.currentCode, data.isDay)
      },
      dom.div {
        class = "sky-weather-current-copy",
        dom.div {
          class = "sky-weather-current-temp",
          sj.roundTemperature(data.currentTemperature),
          dom.span { "°C" }
        },
        dom.div {
          class = "sky-weather-current-desc",
          sj.weatherDescription(data.currentCode)
        }
      }
    },
    dom.div {
      class =
        "sky-weather-rain"
        .. tostring(data.rainClass or ""),
      dom.span {
        class = "sky-weather-rain-icon",
        "☂"
      },
      dom.div {
        dom.strong {
          data.rainText or "降雨信息更新中"
        },
        dom.span {
          "未来 12 小时最高降雨概率 "
          .. tostring(data.maxRain or 0)
          .. "%"
        }
      }
    },
    dom.div(forecastNodes),
    dom.div {
      class = "sky-weather-attribution",
      stale
        and "UPDATING · OPEN-METEO"
        or "FORECAST · OPEN-METEO"
    }
  }

  if trigger ~= nil then
    table.insert(card, trigger)
  end

  return widget.htmlBlock(dom.div(card))
end

function sj.weather()
  local record, key, config = sj.weatherCacheRecord()

  -- First visit: render a fixed-size skeleton immediately, then fetch.
  if record == nil then
    return sj.weatherLoadingCard(config, key)
  end

  local fresh = sj.weatherRecordFresh(record)
  local trigger = nil
  if not fresh then
    trigger = sj.weatherLazyTrigger(key)
  end

  if record.data == nil then
    return sj.weatherLoadingCard(config, key)
  end

  if record.data.error ~= nil then
    return sj.weatherErrorCard(record.data, trigger)
  end

  -- Stale-while-revalidate: old data is visible instantly while the
  -- refresh runs after render.
  return sj.weatherDataCard(
    record.data,
    not fresh,
    trigger
  )
end
```

## 🛫 06｜快捷导航

生成 AIRSHIP CONTROL PANEL 导航入口。

> **自定义提示：** 在 `sj.quickNav()` 中增删 `dom.a`。

```space-lua
-- priority: 70

-- ================= QUICK NAV =================
function sj.quickNav()
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-nav",
      dom.div { "✦ AIRSHIP CONTROL PANEL ✦" },
      dom.div {
        dom.a { href = "Journal", "📖 Journal" },
        dom.a { href = "Project", "⚔ Project" },
        dom.a { href = "Area", "🧭 Area" },
        dom.a { href = "Archive", "🗄 Archive" },
        dom.a { href = "Tasks", "📋 Tasks" },
        dom.a { href = "Tags", "🏷 Tags" },
        dom.a { href = "Favorites", "⭐ Favorites" },
        dom.a { href = "Character Studio", "🎨 Character" },
        dom.a { href = "Theme Workshop", "🛠 Theme" }
      }
    }
  )
end
```

## 🏷️ 07｜标签统计、卡片与 Tags 页面

生成首页标签卡、标签引用统计和完整 Tags 板块页。

> **自定义提示：** 排序逻辑位于 `sj.collectTags()`；不要删除目录过滤。

```space-lua
-- priority: 65

-- ================= TAG CONSTELLATION =================
function sj.collectTags(applyConfiguredExclusions)
  local rows = query[[
    from t = index.tag "tag"
    where t.name ~= nil
    select t
  ]]

  local counts = {}
  local totalUses = 0

  for _, row in ipairs(rows) do
    local name = tostring(row.name)
    local allowed = applyConfiguredExclusions ~= true
      or sj.dashboardObjectAllowed(row)

    if allowed
      and name ~= ""
      and name ~= "meta"
      and name ~= "dashboard-flag"
      and not name:startsWith("meta/")
    then
      counts[name] = (counts[name] or 0) + 1
      totalUses = totalUses + 1
    end
  end

  local tags = {}
  for name, count in pairs(counts) do
    table.insert(
      tags,
      {
        name = name,
        count = count
      }
    )
  end

  table.sort(
    tags,
    function(a, b)
      if a.count == b.count then
        return string.lower(a.name) < string.lower(b.name)
      end
      return a.count > b.count
    end
  )

  return tags, totalUses
end

function sj.tagChip(tagInfo, large)
  local chipClass = "sky-tag-chip"
  if large then
    chipClass = chipClass .. " sky-tag-chip-large"
  end

  return dom.button {
    type = "button",
    class = chipClass,
    title = "查看 #" .. tagInfo.name .. " 的全部引用",
    onclick = function()
      editor.navigate("tag:" .. tagInfo.name)
    end,
    dom.span {
      class = "sky-tag-name",
      "#" .. tagInfo.name
    },
    dom.span {
      class = "sky-tag-count",
      tostring(tagInfo.count)
    }
  }
end

function sj.tagsCard()
  sj.installDashboardTagFit()

  local tags, totalUses = sj.collectTags(true)
  local cloud = {
    class = "sky-tag-cloud"
  }

  if tags[1] == nil then
    table.insert(
      cloud,
      sj.emptyRow("当前 Space 中还没有可展示的标签。")
    )
  else
    for _, tagInfo in ipairs(tags) do
      table.insert(cloud, sj.tagChip(tagInfo, false))
    end
  end

  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-tags-card",
      dom.div {
        class = "sky-tags-header",
        dom.div {
          dom.div {
            class = "sky-tags-title",
            "✦ TAG CONSTELLATION ✦"
          },
          dom.div {
            class = "sky-tags-subtitle",
            "使用频率最高的标签集合"
          }
        },
        sj.pageActionLink(
          "Tags",
          "查看更多",
          "打开全部标签页面"
        )
      },
      dom.div(cloud),
      dom.div {
        class = "sky-tags-footer",
        dom.span {
          tostring(#tags) .. " 个标签"
        },
        dom.span {
          tostring(totalUses) .. " 次引用"
        }
      }
    }
  )
end

-- 保留旧名称，避免 Dashboard 或其他页面仍调用 sj.status() 时失效
function sj.status()
  return sj.tagsCard()
end

function sj.tagsPage()
  local tags, totalUses = sj.collectTags(true)
  local body = {
    class = "sky-tag-index-grid"
  }

  if tags[1] == nil then
    table.insert(
      body,
      sj.emptyRow("当前 Space 中还没有可展示的标签。")
    )
  else
    for _, tagInfo in ipairs(tags) do
      table.insert(body, sj.tagChip(tagInfo, true))
    end
  end

  local topTag = "—"
  if tags[1] ~= nil then
    topTag = "#" .. tags[1].name .. " · " .. tostring(tags[1].count)
  end

  return widget.htmlBlock(
    dom.div {
      class = sj.themeRootClass("sky-section-page sky-tags-page"),
      dom.div {
        class = "sky-section-page-hero sky-tags-page-hero",
        dom.div {
          class = "sky-section-page-kicker",
          "SKY JOURNAL / KNOWLEDGE CONSTELLATION"
        },
        dom.div {
          class = "sky-section-page-title",
          "🏷 TAGS"
        },
        dom.div {
          class = "sky-section-page-subtitle",
          "浏览排除指定目录后仍保留的全部标签。点击任意标签可进入 SilverBullet 对应的虚拟标签页面。"
        }
      },
      dom.div {
        class = "sky-section-page-toolbar",
        dom.a {
          href = "index",
          class = "sky-back-btn",
          "← 返回飞空艇驾驶舱"
        }
      },
      dom.div {
        class = "sky-section-page-stats",
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "UNIQUE TAGS" },
          dom.strong { tostring(#tags) }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "TOTAL REFERENCES" },
          dom.strong { tostring(totalUses) }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "MOST USED" },
          dom.strong { topTag }
        }
      },
      dom.div {
        class = "sky-card sky-list-card sky-section-index-card sky-tags-index-card",
        dom.div {
          class = "sky-list-header",
          dom.div {
            class = "sky-list-heading",
            dom.div {
              class = "sky-list-title",
              "✦ ALL TAGS ✦"
            },
            dom.div {
              class = "sky-list-subtitle",
              "按引用次数从高到低排列"
            }
          }
        },
        dom.div(body)
      },
      dom.div {
        class = "sky-section-page-note",
        "标签统计来源于 Object Index；新标签会在索引更新后自动出现。"
      }
    }
  )
end
```

## 📝 08｜最近笔记

显示最近修改的 8 篇内容笔记。

> **自定义提示：** 修改 `sj.recentNotes()` 查询中的 `limit 8`。

```space-lua
-- priority: 60

-- ================= RECENT NOTES =================
function sj.recentNotes()
  local pages = query[[
    from p = index.contentPages()
    where p.name ~= "Index"
      and p.name ~= "index"
      and not p.name:startsWith("Library/")
    order by p.lastModified desc
    limit 8
    select p
  ]]
  local body = {
    class = "sky-list-body"
  }
  if pages[1] == nil then
    table.insert(body, sj.emptyRow("暂无最近笔记"))
  else
    for _, page in ipairs(pages) do
      table.insert(body, sj.pageRow(page, nil))
    end
  end
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-list-card sky-recent-card",
      sj.listHeader(
        "✦",
        "RECENT FLIGHT LOG",
        "最近更新的 8 篇笔记",
        "Journal"
      ),
      dom.div(body)
    }
  )
end
```

## ⚑ 09｜Active Missions

显示过滤后的未完成任务，首页最多 8 条。

> **自定义提示：** 修改数量时同步调整判断条件和副标题。

```space-lua
-- priority: 55

-- ================= OPEN TASKS =================
function sj.openTasks()
  local indexedTasks = query[[
    from t = index.tasks()
    where not t.done
    select t
  ]]

  local tasks = {}
  for _, task in ipairs(indexedTasks) do
    if sj.dashboardObjectAllowed(task) then
      table.insert(tasks, task)
      if #tasks >= 8 then
        break
      end
    end
  end

  local body = {
    class = "sky-list-body"
  }
  if tasks[1] == nil then
    table.insert(body, sj.emptyRow("当前没有未完成任务，飞空艇状态良好。"))
  else
    for _, task in ipairs(tasks) do
      table.insert(body, sj.taskRow(task))
    end
  end
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-list-card sky-task-card",
      dom.div {
        class = "sky-list-header",
        dom.div {
          class = "sky-list-heading",
          dom.div {
            class = "sky-list-title",
            "⚑ ACTIVE MISSIONS"
          },
          dom.div {
            class = "sky-list-subtitle",
            "最多显示 8 项未完成任务"
          }
        },
        dom.button {
          type = "button",
          class = "sky-create-btn sky-all-tasks-btn",
          title = "打开全部未完成任务",
          onclick = function()
            editor.navigate("Tasks")
          end,
          dom.span {
            class = "sky-create-btn-label",
            "全部任务"
          }
        }
      },
      dom.div(body)
    }
  )
end
```

## 🗂️ 10｜PARA 文件夹卡片

生成 Journal、Project、Area、Archive 四类摘要卡片。

> **自定义提示：** 目录名、标题、图标和说明位于四个 `sj.*List()` 函数。

```space-lua
-- priority: 50

-- ================= PARA FOLDER CARD =================
function sj.folderList(folder, title, icon, description)
  local pages = query[[
    from p = index.subPages(folder)
    order by p.lastModified desc
    limit 8
    select p
  ]]
  local body = {
    class = "sky-list-body"
  }
  if pages[1] == nil then
    table.insert(body, sj.emptyRow("这个航区还没有笔记。"))
  else
    for _, page in ipairs(pages) do
      table.insert(body, sj.pageRow(page, folder))
    end
  end
  return widget.htmlBlock(
    dom.div {
      class = "sky-card sky-list-card sky-folder-card",
      sj.listHeader(icon, title, description, folder),
      dom.div(body),
      dom.a {
        href = folder,
        class = "sky-folder-more",
        "查看全部 " .. folder .. " →"
      }
    }
  )
end

function sj.journalList()
  return sj.folderList(
    "Journal",
    "JOURNAL",
    "📖",
    "日志、随记与每日航行记录"
  )
end

function sj.projectList()
  return sj.folderList(
    "Project",
    "PROJECT",
    "⚔",
    "正在推进并具有明确成果的任务"
  )
end

function sj.areaList()
  return sj.folderList(
    "Area",
    "AREA",
    "🧭",
    "需要长期维护的责任与关注领域"
  )
end

function sj.archiveList()
  return sj.folderList(
    "Archive",
    "ARCHIVE",
    "🗄",
    "已经结束或暂时封存的航行资料"
  )
end
```

## 📚 11｜完整文件夹索引页

生成四个 PARA 板块完整页面、统计卡和新建按钮。

> **自定义提示：** Lua 控制数据与文案，外观由主题 `.sky-section-page*` 控制。

```space-lua
-- priority: 45

-- ================= FULL FOLDER INDEX PAGES =================
function sj.folderIndexPage(folder, title, icon, description)
  local pages = query[[
    from p = index.subPages(folder)
    order by p.lastModified desc
    select p
  ]]
  local body = {
    class = "sky-list-body sky-folder-page-list"
  }
  if pages[1] == nil then
    table.insert(
      body,
      sj.emptyRow("这个航区还没有笔记。点击右上角按钮创建第一篇。")
    )
  else
    for _, page in ipairs(pages) do
      table.insert(body, sj.pageRow(page, folder))
    end
  end
  local pageCount = sj.countRows(pages)
  local latestDate = "—"
  if pages[1] ~= nil then
    latestDate = sj.shortDate(pages[1].lastModified)
  end
  return widget.htmlBlock(
    dom.div {
      class = sj.themeRootClass("sky-section-page"),
      dom.div {
        class = "sky-section-page-hero",
        dom.div {
          class = "sky-section-page-kicker",
          "SKY JOURNAL / " .. string.upper(folder)
        },
        dom.div {
          class = "sky-section-page-title",
          icon .. " " .. title
        },
        dom.div {
          class = "sky-section-page-subtitle",
          description
        }
      },
      dom.div {
        class = "sky-section-page-toolbar",
        dom.a {
          href = "index",
          class = "sky-back-btn",
          "← 返回飞空艇驾驶舱"
        },
        sj.newNoteButton(folder)
      },
      dom.div {
        class = "sky-section-page-stats",
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "TOTAL NOTES" },
          dom.strong { tostring(pageCount) }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "LAST UPDATE" },
          dom.strong { latestDate }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "ROUTE" },
          dom.strong { folder .. "/" }
        }
      },
      dom.div {
        class = "sky-card sky-list-card sky-section-index-card",
        sj.listHeader(
          icon,
          title .. " INDEX",
          "按最近修改时间排列，共 " .. tostring(pageCount) .. " 篇笔记",
          folder,
          false
        ),
        dom.div(body)
      },
      dom.div {
        class = "sky-section-page-note",
        "所有以 “" .. folder .. "/” 开头的页面都会自动汇入本清单。"
      }
    }
  )
end

function sj.journalPage()
  return sj.folderIndexPage(
    "Journal",
    "JOURNAL",
    "📖",
    "日志、随记与每日航行记录"
  )
end

function sj.projectPage()
  return sj.folderIndexPage(
    "Project",
    "PROJECT",
    "⚔",
    "正在推进并具有明确成果的任务"
  )
end

function sj.areaPage()
  return sj.folderIndexPage(
    "Area",
    "AREA",
    "🧭",
    "需要长期维护的责任与关注领域"
  )
end

function sj.archivePage()
  return sj.folderIndexPage(
    "Archive",
    "ARCHIVE",
    "🗄",
    "已经结束或暂时封存的航行资料"
  )
end
```

## 📋 12｜完整 Tasks 页面与主题模式

生成全部未完成任务页，并提供 `themeMode` 与根容器类。

> **自定义提示：** `themeMode` 支持 `system`、`light`、`dark`。

```space-lua
-- priority: 40

-- ================= FULL TASK INDEX PAGE =================
function sj.taskSourceCount(tasks)
  local sources = {}
  for _, task in ipairs(tasks) do
    local source = task.page or "Unknown"
    sources[source] = true
  end
  local count = 0
  for _, _ in pairs(sources) do
    count = count + 1
  end
  return count
end

function sj.tasksPage()
  local indexedTasks = query[[
    from t = index.tasks()
    where not t.done
    order by t.page asc
    select t
  ]]

  local tasks = {}
  for _, task in ipairs(indexedTasks) do
    if sj.dashboardObjectAllowed(task) then
      table.insert(tasks, task)
    end
  end

  local body = {
    class = "sky-list-body sky-folder-page-list sky-task-page-list"
  }
  if tasks[1] == nil then
    table.insert(
      body,
      sj.emptyRow("当前没有未完成任务，所有航线均已清空。")
    )
  else
    for _, task in ipairs(tasks) do
      table.insert(body, sj.taskRow(task))
    end
  end
  local taskCount = sj.countRows(tasks)
  local sourceCount = sj.taskSourceCount(tasks)
  return widget.htmlBlock(
    dom.div {
      class = sj.themeRootClass("sky-section-page"),
      dom.div {
        class = "sky-section-page-hero sky-task-page-hero",
        dom.div {
          class = "sky-section-page-kicker",
          "SKY JOURNAL / MISSION CONTROL"
        },
        dom.div {
          class = "sky-section-page-title",
          "⚑ ACTIVE MISSIONS"
        },
        dom.div {
          class = "sky-section-page-subtitle",
          "汇总排除指定目录后仍保留的未完成任务，并链接回任务所在页面。"
        }
      },
      dom.div {
        class = "sky-section-page-toolbar",
        dom.a {
          href = "index",
          class = "sky-back-btn",
          "← 返回飞空艇驾驶舱"
        }
      },
      dom.div {
        class = "sky-section-page-stats",
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "OPEN MISSIONS" },
          dom.strong { tostring(taskCount) }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "SOURCE PAGES" },
          dom.strong { tostring(sourceCount) }
        },
        dom.div {
          class = "sky-card sky-mini-stat",
          dom.span { "MISSION STATE" },
          dom.strong { "ACTIVE" }
        }
      },
      dom.div {
        class = "sky-card sky-list-card sky-section-index-card",
        dom.div {
          class = "sky-list-header",
          dom.div {
            class = "sky-list-heading",
            dom.div {
              class = "sky-list-title",
              "⚑ ALL OPEN TASKS"
            },
            dom.div {
              class = "sky-list-subtitle",
              "共 " .. tostring(taskCount) .. " 项未完成任务"
            }
          }
        },
        dom.div(body)
      },
      dom.div {
        class = "sky-section-page-note",
        "勾选任务后，索引更新时该任务会自动从本页面移除。"
      }
    }
  )
end

function sj.themeMode()
  local config = sj.configData()
  local mode = string.lower(tostring(config.themeMode or "system"))
  if mode ~= "light" and mode ~= "dark" and mode ~= "system" then
    return "system"
  end
  return mode
end

function sj.themeRootClass(baseClass)
  return baseClass
    .. " sky-theme-root sky-theme-"
    .. sj.themeMode()
end
```

## ✦ 13｜Footer

输出 Sky Journal 页脚状态文字。

> **自定义提示：** 修改 `sj.footer()` 中的文案或内联样式。

```space-lua
-- priority: 20

-- ================= FOOTER =================
function sj.footer()
  return widget.htmlBlock(
    dom.div {
      style = "text-align:center;padding:24px;color:#6c87a7;",
      "Sky Journal — Relink Flight System Active"
    }
  )
end
```

## 🖼️ 14｜可选图片层与初始化

提供 `sj.art(url)`，并在所有函数加载后安装标签动态适配器。

> **自定义提示：** 必须保留末尾 `sj.installDashboardTagFit()`。

```space-lua
-- priority: 10

-- ================= OPTIONAL IMAGE LAYER =================
function sj.art(url)
  return widget.htmlBlock(
    dom.img {
      src = url,
      class = "sky-art"
    }
  )
end

sj.installDashboardTagFit()
```
