# HideIndexToC

## 功能说明

本 Markdown 文档中的 space-lua 作用是隐藏 index 页面中的 ToC。

```space-lua
-- priority: 9
local originalToc = widgets.toc
function widgets.toc(options)
  if editor.getCurrentPage() == "index" then
    return nil
  end
  return originalToc(options)
end
```
