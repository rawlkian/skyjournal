# 功能页面保护

## 功能说明

本 Markdown 内的得 space-lua 用于锁定 SkyJournal 功能页面，如：主页、各板块详情页，使这些页面无法被编辑以增强使用体验。如需增减页面请在 sjPreviewPages 中新增条目或切换 true/false。

SkyJournal 使用了 #<dashboard-flag> 作为顶部锚点书签，用于避免跳转页面时定位于函数行导致界面无法渲染成功。

```space-lua
-- priority: 5
local sjPreviewPages = {
  ["index"] = true,
  ["journal"] = true,
  ["project"] = true,
  ["area"] = true,
  ["tasks"] = true,
  ["tags"] = true,
  ["archive"] = true
}
local sjTemporaryEditPage = nil
local function sjNormalizePageName(pageName)
  return string.lower(pageName or "")
end
local function sjSetPreviewClass(enabled)
  local root = js.window.document.documentElement
  if enabled then
    root.classList.add("sj-dashboard-preview")
  else
    root.classList.remove("sj-dashboard-preview")
  end
end
local function sjSetTitleReadOnly(enabled)
  local titleEditor = js.window.document.querySelector(".sb-mini-editor .cm-content")
  if titleEditor == nil then
    return
  end
  if enabled then
    titleEditor.contentEditable = "false"
  else
    titleEditor.contentEditable = "true"
  end
end
local function sjInstallDashboardKeyGuard()
  local markerId = "sj-dashboard-key-guard-installed"
  if js.window.document.getElementById(markerId) ~= nil then
    return
  end
  local marker = js.window.document.createElement("meta")
  marker.id = markerId
  js.window.document.head.appendChild(marker)
  js.window.addEventListener("keydown", function(e)
    local root = js.window.document.documentElement
    if not root.classList.contains("sj-dashboard-preview") then
      return
    end
    local key = string.lower(e.key or "")
    local isSelectAll = (key == "a" or e.code == "KeyA") and (e.ctrlKey == true or e.metaKey == true)
    if not isSelectAll then
      return
    end
    local target = e.target
    if target ~= nil then
      local tagName = string.lower(target.tagName or "")
      if tagName == "input" or tagName == "textarea" or tagName == "select" then
        return
      end
      if target.closest ~= nil then
        local editableWidget = target.closest(".sb-widget [contenteditable='true'], .sb-code-widget [contenteditable='true'], .sb-lua-directive-block [contenteditable='true']")
        if editableWidget ~= nil then
          return
        end
      end
    end
    e.preventDefault()
    e.stopPropagation()
    e.stopImmediatePropagation()
  end, true)
end
local function sjSetDashboardPreview(enabled)
  sjSetPreviewClass(enabled)
  local currentMode = editor.getUiOption("forcedROMode") == true
  if currentMode ~= enabled then
    editor.setUiOption("forcedROMode", enabled)
    editor.rebuildEditorState()
  end
  sjSetTitleReadOnly(enabled)
  if enabled then
    editor.moveCursor(0, false)
  end
end
local function sjApplyDashboardPreview()
  local pageName = sjNormalizePageName(editor.getCurrentPage())
  local isPreviewPage = sjPreviewPages[pageName] == true
  if sjTemporaryEditPage ~= nil and sjTemporaryEditPage ~= pageName then
    sjTemporaryEditPage = nil
  end
  local shouldPreview = isPreviewPage and sjTemporaryEditPage ~= pageName
  sjSetDashboardPreview(shouldPreview)
end
sjInstallDashboardKeyGuard()
event.listen {
  name = "editor:init",
  run = function()
    sjInstallDashboardKeyGuard()
    sjApplyDashboardPreview()
  end
}
event.listen {
  name = "editor:pageLoaded",
  run = function()
    sjInstallDashboardKeyGuard()
    sjApplyDashboardPreview()
  end
}
command.define {
  name = "SJ: Edit Dashboard Page",
  run = function()
    local pageName = sjNormalizePageName(editor.getCurrentPage())
    if sjPreviewPages[pageName] ~= true then
      editor.flashNotification("当前页面不是 Dashboard 页面。")
      return
    end
    sjTemporaryEditPage = pageName
    sjSetDashboardPreview(false)
    editor.flashNotification("Dashboard 已切换为编辑模式。")
  end
}
command.define {
  name = "SJ: Preview Dashboard Page",
  run = function()
    local pageName = sjNormalizePageName(editor.getCurrentPage())
    if sjPreviewPages[pageName] ~= true then
      editor.flashNotification("当前页面不是 Dashboard 页面。")
      return
    end
    sjTemporaryEditPage = nil
    sjSetDashboardPreview(true)
    editor.flashNotification("Dashboard 已恢复预览模式。")
  end
}
sjApplyDashboardPreview()
```

```space-style
html.sj-dashboard-preview #sb-main .cm-content {
  pointer-events: none !important;
  user-select: none !important;
  caret-color: transparent !important;
}
html.sj-dashboard-preview #sb-main .sb-lua-directive-block,
html.sj-dashboard-preview #sb-main .sb-lua-directive-block *,
html.sj-dashboard-preview #sb-main .sb-inline-content,
html.sj-dashboard-preview #sb-main .sb-inline-content *,
html.sj-dashboard-preview #sb-main .sb-code-widget,
html.sj-dashboard-preview #sb-main .sb-code-widget *,
html.sj-dashboard-preview #sb-main .sb-widget,
html.sj-dashboard-preview #sb-main .sb-widget *,
html.sj-dashboard-preview #sb-main a,
html.sj-dashboard-preview #sb-main button,
html.sj-dashboard-preview #sb-main input,
html.sj-dashboard-preview #sb-main select,
html.sj-dashboard-preview #sb-main textarea,
html.sj-dashboard-preview #sb-main [role="button"] {
  pointer-events: auto !important;
}
html.sj-dashboard-preview #sb-main input,
html.sj-dashboard-preview #sb-main select,
html.sj-dashboard-preview #sb-main textarea {
  user-select: text !important;
}
html.sj-dashboard-preview #sb-main .cm-line:has(.sb-hashtag[data-tag-name="dashboard-flag"]) {
  height: 0 !important;
  min-height: 0 !important;
  max-height: 0 !important;
  line-height: 0 !important;
  font-size: 0 !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  opacity: 0 !important;
  overflow: hidden !important;
  pointer-events: none !important;
  user-select: none !important;
}
html.sj-dashboard-preview #sb-main .sb-hashtag[data-tag-name="dashboard-flag"] {
  display: none !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
}
.sb-hashtag[data-tag-name="dashboard-flag"] {
  display: inline-flex;
  align-items: center;
  padding: 3px 9px;
  border: 1px dashed var(--ui-accent-color);
  border-radius: 999px;
  opacity: 0.65;
  font-size: 0.72rem;
  font-family: monospace;
}
.sb-hashtag[data-tag-name="dashboard-flag"]::before {
  content: "DASHBOARD · ";
  font-weight: 700;
}
```
