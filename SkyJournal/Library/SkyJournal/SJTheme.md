# ✦ SKY JOURNAL GLOBAL THEME ✦

> **版本：v1.8.63**  
> White / Azure / Gold · Deep Navy / Azure / Gold

```text
        .       *        ✦
   ┌──────────────────────────┐
   │   SKY JOURNAL AIRSHIP    │
   │   GLOBAL THEME SYSTEM    │
   └──────────────────────────┘
          \  |  /
       ----  ✦  ----
          /  |  \
```

## 🐺主题说明

SkyJournal 是一款以"碧蓝幻想Relink"作为主设计概念的 SilverBullet 主题兼管理系统。配色主要以天蓝色与淡金色为主，部分 Markdown 渲染样式参考了 Typora 的 Phycat 主题系列。

本文档是完整的主题文件，同时也按照功能拆分并补充了说明，亦可作为 README 阅读。

## 🔤 零加载字体方案

本主题不使用任何 `@font-face`、外部字体文件、预载入脚本或字体服务器。

字体按用途交给操作系统选择：

- **标题与 Dashboard 大标题**：系统衬线字体，保留航海日志与古典幻想感；
- **正文、标题栏、按钮与界面**：系统 UI 无衬线字体，保证跨平台清晰稳定；
- **代码与 Frontmatter**：系统等宽字体；
- **中文字符**：自动使用设备自带的 CJK 字体。

因此页面切换、刷新和 PWA 启动时都不会再发生网络字体下载或回退字体替换。

如需使用自定义字体，请自行编写覆盖用 space-style。但需要注意，SilverBullet 对于静态资源的处理并不算好，可能会影响页面的加载与跳转、刷新速度。可以考虑使用外部在线字体，但配置较麻烦。

## 🗺️ 功能导航

| 区域 | 内容 |
|---|---|
| 01–04 | 主题令牌、背景、基础组件、编辑器正文 |
| 05–06 | SilverBullet 原生界面、字体与阅读布局 |
| 07–09 | Markdown 内容、代码块、TOC、Frontmatter、Widget |
| 10–12 | 移动端标题栏、Dashboard、更多菜单 |
| 13 | 保存状态与 Page Decoration Prefix 对齐 |
| 14 | PWA 安全区域与浏览器系统栏动态取色 |

---

## 🎨 01｜设计令牌与亮暗色调色板

定义全局圆角、颜色、表面、阴影以及 SilverBullet 原生主题变量，是整套主题的基础。

```space-style
/* priority: 20 */

/* =========================================================
   SKY JOURNAL GLOBAL THEME v1.8.63 UNIFIED NATIVE HASHTAGS
   White / Azure / Gold · Deep Navy / Azure / Gold
   ========================================================= */

/* ================= FONT & SHARED TOKENS ================= */

html {
  --sj-radius-xs: 7px;
  --sj-radius-sm: 11px;
  --sj-radius-md: 16px;
  --sj-radius-lg: 22px;
  --sj-radius-pill: 999px;

  /* Original SJ Theme compatibility tokens */
  --sj-radius: 18px;
  --sj-card: var(--sj-surface);
  --sj-card-border: rgba(125, 182, 255, .25);
  --sj-card-shadow: 0 12px 28px rgba(80, 140, 200, .10);
  --sj-corner-color: rgba(212, 177, 106, .65);
  --sj-hero-background: linear-gradient(135deg, #ffffff, #edf6ff);
  --sj-hero-glow: rgba(212, 177, 106, .14);
  --sj-nav-background: linear-gradient(180deg, #ffffff, #f4f9ff);
  --sj-art-shadow: 0 10px 26px rgba(120, 170, 230, .12);

  --sj-blue: #79b8f4;
  --sj-blue-strong: #3978b7;
  --sj-blue-deep: #294f76;
  --sj-gold: #d1ad66;
  --sj-green: #5daf82;
  --sj-red: #d66c72;
  --sj-orange: #d99754;

  --sj-text: #294967;
  --sj-text-soft: #6e88a2;
  --sj-text-faint: #9cb0c2;

  --sj-surface: rgba(255, 255, 255, .88);
  --sj-surface-solid: #ffffff;
  --sj-surface-soft: rgba(244, 249, 255, .88);
  --sj-surface-hover: rgba(232, 244, 255, .94);
  --sj-border: rgba(112, 173, 230, .26);
  --sj-border-strong: rgba(74, 139, 199, .38);
  --sj-shadow:
    0 12px 30px rgba(61, 116, 166, .10),
    0 2px 8px rgba(61, 116, 166, .05);

  --sj-page-background:
    radial-gradient(circle at 12% 8%, rgba(121, 184, 244, .22), transparent 38%),
    radial-gradient(circle at 88% 14%, rgba(209, 173, 102, .10), transparent 40%),
    radial-gradient(circle at 52% 94%, rgba(151, 206, 248, .17), transparent 48%),
    linear-gradient(180deg, #fbfdff 0%, #eef7ff 100%);

  font-size: 16.5px;

  /* SilverBullet core variables — light defaults */
  --ui-accent-color: #3978b7;
  --ui-accent-text-color: #3978b7;
  --ui-accent-contrast-color: #ffffff;

  --highlight-color: rgba(244, 205, 96, .34);
  --link-color: #3279bd;
  --link-missing-color: #bd6b2f;
  --link-invalid-color: #a05eaa;

  --meta-color: #8d5d72;
  --meta-subtle-color: #91a5b8;
  --subtle-color: #71879c;
  --subtle-background-color: rgba(87, 142, 191, .09);

  --root-background-color: #f5faff;
  --root-color: #294967;

  --top-color: #294967;
  --top-background-color: rgba(250, 253, 255, .94);
  --top-border-color: rgba(112, 173, 230, .25);
  --top-sync-error-color: #a85252;
  --top-sync-error-background-color: #fff0ee;
  --top-saved-color: #4c946d;
  --top-unsaved-color: #b87b39;
  --top-loading-color: #3978b7;

  --panel-background-color: rgba(248, 252, 255, .97);
  --panel-border-color: rgba(112, 173, 230, .25);

  --bhs-background-color: #ffffff;
  --bhs-border-color: rgba(112, 173, 230, .28);

  --modal-color: #294967;
  --modal-background-color: #fbfdff;
  --modal-border-color: rgba(74, 139, 199, .34);
  --modal-backdrop-color: rgba(29, 64, 96, .18);
  --modal-header-label-color: #3978b7;
  --modal-help-background-color: #edf6ff;
  --modal-help-color: #5f7891;
  --modal-selected-option-background-color: #3978b7;
  --modal-selected-option-color: #ffffff;
  --modal-hint-background-color: #dceeff;
  --modal-hint-color: #294967;
  --modal-hint-inactive-background-color: #eef5fb;
  --modal-hint-inactive-color: #71879c;
  --modal-description-color: #71879c;
  --modal-selected-option-description-color: #dceeff;

  --notifications-background-color: #ffffff;
  --notifications-border-color: rgba(74, 139, 199, .35);
  --notification-info-background-color: #dcedff;
  --notification-error-background-color: #ffe3e4;
  --notification-warning-background-color: #fff0d3;

  --button-background-color: #f2f8fe;
  --button-hover-background-color: #e6f2fc;
  --button-color: #294967;
  --button-border-color: rgba(74, 139, 199, .30);
  --primary-button-background-color: #3978b7;
  --primary-button-hover-background-color: #2e669b;
  --primary-button-color: #ffffff;
  --primary-button-border-color: transparent;

  --text-field-background-color: rgba(255, 255, 255, .96);

  --progress-background-color: #dceaf6;
  --progress-sync-color: #3978b7;
  --progress-index-color: #d1ad66;

  --action-button-background-color: transparent;
  --action-button-color: #63809b;
  --action-button-hover-color: #3978b7;
  --action-button-active-color: #d1ad66;

  --editor-caret-color: #294967;
  --editor-selection-background-color: rgba(121, 184, 244, .24);

  --editor-panels-bottom-color: #294967;
  --editor-panels-bottom-background-color: #f6fbff;
  --editor-panels-bottom-border-color: rgba(112, 173, 230, .24);
  --editor-panels-bottom-input-background-color: #ffffff;
  --editor-panels-bottom-button-background-image:
    linear-gradient(#ffffff, #edf6ff);
  --editor-panels-bottom-button-active-background-image:
    linear-gradient(#dcecff, #eef7ff);

  --editor-completion-detail-color: #7890a7;
  --editor-completion-detail-selected-color: #eaf5ff;
  --editor-list-bullet-color: #75a6d0;

  --editor-heading-color: #294967;
  --editor-heading-meta-color: #9aafc1;

  --editor-hashtag-background-color: rgba(121, 184, 244, .14);
  --editor-hashtag-color: #3978b7;
  --editor-hashtag-border-color: rgba(57, 120, 183, .22);

  --editor-ruler-color: rgba(112, 173, 230, .26);
  --editor-naked-url-color: #3279bd;
  --editor-code-color: #6c7f91;

  --editor-link-color: #3279bd;
  --editor-link-url-color: #7893aa;
  --editor-link-meta-color: #9aafc1;

  --editor-wiki-link-page-background-color: rgba(121, 184, 244, .09);
  --editor-wiki-link-page-color: #3279bd;
  --editor-wiki-link-page-missing-color: #bd6b2f;
  --editor-wiki-link-page-invalid-color: #a05eaa;
  --editor-wiki-link-color: #667ca2;

  --editor-command-button-color: #294967;
  --editor-command-button-background-color: #edf6ff;
  --editor-command-button-hover-background-color: #dfefff;
  --editor-command-button-meta-color: #8499ad;
  --editor-command-button-border-color: rgba(74, 139, 199, .24);

  --editor-line-meta-color: #9aafc1;
  --editor-meta-color: #8d5d72;

  --editor-table-head-background-color: #deedfb;
  --editor-table-head-color: #294967;
  --editor-table-even-background-color: rgba(224, 239, 252, .42);

  --editor-blockquote-background-color: rgba(230, 242, 252, .64);
  --editor-blockquote-color: #526f89;
  --editor-blockquote-border-color: #d1ad66;

  --editor-code-background-color: rgba(222, 237, 250, .56);
  --editor-struct-color: #b65f68;
  --editor-highlight-background-color: rgba(244, 205, 96, .34);
  --editor-code-comment-color: #8ba0b3;
  --editor-code-variable-color: #3978b7;
  --editor-code-typename-color: #548f68;
  --editor-code-string-color: #9a6b35;
  --editor-code-number-color: #8b67a3;
  --editor-code-operator-color: #73889b;
  --editor-code-info-color: #8298ac;
  --editor-code-atom-color: #b65f68;

  --editor-frontmatter-background-color: rgba(245, 232, 190, .31);
  --editor-frontmatter-color: #71879c;
  --editor-frontmatter-marker-color: #b88b3f;

  --editor-widget-background-color: rgba(236, 246, 255, .72);
  --editor-task-marker-color: #6f8aa2;
  --editor-task-state-color: #6f8aa2;

  --editor-directive-mark-color: #9d6469;
  --editor-directive-color: #6f8295;
  --editor-directive-background-color: rgba(225, 239, 252, .58);

  --danger-color: #d66c72;
  --danger-contrast-color: #ffffff;
  --success-color: #5daf82;

  --alert-error-background-color: #fff0f1;
  --alert-error-color: #b64e56;
  --alert-error-border-color: #efc1c5;
  --alert-warning-background-color: #fff7e7;
  --alert-warning-color: #9b692d;
  --alert-warning-border-color: #ecd6aa;
  --alert-info-background-color: #edf7ff;
  --alert-info-color: #3978b7;
  --alert-info-border-color: #c7e1f5;

  --badge-background-color: #e1f0fd;
  --badge-color: #3978b7;
}

/* ================= DARK MODE TOKENS ================= */

html[data-theme="dark"] {
  color-scheme: dark;

  --sj-blue: #7fc5ff;
  --sj-blue-strong: #61a9e7;
  --sj-blue-deep: #b7dcff;
  --sj-gold: #e4bd70;
  --sj-green: #70c797;
  --sj-red: #ef8389;
  --sj-orange: #e6a15e;

  --sj-text: #e6f1fb;
  --sj-text-soft: #9bb2c8;
  --sj-text-faint: #70879b;

  --sj-surface: rgba(13, 29, 46, .91);
  --sj-surface-solid: #0e2032;
  --sj-surface-soft: rgba(18, 39, 59, .90);
  --sj-surface-hover: rgba(26, 52, 76, .94);
  --sj-border: rgba(105, 181, 242, .20);
  --sj-border-strong: rgba(127, 197, 255, .34);
  --sj-shadow:
    0 15px 35px rgba(0, 0, 0, .32),
    0 2px 10px rgba(0, 0, 0, .20);

  --sj-page-background:
    radial-gradient(circle at 12% 8%, rgba(56, 135, 198, .19), transparent 38%),
    radial-gradient(circle at 88% 14%, rgba(228, 189, 112, .08), transparent 40%),
    radial-gradient(circle at 52% 94%, rgba(38, 91, 134, .17), transparent 48%),
    linear-gradient(180deg, #0a1725 0%, #06101a 100%);

  /* Original SJ Theme components in dark mode */
  --sj-card: var(--sj-surface);
  --sj-card-border: rgba(105, 181, 242, .20);
  --sj-card-shadow: 0 15px 35px rgba(0, 0, 0, .28);
  --sj-corner-color: rgba(228, 189, 112, .62);
  --sj-hero-background:
    radial-gradient(circle at center, rgba(228, 189, 112, .08), transparent 58%),
    linear-gradient(135deg, #10243a, #091522);
  --sj-hero-glow: rgba(228, 189, 112, .10);
  --sj-nav-background: linear-gradient(180deg, #183149, #102338);
  --sj-art-shadow: 0 12px 28px rgba(0, 0, 0, .26);

  --ui-accent-color: #61a9e7;
  --ui-accent-text-color: #9fd1fb;
  --ui-accent-contrast-color: #07121d;

  --highlight-color: rgba(228, 189, 112, .27);
  --link-color: #83c5ff;
  --link-missing-color: #e5a061;
  --link-invalid-color: #d594e2;

  --meta-color: #ef9399;
  --meta-subtle-color: #748da3;
  --subtle-color: #91a8bd;
  --subtle-background-color: rgba(105, 181, 242, .08);

  --root-background-color: #07121d;
  --root-color: #e6f1fb;

  --top-color: #e6f1fb;
  --top-background-color: rgba(10, 24, 38, .96);
  --top-border-color: rgba(105, 181, 242, .20);
  --top-sync-error-color: #ffd0d2;
  --top-sync-error-background-color: #572c31;
  --top-saved-color: #8bd6aa;
  --top-unsaved-color: #e7b572;
  --top-loading-color: #8bcaff;

  --panel-background-color: #081521;
  --panel-border-color: rgba(105, 181, 242, .18);

  --bhs-background-color: #0b1b2a;
  --bhs-border-color: rgba(105, 181, 242, .22);

  --modal-color: #e6f1fb;
  --modal-background-color: #0d2031;
  --modal-border-color: rgba(127, 197, 255, .31);
  --modal-backdrop-color: rgba(0, 0, 0, .54);
  --modal-header-label-color: #a8d7ff;
  --modal-help-background-color: #132b40;
  --modal-help-color: #abc0d2;
  --modal-selected-option-background-color: #315f88;
  --modal-selected-option-color: #ffffff;
  --modal-hint-background-color: #1b3b58;
  --modal-hint-color: #dceeff;
  --modal-hint-inactive-background-color: #13283b;
  --modal-hint-inactive-color: #8ea5b9;
  --modal-description-color: #879db1;
  --modal-selected-option-description-color: #d9eaff;

  --notifications-background-color: #102538;
  --notifications-border-color: rgba(127, 197, 255, .30);
  --notification-info-background-color: #174a70;
  --notification-error-background-color: #70333a;
  --notification-warning-background-color: #735528;

  --button-background-color: #142c41;
  --button-hover-background-color: #1d3c57;
  --button-color: #e6f1fb;
  --button-border-color: rgba(127, 197, 255, .25);
  --primary-button-background-color: #4c91ca;
  --primary-button-hover-background-color: #63a8df;
  --primary-button-color: #07121d;
  --primary-button-border-color: transparent;

  --text-field-background-color: #0d2031;

  --progress-background-color: #193248;
  --progress-sync-color: #8bcaff;
  --progress-index-color: #e4bd70;

  --action-button-background-color: transparent;
  --action-button-color: #8ea8be;
  --action-button-hover-color: #83c5ff;
  --action-button-active-color: #e4bd70;

  --editor-caret-color: #ffffff;
  --editor-selection-background-color: rgba(127, 197, 255, .20);

  --editor-panels-bottom-color: #e6f1fb;
  --editor-panels-bottom-background-color: #0d2031;
  --editor-panels-bottom-border-color: rgba(105, 181, 242, .20);
  --editor-panels-bottom-input-background-color: #0b1b2a;
  --editor-panels-bottom-button-background-image:
    linear-gradient(#18364f, #10283d);
  --editor-panels-bottom-button-active-background-image:
    linear-gradient(#0b1b2a, #18364f);

  --editor-completion-detail-color: #8da3b6;
  --editor-completion-detail-selected-color: #d7eafd;
  --editor-list-bullet-color: #7ea5c5;

  --editor-heading-color: #e4f2ff;
  --editor-heading-meta-color: #71889d;

  --editor-hashtag-background-color: rgba(97, 169, 231, .18);
  --editor-hashtag-color: #a8d7ff;
  --editor-hashtag-border-color: rgba(127, 197, 255, .27);

  --editor-ruler-color: rgba(105, 181, 242, .21);
  --editor-naked-url-color: #83c5ff;
  --editor-code-color: #a7bbcc;

  --editor-link-color: #83c5ff;
  --editor-link-url-color: #7f9bb2;
  --editor-link-meta-color: #71889d;

  --editor-wiki-link-page-background-color: rgba(97, 169, 231, .10);
  --editor-wiki-link-page-color: #83c5ff;
  --editor-wiki-link-page-missing-color: #e5a061;
  --editor-wiki-link-page-invalid-color: #d594e2;
  --editor-wiki-link-color: #a8bad5;

  --editor-command-button-color: #e6f1fb;
  --editor-command-button-background-color: #142c41;
  --editor-command-button-hover-background-color: #1d3c57;
  --editor-command-button-meta-color: #7f96aa;
  --editor-command-button-border-color: rgba(127, 197, 255, .23);

  --editor-line-meta-color: #71889d;
  --editor-meta-color: #ef9399;

  --editor-table-head-background-color: #16334b;
  --editor-table-head-color: #e8f5ff;
  --editor-table-even-background-color: rgba(22, 51, 75, .46);

  --editor-blockquote-background-color: rgba(17, 42, 62, .72);
  --editor-blockquote-color: #afc4d6;
  --editor-blockquote-border-color: #e4bd70;

  --editor-code-background-color: rgba(17, 42, 62, .82);
  --editor-struct-color: #ef8389;
  --editor-highlight-background-color: rgba(228, 189, 112, .27);
  --editor-code-comment-color: #748da3;
  --editor-code-variable-color: #7fc5ff;
  --editor-code-typename-color: #70c797;
  --editor-code-string-color: #e4bd70;
  --editor-code-number-color: #c9a1df;
  --editor-code-operator-color: #91a8bd;
  --editor-code-info-color: #8097aa;
  --editor-code-atom-color: #ef8389;

  --editor-frontmatter-background-color: rgba(88, 66, 28, .34);
  --editor-frontmatter-color: #aabaca;
  --editor-frontmatter-marker-color: #e4bd70;

  --editor-widget-background-color: rgba(18, 44, 65, .72);
  --editor-task-marker-color: #8ca7bd;
  --editor-task-state-color: #8ca7bd;

  --editor-directive-mark-color: #ef9399;
  --editor-directive-color: #9ab0c4;
  --editor-directive-background-color: rgba(21, 45, 66, .68);

  --danger-color: #ef8389;
  --danger-contrast-color: #07121d;
  --success-color: #70c797;

  --alert-error-background-color: #3f2428;
  --alert-error-color: #ffb7bb;
  --alert-error-border-color: #6d3a40;
  --alert-warning-background-color: #3d3320;
  --alert-warning-color: #f0ce92;
  --alert-warning-border-color: #65542f;
  --alert-info-background-color: #153047;
  --alert-info-color: #a9d8ff;
  --alert-info-border-color: #28506e;

  --badge-background-color: #173a55;
  --badge-color: #a8d7ff;
}
```

## ☁️ 02｜页面背景与 Sky Journal 基础组件

负责页面云层背景、Dashboard 通用网格、卡片、金色边角、Hero、导航胶囊与图片卡片。

```space-style
/* priority: 20 */

/* ================= PAGE BACKGROUND ================= */

html,
body,
#sb-root {
  background: var(--root-background-color);
  color: var(--root-color);
}

#sb-main {
  background: var(--sj-page-background) !important;
  color: var(--sj-text);
}

#sb-main::before {
  content: "";
  position: fixed;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background:
    repeating-linear-gradient(
      -14deg,
      transparent 0,
      transparent 180px,
      color-mix(in srgb, var(--sj-blue), transparent 96%) 181px,
      transparent 182px
    );
}

/* ================= ORIGINAL SJ LANDING-PAGE FOUNDATION ================= */

/*
   This section fully integrates the original SJ Theme rules that the
   Dashboard depends on: sky-grid, sky-card, corner ornaments, hero,
   navigation pills and image cards.
*/

.sky-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 16px;
}

.sky-card {
  position: relative;
  padding: 18px;
  border: 1px solid var(--sj-card-border);
  border-radius: var(--sj-radius);
  background: var(--sj-card);
  backdrop-filter: blur(14px);
  box-shadow: var(--sj-card-shadow);
}

/* GBF / Relink-style gold corner ornaments */
.sky-card::before,
.sky-card::after {
  content: "";
  position: absolute;
  width: 18px;
  height: 18px;
  border: 2px solid var(--sj-corner-color);
  opacity: .7;
  pointer-events: none;
}

.sky-card::before {
  top: 8px;
  left: 8px;
  border-right: none;
  border-bottom: none;
}

.sky-card::after {
  right: 8px;
  bottom: 8px;
  border-top: none;
  border-left: none;
}

.sky-hero {
  position: relative;
  overflow: hidden;
  padding: 64px;
  border: 1px solid var(--sj-card-border);
  border-radius: 24px;
  background: var(--sj-hero-background);
  text-align: center;
  box-shadow: var(--sj-card-shadow);
}

.sky-hero::before {
  content: "";
  position: absolute;
  inset: 0;
  pointer-events: none;
  background:
    radial-gradient(circle at center, var(--sj-hero-glow), transparent 60%);
  opacity: .72;
}

.sky-hero-title {
  position: relative;
  color: var(--sj-text);
  font-size: 3.6rem;
  font-weight: 900;
  letter-spacing: .22em;
  text-shadow: 0 12px 30px rgba(120, 170, 230, .18);
}

.sky-hero-subtitle {
  position: relative;
  margin-top: 14px;
  color: var(--sj-text-soft);
  letter-spacing: .08em;
}

.sky-nav {
  border-radius: var(--sj-radius);
}

.sky-nav a {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin: 4px;
  padding: 10px 14px;
  border: 1px solid color-mix(in srgb, var(--sj-gold), transparent 65%);
  border-radius: var(--sj-radius-pill);
  background: var(--sj-nav-background);
  color: var(--sj-text) !important;
  text-decoration: none;
  transition:
    transform .2s ease,
    border-color .2s ease,
    box-shadow .2s ease;
}

.sky-nav a:hover {
  transform: translateY(-2px);
  border-color: color-mix(in srgb, var(--sj-gold), transparent 35%);
  color: var(--sj-blue-deep) !important;
  box-shadow: 0 12px 26px rgba(212, 177, 106, .20);
}

.sky-art {
  width: 100%;
  border: 1px solid var(--sj-card-border);
  border-radius: 16px;
  box-shadow: var(--sj-art-shadow);
}

/* Make all major Sky Journal page containers retain the same rounded language. */
.sky-list-card,
.sky-calendar-card,
.sky-countdown-card,
.sky-tags-card,
.sky-weather-card,
.sky-captain-card,
.sky-section-page-hero,
.sky-section-index-card,
.sky-mini-stat {
  border-radius: var(--sj-radius);
}

/* Preserve the original gold route divider inside the landing page. */
.sky-dashboard hr,
.sky-section-page hr {
  height: 1px;
  border: none;
  background:
    linear-gradient(
      to right,
      transparent,
      var(--sj-gold),
      transparent
    );
}
```

## 🧭 03｜顶部栏、面板、弹窗与通用按钮

统一顶部栏、输入框、弹窗、侧边面板及基础按钮的蓝金圆角视觉语言。

```space-style
/* priority: 20 */

/* ================= TOP BAR ================= */

#sb-top {
  border-bottom: 1px solid var(--top-border-color) !important;
  background: var(--top-background-color) !important;
  color: var(--top-color) !important;
  backdrop-filter: blur(18px) saturate(1.08);
  box-shadow: 0 6px 24px rgba(41, 86, 126, .08);
}

#sb-top input,
#sb-top textarea {
  border: 1px solid var(--sj-border) !important;
  border-radius: var(--sj-radius-pill) !important;
  background: var(--text-field-background-color) !important;
  color: var(--root-color) !important;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, .35),
    0 5px 16px rgba(41, 86, 126, .06);
}

#sb-top input:focus,
#sb-top textarea:focus {
  border-color: var(--sj-gold) !important;
  outline: none !important;
  box-shadow:
    0 0 0 3px color-mix(in srgb, var(--sj-gold), transparent 78%),
    0 7px 20px rgba(41, 86, 126, .10);
}

#sb-top button {
  border-radius: var(--sj-radius-sm) !important;
}

/* ================= PANELS & MODALS ================= */

.sb-panel,
.sb-modal,
.sb-notification,
[role="dialog"] {
  border: 1px solid var(--sj-border) !important;
  border-radius: var(--sj-radius-lg) !important;
  background: var(--modal-background-color) !important;
  color: var(--modal-color) !important;
  box-shadow: var(--sj-shadow) !important;
}

.sb-panel {
  background: var(--panel-background-color) !important;
}

.sb-modal input,
.sb-modal textarea,
.sb-modal select,
[role="dialog"] input,
[role="dialog"] textarea,
[role="dialog"] select {
  border: 1px solid var(--sj-border) !important;
  border-radius: var(--sj-radius-sm) !important;
  background: var(--text-field-background-color) !important;
  color: var(--root-color) !important;
}

.sb-modal input:focus,
.sb-modal textarea:focus,
.sb-modal select:focus,
[role="dialog"] input:focus,
[role="dialog"] textarea:focus,
[role="dialog"] select:focus {
  border-color: var(--sj-blue) !important;
  outline: none !important;
  box-shadow: 0 0 0 3px color-mix(in srgb, var(--sj-blue), transparent 78%);
}

/* ================= BUTTONS ================= */

button,
input[type="button"],
input[type="submit"],
input[type="reset"] {
  border: 1px solid var(--button-border-color) !important;
  border-radius: var(--sj-radius-pill) !important;
  background: var(--button-background-color) !important;
  color: var(--button-color) !important;
  transition:
    transform .16s ease,
    border-color .16s ease,
    background .16s ease,
    box-shadow .16s ease;
}

button:hover,
input[type="button"]:hover,
input[type="submit"]:hover,
input[type="reset"]:hover {
  transform: translateY(-1px);
  border-color: color-mix(in srgb, var(--sj-gold), var(--button-border-color) 35%) !important;
  background: var(--button-hover-background-color) !important;
  box-shadow: 0 7px 18px rgba(41, 86, 126, .10);
}

button:active,
input[type="button"]:active,
input[type="submit"]:active,
input[type="reset"]:active {
  transform: translateY(0) scale(.985);
}

button:focus-visible,
input:focus-visible,
textarea:focus-visible,
select:focus-visible,
a:focus-visible {
  outline: 2px solid var(--sj-gold) !important;
  outline-offset: 2px !important;
}
```

## 📝 04｜编辑器基础、正文元素与响应式规则

设置编辑器正文、页面标题、标题层级、链接、标签、表格、列表、提示块、图片、滚动条、移动端和打印样式。

```space-style
/* priority: 20 */

/* ================= EDITOR & DOCUMENT ================= */

#sb-main .cm-editor,
#sb-main .cm-scroller {
  background: transparent !important;
}

#sb-main .cm-content {
  padding-top: 1.1rem;
  padding-bottom: 5rem;
  color: var(--sj-text);
  font-size: 1.02rem;
  line-height: 1.72;
}

#sb-main .cm-line {
  color: inherit;
}

/* ================= PAGE TITLE ================= */

#sb-main input[type="text"],
#sb-main textarea {
  font-family: var(--sj-font) !important;
}

#sb-main input[type="text"] {
  border-radius: var(--sj-radius-md);
}

html[data-theme="dark"] #sb-main input[type="text"] {
  color: var(--sj-text);
}

/* ================= HEADINGS ================= */

#sb-main h1,
#sb-main h2,
#sb-main h3,
#sb-main h4,
#sb-main h5,
#sb-main h6,
#sb-main .cm-header,
#sb-main .sb-heading {
  color: var(--editor-heading-color) !important;
  font-family: var(--sj-font) !important;
  font-weight: 800;
  letter-spacing: .025em;
}

#sb-main h1,
#sb-main .cm-header-1 {
  margin-top: 1.6em;
  padding-bottom: .28em;
  border-bottom: 1px solid var(--sj-border);
  font-size: 2rem;
}

#sb-main h2,
#sb-main .cm-header-2 {
  margin-top: 1.45em;
  font-size: 1.62rem;
}

#sb-main h2::before {
  content: "✦";
  margin-right: .42em;
  color: var(--sj-gold);
  font-size: .62em;
  vertical-align: .12em;
}

#sb-main h3,
#sb-main .cm-header-3 {
  margin-top: 1.25em;
  font-size: 1.34rem;
}

#sb-main h4,
#sb-main .cm-header-4 {
  font-size: 1.16rem;
}

/* ================= LINKS & TAGS ================= */

#sb-main a,
#sb-main .sb-link,
#sb-main .sb-wiki-link-page {
  color: var(--editor-link-color) !important;
  text-decoration-color: color-mix(in srgb, var(--editor-link-color), transparent 62%);
  text-underline-offset: .18em;
}

#sb-main a:hover,
#sb-main .sb-link:hover,
#sb-main .sb-wiki-link-page:hover {
  color: var(--sj-gold) !important;
  text-decoration-color: var(--sj-gold);
}

#sb-main .sb-hashtag,
#sb-main .sb-tag {
  display: inline-flex;
  align-items: center;
  border: 1px solid var(--editor-hashtag-border-color);
  border-radius: 8px;
  background: var(--editor-hashtag-background-color);
  color: var(--editor-hashtag-color);
  padding: 2px 6px;
}

/* ================= EMPHASIS ================= */

#sb-main strong,
#sb-main b {
  color: color-mix(in srgb, var(--sj-text), var(--sj-blue-strong) 26%);
  font-weight: 850;
}

#sb-main em,
#sb-main i {
  color: color-mix(in srgb, var(--sj-text), var(--sj-gold) 24%);
}

/* ================= TABLES ================= */

#sb-main table,
#sb-main .sb-table {
  width: 100%;
  overflow: hidden;
  border: 1px solid var(--sj-border);
  border-collapse: separate;
  border-spacing: 0;
  border-radius: var(--sj-radius-md);
  background: var(--sj-surface);
  box-shadow: 0 8px 24px rgba(41, 86, 126, .06);
}

#sb-main th,
#sb-main td {
  padding: .68em .82em;
  border-right: 1px solid var(--sj-border);
  border-bottom: 1px solid var(--sj-border);
}

#sb-main th:last-child,
#sb-main td:last-child {
  border-right: 0;
}

#sb-main tr:last-child td {
  border-bottom: 0;
}

#sb-main thead,
#sb-main th {
  background:
    linear-gradient(
      135deg,
      color-mix(in srgb, var(--sj-blue), transparent 76%),
      color-mix(in srgb, var(--sj-gold), transparent 84%)
    );
  color: var(--editor-table-head-color);
  font-weight: 800;
}

#sb-main tbody tr:nth-child(even) {
  background: var(--editor-table-even-background-color);
}

#sb-main tbody tr:hover {
  background: color-mix(in srgb, var(--sj-blue), transparent 91%);
}

/* ================= LISTS & TASKS ================= */

/* Do not alter indentation or marker geometry; only harmonize colors. */
#sb-main ul,
#sb-main ol {
  color: var(--sj-text);
}

#sb-main li::marker {
  color: var(--editor-list-bullet-color);
}

#sb-main input[type="checkbox"] {
  accent-color: var(--sj-blue-strong);
}

/* ================= FRONTMATTER & DIRECTIVES ================= */

#sb-main .sb-directive,
#sb-main .sb-lua-directive-block {
  border-radius: var(--sj-radius-md);
}

/* ================= ADMONITIONS ================= */

#sb-main .sb-admonition {
  overflow: hidden;
  border: 1px solid var(--sj-border);
  border-left-width: 4px;
  border-radius: var(--sj-radius-md);
  background: var(--sj-surface-soft);
  box-shadow: 0 8px 22px rgba(41, 86, 126, .06);
}

#sb-main .sb-admonition[admonition="note" i] {
  border-left-color: var(--sj-blue);
}

#sb-main .sb-admonition[admonition="warning" i] {
  border-left-color: var(--sj-orange);
}

#sb-main .sb-admonition[admonition="danger" i] {
  border-left-color: var(--sj-red);
}

#sb-main .sb-admonition[admonition="success" i] {
  border-left-color: var(--sj-green);
}

/* ================= IMAGES & EMBEDS ================= */

#sb-main .cm-content img,
#sb-main .sb-widget img {
  max-width: 100%;
  border-radius: var(--sj-radius-md);
}

#sb-main .cm-content > img {
  border: 1px solid var(--sj-border);
  box-shadow: 0 10px 28px rgba(41, 86, 126, .10);
}

/* ================= SCROLLBARS ================= */

* {
  scrollbar-width: thin;
  scrollbar-color:
    color-mix(in srgb, var(--sj-blue), transparent 40%)
    transparent;
}

*::-webkit-scrollbar {
  width: 9px;
  height: 9px;
}

*::-webkit-scrollbar-track {
  background: transparent;
}

*::-webkit-scrollbar-thumb {
  border: 2px solid transparent;
  border-radius: var(--sj-radius-pill);
  background:
    color-mix(in srgb, var(--sj-blue), transparent 38%);
  background-clip: padding-box;
}

*::-webkit-scrollbar-thumb:hover {
  background:
    color-mix(in srgb, var(--sj-gold), transparent 22%);
  background-clip: padding-box;
}

/* ================= DASHBOARD COMPATIBILITY ================= */

.sky-dashboard,
.sky-section-page {
  --sj-bg: var(--root-background-color);
  --sj-card: var(--sj-surface);
  --sj-radius: 18px;
  font-family: var(--sj-font) !important;
}

.sky-dashboard *,
.sky-section-page * {
  font-family: inherit;
}

/* Preserve font on tag buttons and form controls inside widgets. */
.sky-dashboard button,
.sky-dashboard input,
.sky-dashboard select,
.sky-dashboard textarea,
.sky-section-page button,
.sky-section-page input,
.sky-section-page select,
.sky-section-page textarea {
  font-family: var(--sj-font) !important;
}

/* ================= MOBILE ================= */

@media (max-width: 760px) {
  html {
    font-size: 16px;
    --editor-width: 100% !important;
  }

  #sb-main .cm-content {
    padding-left: 10px;
    padding-right: 10px;
    line-height: 1.68;
  }

  #sb-main h1,
  #sb-main .cm-header-1 {
    font-size: 1.72rem;
  }

  #sb-main h2,
  #sb-main .cm-header-2 {
    font-size: 1.42rem;
  }

  #sb-main h3,
  #sb-main .cm-header-3 {
    font-size: 1.22rem;
  }

  #sb-top input,
  #sb-top textarea {
    border-radius: var(--sj-radius-md) !important;
  }

  .sb-modal,
  [role="dialog"] {
    border-radius: var(--sj-radius-md) !important;
  }

  #sb-main table {
    font-size: .92rem;
  }
}

/* ================= PRINT ================= */

@media print {
  html,
  body,
  #sb-root,
  #sb-main {
    background: #ffffff !important;
    color: #1f3347 !important;
  }

  #sb-top,
  .sb-panel,
  .sb-notifications {
    display: none !important;
  }

  #sb-main .cm-content {
    max-width: none !important;
  }

  #sb-main a {
    color: #1f5f96 !important;
  }
}
```

## 🧩 05｜原生界面精修与暗色 Dashboard 协调

包含原生标签修复、标题栏输入框、动作按钮、命令面板、配置页标签、引用块以及暗色模式下的 Dashboard 组件协调。

```space-style
/* priority: 20 */

/* =========================================================
   v1.2 TARGETED UI SYNC
   Only adjusts:
   1. Native hashtag rendering
   2. Top page-title field and action icons
   3. Command palette / prompt alignment
   4. Fenced and inline code appearance
   5. Native button visual language
   Other components intentionally remain unchanged.
   ========================================================= */

/* ---------- Targeted light/dark control and code tokens ---------- */

html {
  --sj-control-background:
    linear-gradient(
      180deg,
      rgba(255, 255, 255, .98),
      rgba(240, 247, 255, .95)
    );
  --sj-control-background-hover:
    linear-gradient(
      180deg,
      rgba(255, 255, 255, 1),
      rgba(230, 243, 255, .98)
    );
  --sj-control-border: rgba(212, 177, 106, .46);
  --sj-control-border-hover: rgba(212, 177, 106, .82);
  --sj-control-text: var(--sj-text);
  --sj-control-shadow: 0 8px 18px rgba(125, 182, 255, .16);

  --sj-ref-code-background: #fbfdff;
  --sj-ref-code-border: #d7e8f7;
  --sj-ref-code-border-hover: #d7e8f7;
  --sj-ref-code-text: #334c63;
  --sj-ref-inline-code-background: #edf7ff;
  --sj-ref-inline-code-border: #cfe6f8;
  --sj-ref-inline-code-text: #2f7fc7;
  --sj-ref-code-meta: #7a8fa5;

  --sj-ref-syntax-keyword: #7b61c9;
  --sj-ref-syntax-string: #1b84c6;
  --sj-ref-syntax-string-alt: #1479c9;
  --sj-ref-syntax-number: #d88433;
  --sj-ref-syntax-boolean: #be185d;
  --sj-ref-syntax-variable: #9b5b32;
  --sj-ref-syntax-type: #92400e;
  --sj-ref-syntax-comment: #91a8bb;
  --sj-ref-syntax-link: #1d4ed8;
  --sj-ref-syntax-wiki-link: #7c3aed;
  --sj-ref-syntax-wiki-link-bg: rgba(124, 58, 237, .10);
  --sj-ref-syntax-punctuation: #5f7488;
  --sj-ref-syntax-operator: #2f7fc7;
  --sj-ref-syntax-literal: #047857;
  --sj-ref-syntax-invalid: #dc2626;
  --sj-ref-syntax-emphasis: #92400e;
  --sj-ref-syntax-strong: #374151;
  --sj-ref-syntax-strikethrough: #6b7280;
  --sj-ref-syntax-quote: #6b7280;
}

html[data-theme="dark"] {
  --sj-control-background:
    linear-gradient(
      180deg,
      rgba(28, 54, 79, .98),
      rgba(17, 38, 58, .98)
    );
  --sj-control-background-hover:
    linear-gradient(
      180deg,
      rgba(38, 70, 100, 1),
      rgba(24, 50, 74, 1)
    );
  --sj-control-border: rgba(228, 189, 112, .38);
  --sj-control-border-hover: rgba(228, 189, 112, .76);
  --sj-control-text: var(--sj-text);
  --sj-control-shadow: 0 8px 18px rgba(0, 0, 0, .24);

  --sj-ref-code-background: #1f2b3a;
  --sj-ref-code-border: #39506a;
  --sj-ref-code-border-hover: #496985;
  --sj-ref-code-text: #d7e6f5;
  --sj-ref-inline-code-background: #20364d;
  --sj-ref-inline-code-border: #39506a;
  --sj-ref-inline-code-text: #9ed0ff;
  --sj-ref-code-meta: #9fbedc;

  --sj-ref-syntax-keyword: #c4a7ff;
  --sj-ref-syntax-string: #78c7ff;
  --sj-ref-syntax-string-alt: #91d2ff;
  --sj-ref-syntax-number: #f0ad67;
  --sj-ref-syntax-boolean: #ff8eba;
  --sj-ref-syntax-variable: #e0ab78;
  --sj-ref-syntax-type: #f4bf87;
  --sj-ref-syntax-comment: #7f96aa;
  --sj-ref-syntax-link: #8fc7ff;
  --sj-ref-syntax-wiki-link: #c7a8ff;
  --sj-ref-syntax-wiki-link-bg: rgba(151, 108, 255, .14);
  --sj-ref-syntax-punctuation: #9db1c3;
  --sj-ref-syntax-operator: #8fc7ff;
  --sj-ref-syntax-literal: #75d4a5;
  --sj-ref-syntax-invalid: #ff8b91;
  --sj-ref-syntax-emphasis: #f4bf87;
  --sj-ref-syntax-strong: #eef6ff;
  --sj-ref-syntax-strikethrough: #9aaec0;
  --sj-ref-syntax-quote: #a7bacb;
}

/* ---------- Native hashtag: one stable style in every editor state ---------- */

/*
SilverBullet can render a completed hashtag with an outer .sb-hashtag
wrapper, while the currently edited / IME-composing token may briefly
expose .sb-hashtag-text without that wrapper.

Both paths use the same geometry. Broad [class*="hashtag"] selectors are
intentionally forbidden because they style nested syntax spans twice.
*/
#sb-main .sb-hashtag,
#sb-main .sb-tag,
#sb-main .cm-line .sb-hashtag-text:not(.sb-hashtag *) {
  display: inline-flex !important;
  align-items: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 2px 6px !important;
  border: 1px solid var(--editor-hashtag-border-color) !important;
  border-radius: 8px !important;
  background: var(--editor-hashtag-background-color) !important;
  color: var(--editor-hashtag-color) !important;
  -webkit-text-fill-color: var(--editor-hashtag-color) !important;
  font-family: var(--sj-font) !important;
  font-size: .9em !important;
  font-weight: inherit !important;
  line-height: 1.35 !important;
  vertical-align: baseline !important;
  box-shadow: none !important;
  transform: none !important;
}

/* A nested text node belongs to the already-styled outer chip. */
#sb-main .sb-hashtag .sb-hashtag-text,
#sb-main .sb-hashtag [class*="hashtag"] {
  display: inline !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  color: inherit !important;
  -webkit-text-fill-color: inherit !important;
  font-family: inherit !important;
  font-size: inherit !important;
  font-weight: inherit !important;
  line-height: inherit !important;
  box-shadow: none !important;
  transform: none !important;
}

/* Active-line and IME composition must not enlarge the hashtag chip. */
#sb-main .cm-line.cm-activeLine :is(
  .sb-hashtag,
  .sb-tag,
  .sb-hashtag-text:not(.sb-hashtag *)
),
#sb-main .cm-line :is(
  .sb-hashtag,
  .sb-tag,
  .sb-hashtag-text:not(.sb-hashtag *)
):focus,
#sb-main .cm-line :is(
  .sb-hashtag,
  .sb-tag,
  .sb-hashtag-text:not(.sb-hashtag *)
):focus-within {
  padding: 2px 6px !important;
  border-radius: 8px !important;
  font-size: .9em !important;
  line-height: 1.35 !important;
  transform: none !important;
}

/* ---------- Top bar and page-title field ---------- */

#sb-top {
  height: 70px !important;
  opacity: 1 !important;
  border: 0 !important;
  background: var(--top-background-color) !important;
  box-shadow: none !important;
}

#sb-top,
#sb-top > .main,
#sb-top > .main > .inner {
  border-top: 0 !important;
  border-bottom: 0 !important;
  background-image: none !important;
  box-shadow: none !important;
}

#sb-top > .main,
#sb-top > .main > .inner {
  background: transparent !important;
}

#sb-top > .main > .inner {
  box-sizing: border-box !important;
  gap: 10px !important;
  padding: 15px 14px 0 !important;
}

#sb-top #sb-current-page,
#sb-current-page {
  box-sizing: border-box !important;
  flex: 1 1 auto !important;
  width: auto !important;
  min-width: 0 !important;
  height: 38px !important;
  min-height: 38px !important;
  max-height: 38px !important;
  align-self: flex-start !important;
  margin: 0 !important;
  border: 1px solid var(--sj-border) !important;
  border-radius: 12px !important;
  background: color-mix(in srgb, var(--sj-surface-solid), transparent 15%) !important;
  color: var(--sj-text) !important;
  box-shadow: none !important;
}

#sb-current-page:focus-within {
  border-color: color-mix(in srgb, var(--sj-blue), transparent 42%) !important;
  background: var(--sj-surface-solid) !important;
  outline: 2px solid color-mix(in srgb, var(--sj-blue), transparent 80%) !important;
}

#sb-top #sb-current-page input.sb-page-name-editor,
#sb-top input.sb-input.sb-page-name-editor,
#sb-current-page input.sb-page-name-editor,
input.sb-input.sb-page-name-editor {
  box-sizing: border-box !important;
  width: 100% !important;
  min-height: 36px !important;
  height: 36px !important;
  margin: 0 !important;
  padding: 0 14px 0 18px !important;
  border: 0 !important;
  border-radius: 11px !important;
  background: transparent !important;
  background-image: none !important;
  color: var(--sj-text) !important;
  -webkit-text-fill-color: var(--sj-text) !important;
  caret-color: var(--sj-blue-strong) !important;
  outline: none !important;
  box-shadow: none !important;
  font-family: var(--sj-font) !important;
  font-weight: 800 !important;
  line-height: 36px !important;
  text-indent: 0 !important;
  font-variant-ligatures: none !important;
  font-feature-settings: "liga" 0, "clig" 0, "dlig" 0, "calt" 0 !important;
  font-kerning: none !important;
}

#sb-top #sb-current-page .cm-editor,
#sb-top #sb-current-page .cm-scroller,
#sb-current-page .cm-editor,
#sb-current-page .cm-scroller {
  min-height: 36px !important;
  margin: 0 !important;
  border: 0 !important;
  background: transparent !important;
  color: var(--sj-text) !important;
  box-shadow: none !important;
}

#sb-top #sb-current-page .cm-content,
#sb-current-page .cm-content {
  box-sizing: border-box !important;
  display: flex !important;
  min-height: 36px !important;
  align-items: center !important;
  margin: 0 !important;
  padding: 0 14px 0 18px !important;
  color: var(--sj-text) !important;
  font-family: var(--sj-font) !important;
  font-weight: 800 !important;
  font-variant-ligatures: none !important;
  font-feature-settings: "liga" 0, "clig" 0, "dlig" 0, "calt" 0 !important;
  font-kerning: none !important;
}

#sb-top #sb-current-page .cm-line,
#sb-current-page .cm-line {
  margin: 0 !important;
  padding: 0 !important;
  color: var(--sj-text) !important;
  font-weight: 800 !important;
  line-height: 1.2 !important;
}

#sb-current-page *,
#sb-current-page .cm-line *,
#sb-current-page .cm-content * {
  color: var(--sj-text) !important;
  -webkit-text-fill-color: var(--sj-text) !important;
}

#sb-current-page .cm-cursor {
  border-left-color: var(--sj-blue-strong) !important;
}

/* Top action icons use the same white/blue/gold language as landing buttons. */
#sb-top .sb-actions {
  display: flex !important;
  align-items: center !important;
  gap: 7px !important;
}

#sb-top .sb-actions button,
#sb-top button.action-button {
  display: inline-flex !important;
  width: 38px !important;
  min-width: 38px !important;
  height: 38px !important;
  min-height: 38px !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 1px solid var(--sj-control-border) !important;
  border-radius: 12px !important;
  background: var(--sj-control-background) !important;
  color: var(--sj-control-text) !important;
  box-shadow: none !important;
}

#sb-top .sb-actions button:hover,
#sb-top button.action-button:hover {
  transform: translateY(-1px);
  border-color: var(--sj-control-border-hover) !important;
  background: var(--sj-control-background-hover) !important;
  color: var(--sj-blue-strong) !important;
  box-shadow: var(--sj-control-shadow) !important;
}

/* ---------- Command palette and prompt alignment ---------- */

.sb-modal-box {
  overflow: hidden;
  border: 1px solid var(--sj-border) !important;
  border-radius: 16px !important;
  background: var(--modal-background-color) !important;
  color: var(--modal-color) !important;
  box-shadow: none !important;
}

.sb-modal-box .sb-header,
.sb-modal-box .sb-prompt {
  display: flex !important;
  align-items: center !important;
  gap: 12px !important;
  box-sizing: border-box !important;
}

.sb-modal-box .sb-header {
  padding: 12px 14px !important;
  border-bottom: 1px solid var(--sj-border) !important;
}

.sb-modal-box .sb-prompt {
  padding: 12px 14px !important;
}

.sb-modal-box .sb-header label,
.sb-modal-box .sb-prompt label {
  display: inline-flex !important;
  flex: 0 0 auto !important;
  min-height: 38px !important;
  align-items: center !important;
  margin: 0 !important;
  padding: 0 !important;
  color: var(--sj-blue-strong) !important;
  font-family: var(--sj-font) !important;
  font-weight: 700 !important;
  line-height: 38px !important;
  white-space: nowrap !important;
}

.sb-modal-box .sb-header input[type="text"],
.sb-modal-box .sb-header input[type="search"],
.sb-modal-box .sb-prompt input[type="text"],
.sb-modal-box .sb-prompt input[type="search"],
.sb-modal-box input.cm-textfield,
.sb-modal-box .cm-textfield {
  box-sizing: border-box !important;
  flex: 1 1 auto !important;
  width: auto !important;
  min-width: 0 !important;
  height: 38px !important;
  min-height: 38px !important;
  margin: 0 !important;
  padding: 0 14px !important;
  border: 1px solid var(--sj-border) !important;
  border-radius: 12px !important;
  background: var(--text-field-background-color) !important;
  color: var(--sj-text) !important;
  font-family: var(--sj-font) !important;
  line-height: 38px !important;
  box-shadow: none !important;
}

.sb-modal-box .sb-header input:focus,
.sb-modal-box .sb-prompt input:focus,
.sb-modal-box .cm-textfield:focus {
  border-color: var(--sj-gold) !important;
  outline: 2px solid color-mix(in srgb, var(--sj-gold), transparent 80%) !important;
}

.sb-modal-box .sb-header > button,
.sb-modal-box .sb-prompt > button,
.sb-modal-box .sb-prompt-buttons > button {
  display: inline-flex !important;
  flex: 0 0 auto !important;
  height: 38px !important;
  min-height: 38px !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 14px !important;
  line-height: 1 !important;
}

/* ---------- Native buttons: landing-page visual language ---------- */

button,
.cm-button,
.command-button,
.sb-prompt-buttons button,
.sb-modal-box button,
.sb-lua-wrapper .sb-lua-directive-inline button {
  box-sizing: border-box;
  border: 1px solid var(--sj-control-border) !important;
  border-radius: var(--sj-radius-pill) !important;
  background: var(--sj-control-background) !important;
  color: var(--sj-control-text) !important;
  font-family: var(--sj-font) !important;
  font-weight: 700;
  box-shadow: none !important;
  cursor: pointer;
  transition:
    transform .16s ease,
    border-color .16s ease,
    background .16s ease,
    box-shadow .16s ease,
    color .16s ease;
}

button:hover,
.cm-button:hover,
.command-button:hover,
.sb-prompt-buttons button:hover,
.sb-modal-box button:hover,
.sb-lua-wrapper .sb-lua-directive-inline button:hover {
  transform: translateY(-1px);
  border-color: var(--sj-control-border-hover) !important;
  background: var(--sj-control-background-hover) !important;
  color: var(--sj-blue-strong) !important;
  box-shadow: var(--sj-control-shadow) !important;
}

button:active,
.cm-button:active,
.command-button:active,
.sb-prompt-buttons button:active,
.sb-modal-box button:active {
  transform: translateY(0) scale(.985);
}

/* Dashboard buttons retain their component-specific dimensions. */
.sky-create-btn,
.sky-back-btn,
.sky-calendar-nav-btn,
.sky-calendar-picker-btn,
.sky-calendar-today-btn,
.sky-tag-chip {
  font-family: var(--sj-font) !important;
}

/* ---------- Narrow-screen title and command palette ---------- */

@media (max-width: 640px) {
  #sb-top {
    height: 62px !important;
  }

  #sb-top > .main > .inner {
    gap: 6px !important;
    padding: 12px 8px 0 !important;
  }

  #sb-top #sb-current-page,
  #sb-current-page {
    height: 38px !important;
    min-height: 38px !important;
    max-height: 38px !important;
  }

  #sb-top .sb-actions {
    gap: 5px !important;
  }

  #sb-top .sb-actions button,
  #sb-top button.action-button {
    width: 36px !important;
    min-width: 36px !important;
    height: 36px !important;
    min-height: 36px !important;
  }

  .sb-modal-box .sb-header,
  .sb-modal-box .sb-prompt {
    gap: 8px !important;
  }

  .sb-modal-box .sb-header {
    padding: 10px !important;
  }
}


/* =========================================================
   v1.3 TITLE GAP + BLOCKQUOTE + CONFIG TABS
   Only the requested areas are changed.
   ========================================================= */

/* ---------- 1. Keep a visible gap between title and action buttons ---------- */

#sb-top > .main > .inner {
  column-gap: 0 !important;
}

#sb-top #sb-current-page,
#sb-current-page {
  margin-right: 14px !important;
}

#sb-top .sb-actions {
  flex: 0 0 auto !important;
  margin-left: 0 !important;
}

/* Some builds render one or more actions outside .sb-actions. */
#sb-top #sb-current-page + button,
#sb-top #sb-current-page + .action-button,
#sb-top #sb-current-page + .sb-actions {
  margin-left: 0 !important;
}

/* ---------- 3. Compact Configuration Manager tabs ---------- */

/*
   Covers current role-based tabs and likely class names used by the
   Configuration Manager without changing normal page buttons.
*/
#sb-main [role="tablist"],
#sb-main .sb-config-tabs,
#sb-main .sb-configuration-tabs,
#sb-main .configuration-tabs,
#sb-main [class*="config"][class*="tabs"] {
  display: flex !important;
  align-items: center !important;
  flex-wrap: wrap !important;
  gap: 6px !important;
  margin: 6px 0 10px !important;
}

#sb-main [role="tab"],
#sb-main [role="tablist"] > button,
#sb-main .sb-config-tabs > button,
#sb-main .sb-configuration-tabs > button,
#sb-main .configuration-tabs > button,
#sb-main [class*="config"][class*="tabs"] > button {
  display: inline-flex !important;
  width: auto !important;
  min-width: 0 !important;
  height: 34px !important;
  min-height: 34px !important;
  align-items: center !important;
  justify-content: center !important;
  margin: 0 !important;
  padding: 0 15px !important;
  border: 1px solid var(--sj-control-border) !important;
  border-radius: 11px !important;
  background: var(--sj-control-background) !important;
  color: var(--sj-control-text) !important;
  font-family: var(--sj-font) !important;
  font-size: .9rem !important;
  font-weight: 700 !important;
  line-height: 1 !important;
  box-shadow: none !important;
  transform: none !important;
  white-space: nowrap !important;
}

#sb-main [role="tab"]:hover,
#sb-main [role="tablist"] > button:hover,
#sb-main .sb-config-tabs > button:hover,
#sb-main .sb-configuration-tabs > button:hover,
#sb-main .configuration-tabs > button:hover,
#sb-main [class*="config"][class*="tabs"] > button:hover {
  border-color: var(--sj-control-border-hover) !important;
  background: var(--sj-control-background-hover) !important;
  color: var(--sj-blue-strong) !important;
  box-shadow: 0 5px 13px rgba(61, 116, 166, .10) !important;
  transform: none !important;
}

#sb-main [role="tab"][aria-selected="true"],
#sb-main [role="tablist"] > button[aria-selected="true"],
#sb-main .sb-config-tabs > button.active,
#sb-main .sb-configuration-tabs > button.active,
#sb-main .configuration-tabs > button.active,
#sb-main [class*="config"][class*="tabs"] > button.active {
  border-color: color-mix(in srgb, var(--sj-gold), transparent 26%) !important;
  background:
    linear-gradient(
      180deg,
      color-mix(in srgb, var(--sj-blue), transparent 84%),
      color-mix(in srgb, var(--sj-gold), transparent 91%)
    ) !important;
  color: var(--sj-blue-strong) !important;
}

/* Keep the configuration filter visually proportional to compact tabs. */
#sb-main [class*="config"] input[type="search"],
#sb-main [class*="config"] input[placeholder*="Filter"],
#sb-main [class*="configuration"] input[type="search"],
#sb-main [class*="configuration"] input[placeholder*="Filter"] {
  min-height: 36px !important;
  height: 36px !important;
  padding: 0 13px !important;
  border-radius: 10px !important;
  line-height: 36px !important;
}

/* ---------- Mobile ---------- */

@media (max-width: 640px) {
  #sb-top #sb-current-page,
  #sb-current-page {
    margin-right: 8px !important;
  }

  #sb-main [role="tab"],
  #sb-main [role="tablist"] > button,
  #sb-main .sb-config-tabs > button,
  #sb-main .sb-configuration-tabs > button,
  #sb-main .configuration-tabs > button,
  #sb-main [class*="config"][class*="tabs"] > button {
    height: 32px !important;
    min-height: 32px !important;
    padding: 0 11px !important;
    font-size: .84rem !important;
  }
}


/* =========================================================
   v1.4 DARK DASHBOARD HARMONY
   Only fixes the three dark-mode areas highlighted by the user:
   Captain status pill, folder-page hero, and folder-page back button.
   ========================================================= */

/* Shared dark surfaces for both SilverBullet dark mode and SJConfig dark mode. */
html[data-theme="dark"],
.sky-theme-dark {
  --sj-dark-widget-gradient:
    radial-gradient(
      circle at 88% 12%,
      rgba(228, 189, 112, .08),
      transparent 35%
    ),
    linear-gradient(
      145deg,
      rgba(18, 36, 56, .97),
      rgba(8, 21, 35, .96)
    );
  --sj-dark-widget-soft:
    linear-gradient(
      180deg,
      rgba(27, 53, 77, .96),
      rgba(15, 34, 52, .96)
    );
  --sj-dark-widget-border: rgba(127, 197, 255, .22);
  --sj-dark-widget-border-gold: rgba(228, 189, 112, .40);
  --sj-dark-widget-shadow: 0 14px 34px rgba(0, 0, 0, .30);
  --sj-dark-widget-text: #e6f1fb;
  --sj-dark-widget-text-soft: #9bb2c8;
  --sj-dark-widget-blue: #a8d7ff;
}

/* ---------- Captain status pill ---------- */

html[data-theme="dark"] .sky-dashboard .sky-captain-state,
html[data-theme="dark"] .sky-section-page .sky-captain-state,
.sky-dashboard.sky-theme-dark .sky-captain-state,
.sky-section-page.sky-theme-dark .sky-captain-state {
  border-color: var(--sj-dark-widget-border) !important;
  background: var(--sj-dark-widget-soft) !important;
  color: var(--sj-dark-widget-blue) !important;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, .04),
    0 5px 14px rgba(0, 0, 0, .16) !important;
}

/* Keep the active dot vivid without changing its size or layout. */
html[data-theme="dark"] .sky-captain-state-dot,
.sky-theme-dark .sky-captain-state-dot {
  background: #70c797 !important;
  box-shadow: 0 0 0 4px rgba(112, 199, 151, .12) !important;
}

/* ---------- Folder / task / tag page hero ---------- */

html[data-theme="dark"] .sky-section-page .sky-section-page-hero,
.sky-section-page.sky-theme-dark .sky-section-page-hero {
  border-color: var(--sj-dark-widget-border) !important;
  background: var(--sj-dark-widget-gradient) !important;
  box-shadow: var(--sj-dark-widget-shadow) !important;
}

html[data-theme="dark"] .sky-section-page .sky-section-page-kicker,
.sky-section-page.sky-theme-dark .sky-section-page-kicker {
  color: var(--sj-dark-widget-blue) !important;
}

html[data-theme="dark"] .sky-section-page .sky-section-page-title,
.sky-section-page.sky-theme-dark .sky-section-page-title {
  color: var(--sj-dark-widget-text) !important;
  text-shadow: 0 8px 24px rgba(0, 0, 0, .20);
}

html[data-theme="dark"] .sky-section-page .sky-section-page-subtitle,
.sky-section-page.sky-theme-dark .sky-section-page-subtitle {
  color: var(--sj-dark-widget-text-soft) !important;
}

/* Preserve the warm gold route-corner ornaments in dark mode. */
html[data-theme="dark"] .sky-section-page .sky-section-page-hero::before,
html[data-theme="dark"] .sky-section-page .sky-section-page-hero::after,
.sky-section-page.sky-theme-dark .sky-section-page-hero::before,
.sky-section-page.sky-theme-dark .sky-section-page-hero::after {
  border-color: rgba(228, 189, 112, .64) !important;
}

/* ---------- Folder-page back button ---------- */

html[data-theme="dark"] .sky-section-page .sky-back-btn,
.sky-section-page.sky-theme-dark .sky-back-btn {
  border-color: var(--sj-dark-widget-border-gold) !important;
  background: var(--sj-dark-widget-soft) !important;
  color: var(--sj-dark-widget-text) !important;
  box-shadow: none !important;
}

html[data-theme="dark"] .sky-section-page .sky-back-btn:hover,
.sky-section-page.sky-theme-dark .sky-back-btn:hover {
  transform: translateY(-1px);
  border-color: rgba(228, 189, 112, .78) !important;
  background:
    linear-gradient(
      180deg,
      rgba(38, 70, 100, 1),
      rgba(24, 50, 74, 1)
    ) !important;
  color: var(--sj-dark-widget-blue) !important;
  box-shadow: 0 8px 18px rgba(0, 0, 0, .22) !important;
}
```

## 🔤 06｜字体系统、阅读宽度与编辑器卡片

使用零网络请求的系统字体栈分配标题／正文／代码字体，并控制普通页面、Index Dashboard 与编辑器卡片的阅读布局。

```space-style
/* priority: 20 */

/* =========================================================
   v1.5 LIBRARY TYPOGRAPHY + READING LAYOUT
   ========================================================= */

/* ---------- Native system font stacks: zero network requests ---------- */

/*
No web font declarations are used in this theme.

The stacks below intentionally rely on fonts already supplied by the
operating system. Each platform therefore renders with its own native
typography without downloading, validating or swapping font files.
*/

html {
  /*
  Display headings:
  native serif faces preserve the airship-log / classical fantasy tone.
  */
  --sj-heading-font:
    ui-serif,
    "Iowan Old Style",
    "Palatino Linotype",
    Palatino,
    "Book Antiqua",
    "Songti SC",
    STSong,
    "Noto Serif CJK SC",
    Georgia,
    serif;

  /*
  Interface and body:
  system-ui resolves to San Francisco, Roboto, Segoe UI or the current
  platform's native UI face. The remaining names cover older engines.
  */
  --sj-ui-font:
    system-ui,
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI Variable",
    "Segoe UI",
    "Helvetica Neue",
    "PingFang SC",
    "Hiragino Sans GB",
    "Noto Sans CJK SC",
    "Microsoft YaHei UI",
    "Microsoft YaHei",
    Arial,
    sans-serif;

  --sj-body-font: var(--sj-ui-font);

  /*
  Code:
  use the platform's native monospace family with common OS fallbacks.
  */
  --sj-code-font:
    ui-monospace,
    "SFMono-Regular",
    "Cascadia Mono",
    "Cascadia Code",
    "Roboto Mono",
    "Noto Sans Mono CJK SC",
    Menlo,
    Monaco,
    Consolas,
    "Liberation Mono",
    monospace;

  /* Compatibility with all existing Sky Journal component rules. */
  --sj-font: var(--sj-ui-font);
  --ui-font: var(--sj-ui-font) !important;
  --editor-font: var(--sj-body-font) !important;

  /* SilverBullet's current built-in default. */
  --editor-width: 800px !important;

  --sj-toc-background:
    linear-gradient(
      145deg,
      rgba(236, 247, 255, .90),
      rgba(255, 255, 255, .82)
    );
  --sj-toc-border: rgba(112, 173, 230, .28);
  --sj-toc-hover: rgba(121, 184, 244, .14);

  --sj-frontmatter-background:
    linear-gradient(
      135deg,
      rgba(239, 247, 255, .94),
      rgba(255, 249, 231, .72)
    );
  --sj-frontmatter-border: rgba(112, 173, 230, .30);
  --sj-frontmatter-key: #3978b7;
  --sj-frontmatter-value: #526f89;

  --sj-divider-center: rgba(93, 166, 229, .82);
  --sj-divider-side: rgba(93, 166, 229, .35);
}

html[data-theme="dark"] {
  --sj-toc-background:
    linear-gradient(
      145deg,
      rgba(19, 43, 64, .94),
      rgba(9, 24, 38, .88)
    );
  --sj-toc-border: rgba(127, 197, 255, .22);
  --sj-toc-hover: rgba(127, 197, 255, .11);

  --sj-frontmatter-background:
    linear-gradient(
      135deg,
      rgba(18, 43, 65, .94),
      rgba(43, 37, 24, .68)
    );
  --sj-frontmatter-border: rgba(127, 197, 255, .22);
  --sj-frontmatter-key: #9fd1fb;
  --sj-frontmatter-value: #b1c5d7;

  --sj-divider-center: rgba(116, 177, 235, .78);
  --sj-divider-side: rgba(116, 177, 235, .28);
}

/* ---------- Font assignment ---------- */

/* UI, controls and body text use the native system sans stack. */
html,
body,
dialog,
#sb-root,
#sb-top,
#sb-main,
#sb-main .cm-editor,
#sb-main .cm-scroller,
#sb-main .cm-content,
#sb-main .cm-line,
.sb-modal,
.sb-modal-box,
.sb-panel,
.sb-widget,
.sb-notifications,
.sb-notification,
button,
input,
textarea,
select,
option,
label,
summary {
  font-family: var(--sj-ui-font) !important;
}

/* Page body deliberately follows the body stack. */
#sb-main .cm-content,
#sb-main .cm-line,
.sky-list-row,
.sky-section-page-subtitle,
.sky-section-page-note {
  font-family: var(--sj-body-font) !important;
}

/* Display titles use the native system serif stack with CJK fallbacks. */
#sb-main h1,
#sb-main h2,
#sb-main h3,
#sb-main h4,
#sb-main h5,
#sb-main h6,
#sb-main .cm-header,
#sb-main .sb-heading,
#sb-current-page,
#sb-current-page input,
#sb-current-page .cm-content,
.sky-hero-title,
.sky-section-page-title,
.sky-calendar-title,
.sky-tags-title,
.sky-weather-title,
.sky-countdown-title,
.sky-captain-kicker,
.sky-list-title,
.collapsible-toc h1,
.toc-widget h1 {
  font-family: var(--sj-heading-font) !important;
}

/* Small UI labels stay in the native system sans stack. */
.sky-create-btn,
.sky-back-btn,
.sky-tag-chip,
.sky-calendar-controls,
.sky-calendar-today-count,
.sky-weather-attribution,
.sky-section-page-kicker,
.sky-list-subtitle {
  font-family: var(--sj-ui-font) !important;
}

pre,
code,
kbd,
samp,
span.sb-code,
.sb-line-fenced-code,
.sb-frontmatter,
.sb-line-frontmatter-outside {
  font-family: var(--sj-code-font) !important;
}

/* ---------- Page width: normal pages 800px, Index full width ---------- */

/*
The custom property is scoped to #sb-main only on pages containing the
Sky Journal Dashboard, so the top bar keeps the normal 800px width.
*/
#sb-main:has(.sky-dashboard) {
  --editor-width: min(1500px, calc(100vw - 32px)) !important;
}

/* The title field and right-side actions follow SilverBullet's default width. */
#sb-top > .main {
  width: 100% !important;
  max-width: 800px !important;
  margin-right: auto !important;
  margin-left: auto !important;
}

#sb-top > .main > .inner {
  width: calc(100% - 24px) !important;
  max-width: 800px !important;
  margin-right: auto !important;
  margin-left: auto !important;
}

@media (max-width: 760px) {
  html {
    --editor-width: 100% !important;
  }

  #sb-main:has(.sky-dashboard) {
    --editor-width: 100% !important;
  }

  #sb-top > .main,
  #sb-top > .main > .inner {
    width: 100% !important;
    max-width: 100% !important;
  }

  #sb-main .collapsible-toc,
  #sb-main .toc-widget {
    padding: .9rem 1rem !important;
  }
}


/* =========================================================
   v1.7 EDITOR CARD + QUOTE EDITING CLEANUP
   ========================================================= */

html {
  --sj-editor-card-background: #fbfdff;
  --sj-editor-card-border: rgba(112, 173, 230, .28);
  --sj-editor-card-shadow:
    0 16px 38px rgba(61, 116, 166, .09),
    0 2px 8px rgba(61, 116, 166, .04);
}

html[data-theme="dark"] {
  --sj-editor-card-background: #0d1d2c;
  --sj-editor-card-border: rgba(127, 197, 255, .20);
  --sj-editor-card-shadow:
    0 18px 42px rgba(0, 0, 0, .28),
    0 2px 10px rgba(0, 0, 0, .18);
}

/* ---------- Normal note pages as a reading card ---------- */

/*
Only normal pages receive the editor card. Index contains .sky-dashboard
and therefore keeps its existing full-width transparent canvas.
*/
#sb-main:not(:has(.sky-dashboard)) .cm-editor {
  box-sizing: border-box !important;
  margin-top: 18px !important;
  margin-bottom: 34px !important;
  overflow: hidden !important;
  border: 1px solid var(--sj-editor-card-border) !important;
  border-radius: 18px !important;
  background: var(--sj-editor-card-background) !important;
  box-shadow: var(--sj-editor-card-shadow) !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-scroller {
  background: transparent !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content {
  box-sizing: border-box !important;
  padding-right: clamp(22px, 4vw, 46px) !important;
  padding-left: clamp(22px, 4vw, 46px) !important;
}

/* Keep widgets and editor lines inside the rounded card. */
#sb-main:not(:has(.sky-dashboard)) .cm-gutters {
  border-right-color: var(--sj-editor-card-border) !important;
  background: color-mix(
    in srgb,
    var(--sj-editor-card-background),
    var(--sj-blue) 3%
  ) !important;
}

/* Explicit Index reset: no card, no borders, no forced page padding. */
#sb-main:has(.sky-dashboard) .cm-editor {
  margin: 0 !important;
  overflow: visible !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
}

#sb-main:has(.sky-dashboard) .cm-scroller {
  background: transparent !important;
}

@media (max-width: 760px) {
  #sb-main:not(:has(.sky-dashboard)) .cm-editor {
    margin-top: 10px !important;
    margin-right: 6px !important;
    margin-bottom: 22px !important;
    margin-left: 6px !important;
    border-radius: 14px !important;
  }

  #sb-main:not(:has(.sky-dashboard)) .cm-content {
    padding-right: 16px !important;
    padding-left: 16px !important;
  }
}


/* =========================================================
   v1.7.1 EDITOR HEADER JOIN
   Normal note pages visually connect the editor card to the
   top bar. Index remains full-width and unchanged.
   ========================================================= */

html {
  --sj-editor-shell-background: var(--top-background-color);
}

html[data-theme="dark"] {
  --sj-editor-shell-background: var(--top-background-color);
}

/* The title bar and the canvas behind normal notes share one surface. */
#sb-top {
  background: var(--sj-editor-shell-background) !important;
}

#sb-main:not(:has(.sky-dashboard)) {
  background: var(--sj-editor-shell-background) !important;
}

/* Remove the gap introduced by v1.7 and let the card touch the top bar. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor {
  margin-top: 0 !important;
  border-top-color: var(--sj-editor-card-border) !important;
}

/* Keep the paper/card surface calm and consistent in both modes. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor,
#sb-main:not(:has(.sky-dashboard)) .cm-scroller {
  background-color: var(--sj-editor-card-background) !important;
}

/* Preserve the full-width Dashboard canvas and its existing background. */
#sb-main:has(.sky-dashboard) {
  background: var(--sj-page-background) !important;
}

#sb-main:has(.sky-dashboard) .cm-editor,
#sb-main:has(.sky-dashboard) .cm-scroller {
  background: transparent !important;
}

@media (max-width: 760px) {
  #sb-main:not(:has(.sky-dashboard)) .cm-editor {
    margin-top: 0 !important;
  }
}


/* =========================================================
   v1.7.2 INDEX DASHBOARD FRAME
   Adds the same card-shell language to Index without changing
   the Dashboard's existing cloud background.
   ========================================================= */

html {
  --sj-dashboard-frame-border: var(--sj-editor-card-border);
  --sj-dashboard-frame-shadow:
    0 16px 38px rgba(61, 116, 166, .09),
    0 2px 8px rgba(61, 116, 166, .04);
}

html[data-theme="dark"] {
  --sj-dashboard-frame-border: var(--sj-editor-card-border);
  --sj-dashboard-frame-shadow:
    0 18px 42px rgba(0, 0, 0, .28),
    0 2px 10px rgba(0, 0, 0, .18);
}

/*
The outer page surface uses the same color as the title bar.
The Dashboard background itself is moved onto the editor card,
so its existing light/dark cloud gradient is preserved unchanged.
*/
#sb-main:has(.sky-dashboard) {
  background: var(--sj-editor-shell-background) !important;
}

#sb-main:has(.sky-dashboard) .cm-editor {
  box-sizing: border-box !important;
  margin-top: 0 !important;
  margin-bottom: 34px !important;
  overflow: hidden !important;
  border: 1px solid var(--sj-dashboard-frame-border) !important;
  border-radius: 18px !important;
  background: var(--sj-page-background) !important;
  box-shadow: var(--sj-dashboard-frame-shadow) !important;
}

/* Keep the Dashboard canvas and widgets visually unchanged. */
#sb-main:has(.sky-dashboard) .cm-scroller,
#sb-main:has(.sky-dashboard) .cm-content {
  background: transparent !important;
}

/*
Because the parent canvas matches the title bar, the two exposed areas
outside the editor's rounded top corners blend into the header instead
of showing a mismatched strip.
*/
#sb-main:has(.sky-dashboard) .cm-editor::before,
#sb-main:has(.sky-dashboard) .cm-editor::after {
  pointer-events: none;
}

/* Dark mode relies on the existing dark --sj-page-background token. */
html[data-theme="dark"] #sb-main:has(.sky-dashboard) .cm-editor {
  border-color: var(--sj-dashboard-frame-border) !important;
  background: var(--sj-page-background) !important;
  box-shadow: var(--sj-dashboard-frame-shadow) !important;
}

@media (max-width: 760px) {
  #sb-main:has(.sky-dashboard) .cm-editor {
    margin-top: 0 !important;
    margin-right: 0 !important;
    margin-bottom: 22px !important;
    margin-left: 0 !important;
    border-radius: 14px !important;
  }
}
```

## 📚 07｜正文内容样式：标题、引用、表格与任务

提供 H1–H6 层级、装饰点阵、引用卡片、表格交互以及圆形任务复选框。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8 CONTENT STYLE PORT
   Adapted from the uploaded Markdown CSS:
   - H1–H6 hierarchy and trailing dot-matrix ornaments
   - blockquotes
   - inline/fenced code
   - tables
   - circular task checkboxes
   Colors remain Sky Journal light/dark tokens.
   ========================================================= */

html {
  /* Heading ornaments: one to six dots, recolored through CSS masks. */
  --sj-h1-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='25' r='2.5'/%3E%3C/svg%3E");
  --sj-h2-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='20' r='2.5'/%3E%3Ccircle cx='13' cy='27' r='2.5'/%3E%3C/svg%3E");
  --sj-h3-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='20' r='2.5'/%3E%3Ccircle cx='6' cy='27' r='2.5'/%3E%3Ccircle cx='13' cy='27' r='2.5'/%3E%3C/svg%3E");
  --sj-h4-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='20' r='2.5'/%3E%3Ccircle cx='6' cy='27' r='2.5'/%3E%3Ccircle cx='13' cy='20' r='2.5'/%3E%3Ccircle cx='13' cy='27' r='2.5'/%3E%3C/svg%3E");
  --sj-h5-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='13' r='2.5'/%3E%3Ccircle cx='6' cy='20' r='2.5'/%3E%3Ccircle cx='6' cy='27' r='2.5'/%3E%3Ccircle cx='13' cy='20' r='2.5'/%3E%3Ccircle cx='13' cy='27' r='2.5'/%3E%3C/svg%3E");
  --sj-h6-icon:
    url("data:image/svg+xml,%3Csvg viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='6' cy='13' r='2.5'/%3E%3Ccircle cx='6' cy='20' r='2.5'/%3E%3Ccircle cx='6' cy='27' r='2.5'/%3E%3Ccircle cx='13' cy='13' r='2.5'/%3E%3Ccircle cx='13' cy='20' r='2.5'/%3E%3Ccircle cx='13' cy='27' r='2.5'/%3E%3C/svg%3E");

  --sj-heading-primary: var(--sj-blue-strong);
  --sj-heading-deep: var(--sj-blue-deep);
  --sj-heading-soft: color-mix(in srgb, var(--sj-blue), transparent 42%);
  --sj-heading-h2-text: #ffffff;
  --sj-heading-h2-background:
    linear-gradient(
      110deg,
      color-mix(in srgb, var(--sj-blue), white 30%),
      var(--sj-blue-strong),
      color-mix(in srgb, var(--sj-blue), var(--sj-gold) 18%)
    );

  --sj-quote-surface:
    linear-gradient(
      135deg,
      color-mix(in srgb, var(--sj-surface-soft), white 18%),
      color-mix(in srgb, var(--sj-surface), var(--sj-blue) 5%)
    );
  --sj-quote-surface-hover:
    linear-gradient(
      135deg,
      color-mix(in srgb, var(--sj-surface-soft), var(--sj-blue) 6%),
      color-mix(in srgb, var(--sj-surface), var(--sj-gold) 4%)
    );
  --sj-quote-border: color-mix(in srgb, var(--sj-blue), transparent 65%);
  --sj-quote-icon: var(--sj-gold);
  --sj-quote-text: var(--sj-text-soft);

  --sj-code-surface: #f7fbff;
  --sj-code-surface-soft: #edf6ff;
  --sj-code-header:
    linear-gradient(
      180deg,
      color-mix(in srgb, var(--sj-surface-solid), var(--sj-blue) 5%),
      color-mix(in srgb, var(--sj-surface-soft), var(--sj-blue) 7%)
    );
  --sj-code-border: color-mix(in srgb, var(--sj-blue), transparent 58%);
  --sj-code-text: #3d5870;
  --sj-inline-code-surface: #eaf5ff;
  --sj-inline-code-text: #2f75ad;
  --sj-inline-code-hover: var(--sj-blue-strong);

  --sj-table-surface: color-mix(in srgb, var(--sj-surface-solid), transparent 3%);
  --sj-table-header:
    linear-gradient(
      110deg,
      color-mix(in srgb, var(--sj-blue), transparent 78%),
      color-mix(in srgb, var(--sj-gold), transparent 84%)
    );
  --sj-table-border: color-mix(in srgb, var(--sj-blue), transparent 68%);
  --sj-table-cell-border: color-mix(in srgb, var(--sj-blue), transparent 82%);
  --sj-table-hover: color-mix(in srgb, var(--sj-blue), transparent 91%);
  --sj-table-cell-hover: color-mix(in srgb, var(--sj-blue), transparent 86%);
}

html[data-theme="dark"] {
  --sj-heading-primary: #8fcaff;
  --sj-heading-deep: #d7ebff;
  --sj-heading-soft: rgba(143, 202, 255, .58);
  --sj-heading-h2-text: #eef8ff;
  --sj-heading-h2-background:
    linear-gradient(
      110deg,
      #234967,
      #2f78ae,
      color-mix(in srgb, #2f78ae, var(--sj-gold) 18%)
    );

  --sj-quote-surface:
    linear-gradient(
      135deg,
      rgba(19, 43, 64, .94),
      rgba(10, 27, 43, .92)
    );
  --sj-quote-surface-hover:
    linear-gradient(
      135deg,
      rgba(24, 52, 76, .98),
      rgba(13, 33, 51, .96)
    );
  --sj-quote-border: rgba(127, 197, 255, .22);
  --sj-quote-icon: var(--sj-gold);
  --sj-quote-text: #b8cada;

  --sj-code-surface: #101f2e;
  --sj-code-surface-soft: #142a3f;
  --sj-code-header:
    linear-gradient(
      180deg,
      rgba(27, 55, 80, .98),
      rgba(17, 38, 58, .98)
    );
  --sj-code-border: rgba(127, 197, 255, .24);
  --sj-code-text: #d7e6f5;
  --sj-inline-code-surface: #17324a;
  --sj-inline-code-text: #9ed0ff;
  --sj-inline-code-hover: #4b95cc;

  --sj-table-surface: rgba(13, 30, 47, .96);
  --sj-table-header:
    linear-gradient(
      110deg,
      rgba(63, 128, 181, .30),
      rgba(228, 189, 112, .13)
    );
  --sj-table-border: rgba(127, 197, 255, .24);
  --sj-table-cell-border: rgba(127, 197, 255, .12);
  --sj-table-hover: rgba(127, 197, 255, .075);
  --sj-table-cell-hover: rgba(127, 197, 255, .13);
}

/* ---------- H1–H6 ---------- */

#sb-main:not(:has(.sky-dashboard)) .cm-content > .cm-line:is(
  .sb-line-h1,
  .sb-line-h2,
  .sb-line-h3,
  .sb-line-h4,
  .sb-line-h5,
  .sb-line-h6
),
#sb-main:not(:has(.sky-dashboard)) .cm-content > :is(
  h1,
  h2,
  h3,
  h4,
  h5,
  h6
) {
  box-sizing: border-box;
  color: var(--sj-heading-deep) !important;
  font-family: var(--sj-heading-font) !important;
  font-weight: 700 !important;
  letter-spacing: .025em;
  transition:
    color .26s ease,
    transform .26s ease,
    padding .26s ease,
    background-position .42s ease,
    box-shadow .26s ease;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .cm-line:is(
  .sb-line-h1,
  .sb-line-h2,
  .sb-line-h3,
  .sb-line-h4,
  .sb-line-h5,
  .sb-line-h6
)::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > :is(
  h1,
  h2,
  h3,
  h4,
  h5,
  h6
)::after {
  content: "";
  display: inline-block;
  width: 1.45em;
  height: 1.45em;
  margin-left: .12em;
  vertical-align: -.36em;
  background: var(--sj-heading-soft);
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  -webkit-mask-position: center;
  mask-position: center;
  -webkit-mask-size: 1.25em 1.25em;
  mask-size: 1.25em 1.25em;
  opacity: .9;
  transition:
    transform .28s cubic-bezier(.34, 1.56, .64, 1),
    background-color .26s ease;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1::after {
  -webkit-mask-image: var(--sj-h1-icon);
  mask-image: var(--sj-h1-icon);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2::after {
  -webkit-mask-image: var(--sj-h2-icon);
  mask-image: var(--sj-h2-icon);
  background: color-mix(in srgb, white, var(--sj-gold) 18%);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h3::after {
  -webkit-mask-image: var(--sj-h3-icon);
  mask-image: var(--sj-h3-icon);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h4::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h4::after {
  -webkit-mask-image: var(--sj-h4-icon);
  mask-image: var(--sj-h4-icon);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h5::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h5::after {
  -webkit-mask-image: var(--sj-h5-icon);
  mask-image: var(--sj-h5-icon);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h6::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h6::after {
  -webkit-mask-image: var(--sj-h6-icon);
  mask-image: var(--sj-h6-icon);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .cm-line:is(
  .sb-line-h1,
  .sb-line-h2,
  .sb-line-h3,
  .sb-line-h4,
  .sb-line-h5,
  .sb-line-h6
):hover::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > :is(
  h1,
  h2,
  h3,
  h4,
  h5,
  h6
):hover::after {
  transform: rotate(10deg) scale(1.14);
  background: var(--sj-gold);
}

/* H1: centered title with a short line expanding on hover/focus. */
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1 {
  position: relative;
  width: fit-content;
  min-width: 120px;
  margin: 1.35em auto .9em !important;
  padding: 0 0 .58em !important;
  border: 0 !important;
  font-size: 1.8rem !important;
  line-height: 1.4 !important;
  text-align: center;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1::before {
  content: "";
  position: absolute;
  left: 50%;
  bottom: 0;
  width: 42px;
  height: 4px;
  border-radius: 999px;
  background: var(--sj-heading-h2-background);
  transform: translateX(-50%);
  transition: width .38s cubic-bezier(.25, .8, .25, 1);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1:hover,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1:hover {
  color: var(--sj-heading-primary) !important;
  transform: translateY(-2px);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1.cm-activeLine::before {
  width: 100%;
}

/* H2: compact blue/gold gradient plate. */
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2 {
  width: fit-content;
  margin: 1.2em 0 .78em !important;
  padding: .3em .78em !important;
  border: 0 !important;
  border-radius: 9px !important;
  background: var(--sj-heading-h2-background) !important;
  background-size: 200% auto !important;
  background-position: 0 center !important;
  color: var(--sj-heading-h2-text) !important;
  font-size: 1.4rem !important;
  line-height: 1.5 !important;
  box-shadow: 0 4px 12px rgba(61, 116, 166, .12);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > h2::before {
  content: none !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2:hover,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2:hover {
  background-position: 100% center !important;
  transform: scale(1.012);
  box-shadow: 0 8px 20px rgba(61, 116, 166, .20);
}

/* H3: slim vertical route marker. */
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h3 {
  position: relative;
  width: fit-content;
  margin: 1.15em 0 .68em !important;
  padding: 0 0 0 .72em !important;
  font-size: 1.3rem !important;
  line-height: 1.5 !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h3::before {
  content: "";
  position: absolute;
  left: -.16em;
  top: 50%;
  width: 5px;
  height: 62%;
  border-radius: 999px;
  background: var(--sj-heading-primary);
  transform: translateY(-50%);
  transition:
    width .25s ease,
    height .25s ease,
    background .25s ease;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3:hover,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h3:hover {
  padding-left: 1.1em !important;
  color: var(--sj-heading-primary) !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h3:hover::before {
  width: 7px;
  height: 70%;
  background: var(--sj-gold);
}

/* H4–H6: progressively lighter route markers. */
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h4,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h4 {
  margin: 1.05em 0 .58em !important;
  font-size: 1.15rem !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h5,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h5,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h6,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h6 {
  margin: 1em 0 .55em !important;
  font-size: 1.08rem !important;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h4::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h4::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h5::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h5::before {
  content: "";
  display: inline-block;
  box-sizing: border-box;
  width: .62em;
  height: .62em;
  margin-right: .48em;
  border-radius: 50%;
  vertical-align: .04em;
  transition:
    transform .26s cubic-bezier(.34, 1.56, .64, 1),
    background .26s ease,
    box-shadow .26s ease;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h4::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h4::before {
  border: 1px solid var(--sj-heading-primary);
  background: var(--sj-heading-primary);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h5::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h5::before {
  border: 2px solid var(--sj-heading-primary);
  background: transparent;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h6::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h6::before {
  content: "—";
  display: inline-block;
  margin-right: .45em;
  color: var(--sj-heading-primary);
  font-weight: 800;
  transition: transform .25s ease;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .cm-line:is(
  .sb-line-h4,
  .sb-line-h5,
  .sb-line-h6
):hover,
#sb-main:not(:has(.sky-dashboard)) .cm-content > :is(
  h4,
  h5,
  h6
):hover {
  color: var(--sj-heading-primary) !important;
  transform: translateX(6px);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h4:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h4:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h5:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h5:hover::before {
  transform: scale(1.22);
  background: var(--sj-gold);
  border-color: var(--sj-gold);
  box-shadow: 0 0 0 4px color-mix(in srgb, var(--sj-gold), transparent 82%);
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h6:hover::before,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h6:hover::before {
  transform: scaleX(1.7);
  color: var(--sj-gold);
}

/* ---------- Blockquotes ---------- */

/*
Rendered blockquotes outside CodeMirror retain the Sky Journal card.

Inside CodeMirror, however, the theme does not style the rendered
blockquote wrapper itself. The editor card is drawn exclusively on lines
that SilverBullet marks as containing a real QuoteMark.
*/
#sb-main:not(:has(.sky-dashboard))
:not(.cm-editor) > blockquote,
#sb-main:not(:has(.sky-dashboard))
:not(.cm-editor) > .sb-blockquote {
  position: relative;
  box-sizing: border-box;
  margin: 1.1rem 0 !important;
  padding: 1rem 1.15rem 1rem 3rem !important;
  border: 1px solid var(--sj-quote-border) !important;
  border-radius: 16px !important;
  background: var(--sj-quote-surface) !important;
  color: var(--sj-quote-text) !important;
  line-height: 1.68;
  box-shadow: 0 8px 22px rgba(61, 116, 166, .06) !important;
}

#sb-main:not(:has(.sky-dashboard))
:not(.cm-editor) > blockquote::before,
#sb-main:not(:has(.sky-dashboard))
:not(.cm-editor) > .sb-blockquote::before {
  content: "✦";
  position: absolute;
  left: 1rem;
  top: 1.02rem;
  color: var(--sj-quote-icon);
  font-family: var(--sj-ui-font) !important;
  font-size: 1.05rem;
  line-height: 1;
}

/*
Compatibility selector for SilverBullet editor versions:

Current builds attach .sb-blockquote-outside directly to .cm-line via
Decoration.line(). Some older/client-cached builds may expose the same
marker as a direct child. Both shapes identify a line with an actual
Markdown QuoteMark.

A marker-less lazy continuation line matches neither selector and is
therefore never painted as a quote card by the theme.
*/
#sb-main:not(:has(.sky-dashboard)) .cm-editor
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
) {
  position: relative !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: .34rem 1.15rem .34rem 3rem !important;
  border-top: 0 !important;
  border-right: 1px solid var(--sj-quote-border) !important;
  border-bottom: 0 !important;
  border-left: 1px solid var(--sj-quote-border) !important;
  border-radius: 0 !important;
  background: var(--sj-quote-surface) !important;
  color: var(--sj-quote-text) !important;
  text-indent: 0 !important;
  line-height: 1.68 !important;
  box-shadow: none !important;
}

/*
Neutralize any inner quote wrapper rendered by CodeMirror. The outer
explicit line owns the card, so an inner wrapper must not create a second
background or extend the card over lazy continuation content.
*/
#sb-main:not(:has(.sky-dashboard)) .cm-editor
.cm-line > :is(
  blockquote,
  .sb-blockquote,
  .sb-blockquote-outside
) {
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  color: inherit !important;
  box-shadow: none !important;
}

/* First explicit quote line. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
):not(
  :where(
    .cm-line.sb-blockquote-outside,
    .cm-line:has(> .sb-blockquote-outside)
  )
  +
  :where(
    .cm-line.sb-blockquote-outside,
    .cm-line:has(> .sb-blockquote-outside)
  )
) {
  margin-top: .6rem !important;
  padding-top: .95rem !important;
  border-top: 1px solid var(--sj-quote-border) !important;
  border-top-left-radius: 16px !important;
  border-top-right-radius: 16px !important;
}

/* Decorative marker on the first explicit line only. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
):not(
  :where(
    .cm-line.sb-blockquote-outside,
    .cm-line:has(> .sb-blockquote-outside)
  )
  +
  :where(
    .cm-line.sb-blockquote-outside,
    .cm-line:has(> .sb-blockquote-outside)
  )
)::before {
  content: "✦";
  position: absolute;
  left: 1rem;
  top: 1.02rem;
  color: var(--sj-quote-icon);
  font-family: var(--sj-ui-font) !important;
  font-size: 1.05rem;
  line-height: 1;
  pointer-events: none;
}

/* Last explicit quote line. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
):not(
  :has(
    +
    :where(
      .cm-line.sb-blockquote-outside,
      .cm-line:has(> .sb-blockquote-outside)
    )
  )
) {
  margin-bottom: .6rem !important;
  padding-bottom: .95rem !important;
  border-bottom: 1px solid var(--sj-quote-border) !important;
  border-bottom-right-radius: 16px !important;
  border-bottom-left-radius: 16px !important;
}

/* Visually merge adjacent explicit quote lines. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
)
+
:where(
  .cm-line.sb-blockquote-outside,
  .cm-line:has(> .sb-blockquote-outside)
) {
  margin-top: -1px !important;
}

/* Active explicit quote lines keep the same card surface. */
#sb-main:not(:has(.sky-dashboard)) .cm-editor
.cm-line.cm-activeLine:is(
  .sb-blockquote-outside,
  :has(> .sb-blockquote-outside)
) {
  background: var(--sj-quote-surface-hover) !important;
}

/*
No editor-wide blockquote selector is used below this point.

In particular, the theme intentionally does not paint:
- .cm-editor blockquote
- .cm-editor .sb-blockquote
- marker-less lines merely parsed as lazy blockquote continuations
*/

/* ---------- Tables ---------- */

#sb-main table,
#sb-main .sb-table,
#sb-main .sb-table-widget table {
  width: 100% !important;
  margin: 1.1rem 0 !important;
  overflow: hidden;
  border: 1px solid var(--sj-table-border) !important;
  border-collapse: separate !important;
  border-spacing: 0 !important;
  border-radius: 10px !important;
  background: var(--sj-table-surface) !important;
  color: var(--sj-text) !important;
  font-size: .9rem;
  line-height: 1.58;
  box-shadow: 0 8px 22px rgba(61, 116, 166, .055) !important;
}

#sb-main table :is(th, td),
#sb-main .sb-table :is(th, td),
#sb-main .sb-table-widget table :is(th, td) {
  box-sizing: border-box;
  padding: .58rem .76rem !important;
  border-top: 0 !important;
  border-left: 0 !important;
  border-right: 1px solid var(--sj-table-cell-border) !important;
  border-bottom: 1px solid var(--sj-table-cell-border) !important;
  background: transparent;
  color: var(--sj-text) !important;
  transition:
    color .18s ease,
    background .18s ease,
    box-shadow .18s ease;
}

#sb-main table :is(th, td):last-child,
#sb-main .sb-table :is(th, td):last-child,
#sb-main .sb-table-widget table :is(th, td):last-child {
  border-right: 0 !important;
}

#sb-main table tr:last-child td,
#sb-main .sb-table tr:last-child td,
#sb-main .sb-table-widget table tr:last-child td {
  border-bottom: 0 !important;
}

#sb-main table thead,
#sb-main table th,
#sb-main .sb-table thead,
#sb-main .sb-table th,
#sb-main .sb-table-widget table thead,
#sb-main .sb-table-widget table th {
  background: var(--sj-table-header) !important;
  color: var(--sj-heading-deep) !important;
  font-weight: 750 !important;
  white-space: nowrap;
}

#sb-main table tbody tr:hover td,
#sb-main .sb-table tbody tr:hover td,
#sb-main .sb-table-widget table tbody tr:hover td {
  background: var(--sj-table-hover) !important;
}

#sb-main table tbody td:hover,
#sb-main .sb-table tbody td:hover,
#sb-main .sb-table-widget table tbody td:hover {
  background: var(--sj-table-cell-hover) !important;
  color: var(--sj-heading-primary) !important;
  box-shadow: inset 0 0 0 1px var(--sj-table-border);
}

/* ---------- Circular task checkboxes ---------- */

/*
SilverBullet's official editor CSS uses native input[type="checkbox"]
for both source-mode tasks and rendered Markdown tasks. Only the shape
and palette change here; list indentation and checkbox positioning stay
under SilverBullet's own layout rules.
*/
#sb-main input[type="checkbox"] {
  appearance: none !important;
  -webkit-appearance: none !important;
  display: inline-block !important;
  box-sizing: border-box !important;
  width: 1.25em !important;
  height: 1.25em !important;
  margin: 0 !important;
  padding: 0 !important;
  position: relative;
  vertical-align: middle;
  border: 1.5px solid var(--sj-heading-primary) !important;
  border-radius: 50% !important;
  background: var(--sj-editor-card-background) !important;
  color: #ffffff !important;
  cursor: pointer;
  box-shadow:
    0 0 0 3px color-mix(in srgb, var(--sj-blue), transparent 91%);
  transition:
    transform .18s ease,
    background .18s ease,
    border-color .18s ease,
    box-shadow .18s ease;
}

#sb-main input[type="checkbox"]:hover {
  transform: scale(1.08);
  border-color: var(--sj-gold) !important;
  box-shadow:
    0 0 0 4px color-mix(in srgb, var(--sj-gold), transparent 84%);
}

#sb-main input[type="checkbox"]:checked {
  border-color: var(--sj-heading-primary) !important;
  background: var(--sj-heading-primary) !important;
  color: #ffffff !important;
  animation: sj-task-checkbox-pulse .32s ease;
}

#sb-main input[type="checkbox"]:checked::after {
  content: "" !important;
  position: absolute !important;
  left: 29% !important;
  top: 10% !important;
  width: 31% !important;
  height: 59% !important;
  border: solid currentColor !important;
  border-width: 0 2px 2px 0 !important;
  transform: rotate(45deg) !important;
}

#sb-main input[type="checkbox"]:focus-visible {
  outline: 2px solid var(--sj-gold) !important;
  outline-offset: 2px !important;
}

@keyframes sj-task-checkbox-pulse {
  0% { transform: scale(1); }
  55% { transform: scale(1.14); }
  100% { transform: scale(1); }
}

@media (prefers-reduced-motion: reduce) {
  #sb-main:not(:has(.sky-dashboard)) .cm-content > :is(
    h1,
    h2,
    h3,
    h4,
    h5,
    h6
  ),
  #sb-main:not(:has(.sky-dashboard)) .cm-content > .cm-line:is(
    .sb-line-h1,
    .sb-line-h2,
    .sb-line-h3,
    .sb-line-h4,
    .sb-line-h5,
    .sb-line-h6
  ),
  #sb-main blockquote,
  #sb-main .sb-blockquote,
  #sb-main input[type="checkbox"] {
    transition: none !important;
    animation: none !important;
  }
}

@media (max-width: 760px) {
  #sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1,
  #sb-main:not(:has(.sky-dashboard)) .cm-content > h1 {
    font-size: 1.58rem !important;
  }

  #sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2,
  #sb-main:not(:has(.sky-dashboard)) .cm-content > h2 {
    font-size: 1.28rem !important;
  }

  #sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h3,
  #sb-main:not(:has(.sky-dashboard)) .cm-content > h3 {
    font-size: 1.18rem !important;
  }

  #sb-main table,
  #sb-main .sb-table,
  #sb-main .sb-table-widget table {
    font-size: .84rem;
  }

  #sb-main table :is(th, td),
  #sb-main .sb-table :is(th, td),
  #sb-main .sb-table-widget table :is(th, td) {
    padding: .5rem .58rem !important;
  }
}
```

## 💻 08｜分割线、行内代码与围栏代码块

实现中央星标虚线分割线、行内代码、渲染代码块与 SilverBullet 源码模式围栏代码块。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.1 DASHED STAR DIVIDER
   Visual form:
   - - - - - - - ✦ - - - - - - -
   ========================================================= */

html {
  --sj-divider-dash-color:
    color-mix(in srgb, var(--sj-blue-strong), transparent 28%);
  --sj-divider-star-color: var(--sj-gold);
}

html[data-theme="dark"] {
  --sj-divider-dash-color:
    color-mix(in srgb, #8fcaff, transparent 28%);
  --sj-divider-star-color: var(--sj-gold);
}

#sb-main hr,
#sb-main .sb-hr,
#sb-main .sb-line-hr {
  position: relative !important;
  display: block !important;
  box-sizing: border-box !important;
  width: min(100%, 560px) !important;
  height: 30px !important;
  margin: 1.85rem auto !important;
  padding: 0 !important;
  overflow: visible !important;
  border: 0 !important;
  background: none !important;
  color: transparent !important;
  box-shadow: none !important;
}

/* Hide the raw Markdown ruler markers while editing. */
#sb-main .sb-line-hr > * {
  opacity: 0 !important;
}

/* Seven short dashes on each side, with a fixed central gap. */
#sb-main hr::before,
#sb-main .sb-hr::before,
#sb-main .sb-line-hr::before {
  content: "- - - - - - -       - - - - - - -";
  position: absolute;
  top: 50%;
  left: 50%;
  display: block;
  width: max-content;
  max-width: 100%;
  transform: translate(-50%, -50%);
  color: var(--sj-divider-dash-color);
  font-family: var(--sj-ui-font) !important;
  font-size: .92rem;
  font-weight: 600;
  line-height: 1;
  letter-spacing: .08em;
  white-space: pre;
  pointer-events: none;
}

/* Gold route star placed in the center gap. */
#sb-main hr::after,
#sb-main .sb-hr::after,
#sb-main .sb-line-hr::after {
  content: "✦";
  position: absolute;
  top: 50%;
  left: 50%;
  display: block;
  padding: 0;
  transform: translate(-50%, -52%);
  background: transparent !important;
  color: var(--sj-divider-star-color);
  font-family: var(--sj-ui-font) !important;
  font-size: .9rem;
  font-weight: 800;
  line-height: 1;
  text-shadow:
    0 0 10px color-mix(in srgb, var(--sj-gold), transparent 62%);
  pointer-events: none;
}

@media (max-width: 520px) {
  #sb-main hr,
  #sb-main .sb-hr,
  #sb-main .sb-line-hr {
    width: 100% !important;
    margin: 1.55rem auto !important;
  }

  #sb-main hr::before,
  #sb-main .sb-hr::before,
  #sb-main .sb-line-hr::before {
    font-size: .76rem;
    letter-spacing: .035em;
  }

  #sb-main hr::after,
  #sb-main .sb-hr::after,
  #sb-main .sb-line-hr::after {
    font-size: .82rem;
  }
}


/* =========================================================
   v1.8.2 HEADING + FENCED CODE FIX
   ========================================================= */

/* ---------- H1 / H2: no trailing dot ornament ---------- */

/*
The trailing ornament changes the intrinsic width of centered H1 and
the compact H2 plate. H3–H6 keep their dot-matrix ornaments.
*/
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h1::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h1::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2::after,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2::after {
  content: none !important;
  display: none !important;
  width: 0 !important;
  height: 0 !important;
  margin: 0 !important;
  -webkit-mask-image: none !important;
  mask-image: none !important;
}

/* H2 uses a soft off-white foreground against the blue/gold plate. */
html {
  --sj-heading-h2-text: #f3f7fb;
}

html[data-theme="dark"] {
  --sj-heading-h2-text: #edf5fb;
}

#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2,
#sb-main:not(:has(.sky-dashboard)) .cm-content > .sb-line-h2 *,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2,
#sb-main:not(:has(.sky-dashboard)) .cm-content > h2 * {
  color: var(--sj-heading-h2-text) !important;
  -webkit-text-fill-color: var(--sj-heading-h2-text) !important;
}

/* Markdown markers remain visible but slightly quieter while editing. */
#sb-main:not(:has(.sky-dashboard))
.cm-content > .sb-line-h2 .sb-meta {
  opacity: .74;
}

/* ---------- Inline code: one source of truth ---------- */

#sb-main span.sb-code,
#sb-main code:not(pre code),
#sb-main .cm-inlineCode {
  display: inline;
  box-sizing: border-box;
  margin: 0 .1em !important;
  padding: .1em .42em !important;
  border: 1px solid var(--sj-code-border) !important;
  border-radius: 7px !important;
  background: var(--sj-inline-code-surface) !important;
  color: var(--sj-inline-code-text) !important;
  font-family: var(--sj-code-font) !important;
  font-size: .9em !important;
  line-height: inherit !important;
  vertical-align: baseline;
  box-shadow: none !important;
  transition:
    color .18s ease,
    background .18s ease,
    border-color .18s ease,
    box-shadow .18s ease;
}

#sb-main span.sb-code:hover,
#sb-main code:not(pre code):hover,
#sb-main .cm-inlineCode:hover {
  border-color: var(--sj-inline-code-hover) !important;
  background: var(--sj-inline-code-hover) !important;
  color: #ffffff !important;
  box-shadow:
    0 4px 10px
    color-mix(in srgb, var(--sj-blue), transparent 76%) !important;
}

/* ---------- Rendered code blocks ---------- */

#sb-main pre,
#sb-main .sb-code-block {
  position: relative;
  box-sizing: border-box;
  overflow: auto;
  margin: 1rem 0 !important;
  padding: 2.65rem 1rem 1rem !important;
  border: 1px solid var(--sj-code-border) !important;
  border-radius: 11px !important;
  background: var(--sj-code-surface) !important;
  color: var(--sj-code-text) !important;
  font-family: var(--sj-code-font) !important;
  box-shadow: 0 8px 22px rgba(61, 116, 166, .07) !important;
}

#sb-main pre::before,
#sb-main .sb-code-block::before {
  content: "";
  position: absolute;
  inset: 0 0 auto 0;
  height: 31px;
  border-bottom: 1px solid var(--sj-code-border);
  border-radius: 10px 10px 0 0;
  background:
    radial-gradient(
      circle at 16px 15px,
      #ef7b7b 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 31px 15px,
      #e5bd69 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 46px 15px,
      #76c597 0 4px,
      transparent 4.5px
    ),
    var(--sj-code-header);
}

#sb-main pre code,
#sb-main .sb-code-block * {
  font-family: var(--sj-code-font) !important;
}

/* ---------- SilverBullet source-mode fenced code ---------- */

/*
A fenced block is a run of consecutive .sb-line-fenced-code editor
lines. The opening fence also contains .sb-actions and .sb-meta, so
those classes cannot be used to decide where the block ends.
*/
#sb-main .cm-content > .sb-line-fenced-code {
  position: relative;
  box-sizing: border-box !important;
  min-height: 1.68em;
  margin: 0 !important;
  padding: .08rem 1rem !important;
  overflow: visible !important;
  border-top: 0 !important;
  border-right: 1px solid var(--sj-code-border) !important;
  border-bottom: 0 !important;
  border-left: 1px solid var(--sj-code-border) !important;
  border-radius: 0 !important;
  background: var(--sj-code-surface) !important;
  color: var(--sj-code-text) !important;
  font-family: var(--sj-code-font) !important;
  font-size: .9em !important;
  line-height: 1.68 !important;
  box-shadow: none !important;
}

/*
Opening and closing rows are identified by their own DOM contents,
rather than by adjacency. This keeps two immediately adjacent fenced
blocks visually independent.
*/

/* Opening fence: owns the language label and/or action bar. */
#sb-main .cm-content >
.sb-line-code-outside.sb-line-fenced-code:has(
  .sb-code-info,
  .sb-actions
) {
  min-height: 34px !important;
  margin-top: 1rem !important;
  margin-bottom: 0 !important;
  padding: 0 !important;
  border-top: 1px solid var(--sj-code-border) !important;
  border-right: 1px solid var(--sj-code-border) !important;
  border-bottom: 1px solid var(--sj-code-border) !important;
  border-left: 1px solid var(--sj-code-border) !important;
  border-radius: 11px 11px 0 0 !important;
  background:
    radial-gradient(
      circle at 16px 16px,
      #ef7b7b 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 31px 16px,
      #e5bd69 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 46px 16px,
      #76c597 0 4px,
      transparent 4.5px
    ),
    var(--sj-code-header) !important;
}

/* Closing fence: has no language label or action bar. */
#sb-main .cm-content >
.sb-line-code-outside.sb-line-fenced-code:not(:has(
  .sb-code-info,
  .sb-actions
)) {
  min-height: .72rem !important;
  margin-top: 0 !important;
  margin-bottom: 1rem !important;
  padding: 0 !important;
  border-top: 0 !important;
  border-right: 1px solid var(--sj-code-border) !important;
  border-bottom: 1px solid var(--sj-code-border) !important;
  border-left: 1px solid var(--sj-code-border) !important;
  border-radius: 0 0 11px 11px !important;
  background: var(--sj-code-surface) !important;
}

/* Actual code lines stay square between their own opening and closing rows. */
#sb-main .cm-content >
.sb-line-fenced-code:not(.sb-line-code-outside) {
  margin-top: 0 !important;
  margin-bottom: 0 !important;
  border-radius: 0 !important;
}

/*
Follow SilverBullet's own behavior: opening/closing Markdown fences are
transparent, while the language label and copy action remain visible.
*/
#sb-main .cm-content >
.sb-line-code-outside.sb-line-fenced-code {
  color: transparent !important;
}

#sb-main .cm-content >
.sb-line-code-outside.sb-line-fenced-code .sb-meta {
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-code-info {
  position: absolute !important;
  top: 8px !important;
  right: 42px !important;
  z-index: 2;
  display: block !important;
  float: none !important;
  padding: 0 !important;
  color:
    color-mix(
      in srgb,
      var(--sj-code-text),
      transparent 28%
    ) !important;
  -webkit-text-fill-color:
    color-mix(
      in srgb,
      var(--sj-code-text),
      transparent 28%
    ) !important;
  font-size: .78rem !important;
  line-height: 1 !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-actions {
  position: absolute !important;
  top: 4px !important;
  right: 7px !important;
  z-index: 3;
  float: none !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-actions button,
#sb-main .cm-content >
.sb-line-fenced-code .sb-code-copy-button {
  width: 25px !important;
  min-width: 25px !important;
  max-width: 25px !important;
  height: 24px !important;
  min-height: 24px !important;
  max-height: 24px !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 6px !important;
  background: transparent !important;
  color:
    color-mix(
      in srgb,
      var(--sj-code-text),
      transparent 26%
    ) !important;
  box-shadow: none !important;
  transform: none !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-actions button:hover,
#sb-main .cm-content >
.sb-line-fenced-code .sb-code-copy-button:hover {
  background:
    color-mix(
      in srgb,
      var(--sj-blue),
      transparent 87%
    ) !important;
  color: var(--sj-heading-primary) !important;
}

/* Code text and syntax. */
/*
Fenced-code content must never inherit the rounded inline-code capsule.
This reset applies to every fenced language, not only plain text.
*/
#sb-main .cm-content >
.sb-line-fenced-code .sb-code,
#sb-main .cm-content >
.sb-line-fenced-code span.sb-code {
  display: inline !important;
  box-sizing: content-box !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  background-color: transparent !important;
  color: var(--sj-code-text) !important;
  font-family: var(--sj-code-font) !important;
  line-height: inherit !important;
  vertical-align: baseline !important;
  box-shadow: none !important;
  transform: none !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-code > * {
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background-color: transparent !important;
  box-shadow: none !important;
}

#sb-main .cm-content >
.sb-line-fenced-code * {
  font-family: var(--sj-code-font) !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-keyword {
  color: var(--editor-code-variable-color) !important;
  font-weight: 700 !important;
}

#sb-main .cm-content >
.sb-line-fenced-code :is(
  .sb-string,
  .sb-string2,
  .sb-regexp
) {
  color: var(--editor-code-string-color) !important;
}

#sb-main .cm-content >
.sb-line-fenced-code .sb-number {
  color: var(--editor-code-number-color) !important;
}

#sb-main .cm-content >
.sb-line-fenced-code :is(
  .sb-typeName,
  .sb-bool,
  .sb-literal
) {
  color: var(--editor-code-typename-color) !important;
}

#sb-main .cm-content >
.sb-line-fenced-code :is(
  .sb-comment,
  .sb-comment-marker
) {
  color: var(--editor-code-comment-color) !important;
  font-style: italic !important;
}

#sb-main .cm-content >
.sb-line-fenced-code :is(
  .sb-operator,
  .sb-punctuation
) {
  color: var(--editor-code-operator-color) !important;
}

/* Prevent the current line highlight from splitting the code surface. */
#sb-main .cm-content >
.sb-line-fenced-code.cm-activeLine {
  background-color: var(--sj-code-surface) !important;
}

#sb-main .cm-content >
.sb-line-code-outside.sb-line-fenced-code:has(
  .sb-code-info,
  .sb-actions
).cm-activeLine {
  background:
    radial-gradient(
      circle at 16px 16px,
      #ef7b7b 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 31px 16px,
      #e5bd69 0 4px,
      transparent 4.5px
    ),
    radial-gradient(
      circle at 46px 16px,
      #76c597 0 4px,
      transparent 4.5px
    ),
    var(--sj-code-header) !important;
}


/*
CodeMirror's drawSelection layer normally sits behind editor content.
That works while .cm-line backgrounds are transparent, but fenced-code
rows use an opaque card surface and would cover the selection rectangles.

Only editors containing fenced code lift the existing CodeMirror
selection layer above content. The theme does not replace, recolor or
redraw the selection itself.
*/
#sb-main
.cm-editor:has(
  .cm-content > .sb-line-fenced-code
)
> .cm-scroller
> .cm-selectionLayer:has(.cm-selectionBackground) {
  z-index: 1 !important;
  pointer-events: none !important;
}

/*
Keep cursors and iOS selection handles above the lifted selection fill.
CodeMirror normally gives the cursor layer a high positive z-index; this
explicit rule protects that ordering from other theme modules.
*/
#sb-main
.cm-editor:has(
  .cm-content > .sb-line-fenced-code
)
> .cm-scroller
> .cm-cursorLayer {
  z-index: 150 !important;
  pointer-events: none !important;
}
```

## 🗂️ 09｜TOC、Frontmatter、Widget 工具栏与列表微调

针对真实 DOM 精修目录卡片、可折叠 Frontmatter、标题栏字体、Lua Widget 工具栏，以及列表圆点和任务圆圈的微像素对齐。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.5 EXACT DOM TARGETS
   Based on the actual DOM shown in DevTools:
   TOC:
   .sb-lua-directive-block.sb-lua-top-widget
     > div
       > .button-bar
       > .content
         > details
           > summary.sb-toc-summary
           > ul

   Frontmatter:
   .cm-line.sb-line-frontmatter-outside.sb-frontmatter
   .cm-line.sb-frontmatter
   .cm-line.sb-line-frontmatter-outside.sb-frontmatter
   ========================================================= */

html {
  --sj-toc-shell-background:
    radial-gradient(
      circle at 0% 0%,
      rgba(121, 184, 244, .15),
      transparent 42%
    ),
    radial-gradient(
      circle at 100% 120%,
      rgba(209, 173, 102, .10),
      transparent 38%
    ),
    rgba(251, 253, 255, .94);
  --sj-toc-header-background:
    linear-gradient(
      110deg,
      rgba(228, 243, 255, .98),
      rgba(247, 251, 255, .95)
    );
  --sj-toc-border: rgba(112, 173, 230, .28);
  --sj-toc-divider: rgba(112, 173, 230, .20);
  --sj-toc-shadow:
    0 14px 34px rgba(61, 116, 166, .09);
  --sj-toc-button-background:
    linear-gradient(
      180deg,
      rgba(255, 255, 255, .99),
      rgba(239, 247, 255, .97)
    );
  --sj-toc-button-hover:
    linear-gradient(
      180deg,
      rgba(255, 255, 255, 1),
      rgba(228, 242, 255, .99)
    );
  --sj-toc-button-border: rgba(209, 173, 102, .48);

  --sj-fm-background:
    linear-gradient(
      135deg,
      rgba(239, 248, 255, .97),
      rgba(255, 252, 241, .86)
    );
  --sj-fm-background-hover:
    linear-gradient(
      135deg,
      rgba(232, 245, 255, .99),
      rgba(255, 249, 230, .92)
    );
  --sj-fm-border: rgba(92, 157, 216, .38);
  --sj-fm-key: #3978b7;
  --sj-fm-value: #526f89;
  --sj-fm-string: #8d6a36;
  --sj-fm-badge-background:
    linear-gradient(
      135deg,
      var(--sj-blue-strong),
      color-mix(
        in srgb,
        var(--sj-blue-strong),
        var(--sj-gold) 18%
      )
    );
  --sj-fm-badge-text: #f3f7fb;
}

html[data-theme="dark"] {
  --sj-toc-shell-background:
    radial-gradient(
      circle at 0% 0%,
      rgba(74, 147, 207, .15),
      transparent 42%
    ),
    radial-gradient(
      circle at 100% 120%,
      rgba(228, 189, 112, .07),
      transparent 38%
    ),
    rgba(12, 29, 45, .96);
  --sj-toc-header-background:
    linear-gradient(
      110deg,
      rgba(24, 51, 75, .99),
      rgba(15, 35, 53, .97)
    );
  --sj-toc-border: rgba(127, 197, 255, .22);
  --sj-toc-divider: rgba(127, 197, 255, .16);
  --sj-toc-shadow:
    0 16px 38px rgba(0, 0, 0, .27);
  --sj-toc-button-background:
    linear-gradient(
      180deg,
      rgba(30, 57, 82, .99),
      rgba(17, 38, 58, .99)
    );
  --sj-toc-button-hover:
    linear-gradient(
      180deg,
      rgba(40, 72, 101, 1),
      rgba(24, 50, 74, 1)
    );
  --sj-toc-button-border: rgba(228, 189, 112, .36);

  --sj-fm-background:
    linear-gradient(
      135deg,
      rgba(17, 40, 60, .98),
      rgba(38, 34, 23, .78)
    );
  --sj-fm-background-hover:
    linear-gradient(
      135deg,
      rgba(21, 48, 71, .99),
      rgba(45, 39, 25, .84)
    );
  --sj-fm-border: rgba(127, 197, 255, .26);
  --sj-fm-key: #9fd1fb;
  --sj-fm-value: #b7cada;
  --sj-fm-string: #e4bd70;
  --sj-fm-badge-background:
    linear-gradient(
      135deg,
      #2f78ae,
      color-mix(in srgb, #2f78ae, var(--sj-gold) 20%)
    );
  --sj-fm-badge-text: #edf5fb;
}

/* ---------- TOC: exact SilverBullet DOM ---------- */

/* Reset SilverBullet's default top-widget frame. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) {
  display: block !important;
  min-height: 0 !important;
  margin: 1.1rem 0 1.45rem !important;
  padding: 0 !important;
  overflow: visible !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
  white-space: normal !important;
}

/* The immediate child is the real single-card shell. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div {
  position: relative !important;
  box-sizing: border-box !important;
  overflow: hidden !important;
  border: 1px solid var(--sj-toc-border) !important;
  border-radius: 18px !important;
  background: var(--sj-toc-shell-background) !important;
  box-shadow: var(--sj-toc-shadow) !important;
}

/* Reset the content wrapper from SilverBullet's default 10px padding. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .content {
  box-sizing: border-box !important;
  max-height: 500px !important;
  margin: 0 !important;
  padding: 0 !important;
  overflow: auto !important;
  background: transparent !important;
}

/* Details itself should not add another frame. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .content > details {
  display: block !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
}

/* Exact summary class from the screenshot. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
summary.sb-toc-summary {
  display: flex !important;
  box-sizing: border-box !important;
  width: 100% !important;
  min-height: 58px !important;
  align-items: center !important;
  margin: 0 !important;
  padding: 15px 112px 15px 18px !important;
  border: 0 !important;
  border-bottom: 1px solid var(--sj-toc-divider) !important;
  border-radius: 0 !important;
  background: var(--sj-toc-header-background) !important;
  color: var(--sj-blue-deep) !important;
  font-family: var(--sj-heading-font) !important;
  font-size: 1.02rem !important;
  font-weight: 700 !important;
  line-height: 1.25 !important;
  letter-spacing: .02em !important;
  cursor: pointer !important;
  box-shadow: none !important;
}

html[data-theme="dark"]
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
summary.sb-toc-summary {
  color: #d7ebff !important;
}

/* Prevent heading styles from leaking into the TOC summary. */
#sb-main:not(:has(.sky-dashboard))
summary.sb-toc-summary::before,
#sb-main:not(:has(.sky-dashboard))
summary.sb-toc-summary::after {
  box-sizing: border-box;
}

/* Exact button-bar path from the screenshot. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar {
  position: absolute !important;
  top: 10px !important;
  right: 12px !important;
  z-index: 20 !important;
  display: flex !important;
  align-items: center !important;
  gap: 8px !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
}

/* Exact reload/copy buttons. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar > button {
  display: inline-flex !important;
  flex: 0 0 38px !important;
  width: 38px !important;
  min-width: 38px !important;
  max-width: 38px !important;
  height: 38px !important;
  min-height: 38px !important;
  max-height: 38px !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 1px solid var(--sj-toc-button-border) !important;
  border-radius: 11px !important;
  background: var(--sj-toc-button-background) !important;
  color: var(--sj-blue-deep) !important;
  box-shadow: none !important;
  transform: none !important;
}

html[data-theme="dark"]
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar > button {
  color: #d7ebff !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar > button:hover {
  border-color: var(--sj-gold) !important;
  background: var(--sj-toc-button-hover) !important;
  color: var(--sj-blue-strong) !important;
  box-shadow:
    0 7px 16px rgba(61, 116, 166, .12) !important;
  transform: translateY(-1px) !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar > button > svg {
  display: block !important;
  width: 17px !important;
  height: 17px !important;
  margin: 0 !important;
}

/* TOC list body. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details > ul {
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: .85rem 1rem 1rem 1.25rem !important;
  list-style: none !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details ul {
  list-style: none !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details ul ul {
  margin: .1rem 0 .1rem .55rem !important;
  padding-left: .7rem !important;
  border-left: 1px dashed var(--sj-toc-divider);
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li {
  position: relative;
  margin: .06rem 0 !important;
  padding: 0 !important;
  border-radius: 9px;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li::marker {
  content: "";
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a {
  position: relative;
  display: block;
  box-sizing: border-box;
  width: 100%;
  padding: .3rem .5rem .3rem 1.08rem;
  border-radius: 9px;
  color: var(--sj-text-soft) !important;
  font-family: var(--sj-ui-font) !important;
  font-size: .9rem;
  line-height: 1.42;
  text-decoration: none !important;
  transition:
    color .18s ease,
    background .18s ease,
    padding .18s ease,
    transform .18s ease;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a::before {
  content: "";
  position: absolute;
  left: .4rem;
  top: 50%;
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background: var(--sj-blue);
  transform: translateY(-50%);
  opacity: .75;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a:hover {
  padding-left: 1.32rem;
  background:
    color-mix(
      in srgb,
      var(--sj-blue),
      transparent 89%
    ) !important;
  color: var(--sj-blue-strong) !important;
  transform: translateX(2px);
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a:hover::before {
  background: var(--sj-gold);
  opacity: 1;
}

/* ---------- Frontmatter: exact three-line DOM ---------- */

/*
The screenshot confirms all three editor lines carry .sb-frontmatter:
1. opening fence: .sb-line-frontmatter-outside.sb-frontmatter
2. content row:   .sb-frontmatter
3. closing fence: .sb-line-frontmatter-outside.sb-frontmatter
*/
#sb-main:not(:has(.sky-dashboard))
.cm-content > .cm-line.sb-frontmatter {
  position: relative;
  box-sizing: border-box !important;
  min-height: 1.55em;
  margin: 0 !important;
  padding: .22rem 1rem !important;
  border-top: 0 !important;
  border-right: 1px solid var(--sj-fm-border) !important;
  border-bottom: 0 !important;
  border-left: 1px solid var(--sj-fm-border) !important;
  border-radius: 0 !important;
  background: var(--sj-fm-background) !important;
  color: var(--sj-fm-value) !important;
  -webkit-text-fill-color: var(--sj-fm-value) !important;
  font-family: var(--sj-code-font) !important;
  box-shadow: none !important;
}

/* Remove one-pixel seams between the three consecutive lines. */
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-frontmatter +
.cm-line.sb-frontmatter {
  margin-top: -1px !important;
}

/* Opening fence: identified because the next line is also frontmatter. */
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
) {
  min-height: 34px !important;
  margin-top: 1rem !important;
  padding: 0 !important;
  border-top: 1px solid var(--sj-fm-border) !important;
  border-top-left-radius: 12px !important;
  border-top-right-radius: 12px !important;
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
}

/* Badge belongs only to the opening fence. */
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after {
  content: "frontmatter";
  position: absolute;
  top: 0;
  right: 12px;
  z-index: 3;
  display: inline-flex;
  min-height: 24px;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  padding: 0 10px;
  border-radius: 0 0 8px 8px;
  background: var(--sj-fm-badge-background);
  color: var(--sj-fm-badge-text);
  -webkit-text-fill-color: var(--sj-fm-badge-text);
  font-family: var(--sj-ui-font) !important;
  font-size: .64rem;
  font-weight: 800;
  line-height: 1;
  letter-spacing: .08em;
  box-shadow: 0 4px 10px rgba(61, 116, 166, .14);
  pointer-events: none;
}

/* Content lines: visible metadata. */
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside
) {
  min-height: 1.7em !important;
  padding: .34rem 1rem !important;
  color: var(--sj-fm-value) !important;
  -webkit-text-fill-color: var(--sj-fm-value) !important;
}

/* Closing fence: no following frontmatter line. */
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:not(
  :has(+ .cm-line.sb-frontmatter)
) {
  min-height: 12px !important;
  margin-bottom: 1rem !important;
  padding: 0 !important;
  border-bottom: 1px solid var(--sj-fm-border) !important;
  border-bottom-right-radius: 12px !important;
  border-bottom-left-radius: 12px !important;
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
}

/* Hide the raw --- text and any marker content on fence lines. */
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-line-frontmatter-outside.sb-frontmatter,
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-line-frontmatter-outside.sb-frontmatter * {
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
}

/* Restore the badge after the transparent fence rule. */
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after {
  color: var(--sj-fm-badge-text) !important;
  -webkit-text-fill-color: var(--sj-fm-badge-text) !important;
}

/* Reset older broad .sb-frontmatter styling on inner syntax spans. */
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside
) *,
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside
) .sb-frontmatter {
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
  font-family: var(--sj-code-font) !important;
  font-size: .88rem !important;
  line-height: 1.58 !important;
}

/* Frontmatter syntax colors. */
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside
)
:is(
  .sb-propertyName,
  .sb-keyword,
  .sb-atom
) {
  color: var(--sj-fm-key) !important;
  -webkit-text-fill-color: var(--sj-fm-key) !important;
  font-weight: 700 !important;
}

#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside
)
:is(
  .sb-string,
  .sb-string2
) {
  color: var(--sj-fm-string) !important;
  -webkit-text-fill-color: var(--sj-fm-string) !important;
}

/* Keep active-line editing from creating a yellow pill. */
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-frontmatter.cm-activeLine {
  background: var(--sj-fm-background) !important;
}

/* Unified hover state for the complete frontmatter group. */
#sb-main:not(:has(.sky-dashboard))
.cm-content:has(
  > .cm-line.sb-frontmatter:hover
) >
.cm-line.sb-frontmatter {
  background: var(--sj-fm-background-hover) !important;
}

/* ---------- H6: smaller leading line ---------- */

#sb-main:not(:has(.sky-dashboard))
.cm-content > .sb-line-h6::before,
#sb-main:not(:has(.sky-dashboard))
.cm-content > h6::before {
  content: "" !important;
  display: inline-block !important;
  width: .42em !important;
  height: 2px !important;
  margin-right: .36em !important;
  border: 0 !important;
  border-radius: 999px !important;
  background: var(--sj-heading-primary) !important;
  vertical-align: .19em !important;
  transform: none !important;
}

#sb-main:not(:has(.sky-dashboard))
.cm-content > .sb-line-h6:hover::before,
#sb-main:not(:has(.sky-dashboard))
.cm-content > h6:hover::before {
  width: .48em !important;
  background: var(--sj-gold) !important;
  transform: none !important;
}

@media (max-width: 760px) {
  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  ) > div {
    border-radius: 14px !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  )
  summary.sb-toc-summary {
    min-height: 54px !important;
    padding: 14px 96px 14px 15px !important;
    font-size: .95rem !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  ) > div > .button-bar {
    top: 9px !important;
    right: 9px !important;
    gap: 6px !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  ) > div > .button-bar > button {
    flex-basis: 34px !important;
    width: 34px !important;
    min-width: 34px !important;
    max-width: 34px !important;
    height: 34px !important;
    min-height: 34px !important;
    max-height: 34px !important;
    border-radius: 10px !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .cm-content >
  .cm-line.sb-frontmatter:not(
    .sb-line-frontmatter-outside
  ) {
    padding-right: .78rem !important;
    padding-left: .78rem !important;
  }
}


/* =========================================================
   v1.8.6 TITLE / TOC SPACING / FRONTMATTER BADGE FIX
   ========================================================= */

/* ---------- Top page title: exact vertical centering ---------- */

/*
The title field is a 38px shell containing either a native input or a
small CodeMirror editor. Keep both render paths on the same vertical
center line and remove the old 4px block padding that pushed text down.
*/
#sb-top #sb-current-page,
#sb-current-page {
  display: flex !important;
  align-items: center !important;
  justify-content: stretch !important;
}

/* Native page-name input path. */
#sb-top #sb-current-page input.sb-page-name-editor,
#sb-top input.sb-input.sb-page-name-editor,
#sb-current-page input.sb-page-name-editor,
input.sb-input.sb-page-name-editor {
  position: relative !important;
  top: 0 !important;
  align-self: center !important;
  box-sizing: border-box !important;
  width: 100% !important;
  height: 36px !important;
  min-height: 36px !important;
  max-height: 36px !important;
  margin: 0 !important;
  padding: 0 14px 1px 18px !important;
  font-size: clamp(1.08rem, 1.35vw, 1.20rem) !important;
  font-weight: 750 !important;
  line-height: normal !important;
  vertical-align: middle !important;
}

/* CodeMirror page-name editor path. */
#sb-top #sb-current-page .cm-editor,
#sb-top #sb-current-page .cm-scroller,
#sb-current-page .cm-editor,
#sb-current-page .cm-scroller {
  box-sizing: border-box !important;
  width: 100% !important;
  height: 36px !important;
  min-height: 36px !important;
  max-height: 36px !important;
}

#sb-top #sb-current-page .cm-content,
#sb-current-page .cm-content {
  display: flex !important;
  box-sizing: border-box !important;
  min-height: 36px !important;
  height: 36px !important;
  align-items: center !important;
  margin: 0 !important;
  padding: 0 14px 0 18px !important;
  font-size: clamp(1.08rem, 1.35vw, 1.20rem) !important;
  font-weight: 750 !important;
  line-height: 1 !important;
}

#sb-top #sb-current-page .cm-line,
#sb-current-page .cm-line,
#sb-current-page .cm-line * {
  position: relative !important;
  top: 0 !important;
  margin: 0 !important;
  padding: 0 !important;
  font-size: inherit !important;
  font-weight: inherit !important;
  line-height: 1.2 !important;
}

/*
Mixed platform system fonts can have a slightly low visual center. A tiny
optical lift is applied only to the glyph line, not to the title shell.
*/
#sb-top #sb-current-page .cm-line,
#sb-current-page .cm-line {
  transform: translateY(-.5px) !important;
}

@media (max-width: 760px) {
  #sb-top #sb-current-page input.sb-page-name-editor,
  #sb-top input.sb-input.sb-page-name-editor,
  #sb-current-page input.sb-page-name-editor,
  input.sb-input.sb-page-name-editor,
  #sb-top #sb-current-page .cm-content,
  #sb-current-page .cm-content {
    font-size: 1.05rem !important;
  }
}

/* ---------- TOC list: genuinely compact nested rhythm ---------- */

/*
SilverBullet's widget base CSS adds ul li::before bullets. The TOC also
draws its own link dot, so both appeared at once. Reset the native/widget
bullet completely, then keep only the themed link dot.
*/
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details ul {
  display: block !important;
  box-sizing: border-box !important;
  min-height: 0 !important;
  margin-top: 0 !important;
  margin-right: 0 !important;
  margin-bottom: 0 !important;
  padding-top: 0 !important;
  padding-right: 0 !important;
  padding-bottom: 0 !important;
  list-style: none !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details > ul {
  padding: .62rem .88rem .72rem 1.08rem !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details ul ul {
  margin-left: .42rem !important;
  padding-left: .58rem !important;
  border-left: 1px dashed var(--sj-toc-divider) !important;
}

#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li {
  display: block !important;
  box-sizing: border-box !important;
  min-height: 0 !important;
  height: auto !important;
  margin: 0 !important;
  padding: 0 !important;
  line-height: 1 !important;
  list-style: none !important;
}

/* Remove SilverBullet's built-in widget bullet and browser marker. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li::before,
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li::after,
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li::marker {
  content: none !important;
  display: none !important;
  width: 0 !important;
  margin: 0 !important;
}

/* Compact item height while preserving clear hierarchy. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a {
  display: inline-flex !important;
  width: fit-content !important;
  min-width: 0 !important;
  min-height: 20px !important;
  align-items: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: .06rem .42rem .06rem .92rem !important;
  border-radius: 7px !important;
  font-size: .84rem !important;
  line-height: 1.14 !important;
}

/* Keep only this single themed dot. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > a::before {
  left: .34rem !important;
  width: 3px !important;
  height: 3px !important;
}

/* Nested lists begin immediately below their parent item. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
)
details li > ul {
  margin-top: 0 !important;
  margin-bottom: 0 !important;
}

/* ---------- Frontmatter: remove the orange marker remnant ---------- */

#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-line-frontmatter-outside.sb-frontmatter
.sb-frontmatter-marker,
#sb-main:not(:has(.sky-dashboard))
.cm-line.sb-line-frontmatter-outside.sb-frontmatter
[class*="frontmatter-marker"] {
  display: none !important;
  width: 0 !important;
  height: 0 !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
  opacity: 0 !important;
}

#sb-main:not(:has(.sky-dashboard))
.cm-content > .cm-line.sb-frontmatter {
  background: var(--sj-fm-background) !important;
}

#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after {
  border: 0 !important;
  outline: 0 !important;
}

@media (max-width: 760px) {
  #sb-top #sb-current-page input.sb-page-name-editor,
  #sb-top input.sb-input.sb-page-name-editor,
  #sb-current-page input.sb-page-name-editor,
  input.sb-input.sb-page-name-editor,
  #sb-top #sb-current-page .cm-content,
  #sb-current-page .cm-content {
    font-size: 1.05rem !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  )
  details li > a {
    padding-top: .14rem !important;
    padding-bottom: .14rem !important;
  }
}


/* ---------- v1.8.7 persistent Frontmatter surface ---------- */

/*
The previous background-image:none removed the gradient from the opening
and closing rows. Every .cm-line.sb-frontmatter now keeps the same
surface even when it is not hovered or active.
*/
#sb-main:not(:has(.sky-dashboard))
.cm-content > .cm-line.sb-frontmatter,
#sb-main:not(:has(.sky-dashboard))
.cm-content > .cm-line.sb-frontmatter.cm-activeLine {
  background: var(--sj-fm-background) !important;
  background-image: var(--sj-fm-background) !important;
}

#sb-main:not(:has(.sky-dashboard))
.cm-content:has(
  > .cm-line.sb-frontmatter:hover
) > .cm-line.sb-frontmatter {
  background: var(--sj-fm-background-hover) !important;
  background-image: var(--sj-fm-background-hover) !important;
}


/* =========================================================
   v1.8.8 NATIVE SYSTEM TITLE BAR
   The page-name field uses the platform-native UI font stack.
   ========================================================= */

#sb-top #sb-current-page,
#sb-current-page,
#sb-top #sb-current-page input.sb-page-name-editor,
#sb-top input.sb-input.sb-page-name-editor,
#sb-current-page input.sb-page-name-editor,
input.sb-input.sb-page-name-editor,
#sb-top #sb-current-page .cm-editor,
#sb-top #sb-current-page .cm-scroller,
#sb-top #sb-current-page .cm-content,
#sb-top #sb-current-page .cm-line,
#sb-current-page .cm-editor,
#sb-current-page .cm-scroller,
#sb-current-page .cm-content,
#sb-current-page .cm-line,
#sb-current-page .cm-line * {
  font-family: var(--sj-ui-font) !important;
}


/* =========================================================
   v1.8.9 UNIFIED WIDGET BUTTON BARS
   Unifies reload / copy / edit / open controls for every
   SilverBullet Lua directive button-bar.
   ========================================================= */

/*
Shared geometry for every widget button bar. This removes SilverBullet's
default negative button margins and gives all controls the same spacing,
shape, border, background and icon alignment as the TOC toolbar.
*/
#sb-main .sb-lua-directive-block .button-bar {
  display: flex !important;
  align-items: center !important;
  justify-content: flex-end !important;
  gap: 8px !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  box-shadow: none !important;
}

#sb-main .sb-lua-directive-block .button-bar > button {
  display: inline-flex !important;
  flex: 0 0 38px !important;
  width: 38px !important;
  min-width: 38px !important;
  max-width: 38px !important;
  height: 38px !important;
  min-height: 38px !important;
  max-height: 38px !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 !important;
  overflow: hidden !important;
  border: 1px solid var(--sj-toc-button-border) !important;
  border-radius: 11px !important;
  background: var(--sj-toc-button-background) !important;
  color: var(--sj-blue-deep) !important;
  font-family: var(--sj-ui-font) !important;
  line-height: 1 !important;
  box-shadow: none !important;
  transform: none !important;
  appearance: none !important;
  -webkit-appearance: none !important;
  transition:
    border-color .18s ease,
    background .18s ease,
    color .18s ease,
    box-shadow .18s ease,
    transform .18s ease !important;
}

html[data-theme="dark"]
#sb-main .sb-lua-directive-block .button-bar > button {
  color: #d7ebff !important;
}

#sb-main .sb-lua-directive-block .button-bar > button:hover {
  border-color: var(--sj-gold) !important;
  background: var(--sj-toc-button-hover) !important;
  color: var(--sj-blue-strong) !important;
  box-shadow:
    0 7px 16px rgba(61, 116, 166, .12) !important;
  transform: translateY(-1px) !important;
}

#sb-main .sb-lua-directive-block .button-bar > button:active {
  transform: translateY(0) scale(.97) !important;
}

#sb-main .sb-lua-directive-block .button-bar > button:focus-visible {
  outline: 2px solid var(--sj-gold) !important;
  outline-offset: 2px !important;
}

#sb-main .sb-lua-directive-block .button-bar > button > svg {
  display: block !important;
  flex: 0 0 auto !important;
  width: 17px !important;
  height: 17px !important;
  margin: 0 !important;
  padding: 0 !important;
  stroke-width: 2 !important;
}

/*
Inline Lua widgets use their rendered wrapper as the positioning context.
The action toolbar is removed from normal document flow and restored to
the widget's top-right corner, matching SilverBullet's overlay behavior.
*/
#sb-main
.sb-lua-wrapper
.sb-inline-content.sb-lua-directive-block
> div,
#sb-main
.sb-inline-content.sb-lua-directive-block
> div {
  position: relative !important;
}

#sb-main
.sb-lua-wrapper
.sb-inline-content.sb-lua-directive-block
> div
> .button-bar,
#sb-main
.sb-inline-content.sb-lua-directive-block
> div
> .button-bar {
  position: absolute !important;
  top: 8px !important;
  right: 8px !important;
  bottom: auto !important;
  left: auto !important;
  z-index: 20 !important;
  width: max-content !important;
  max-width: calc(100% - 16px) !important;
  margin: 0 !important;
  pointer-events: auto !important;
}

/*
Top widgets keep their own placement. TOC remains absolutely positioned
in its header, while other top widgets receive the same visual geometry.
*/
#sb-main
.sb-lua-directive-block.sb-lua-top-widget
> div
> .button-bar:not(:has(+ .content .sb-toc-summary)) {
  gap: 8px !important;
}

/* Reassert TOC placement after the global button reset. */
#sb-main:not(:has(.sky-dashboard))
.sb-lua-directive-block.sb-lua-top-widget:has(
  .sb-toc-summary
) > div > .button-bar {
  position: absolute !important;
  top: 10px !important;
  right: 12px !important;
  bottom: auto !important;
  left: auto !important;
  width: auto !important;
  margin: 0 !important;
}

@media (max-width: 760px) {
  #sb-main .sb-lua-directive-block .button-bar {
    gap: 6px !important;
  }

  #sb-main .sb-lua-directive-block .button-bar > button {
    flex-basis: 34px !important;
    width: 34px !important;
    min-width: 34px !important;
    max-width: 34px !important;
    height: 34px !important;
    min-height: 34px !important;
    max-height: 34px !important;
    border-radius: 10px !important;
  }

  #sb-main .sb-lua-directive-block .button-bar > button > svg {
    width: 16px !important;
    height: 16px !important;
  }

  #sb-main:not(:has(.sky-dashboard))
  .sb-lua-directive-block.sb-lua-top-widget:has(
    .sb-toc-summary
  ) > div > .button-bar {
    top: 9px !important;
    right: 9px !important;
  }
}






/* =========================================================
   v1.8.18 MARKER MICRO ALIGNMENT
   Fine-tuned from the supplied screenshot:
   - list dot was slightly too low
   - task circle was slightly too high
   - both now converge on the text strikethrough center
   ========================================================= */

html {
  --sj-list-solid-dot-size: 7px;
  --sj-task-line-height: 24px;
  --sj-plain-list-text-gap: .22em;

  /*
  These offsets are intentionally separate because the dot pseudo-element
  and the checkbox are positioned inside different containing boxes.
  A single shared value cannot produce the same visual center.
  */
  --sj-list-dot-center-shift-y: .25px;
  --sj-task-checkbox-center-shift-y: 2.5px;
}

/* ---------- Editor list dot ---------- */

#sb-main .cm-line.sb-line-ul > .cm-list-bullet {
  position: relative !important;
  top: auto !important;
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
  -webkit-text-stroke: 0 !important;
  text-shadow: none !important;
  font-weight: inherit !important;
  line-height: inherit !important;
  vertical-align: baseline !important;
  transform: none !important;
}

#sb-main .cm-line.sb-line-ul > .cm-list-bullet::after {
  content: "" !important;
  position: absolute !important;
  top:
    calc(
      50% + var(--sj-list-dot-center-shift-y)
    ) !important;
  left: 50% !important;
  display: block !important;
  width: var(--sj-list-solid-dot-size) !important;
  height: var(--sj-list-solid-dot-size) !important;
  margin: 0 !important;
  border: 0 !important;
  border-radius: 50% !important;
  background: var(--editor-list-bullet-color) !important;
  box-shadow:
    0 0 0 1px
    color-mix(
      in srgb,
      var(--editor-list-bullet-color),
      transparent 76%
    ) !important;
  transform: translate(-50%, -50%) !important;
  pointer-events: none !important;
}

/* ---------- Editor task checkbox ---------- */

#sb-main
.cm-line.sb-line-ul.sb-line-task
> .sb-checkbox {
  position: relative !important;
  top: auto !important;
  display: inline-block !important;
  width: 3ch !important;
  height: var(--sj-task-line-height) !important;
  min-height: var(--sj-task-line-height) !important;
  max-height: var(--sj-task-line-height) !important;
  margin: 0 !important;
  padding: 0 !important;
  text-align: center !important;
  text-indent: 0 !important;
  line-height: var(--sj-task-line-height) !important;
  vertical-align: top !important;
  transform: none !important;
}

#sb-main
.cm-line.sb-line-ul.sb-line-task
> .sb-checkbox
input[type="checkbox"] {
  position: absolute !important;
  top:
    calc(
      50% + var(--sj-task-checkbox-center-shift-y)
    ) !important;
  left: 50% !important;
  display: block !important;
  margin: 0 !important;
  vertical-align: initial !important;
  transform: translate(-50%, -50%) !important;
  transform-origin: 50% 50% !important;
}

#sb-main
.cm-line.sb-line-ul.sb-line-task
> .sb-checkbox
input[type="checkbox"]:hover {
  transform:
    translate(-50%, -50%)
    scale(1.08) !important;
}

#sb-main
.cm-line.sb-line-ul.sb-line-task
> .sb-checkbox
input[type="checkbox"]:checked {
  animation: none !important;
}

#sb-main
.cm-line.sb-line-ul.sb-line-task
> .sb-list.sb-task {
  position: static !important;
  top: auto !important;
  margin: 0 !important;
  vertical-align: baseline !important;
  transform: none !important;
}

/* ---------- Plain-list text gap ---------- */

#sb-main
.cm-line.sb-line-ul:not(.sb-line-task)
> .sb-list:last-child {
  margin-left: var(--sj-plain-list-text-gap) !important;
}

/* ---------- Rendered Markdown lists ---------- */

#sb-main ul > li::marker {
  color: var(--editor-list-bullet-color) !important;
  font-size: 1.18em !important;
  font-weight: 900 !important;
}

#sb-main
:is(
  .sb-markdown-widget,
  .sb-lua-directive-block,
  .sb-lua-directive-inline,
  .sb-markdown-top-widget,
  .sb-markdown-bottom-widget
)
ul li::before {
  color: var(--editor-list-bullet-color) !important;
  font-size: 1.18em !important;
  font-weight: 900 !important;
  text-shadow:
    .3px 0 0 currentColor,
    -.3px 0 0 currentColor;
}

#sb-main
:is(
  .sb-markdown-widget,
  .sb-lua-directive-block,
  .sb-lua-directive-inline,
  .sb-markdown-top-widget,
  .sb-markdown-bottom-widget
)
ul li:not(:has(input[type="checkbox"])) {
  padding-left: .18em;
}

#sb-main li:has(input[type="checkbox"])
input[type="checkbox"] {
  position: relative !important;
  top: 1px !important;
  vertical-align: middle !important;
}

@media (max-width: 760px) {
  html {
    --sj-list-solid-dot-size: 6px;
    --sj-task-line-height: 24px;
    --sj-plain-list-text-gap: .18em;
    --sj-list-dot-center-shift-y: .25px;
    --sj-task-checkbox-center-shift-y: 2px;
  }
}

/* ---------- Frontmatter badge collapse ---------- */

/*
The badge belongs to the opening fence row. It is the only interactive
surface used by the collapse controller.

The controller toggles one class on <html>; it never mutates CodeMirror
lines or decorations.
*/
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after {
  cursor: pointer;
  pointer-events: auto;
  touch-action: manipulation;
  user-select: none;
  transition:
    filter 160ms ease,
    box-shadow 160ms ease,
    transform 160ms ease;
}

#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after:hover {
  filter: brightness(1.06);
  box-shadow:
    0 6px 14px rgba(61, 116, 166, .19);
  transform: translateY(1px);
}

/*
Collapsed mode hides only Frontmatter rows. The opening fence remains as
a transparent 28px anchor so its ::after badge stays visible and can
always restore the block.
*/
html.sj-frontmatter-collapsed
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-frontmatter:not(
  .sb-line-frontmatter-outside:has(
    + .cm-line.sb-frontmatter
  )
) {
  display: none !important;
}

html.sj-frontmatter-collapsed
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
) {
  display: block !important;
  visibility: visible !important;
  min-height: 28px !important;
  height: 28px !important;
  max-height: 28px !important;
  margin-top: .45rem !important;
  margin-bottom: .65rem !important;
  padding: 0 !important;
  overflow: visible !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  background-image: none !important;
  color: transparent !important;
  -webkit-text-fill-color: transparent !important;
  box-shadow: none !important;
}

html.sj-frontmatter-collapsed
#sb-main:not(:has(.sky-dashboard))
.cm-content:has(
  > .cm-line.sb-frontmatter:hover
) >
.cm-line.sb-frontmatter {
  background: transparent !important;
  background-image: none !important;
}

/* In collapsed mode the badge becomes a complete floating pill. */
html.sj-frontmatter-collapsed
#sb-main:not(:has(.sky-dashboard))
.cm-content >
.cm-line.sb-line-frontmatter-outside.sb-frontmatter:has(
  + .cm-line.sb-frontmatter
)::after {
  content: "frontmatter";
  top: 0;
  right: 12px;
  min-height: 26px;
  border-radius: 8px;
}
```

```space-lua
-- priority: 20

-- =========================================================
-- FRONTMATTER BADGE COLLAPSE CONTROLLER
--
-- The controller only toggles a class on document.documentElement.
-- It never edits CodeMirror-managed DOM nodes, line classes or content.
-- =========================================================

sjFrontmatterCollapse = sjFrontmatterCollapse or {}

function sjFrontmatterCollapse.install()
  if js == nil or js.window == nil then
    return
  end

  js.window.eval([[
(function () {
  const controllerKey = "__sjFrontmatterCollapseController";
  const collapsedClass = "sj-frontmatter-collapsed";
  const storagePrefix = "sj-frontmatter-collapsed:";

  if (
    window[controllerKey] &&
    typeof window[controllerKey].destroy === "function"
  ) {
    window[controllerKey].destroy();
  }

  const root = document.documentElement;
  let currentPageKey = "";
  let titleObserver = null;
  let titleObserverTimer = 0;

  function pageName() {
    const titleRoot = document.querySelector("#sb-current-page");

    if (!titleRoot) {
      return window.location.pathname;
    }

    const input = titleRoot.querySelector(
      "input.sb-page-name-editor"
    );

    const value = input
      ? input.value
      : titleRoot.textContent;

    return String(value || window.location.pathname).trim();
  }

  function pageKey() {
    return (
      window.location.origin +
      window.location.pathname +
      "|" +
      pageName()
    );
  }

  function storageKey(key) {
    return storagePrefix + key;
  }

  function readCollapsed(key) {
    try {
      return window.sessionStorage.getItem(
        storageKey(key)
      ) === "1";
    } catch (_) {
      return false;
    }
  }

  function writeCollapsed(key, collapsed) {
    try {
      if (collapsed) {
        window.sessionStorage.setItem(
          storageKey(key),
          "1"
        );
      } else {
        window.sessionStorage.removeItem(
          storageKey(key)
        );
      }
    } catch (_) {
      /* Storage may be unavailable in private mode. */
    }
  }

  function applyForCurrentPage() {
    const nextKey = pageKey();

    if (nextKey === currentPageKey) {
      return;
    }

    currentPageKey = nextKey;
    root.classList.toggle(
      collapsedClass,
      readCollapsed(currentPageKey)
    );
  }

  function openingFenceFromEvent(event) {
    if (!(event.target instanceof Element)) {
      return null;
    }

    const line = event.target.closest(
      ".cm-line.sb-line-frontmatter-outside.sb-frontmatter"
    );

    if (!line) {
      return null;
    }

    const nextLine = line.nextElementSibling;

    if (
      !(nextLine instanceof HTMLElement) ||
      !nextLine.classList.contains("cm-line") ||
      !nextLine.classList.contains("sb-frontmatter")
    ) {
      return null;
    }

    /*
    The badge is positioned at top-right:
      right: 12px
      approximate clickable width: 132px
      clickable height: 34px

    Clicks elsewhere on the fence remain normal editor clicks.
    */
    const rect = line.getBoundingClientRect();
    const hitLeft = rect.right - 144;
    const hitRight = rect.right - 4;
    const hitTop = rect.top - 2;
    const hitBottom = rect.top + 36;

    if (
      event.clientX < hitLeft ||
      event.clientX > hitRight ||
      event.clientY < hitTop ||
      event.clientY > hitBottom
    ) {
      return null;
    }

    return line;
  }

  function handlePointerDown(event) {
    if (!openingFenceFromEvent(event)) {
      return;
    }

    event.preventDefault();
    event.stopPropagation();
  }

  function handleClick(event) {
    if (!openingFenceFromEvent(event)) {
      return;
    }

    event.preventDefault();
    event.stopPropagation();

    currentPageKey = pageKey();

    const collapsed = !root.classList.contains(
      collapsedClass
    );

    root.classList.toggle(collapsedClass, collapsed);
    writeCollapsed(currentPageKey, collapsed);
  }

  function schedulePageSync() {
    if (titleObserverTimer !== 0) {
      return;
    }

    titleObserverTimer = window.setTimeout(function () {
      titleObserverTimer = 0;
      applyForCurrentPage();
    }, 32);
  }

  function attachTitleObserver() {
    if (titleObserver) {
      titleObserver.disconnect();
      titleObserver = null;
    }

    const topBar = document.querySelector("#sb-top");

    if (!topBar) {
      return;
    }

    titleObserver = new MutationObserver(
      schedulePageSync
    );

    titleObserver.observe(topBar, {
      subtree: true,
      childList: true,
      characterData: true
    });
  }

  document.addEventListener(
    "pointerdown",
    handlePointerDown,
    true
  );
  document.addEventListener(
    "click",
    handleClick,
    true
  );

  window.addEventListener(
    "popstate",
    schedulePageSync
  );
  window.addEventListener(
    "hashchange",
    schedulePageSync
  );
  window.addEventListener(
    "pageshow",
    schedulePageSync
  );
  window.addEventListener(
    "focus",
    schedulePageSync
  );

  attachTitleObserver();
  applyForCurrentPage();

  window.setTimeout(function () {
    attachTitleObserver();
    applyForCurrentPage();
  }, 250);

  window[controllerKey] = {
    destroy: function () {
      document.removeEventListener(
        "pointerdown",
        handlePointerDown,
        true
      );
      document.removeEventListener(
        "click",
        handleClick,
        true
      );

      window.removeEventListener(
        "popstate",
        schedulePageSync
      );
      window.removeEventListener(
        "hashchange",
        schedulePageSync
      );
      window.removeEventListener(
        "pageshow",
        schedulePageSync
      );
      window.removeEventListener(
        "focus",
        schedulePageSync
      );

      if (titleObserver) {
        titleObserver.disconnect();
      }

      if (titleObserverTimer !== 0) {
        window.clearTimeout(titleObserverTimer);
      }
    }
  };
})();
  ]])
end

sjFrontmatterCollapse.install()
```

## 📱 10｜移动端标题栏基础稳定性

固定移动端标题栏三按钮的同轴位置、更多菜单容器尺寸、按钮间距与展开时的基础稳定性。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.23 MOBILE TOP-BAR STABILITY
   - Keep standalone actions fixed when the hamburger expands
   - Prevent the hamburger button from being clipped or scrolled
   - Remove touch-hover vertical movement on top-bar buttons
   ========================================================= */

@media (max-width: 640px) {
  /*
  SilverBullet renders standalone mobile actions and the hamburger menu
  as two sibling .sb-actions groups. The expanding hamburger becomes the
  tallest flex item; without an explicit cross-axis position, the first
  group stretches to that height and its centered buttons move downward.
  */
  #sb-top .wrapper > .sb-actions:not(.hamburger):not(.bottom-bar) {
    align-self: flex-start !important;
    height: 36px !important;
    min-height: 36px !important;
    max-height: 36px !important;
    align-items: center !important;
  }

  /* Let the fly-out escape the fixed-height title bar without scrolling it. */
  #sb-top,
  #sb-top > .main,
  #sb-top > .main > .inner,
  #sb-top > .main > .inner > .wrapper {
    overflow: visible !important;
  }

  #sb-top > .main {
    overflow-y: visible !important;
    scrollbar-gutter: auto !important;
  }

  /*
  The themed button is exactly 36px high, while SilverBullet's default
  collapsed max-height is 2.2rem (35.2px at 16px). Match the container
  to the button so neither border is clipped.
  */
  #sb-top .wrapper > .sb-actions.hamburger {
    align-self: flex-start !important;
    min-height: 36px !important;
    max-height: 36px !important;
    overflow: hidden !important;
    overflow: clip !important;
    overflow-y: clip !important;
    overscroll-behavior: none !important;
    scrollbar-gutter: auto !important;
    scrollbar-width: none !important;
    scroll-behavior: auto !important;
    touch-action: manipulation !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger.open,
  #sb-top .wrapper > .sb-actions.hamburger.open:hover {
    max-height: calc(100dvh - 24px) !important;
    overflow: hidden !important;
    overflow: clip !important;
    overflow-y: clip !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger::-webkit-scrollbar {
    display: none !important;
    width: 0 !important;
    height: 0 !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger > a {
    display: block !important;
    flex: 0 0 auto !important;
    line-height: 0 !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger > button,
  #sb-top .wrapper > .sb-actions.hamburger > a > button {
    flex: 0 0 36px !important;
    touch-action: manipulation !important;
  }

  /*
  Touch browsers can retain :hover after a tap. The global -1px hover
  lift then makes the first button look as if it slid under the clip edge.
  Keep top-bar controls stationary on narrow screens.
  */
  #sb-top .sb-actions button,
  #sb-top .sb-actions button:hover,
  #sb-top .sb-actions button:active,
  #sb-top button.action-button,
  #sb-top button.action-button:hover,
  #sb-top button.action-button:active {
    transform: none !important;
  }
}

/* =========================================================
   v1.8.24 MOBILE ACTION ROW ALIGNMENT
   Keep Home, Page and Hamburger buttons on one horizontal line.
   ========================================================= */

@media (max-width: 640px) {
  /*
  SilverBullet's native mobile hamburger receives margin-top: 2px.
  Reset that offset so it shares the same top edge as the two
  standalone action buttons.
  */
  #sb-top > .main > .inner > .wrapper {
    align-items: flex-start !important;
  }

  #sb-top .wrapper > .sb-actions:not(.bottom-bar),
  #sb-top .wrapper > .sb-actions.hamburger {
    margin-top: 0 !important;
    top: 0 !important;
  }

  /* Keep the three visible first-row buttons on the same 36px track. */
  #sb-top
  .wrapper
  > .sb-actions:not(.bottom-bar)
  > button,
  #sb-top
  .wrapper
  > .sb-actions:not(.bottom-bar)
  > a
  > button {
    align-self: flex-start !important;
    margin-top: 0 !important;
    margin-bottom: 0 !important;
  }
}

/* =========================================================
   v1.8.26 MOBILE HAMBURGER CENTERING + EQUAL BUTTON GAP
   - Center every hamburger action inside the expanded panel
   - Keep Button 2 → Button 3 spacing equal to Button 1 → Button 2
   ========================================================= */

@media (max-width: 640px) {
  /*
  The first two action buttons are 36px wide with a 5px internal gap.
  Make the hamburger panel 46px wide with 5px inner space on each side:
  36px button + 5px + 5px. With no external margin, the visible gap
  between Button 2 and the centered hamburger button is also exactly 5px.
  */
  #sb-top .wrapper > .sb-actions.hamburger {
    box-sizing: border-box !important;
    flex: 0 0 46px !important;
    width: 46px !important;
    min-width: 46px !important;
    max-width: 46px !important;
    margin-right: 0 !important;
    margin-left: 0 !important;
    padding-right: 5px !important;
    padding-left: 5px !important;
    align-items: center !important;
    text-align: center !important;
  }

  /*
  Some menu actions are direct buttons, while link actions are wrapped
  in an <a>. Give both paths the same centered 36px alignment track.
  */
  #sb-top .wrapper > .sb-actions.hamburger > a {
    display: flex !important;
    flex: 0 0 36px !important;
    width: 36px !important;
    min-width: 36px !important;
    max-width: 36px !important;
    align-items: center !important;
    justify-content: center !important;
    box-sizing: border-box !important;
    margin-right: auto !important;
    margin-left: auto !important;
    padding: 0 !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger > button,
  #sb-top .wrapper > .sb-actions.hamburger > a > button {
    flex: 0 0 36px !important;
    width: 36px !important;
    min-width: 36px !important;
    max-width: 36px !important;
    margin-right: auto !important;
    margin-left: auto !important;
    align-self: center !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger
  :is(button, a > button) > svg {
    display: block !important;
    margin: 0 !important;
  }
}
```

## ✈️ 11｜Dashboard 与板块页面完整样式

包含 Dashboard 布局、Captain、倒数日、热力图、标签、天气、任务、板块索引页、暗色模式、交互控件和移动端适配。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.27 DASHBOARD STYLE INTEGRATION
   All Sky Journal Dashboard, section-page, mobile navigation,
   calendar-control and presentation-widget CSS now lives here.
   The SJ Dashboard page contains Space Lua layout only.
   ========================================================= */

.sky-dashboard {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.sky-dashboard-block {
  margin-top: 0;
}
.sky-overview-grid {
  display: grid;
  grid-template-columns: minmax(0, 1.15fr) minmax(0, .85fr);
  gap: 16px;
}
.sky-para-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
}
.sky-section-heading {
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 16px;
  padding: 8px 4px 0;
  color: var(--sj-text, #2c4a6b);
  letter-spacing: .08em;
  font-weight: 700;
}
.sky-section-heading small {
  color: var(--sj-text-soft, #6c87a7);
  font-size: .72rem;
  font-weight: 500;
  letter-spacing: .04em;
}
.sky-list-card {
  min-width: 0;
  overflow: hidden;
}
.sky-list-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 14px;
  margin-bottom: 12px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(125, 182, 255, .22);
}
.sky-list-heading {
  min-width: 0;
}
.sky-list-title {
  color: var(--sj-text, #2c4a6b);
  font-size: .84rem;
  font-weight: 800;
  letter-spacing: .1em;
}
.sky-list-subtitle {
  margin-top: 3px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .72rem;
  line-height: 1.4;
}
.sky-create-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex: 0 0 auto;
  appearance: none;
  border: 1px solid rgba(212, 177, 106, .46);
  border-radius: 999px;
  background: linear-gradient(180deg, rgba(255,255,255,.98), rgba(240,247,255,.95));
  color: var(--sj-text, #2c4a6b);
  cursor: pointer;
  font: inherit;
  font-size: .72rem;
  font-weight: 700;
  padding: 7px 11px;
  text-decoration: none;
  white-space: nowrap;
  transition: transform .18s ease, box-shadow .18s ease, border-color .18s ease;
}
.sky-create-btn:hover {
  transform: translateY(-1px);
  border-color: rgba(212, 177, 106, .8);
  box-shadow: 0 8px 18px rgba(125, 182, 255, .16);
}
.sky-list-body {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.sky-list-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  min-width: 0;
  padding: 8px 10px;
  border-radius: 10px;
  color: var(--sj-text, #2c4a6b);
  text-decoration: none;
  transition: background .16s ease, transform .16s ease;
}
.sky-list-row:hover {
  background: rgba(125, 182, 255, .1);
  transform: translateX(2px);
}
.sky-list-row-main {
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-list-meta {
  flex: 0 0 auto;
  max-width: 38%;
  overflow: hidden;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .7rem;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-list-empty {
  padding: 18px 10px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .82rem;
  text-align: center;
}
.sky-folder-more {
  display: inline-block;
  margin-top: 12px;
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .72rem;
  font-weight: 700;
  text-decoration: none;
}
.sky-folder-more:hover {
  text-decoration: underline;
}
.sky-status-line {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  margin-top: 5px;
}
.sky-status-line span {
  color: var(--sj-blue-deep, #3f6fa8);
  font-weight: 800;
}
@media (max-width: 900px) {
  .sky-overview-grid,
  .sky-para-grid {
    grid-template-columns: 1fr;
  }
  .sky-section-heading {
    align-items: flex-start;
    flex-direction: column;
    gap: 3px;
  }
}
@media (max-width: 560px) {
  .sky-list-header {
    align-items: flex-start;
    flex-wrap: wrap;
  }
  .sky-list-header > .sky-create-btn {
    width: auto;
  }
}


/* ================= CAPTAIN PROFILE ================= */
.sky-captain-card {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 96px;
  align-items: center;
  gap: 18px;
  min-height: 138px;
  overflow: hidden;
  background:
    radial-gradient(circle at 88% 18%, rgba(212, 177, 106, .16), transparent 34%),
    linear-gradient(145deg, rgba(255,255,255,.94), rgba(236,246,255,.9));
}
.sky-captain-card::after {
  opacity: .8;
}
.sky-captain-copy {
  min-width: 0;
  padding-left: 2px;
}
.sky-captain-kicker {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .72rem;
  font-weight: 900;
  letter-spacing: .12em;
}
.sky-captain-name {
  margin-top: 8px;
  color: var(--sj-text, #2c4a6b);
  font-size: 1.45rem;
  font-weight: 900;
  letter-spacing: .04em;
  line-height: 1.1;
}
.sky-captain-role {
  margin-top: 6px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .74rem;
  line-height: 1.45;
}
.sky-captain-state {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  margin-top: 13px;
  padding: 5px 9px;
  border: 1px solid rgba(125, 182, 255, .26);
  border-radius: 999px;
  background: rgba(255,255,255,.7);
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .58rem;
  font-weight: 800;
  letter-spacing: .08em;
}
.sky-captain-state-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #6abf8a;
  box-shadow: 0 0 0 4px rgba(106, 191, 138, .12);
}
.sky-captain-avatar-frame {
  position: relative;
  display: grid;
  width: 88px;
  height: 88px;
  place-items: center;
  justify-self: end;
  padding: 4px;
  border-radius: 50%;
  background:
    conic-gradient(
      from 210deg,
      rgba(212,177,106,.95),
      rgba(125,182,255,.8),
      rgba(255,255,255,.95),
      rgba(212,177,106,.95)
    );
  box-shadow:
    0 12px 28px rgba(63,111,168,.18),
    0 0 0 5px rgba(255,255,255,.72);
}
.sky-captain-avatar-frame::before,
.sky-captain-avatar-frame::after {
  content: "";
  position: absolute;
  pointer-events: none;
  border-radius: 50%;
}
.sky-captain-avatar-frame::before {
  inset: -8px;
  border: 1px solid rgba(212,177,106,.34);
}
.sky-captain-avatar-frame::after {
  inset: -13px;
  border: 1px dashed rgba(125,182,255,.24);
}
.sky-captain-avatar,
.sky-captain-avatar-placeholder {
  display: grid;
  width: 100%;
  height: 100%;
  place-items: center;
  border: 3px solid rgba(255,255,255,.95);
  border-radius: 50%;
  box-sizing: border-box;
}
.sky-captain-avatar {
  background: #eef7ff;
  object-fit: cover;
  object-position: center;
}
.sky-captain-avatar-placeholder {
  background:
    radial-gradient(circle at 32% 24%, rgba(255,255,255,.92), transparent 26%),
    linear-gradient(145deg, #dceeff, #8dbbe8);
  color: #fff;
  font-size: 1.15rem;
  font-weight: 900;
  letter-spacing: .08em;
  text-shadow: 0 2px 8px rgba(44,74,107,.24);
}
@media (max-width: 560px) {
  .sky-captain-card {
    grid-template-columns: minmax(0, 1fr) 76px;
    min-height: 120px;
  }
  .sky-captain-avatar-frame {
    width: 70px;
    height: 70px;
  }
  .sky-captain-name {
    font-size: 1.24rem;
  }
}


/* ================= COUNTDOWN ROUTE ================= */
.sky-countdown-card {
  position: relative;
  display: flex;
  flex-direction: column;
  min-width: 0;
  min-height: 238px;
  overflow: hidden;
  background:
    radial-gradient(circle at 88% 16%, rgba(212,177,106,.18), transparent 35%),
    radial-gradient(circle at 8% 92%, rgba(125,182,255,.17), transparent 42%),
    linear-gradient(145deg, rgba(255,255,255,.95), rgba(236,246,255,.9));
}
.sky-countdown-card::before {
  opacity: .9;
}
.sky-countdown-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
}
.sky-countdown-header .sky-create-btn {
  width: auto;
}
.sky-countdown-title {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .72rem;
  font-weight: 900;
  letter-spacing: .11em;
}
.sky-countdown-subtitle {
  margin-top: 3px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .65rem;
}
.sky-countdown-body {
  display: flex;
  flex: 1 1 auto;
  flex-direction: column;
  justify-content: center;
  min-height: 0;
  padding: 14px 0 12px;
}
.sky-countdown-event {
  max-width: 100%;
  overflow: hidden;
  color: var(--sj-text, #2c4a6b);
  font-size: .82rem;
  font-weight: 850;
  line-height: 1.4;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-countdown-main {
  display: flex;
  align-items: baseline;
  gap: 9px;
  margin-top: 8px;
}
.sky-countdown-number {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: clamp(2rem, 3.6vw, 3rem);
  font-weight: 950;
  letter-spacing: -.04em;
  line-height: 1;
  text-shadow: 0 7px 18px rgba(63,111,168,.12);
}
.sky-countdown-label {
  color: var(--sj-gold, #d4b16a);
  font-size: .58rem;
  font-weight: 900;
  letter-spacing: .1em;
}
.sky-countdown-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  margin-top: auto;
  padding-top: 10px;
  border-top: 1px solid rgba(125,182,255,.16);
  color: var(--sj-text-soft, #6c87a7);
  font-size: .56rem;
  line-height: 1.3;
}
.sky-countdown-date {
  min-width: 0;
  overflow: hidden;
  font-weight: 750;
  letter-spacing: .05em;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-countdown-status {
  flex: 0 0 auto;
  color: var(--sj-gold, #d4b16a);
  font-size: .52rem;
  font-weight: 900;
  letter-spacing: .08em;
}
.sky-countdown-today {
  background:
    radial-gradient(circle at 82% 18%, rgba(212,177,106,.26), transparent 38%),
    linear-gradient(145deg, rgba(255,255,255,.97), rgba(255,247,226,.9));
}
.sky-countdown-today .sky-countdown-number {
  color: var(--sj-gold, #d4b16a);
  font-size: 2rem;
  letter-spacing: .04em;
}
.sky-countdown-past {
  filter: saturate(.82);
}
.sky-countdown-unset .sky-countdown-number {
  opacity: .46;
}
.sky-action-link {
  min-height: auto;
}

/* ================= MONTHLY ACTIVITY CALENDAR ================= */
.sky-calendar-card {
  --sky-calendar-gap: clamp(3px, .55vw, 7px);
  container-type: inline-size;
  display: flex;
  flex-direction: column;
  min-width: 0;
  min-height: 238px;
  overflow: hidden;
  background:
    radial-gradient(circle at 90% 10%, rgba(212,177,106,.13), transparent 34%),
    linear-gradient(145deg, rgba(255,255,255,.95), rgba(236,246,255,.9));
}
.sky-calendar-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 11px;
}
.sky-calendar-title {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .72rem;
  font-weight: 900;
  letter-spacing: .1em;
}
.sky-calendar-subtitle {
  margin-top: 3px;
  color: var(--sj-text, #2c4a6b);
  font-size: .77rem;
  font-weight: 800;
  letter-spacing: .08em;
}
.sky-calendar-today-count {
  flex: 0 0 auto;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .58rem;
  font-weight: 800;
  letter-spacing: .06em;
}
.sky-calendar-today-count span {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: 1rem;
  font-weight: 950;
}
.sky-calendar-weekdays,
.sky-calendar-grid {
  display: grid;
  width: 100%;
  grid-template-columns: repeat(7, minmax(0, 1fr));
  gap: var(--sky-calendar-gap);
  box-sizing: border-box;
}
.sky-calendar-weekdays {
  margin-bottom: 5px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: clamp(.42rem, 2.2cqw, .58rem);
  font-weight: 800;
  letter-spacing: .02em;
  text-align: center;
}
.sky-calendar-grid {
  align-items: stretch;
}
.sky-calendar-day {
  position: relative;
  display: flex;
  width: 100%;
  min-width: 0;
  height: auto;
  align-items: flex-start;
  justify-content: flex-start;
  aspect-ratio: 1 / 1;
  padding: clamp(3px, 1.7cqw, 6px);
  border: 1px solid rgba(125,182,255,.17);
  border-radius: clamp(5px, 2cqw, 8px);
  box-sizing: border-box;
  color: var(--sj-text, #2c4a6b);
  background: rgba(125,182,255,.07);
  transition: transform .14s ease, box-shadow .14s ease, filter .14s ease;
}
.sky-calendar-day:not(.sky-calendar-empty):hover {
  z-index: 2;
  transform: translateY(-2px) scale(1.04);
  box-shadow: 0 7px 15px rgba(63,111,168,.18);
  filter: saturate(1.08);
}
.sky-calendar-date-number {
  font-size: clamp(.5rem, 3.2cqw, .72rem);
  font-weight: 850;
  line-height: 1;
}
.sky-calendar-activity-count {
  position: absolute;
  right: clamp(2px, 1cqw, 4px);
  bottom: clamp(2px, 1cqw, 4px);
  display: grid;
  min-width: clamp(11px, 4.2cqw, 17px);
  height: clamp(11px, 4.2cqw, 17px);
  place-items: center;
  padding: 0 2px;
  border-radius: 999px;
  background: rgba(255,255,255,.82);
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: clamp(.4rem, 2.1cqw, .55rem);
  font-weight: 950;
  line-height: 1;
  box-sizing: border-box;
}
.sky-calendar-level-0 {
  background: rgba(125,182,255,.06);
}
.sky-calendar-level-1 {
  background: #e6f3ff;
  border-color: rgba(125,182,255,.22);
}
.sky-calendar-level-2 {
  background: #c8e3fc;
  border-color: rgba(89,155,220,.25);
}
.sky-calendar-level-3 {
  background: #94c3ef;
  border-color: rgba(63,111,168,.28);
}
.sky-calendar-level-4 {
  background: linear-gradient(145deg, #69a6de, #d9bd7c);
  border-color: rgba(212,177,106,.44);
  color: #fff;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,.15);
}
.sky-calendar-level-4 .sky-calendar-activity-count {
  background: rgba(255,255,255,.9);
}
.sky-calendar-weekend .sky-calendar-date-number {
  color: var(--sj-gold, #d4b16a);
}
.sky-calendar-today {
  border: 2px solid rgba(212,177,106,.88);
  box-shadow: 0 0 0 3px rgba(212,177,106,.12);
}
.sky-calendar-future {
  opacity: .45;
}
.sky-calendar-empty {
  border-color: transparent;
  background: transparent;
  pointer-events: none;
}
.sky-calendar-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  margin-top: 10px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .55rem;
  line-height: 1.3;
}
.sky-calendar-footer span:last-child {
  text-align: right;
}
@media (max-width: 640px) {
  .sky-calendar-card {
    --sky-calendar-gap: clamp(3px, 1.15vw, 6px);
  }
  .sky-calendar-weekdays,
  .sky-calendar-grid {
    width: 100%;
  }
  .sky-calendar-day {
    border-radius: clamp(5px, 2.1vw, 8px);
    padding: clamp(3px, 1.4vw, 5px);
  }
  .sky-calendar-date-number {
    font-size: clamp(.54rem, 2.6vw, .74rem);
  }
  .sky-calendar-activity-count {
    right: 2px;
    bottom: 2px;
    min-width: clamp(11px, 4vw, 16px);
    height: clamp(11px, 4vw, 16px);
    font-size: clamp(.4rem, 2vw, .52rem);
  }
  .sky-calendar-footer {
    align-items: flex-start;
    flex-direction: column;
  }
  .sky-calendar-footer span:last-child {
    text-align: left;
  }
}

/* ================= TAG CONSTELLATION ================= */
.sky-tags-card {
  display: flex;
  flex-direction: column;
  min-height: 238px;
  overflow: hidden;
  background:
    radial-gradient(circle at 86% 16%, rgba(212,177,106,.17), transparent 34%),
    radial-gradient(circle at 12% 88%, rgba(125,182,255,.16), transparent 40%),
    linear-gradient(145deg, rgba(255,255,255,.95), rgba(236,246,255,.9));
}
.sky-tags-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
}
.sky-tags-title {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .72rem;
  font-weight: 900;
  letter-spacing: .1em;
}
.sky-tags-subtitle {
  margin-top: 3px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .65rem;
}
.sky-tag-cloud {
  display: flex;
  align-content: flex-start;
  align-items: flex-start;
  flex: 1 1 auto;
  flex-wrap: wrap;
  gap: 7px;
  margin-top: 16px;
}
.sky-tag-chip {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  max-width: 100%;
  padding: 6px 8px 6px 10px;
  border: 1px solid rgba(125,182,255,.22);
  border-radius: 999px;
  background: rgba(255,255,255,.73);
  color: var(--sj-text, #2c4a6b);
  font-size: .63rem;
  font-weight: 750;
  line-height: 1;
  text-decoration: none;
  box-shadow: 0 5px 12px rgba(63,111,168,.06);
  transition: transform .14s ease, border-color .14s ease, box-shadow .14s ease;
}
.sky-tag-chip:hover {
  transform: translateY(-2px);
  border-color: rgba(212,177,106,.62);
  box-shadow: 0 8px 18px rgba(63,111,168,.12);
}
.sky-tag-name {
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-tag-count {
  display: grid;
  min-width: 18px;
  height: 18px;
  place-items: center;
  padding: 0 4px;
  border-radius: 999px;
  background: linear-gradient(145deg, rgba(125,182,255,.18), rgba(212,177,106,.18));
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .54rem;
  font-weight: 950;
  box-sizing: border-box;
}
.sky-tags-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  margin-top: 13px;
  padding-top: 10px;
  border-top: 1px solid rgba(125,182,255,.16);
  color: var(--sj-text-soft, #6c87a7);
  font-size: .58rem;
}
.sky-tags-page-hero {
  background:
    radial-gradient(circle at 84% 14%, rgba(212,177,106,.2), transparent 34%),
    radial-gradient(circle at 9% 86%, rgba(125,182,255,.2), transparent 38%),
    linear-gradient(135deg, rgba(255,255,255,.97), rgba(235,246,255,.94));
}
.sky-tags-index-card {
  overflow: visible;
}
.sky-tag-index-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.sky-tag-chip-large {
  padding: 9px 11px 9px 13px;
  font-size: .72rem;
}
.sky-tag-chip-large .sky-tag-count {
  min-width: 22px;
  height: 22px;
  font-size: .6rem;
}
@media (max-width: 560px) {
  .sky-tags-card {
    min-height: auto;
  }
  .sky-tag-chip {
    max-width: 100%;
  }
}

/* ================= TASK INDEX PAGE ================= */
.sky-task-page-hero {
  background:
    radial-gradient(circle at 84% 16%, rgba(212,177,106,.2), transparent 34%),
    radial-gradient(circle at 10% 8%, rgba(125,182,255,.22), transparent 42%),
    linear-gradient(135deg, rgba(255,255,255,.97), rgba(235,246,255,.94));
}
.sky-task-page-list .sky-task-row {
  border: 1px solid rgba(125,182,255,.13);
  background: rgba(255,255,255,.44);
}
.sky-task-page-list .sky-task-row:hover {
  border-color: rgba(212,177,106,.36);
  background: rgba(212,177,106,.08);
}

/* ================= FULL FOLDER INDEX PAGES ================= */
.sky-section-page {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.sky-section-page-hero {
  position: relative;
  overflow: hidden;
  padding: 34px 38px;
  border: 1px solid rgba(125, 182, 255, .26);
  border-radius: 24px;
  background:
    radial-gradient(circle at 82% 18%, rgba(212, 177, 106, .18), transparent 34%),
    radial-gradient(circle at 12% 10%, rgba(125, 182, 255, .24), transparent 42%),
    linear-gradient(135deg, rgba(255,255,255,.97), rgba(235,246,255,.94));
  box-shadow: 0 18px 44px rgba(80, 140, 200, .12);
}
.sky-section-page-hero::before,
.sky-section-page-hero::after {
  content: "";
  position: absolute;
  width: 42px;
  height: 42px;
  pointer-events: none;
}
.sky-section-page-hero::before {
  top: 12px;
  left: 12px;
  border-top: 2px solid rgba(212, 177, 106, .62);
  border-left: 2px solid rgba(212, 177, 106, .62);
}
.sky-section-page-hero::after {
  right: 12px;
  bottom: 12px;
  border-right: 2px solid rgba(212, 177, 106, .62);
  border-bottom: 2px solid rgba(212, 177, 106, .62);
}
.sky-section-page-kicker {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .68rem;
  font-weight: 800;
  letter-spacing: .18em;
}
.sky-section-page-title {
  margin-top: 8px;
  color: var(--sj-text, #2c4a6b);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 900;
  letter-spacing: .08em;
  line-height: 1.05;
}
.sky-section-page-subtitle {
  max-width: 760px;
  margin-top: 10px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .88rem;
  line-height: 1.65;
}
.sky-section-page-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}
.sky-back-btn {
  display: inline-flex;
  align-items: center;
  min-height: 34px;
  padding: 0 13px;
  border: 1px solid rgba(125, 182, 255, .28);
  border-radius: 999px;
  background: rgba(255,255,255,.74);
  color: var(--sj-text, #2c4a6b);
  font-size: .72rem;
  font-weight: 700;
  text-decoration: none;
  transition: transform .18s ease, box-shadow .18s ease, border-color .18s ease;
}
.sky-back-btn:hover {
  transform: translateY(-1px);
  border-color: rgba(125, 182, 255, .58);
  box-shadow: 0 8px 18px rgba(125, 182, 255, .14);
}
.sky-section-page-stats {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}
.sky-mini-stat {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 14px;
  min-width: 0;
}
.sky-mini-stat span {
  color: var(--sj-text-soft, #6c87a7);
  font-size: .66rem;
  font-weight: 800;
  letter-spacing: .11em;
}
.sky-mini-stat strong {
  min-width: 0;
  overflow: hidden;
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: 1rem;
  font-weight: 900;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-section-index-card {
  padding: 20px;
}
.sky-folder-page-list {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 7px 12px;
}
.sky-folder-page-list .sky-list-row {
  border: 1px solid rgba(125, 182, 255, .13);
  background: rgba(255,255,255,.44);
}
.sky-folder-page-list .sky-list-row:hover {
  border-color: rgba(125, 182, 255, .30);
  background: rgba(125, 182, 255, .10);
}
.sky-section-page-note {
  padding: 0 8px 8px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .68rem;
  text-align: center;
}


/*
Section-page empty states.

Folder and task detail pages use a two-column grid on wider screens.
When there is only one empty-state element, CSS Grid normally places it
in the first column, which limits the text to half of the card and causes
unnatural line wrapping.

Tags uses a wrapping flex row, so its empty state must explicitly occupy
the full row as well.
*/
.sky-folder-page-list > .sky-list-empty {
  grid-column: 1 / -1;
  justify-self: stretch;
  width: 100%;
}

.sky-tag-index-grid > .sky-list-empty {
  flex: 1 0 100%;
  width: 100%;
}

.sky-folder-page-list > .sky-list-empty,
.sky-tag-index-grid > .sky-list-empty {
  display: flex;
  box-sizing: border-box;
  min-width: 0;
  min-height: 112px;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 28px clamp(18px, 5vw, 56px);
  color: var(--sj-text-soft, #6c87a7);
  font-size: .82rem;
  line-height: 1.72;
  text-align: center;
  text-wrap: balance;
  overflow-wrap: anywhere;
}
@media (max-width: 820px) {
  .sky-section-page-stats,
  .sky-folder-page-list {
    grid-template-columns: 1fr;
  }
}
@media (max-width: 560px) {
  .sky-section-page-hero {
    padding: 28px 24px;
  }
  .sky-section-page-toolbar {
    align-items: stretch;
    flex-direction: column;
  }
  .sky-back-btn,
  .sky-section-page-toolbar .sky-create-btn {
    justify-content: center;
    width: 100%;
    box-sizing: border-box;
  }
  .sky-folder-page-list > .sky-list-empty,
  .sky-tag-index-grid > .sky-list-empty {
    min-height: 84px;
    padding: 22px 16px;
    text-wrap: pretty;
  }
}


/* ================= MOBILE DASHBOARD OPTIMIZATION ================= */

/* Keep the hero compact and prevent SKY JOURNAL from breaking into two lines. */
.sky-dashboard .sky-hero {
  box-sizing: border-box;
  padding: clamp(34px, 6vw, 64px) clamp(18px, 5vw, 48px);
}
.sky-dashboard .sky-hero-title {
  max-width: 100%;
  font-size: clamp(2rem, 6vw, 3.6rem);
  letter-spacing: clamp(.08em, 1.25vw, .22em);
  line-height: 1;
  white-space: nowrap;
}
.sky-dashboard .sky-hero-subtitle {
  font-size: clamp(.7rem, 2vw, .92rem);
  line-height: 1.4;
}

/* Tablet: use two balanced HUD columns instead of uneven auto-fit cards. */
@media (min-width: 641px) and (max-width: 1080px) {
  .sky-dashboard-block {
    grid-template-columns: repeat(2, minmax(0, 1fr)) !important;
  }
}

/* Phone layout */
@media (max-width: 640px) {
  .sky-dashboard {
    gap: 12px;
    min-width: 0;
  }

  .sky-dashboard .sky-hero {
    padding: 27px 14px;
    border-radius: 18px;
  }
  .sky-dashboard .sky-hero-title {
    font-size: clamp(1.5rem, 8vw, 2.05rem);
    letter-spacing: .065em;
    line-height: 1;
    white-space: nowrap;
  }
  .sky-dashboard .sky-hero-subtitle {
    margin-top: 8px;
    font-size: .7rem;
    letter-spacing: .035em;
  }

  .sky-dashboard-block,
  .sky-overview-grid,
  .sky-para-grid {
    grid-template-columns: minmax(0, 1fr) !important;
    gap: 12px;
  }

  .sky-card,
  .sky-list-card,
  .sky-calendar-card,
  .sky-countdown-card,
  .sky-tags-card,
  .sky-captain-card {
    width: 100%;
    min-width: 0;
    box-sizing: border-box;
  }

  .sky-captain-card,
  .sky-calendar-card,
  .sky-countdown-card,
  .sky-tags-card {
    min-height: auto;
  }

  .sky-captain-card {
    grid-template-columns: minmax(0, 1fr) 70px;
    gap: 12px;
    padding: 16px;
  }
  .sky-captain-avatar-frame {
    width: 64px;
    height: 64px;
  }
  .sky-captain-kicker,
  .sky-calendar-title,
  .sky-countdown-title,
  .sky-tags-title {
    font-size: .66rem;
    letter-spacing: .075em;
  }
  .sky-captain-name {
    margin-top: 6px;
    font-size: 1.18rem;
  }
  .sky-captain-role {
    font-size: .68rem;
  }
  .sky-captain-state {
    margin-top: 10px;
    padding: 4px 7px;
    font-size: .51rem;
  }

  .sky-calendar-card {
    padding: 16px 12px;
  }
  .sky-calendar-header,
  .sky-countdown-header,
  .sky-tags-header {
    gap: 8px;
  }
  .sky-calendar-weekdays,
  .sky-calendar-grid {
    width: 100%;
  }
  .sky-calendar-date-number {
    font-size: .62rem;
  }
  .sky-calendar-footer {
    gap: 4px;
    margin-top: 9px;
    font-size: .52rem;
  }

  .sky-countdown-card {
    padding: 16px;
  }
  .sky-countdown-header .sky-create-btn,
  .sky-tags-header .sky-create-btn {
    width: auto !important;
    padding: 6px 9px;
    font-size: .64rem;
  }
  .sky-countdown-body {
    padding: 14px 0 11px;
  }
  .sky-countdown-event {
    font-size: .78rem;
  }
  .sky-countdown-main {
    align-items: flex-end;
    gap: 7px;
    margin-top: 8px;
  }
  .sky-countdown-number {
    font-size: clamp(2.2rem, 14vw, 3rem);
  }
  .sky-countdown-label {
    padding-bottom: 3px;
    font-size: .53rem;
  }
  .sky-countdown-footer {
    font-size: .52rem;
  }
  .sky-countdown-status {
    display: none;
  }

  .sky-tags-card {
    padding: 16px;
  }
  .sky-tag-cloud {
    gap: 6px;
    margin-top: 13px;
  }
  .sky-tag-chip {
    padding: 6px 8px;
    font-size: .6rem;
  }

  .sky-nav {
    padding: 16px;
  }
  .sky-nav > div:last-child {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 7px;
    margin-top: 12px;
  }
  .sky-nav a {
    display: flex;
    min-width: 0;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    margin: 0;
    padding: 9px 6px;
    overflow: hidden;
    font-size: .66rem;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .sky-section-heading {
    gap: 2px;
    padding: 4px 2px 0;
    letter-spacing: .055em;
  }
  .sky-section-heading span {
    font-size: .78rem;
  }
  .sky-section-heading small {
    font-size: .62rem;
    line-height: 1.35;
  }

  .sky-list-card {
    padding: 15px;
  }
  .sky-list-header {
    align-items: flex-start;
    flex-direction: row;
    flex-wrap: nowrap;
    gap: 8px;
    margin-bottom: 9px;
    padding-bottom: 9px;
  }
  .sky-list-heading {
    flex: 1 1 auto;
  }
  .sky-list-header > .sky-create-btn {
    flex: 0 0 auto;
    width: auto;
    padding: 6px 8px;
    font-size: .62rem;
  }
  .sky-list-title {
    font-size: .74rem;
    letter-spacing: .07em;
  }
  .sky-list-subtitle {
    font-size: .64rem;
  }
  .sky-list-row {
    gap: 8px;
    padding: 8px 7px;
  }
  .sky-list-row-main {
    font-size: .75rem;
  }
  .sky-list-meta {
    max-width: 32%;
    font-size: .61rem;
  }

  .sky-dashboard > .sb-widget,
  .sky-dashboard .sb-widget {
    min-width: 0;
    max-width: 100%;
  }

  .sky-dashboard + .sky-footer,
  .sky-dashboard .sky-footer {
    font-size: .66rem;
  }
}

/* Extra narrow phones */
@media (max-width: 380px) {
  .sky-dashboard .sky-hero {
    padding: 24px 10px;
  }
  .sky-dashboard .sky-hero-title {
    font-size: clamp(1.38rem, 7.7vw, 1.75rem);
    letter-spacing: .045em;
  }
  .sky-dashboard .sky-hero-subtitle {
    font-size: .64rem;
  }

  .sky-calendar-card {
    --sky-calendar-gap: 3px;
  }

  .sky-countdown-date {
    max-width: 100%;
  }

  .sky-nav a {
    font-size: .61rem;
  }
}


/* ================= FIVE-CARD PRIMARY HUD ================= */
.sky-dashboard-block {
  display: grid;
  grid-template-columns:
    minmax(190px, .84fr)
    minmax(300px, 1.30fr)
    minmax(220px, 1fr)
    minmax(250px, 1.08fr);
  align-items: stretch;
  gap: 14px;
}
.sky-hud-stack {
  display: grid;
  grid-template-rows: repeat(2, minmax(0, 1fr));
  gap: 12px;
  min-width: 0;
  height: 100%;
}
.sky-hud-stack > *,
.sky-hud-stack > .sb-widget {
  min-width: 0;
  min-height: 0;
  height: 100%;
}
.sky-dashboard-block .sky-calendar-card,
.sky-dashboard-block .sky-tags-card,
.sky-dashboard-block .sky-weather-card {
  min-height: 310px;
  height: 100%;
  box-sizing: border-box;
}

/* Compact Captain card inside the stacked left column */
.sky-hud-stack .sky-captain-card {
  grid-template-columns: minmax(0, 1fr) 58px;
  gap: 10px;
  min-height: 0;
  height: 100%;
  padding: 13px 14px;
}
.sky-hud-stack .sky-captain-avatar-frame {
  width: 54px;
  height: 54px;
}
.sky-hud-stack .sky-captain-kicker {
  font-size: .59rem;
  letter-spacing: .075em;
}
.sky-hud-stack .sky-captain-name {
  margin-top: 5px;
  font-size: 1.05rem;
}
.sky-hud-stack .sky-captain-role {
  margin-top: 3px;
  font-size: .59rem;
}
.sky-hud-stack .sky-captain-state {
  margin-top: 7px;
  padding: 3px 6px;
  font-size: .45rem;
}

/* Compact countdown card inside the stacked left column */
.sky-hud-stack .sky-countdown-card {
  min-height: 0;
  height: 100%;
  padding: 13px 14px;
}
.sky-hud-stack .sky-countdown-title {
  font-size: .58rem;
  letter-spacing: .07em;
}
.sky-hud-stack .sky-countdown-subtitle {
  font-size: .55rem;
}
.sky-hud-stack .sky-countdown-header .sky-create-btn {
  padding: 5px 7px;
  font-size: .58rem;
}
.sky-hud-stack .sky-countdown-body {
  align-items: center;
  flex-direction: row;
  justify-content: space-between;
  gap: 8px;
  padding: 8px 0 6px;
}
.sky-hud-stack .sky-countdown-event {
  display: -webkit-box;
  max-width: 48%;
  overflow: hidden;
  font-size: .68rem;
  line-height: 1.35;
  white-space: normal;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}
.sky-hud-stack .sky-countdown-main {
  flex: 0 0 auto;
  gap: 5px;
  margin-top: 0;
}
.sky-hud-stack .sky-countdown-number {
  font-size: 1.9rem;
}
.sky-hud-stack .sky-countdown-label {
  max-width: 54px;
  font-size: .43rem;
  line-height: 1.2;
}
.sky-hud-stack .sky-countdown-footer {
  margin-top: 0;
  padding-top: 6px;
  font-size: .46rem;
}
.sky-hud-stack .sky-countdown-status {
  display: none;
}

/* ================= WEATHER ROUTE ================= */
.sky-weather-card {
  display: flex;
  flex-direction: column;
  min-width: 0;
  overflow: hidden;
  padding: 17px;
  background:
    radial-gradient(circle at 88% 10%, rgba(255,214,125,.22), transparent 33%),
    radial-gradient(circle at 8% 88%, rgba(125,182,255,.19), transparent 38%),
    linear-gradient(145deg, rgba(255,255,255,.96), rgba(232,244,255,.92));
}
.sky-weather-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 10px;
}
.sky-weather-header .sky-create-btn {
  padding: 6px 9px;
  font-size: .64rem;
}
.sky-weather-title {
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .7rem;
  font-weight: 900;
  letter-spacing: .09em;
}
.sky-weather-location {
  max-width: 170px;
  margin-top: 3px;
  overflow: hidden;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .62rem;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.sky-weather-current {
  display: flex;
  align-items: center;
  gap: 13px;
  margin-top: 14px;
}
.sky-weather-current-icon {
  display: grid;
  width: 62px;
  height: 62px;
  place-items: center;
  flex: 0 0 auto;
  border: 1px solid rgba(255,255,255,.86);
  border-radius: 20px;
  background:
    radial-gradient(circle at 34% 28%, rgba(255,255,255,.96), transparent 34%),
    linear-gradient(145deg, rgba(255,214,125,.38), rgba(125,182,255,.25));
  font-size: 2.15rem;
  box-shadow:
    0 10px 22px rgba(63,111,168,.12),
    inset 0 0 0 1px rgba(125,182,255,.12);
}
.sky-weather-current-copy {
  min-width: 0;
}
.sky-weather-current-temp {
  color: var(--sj-text, #2c4a6b);
  font-size: 2.25rem;
  font-weight: 950;
  letter-spacing: -.05em;
  line-height: 1;
}
.sky-weather-current-temp span {
  margin-left: 3px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .8rem;
  font-weight: 750;
  letter-spacing: 0;
}
.sky-weather-current-desc {
  margin-top: 5px;
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .69rem;
  font-weight: 800;
}
.sky-weather-rain {
  display: flex;
  align-items: center;
  gap: 9px;
  margin-top: 13px;
  padding: 9px 10px;
  border: 1px solid rgba(125,182,255,.18);
  border-radius: 12px;
  background: rgba(255,255,255,.57);
}
.sky-weather-rain-icon {
  display: grid;
  width: 27px;
  height: 27px;
  place-items: center;
  flex: 0 0 auto;
  border-radius: 9px;
  background: rgba(125,182,255,.13);
  color: var(--sj-blue-deep, #3f6fa8);
  font-size: .94rem;
}
.sky-weather-rain div {
  min-width: 0;
}
.sky-weather-rain strong,
.sky-weather-rain span {
  display: block;
}
.sky-weather-rain strong {
  color: var(--sj-text, #2c4a6b);
  font-size: .65rem;
}
.sky-weather-rain div > span {
  margin-top: 2px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .54rem;
}
.sky-weather-rain-medium {
  border-color: rgba(125,182,255,.34);
  background: rgba(125,182,255,.09);
}
.sky-weather-rain-high {
  border-color: rgba(212,177,106,.42);
  background: linear-gradient(135deg, rgba(125,182,255,.11), rgba(212,177,106,.11));
}
.sky-weather-forecast-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 7px;
  margin-top: 12px;
}
.sky-weather-forecast-day {
  min-width: 0;
  padding: 8px 5px;
  border: 1px solid rgba(125,182,255,.13);
  border-radius: 12px;
  background: rgba(255,255,255,.47);
  text-align: center;
}
.sky-weather-forecast-label {
  color: var(--sj-text-soft, #6c87a7);
  font-size: .51rem;
  font-weight: 750;
}
.sky-weather-forecast-icon {
  margin: 4px 0 3px;
  font-size: 1.05rem;
}
.sky-weather-forecast-temp {
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 4px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .53rem;
}
.sky-weather-forecast-temp strong {
  color: var(--sj-text, #2c4a6b);
  font-size: .65rem;
}
.sky-weather-attribution {
  margin-top: auto;
  padding-top: 9px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .45rem;
  font-weight: 750;
  letter-spacing: .08em;
  text-align: right;
  opacity: .75;
}
.sky-weather-error-body {
  display: flex;
  align-items: center;
  flex: 1 1 auto;
  flex-direction: column;
  justify-content: center;
  padding: 18px 8px;
  text-align: center;
}
.sky-weather-error-icon {
  font-size: 2rem;
}
.sky-weather-error-title {
  margin-top: 8px;
  color: var(--sj-text, #2c4a6b);
  font-size: .78rem;
  font-weight: 850;
}
.sky-weather-error-message {
  margin-top: 5px;
  color: var(--sj-text-soft, #6c87a7);
  font-size: .62rem;
  line-height: 1.45;
}

/* Two-column HUD on medium screens */
@media (min-width: 641px) and (max-width: 1080px) {
  .sky-dashboard-block {
    grid-template-columns: repeat(2, minmax(0, 1fr)) !important;
  }
  .sky-dashboard-block .sky-calendar-card,
  .sky-dashboard-block .sky-tags-card,
  .sky-dashboard-block .sky-weather-card {
    min-height: 310px;
  }
}

/* On phones every visual card returns to a full-width vertical flow. */
@media (max-width: 640px) {
  .sky-dashboard-block {
    grid-template-columns: minmax(0, 1fr) !important;
  }
  .sky-hud-stack {
    grid-template-rows: auto;
    gap: 12px;
    height: auto;
  }
  .sky-hud-stack > *,
  .sky-hud-stack > .sb-widget {
    height: auto;
  }

  .sky-hud-stack .sky-captain-card {
    grid-template-columns: minmax(0, 1fr) 70px;
    min-height: auto;
    padding: 16px;
  }
  .sky-hud-stack .sky-captain-avatar-frame {
    width: 64px;
    height: 64px;
  }
  .sky-hud-stack .sky-captain-kicker {
    font-size: .66rem;
  }
  .sky-hud-stack .sky-captain-name {
    font-size: 1.18rem;
  }
  .sky-hud-stack .sky-captain-role {
    font-size: .68rem;
  }
  .sky-hud-stack .sky-captain-state {
    font-size: .51rem;
  }

  .sky-hud-stack .sky-countdown-card {
    min-height: auto;
    padding: 16px;
  }
  .sky-hud-stack .sky-countdown-title {
    font-size: .66rem;
  }
  .sky-hud-stack .sky-countdown-subtitle {
    font-size: .65rem;
  }
  .sky-hud-stack .sky-countdown-body {
    align-items: flex-start;
    flex-direction: column;
    padding: 14px 0 11px;
  }
  .sky-hud-stack .sky-countdown-event {
    display: block;
    max-width: 100%;
    font-size: .78rem;
    white-space: nowrap;
  }
  .sky-hud-stack .sky-countdown-main {
    margin-top: 8px;
  }
  .sky-hud-stack .sky-countdown-number {
    font-size: clamp(2.2rem, 14vw, 3rem);
  }
  .sky-hud-stack .sky-countdown-label {
    max-width: none;
    font-size: .53rem;
  }
  .sky-hud-stack .sky-countdown-footer {
    font-size: .52rem;
  }

  .sky-dashboard-block .sky-calendar-card,
  .sky-dashboard-block .sky-tags-card,
  .sky-dashboard-block .sky-weather-card {
    min-height: auto;
    height: auto;
  }

  .sky-weather-card {
    padding: 16px;
  }
  .sky-weather-location {
    max-width: 220px;
  }
  .sky-weather-current {
    margin-top: 15px;
  }
  .sky-weather-current-icon {
    width: 70px;
    height: 70px;
    font-size: 2.45rem;
  }
  .sky-weather-current-temp {
    font-size: 2.65rem;
  }
  .sky-weather-rain {
    margin-top: 14px;
  }
  .sky-weather-forecast-day {
    padding: 10px 6px;
  }
}


/* ================= v8.9 EQUAL FOUR-COLUMN HUD ================= */
.sky-hud-panel {
  min-width: 0;
  min-height: 0;
}
.sky-hud-panel > .sb-widget,
.sky-hud-panel > .sb-lua-directive-block,
.sky-hud-panel > * {
  min-width: 0;
}
.sky-hud-panel .sky-card {
  box-sizing: border-box;
}

/* Desktop: four genuinely equal columns.
   The calendar panel supplies the row height from its own column width. */
@media (min-width: 960px) {
  .sky-dashboard-block {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr)) !important;
    grid-template-rows: auto;
    align-items: stretch;
    gap: 14px;
    width: 100%;
    min-width: 0;
  }

  .sky-hud-calendar-panel {
    min-height: 0;
    height: auto;
    contain: none;
  }

  /* These three columns must not increase the row height.
     They stretch to the height established by the calendar column. */
  .sky-hud-stack-panel,
  .sky-hud-tags-panel,
  .sky-hud-weather-panel {
    contain: size layout;
    height: 100%;
    min-height: 0;
  }

  .sky-hud-panel > .sb-widget,
  .sky-hud-panel > .sb-lua-directive-block,
  .sky-hud-panel > .sb-inline-content,
  .sky-hud-panel > * {
    height: 100%;
    min-height: 0;
  }

  .sky-hud-panel .sky-calendar-card,
  .sky-hud-panel .sky-tags-card,
  .sky-hud-panel .sky-weather-card {
    width: 100%;
    height: 100% !important;
    min-height: 0 !important;
    max-height: 100%;
    overflow: hidden;
  }

  .sky-hud-stack {
    display: grid;
    grid-template-rows: repeat(2, minmax(0, 1fr));
    gap: 12px;
    width: 100%;
    height: 100%;
    min-height: 0;
  }

  .sky-hud-stack > *,
  .sky-hud-stack > .sb-widget,
  .sky-hud-stack > .sb-lua-directive-block,
  .sky-hud-stack > .sb-inline-content {
    min-width: 0;
    min-height: 0;
    height: 100%;
    overflow: hidden;
  }

  .sky-hud-stack .sky-captain-card,
  .sky-hud-stack .sky-countdown-card {
    width: 100%;
    height: 100% !important;
    min-height: 0 !important;
    max-height: 100%;
    overflow: hidden;
  }

  /* The calendar column alone defines the intrinsic row height.
     Do not force it to fill an artificial aspect-ratio box. */
  .sky-hud-calendar-panel > .sb-widget,
  .sky-hud-calendar-panel > .sb-lua-directive-block,
  .sky-hud-calendar-panel > .sb-inline-content,
  .sky-hud-calendar-panel > * {
    height: auto !important;
    min-height: 0;
  }

  .sky-hud-calendar-panel .sky-calendar-card {
    aspect-ratio: auto;
    height: auto !important;
    min-height: 0 !important;
    max-height: none;
    overflow: visible;
  }
}

/* Tablet: two equal columns with fixed matched panel heights.
   The stacked Captain/Countdown column still remains one grid cell. */
@media (min-width: 641px) and (max-width: 959px) {
  .sky-dashboard-block {
    grid-template-columns: repeat(2, minmax(0, 1fr)) !important;
    align-items: stretch;
  }

  .sky-hud-panel {
    height: 330px;
    min-height: 330px;
  }

  .sky-hud-panel > .sb-widget,
  .sky-hud-panel > .sb-lua-directive-block,
  .sky-hud-panel > .sb-inline-content,
  .sky-hud-panel > * {
    height: 100%;
    min-height: 0;
  }

  .sky-hud-stack {
    display: grid;
    grid-template-rows: repeat(2, minmax(0, 1fr));
    gap: 12px;
    height: 100%;
  }

  .sky-hud-stack .sky-captain-card,
  .sky-hud-stack .sky-countdown-card,
  .sky-hud-panel .sky-calendar-card,
  .sky-hud-panel .sky-tags-card,
  .sky-hud-panel .sky-weather-card {
    height: 100% !important;
    min-height: 0 !important;
    overflow: hidden;
  }
}

/* Phone: unwrap the column panels and return every card to normal document flow. */
@media (max-width: 640px) {
  .sky-hud-panel {
    height: auto;
    min-height: 0;
    overflow: visible;
  }

  .sky-hud-panel > .sb-widget,
  .sky-hud-panel > .sb-lua-directive-block,
  .sky-hud-panel > .sb-inline-content,
  .sky-hud-panel > * {
    height: auto;
  }

  .sky-hud-stack {
    height: auto;
  }
}


/* ================= v9.1 CAPTAIN ALIGNMENT + DENSE WEATHER ================= */

/* Align the outer avatar halo with the right-side gold corner guide.
   Card padding is 14px and the outer halo extends 13px, so a 12px inward
   margin places the halo tangent approximately 13px from the card edge. */
.sky-hud-stack .sky-captain-avatar-frame {
  margin-right: 12px;
}

/* Weather card becomes a compact, self-scaling four-area grid:
   header / current+rain / 3-day forecast / attribution. */
.sky-weather-card {
  container-type: inline-size;
  display: grid !important;
  grid-template-columns: minmax(0, .88fr) minmax(0, 1.12fr);
  grid-template-rows:
    auto
    minmax(84px, .9fr)
    minmax(104px, 1.1fr)
    auto;
  grid-template-areas:
    "header header"
    "current rain"
    "forecast forecast"
    "attribution attribution";
  align-items: stretch;
  gap: clamp(8px, 2.2cqw, 14px);
}

/* Remove old flex spacing so the grid itself controls density. */
.sky-weather-header {
  grid-area: header;
}
.sky-weather-current {
  grid-area: current;
  align-self: stretch;
  min-width: 0;
  margin-top: 0;
  padding: clamp(8px, 2.4cqw, 13px);
  border: 1px solid rgba(125,182,255,.15);
  border-radius: clamp(12px, 3.4cqw, 18px);
  background:
    radial-gradient(circle at 25% 18%, rgba(255,255,255,.86), transparent 36%),
    linear-gradient(145deg, rgba(255,214,125,.12), rgba(125,182,255,.10));
  box-sizing: border-box;
}
.sky-weather-rain {
  grid-area: rain;
  align-self: stretch;
  min-width: 0;
  margin-top: 0;
  padding: clamp(8px, 2.4cqw, 13px);
  border-radius: clamp(12px, 3.4cqw, 18px);
  box-sizing: border-box;
}
.sky-weather-forecast-grid {
  grid-area: forecast;
  min-height: 0;
  height: 100%;
  margin-top: 0;
}
.sky-weather-attribution {
  grid-area: attribution;
  margin-top: 0;
  padding-top: 0;
}

/* Scale the current-weather cluster with the actual card width. */
.sky-weather-current {
  gap: clamp(8px, 2.8cqw, 14px);
}
.sky-weather-current-icon {
  width: clamp(44px, 16cqw, 68px);
  height: clamp(44px, 16cqw, 68px);
  border-radius: clamp(14px, 4.5cqw, 21px);
  font-size: clamp(1.55rem, 8cqw, 2.35rem);
}
.sky-weather-current-temp {
  font-size: clamp(1.55rem, 9.5cqw, 2.55rem);
}
.sky-weather-current-temp span {
  font-size: clamp(.62rem, 3cqw, .84rem);
}
.sky-weather-current-desc {
  margin-top: clamp(3px, 1cqw, 6px);
  font-size: clamp(.58rem, 2.7cqw, .74rem);
}

/* Rain report shares the same horizontal band as the current weather. */
.sky-weather-rain {
  gap: clamp(7px, 2cqw, 11px);
}
.sky-weather-rain-icon {
  width: clamp(25px, 7.5cqw, 34px);
  height: clamp(25px, 7.5cqw, 34px);
  border-radius: clamp(8px, 2.3cqw, 11px);
  font-size: clamp(.82rem, 4cqw, 1.05rem);
}
.sky-weather-rain strong {
  font-size: clamp(.56rem, 2.5cqw, .7rem);
  line-height: 1.3;
}
.sky-weather-rain div > span {
  margin-top: clamp(2px, .8cqw, 5px);
  font-size: clamp(.48rem, 2.1cqw, .6rem);
  line-height: 1.35;
}

/* Let the three forecast cells expand to consume the remaining card height. */
.sky-weather-forecast-grid {
  gap: clamp(6px, 1.8cqw, 10px);
}
.sky-weather-forecast-day {
  display: flex;
  min-height: 0;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  padding: clamp(8px, 2.6cqw, 14px) clamp(4px, 1.6cqw, 8px);
  border-radius: clamp(11px, 3cqw, 16px);
}
.sky-weather-forecast-label {
  font-size: clamp(.48rem, 2cqw, .58rem);
}
.sky-weather-forecast-icon {
  margin: clamp(4px, 1.2cqw, 7px) 0;
  font-size: clamp(1.02rem, 5.6cqw, 1.55rem);
}
.sky-weather-forecast-temp {
  gap: clamp(3px, 1cqw, 6px);
  font-size: clamp(.49rem, 2cqw, .58rem);
}
.sky-weather-forecast-temp strong {
  font-size: clamp(.58rem, 2.6cqw, .74rem);
}
.sky-weather-attribution {
  font-size: clamp(.42rem, 1.7cqw, .5rem);
}

/* Narrow full-width cards still keep current conditions and rain side by side,
   but tighten the split and typography proportionally. */
@media (max-width: 640px) {
  .sky-hud-stack .sky-captain-avatar-frame {
    margin-right: 10px;
  }

  .sky-weather-card {
    grid-template-columns: minmax(0, .92fr) minmax(0, 1.08fr);
    grid-template-rows:
      auto
      minmax(88px, auto)
      minmax(108px, auto)
      auto;
  }

  .sky-weather-current,
  .sky-weather-rain {
    padding: clamp(8px, 3vw, 13px);
  }
}

/* Very narrow phones: preserve the same-row logic without overflow. */
@media (max-width: 380px) {
  .sky-weather-card {
    gap: 8px;
  }
  .sky-weather-current {
    gap: 6px;
  }
  .sky-weather-current-icon {
    width: 42px;
    height: 42px;
    font-size: 1.45rem;
  }
  .sky-weather-current-temp {
    font-size: 1.5rem;
  }
  .sky-weather-rain {
    gap: 6px;
  }
  .sky-weather-rain-icon {
    width: 24px;
    height: 24px;
  }
}


/* ================= v10.0 INTERACTIVE CALENDAR + TYPE SCALE ================= */

/* Slightly larger dashboard typography without changing the four-column geometry. */
.sky-dashboard {
  font-size: 1.045em;
}
.sky-list-row-main,
.sky-list-subtitle,
.sky-section-page-subtitle,
.sky-section-page-note {
  line-height: 1.48;
}

/* Month/year navigation */
.sky-calendar-controls {
  display: flex;
  align-items: center;
  flex-wrap: nowrap;
  gap: clamp(3px, 1cqw, 6px);
  margin-top: 5px;
}
.sky-calendar-nav-btn,
.sky-calendar-picker-btn,
.sky-calendar-today-btn {
  appearance: none;
  display: inline-flex;
  min-width: 0;
  height: clamp(22px, 6.5cqw, 29px);
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  padding: 0 clamp(6px, 1.8cqw, 10px);
  border: 1px solid rgba(125,182,255,.22);
  border-radius: 999px;
  background: rgba(255,255,255,.64);
  color: var(--sj-blue-deep, #3f6fa8);
  font: inherit;
  font-size: clamp(.48rem, 2cqw, .62rem);
  font-weight: 850;
  line-height: 1;
  cursor: pointer;
  transition:
    transform .14s ease,
    border-color .14s ease,
    box-shadow .14s ease,
    background .14s ease;
}
.sky-calendar-nav-btn {
  width: clamp(22px, 6.5cqw, 29px);
  padding: 0;
  font-size: clamp(.8rem, 3.3cqw, 1rem);
}
.sky-calendar-today-btn {
  width: clamp(24px, 7cqw, 31px);
  padding: 0;
  color: var(--sj-gold, #d4b16a);
}
.sky-calendar-year-btn {
  padding-inline: clamp(7px, 2cqw, 11px);
}
.sky-calendar-nav-btn:hover,
.sky-calendar-picker-btn:hover,
.sky-calendar-today-btn:hover {
  transform: translateY(-1px);
  border-color: rgba(212,177,106,.6);
  background: rgba(255,255,255,.88);
  box-shadow: 0 6px 14px rgba(63,111,168,.11);
}

/* Calendar days are links now. Reset anchor/button-like styling. */
a.sky-calendar-day {
  color: var(--sj-text, #2c4a6b);
  text-decoration: none;
}
a.sky-calendar-day:visited {
  color: var(--sj-text, #2c4a6b);
}
a.sky-calendar-day:focus-visible {
  outline: 2px solid var(--sj-gold, #d4b16a);
  outline-offset: 2px;
}

/* Rain icon sits above the copy instead of sharing its text row. */
.sky-weather-rain {
  align-items: flex-start !important;
  flex-direction: column;
  justify-content: center;
}
.sky-weather-rain-icon {
  margin-bottom: clamp(2px, .8cqw, 5px);
}
.sky-weather-rain > div {
  width: 100%;
}

/* Keep the new controls readable on narrow cards. */
@media (max-width: 1180px) and (min-width: 641px) {
  .sky-calendar-controls {
    gap: 3px;
  }
  .sky-calendar-picker-btn {
    padding-inline: 6px;
  }
}
@media (max-width: 640px) {
  .sky-dashboard {
    font-size: 1.025em;
  }
  .sky-calendar-controls {
    flex-wrap: wrap;
  }
  .sky-calendar-today-count {
    padding-top: 2px;
  }
  .sky-weather-rain {
    min-height: 0;
  }
}

/* ================= v10.0 DASHBOARD DARK PALETTE ================= */
.sky-dashboard {
  --sj-panel-gradient:
    linear-gradient(
      145deg,
      rgba(255,255,255,.96),
      rgba(234,245,255,.92)
    );
  --sj-panel-soft: rgba(255,255,255,.58);
  --sj-panel-strong: rgba(255,255,255,.82);
  --sj-dashboard-border: rgba(125,182,255,.22);
  --sj-dashboard-shadow: rgba(63,111,168,.12);
}

.sky-dashboard.sky-theme-dark,
html[data-theme="dark"] .sky-dashboard.sky-theme-system {
  --sj-bg: #07111d;
  --sj-card: rgba(13,27,43,.91);
  --sj-blue: #78bfff;
  --sj-blue-deep: #a8d4ff;
  --sj-gold: #e6bd72;
  --sj-text: #e6f1ff;
  --sj-text-soft: #91aac3;
  --sj-panel-gradient:
    radial-gradient(circle at 88% 12%, rgba(230,189,114,.09), transparent 35%),
    linear-gradient(145deg, rgba(18,36,56,.96), rgba(8,21,35,.95));
  --sj-panel-soft: rgba(16,35,54,.76);
  --sj-panel-strong: rgba(22,44,67,.9);
  --sj-dashboard-border: rgba(120,191,255,.20);
  --sj-dashboard-shadow: rgba(0,0,0,.34);
  color: var(--sj-text);
}

.sky-dashboard .sky-card,
.sky-dashboard .sky-hero,
.sky-dashboard .sky-section-page-hero {
  background: var(--sj-panel-gradient) !important;
  border-color: var(--sj-dashboard-border) !important;
  box-shadow: 0 14px 34px var(--sj-dashboard-shadow) !important;
}

.sky-dashboard .sky-nav a,
.sky-dashboard .sky-create-btn,
.sky-dashboard .sky-back-btn,
.sky-dashboard .sky-calendar-nav-btn,
.sky-dashboard .sky-calendar-picker-btn,
.sky-dashboard .sky-calendar-today-btn,
.sky-dashboard .sky-tag-chip,
.sky-dashboard .sky-weather-current,
.sky-dashboard .sky-weather-rain,
.sky-dashboard .sky-weather-forecast-day,
.sky-dashboard .sky-list-row,
.sky-dashboard .sky-mini-stat {
  background: var(--sj-panel-soft) !important;
  border-color: var(--sj-dashboard-border) !important;
  color: var(--sj-text) !important;
}

.sky-dashboard .sky-calendar-level-0 {
  background: color-mix(in srgb, var(--sj-panel-soft), transparent 18%) !important;
}
.sky-dashboard .sky-calendar-level-1 {
  background: color-mix(in srgb, var(--sj-blue), transparent 78%) !important;
}
.sky-dashboard .sky-calendar-level-2 {
  background: color-mix(in srgb, var(--sj-blue), transparent 62%) !important;
}
.sky-dashboard .sky-calendar-level-3 {
  background: color-mix(in srgb, var(--sj-blue), transparent 42%) !important;
}
.sky-dashboard .sky-calendar-level-4 {
  background:
    linear-gradient(
      145deg,
      color-mix(in srgb, var(--sj-blue), #14314d 25%),
      color-mix(in srgb, var(--sj-gold), #3b2b16 35%)
    ) !important;
}

.sky-dashboard.sky-theme-dark .sky-weather-current-icon,
html[data-theme="dark"] .sky-dashboard.sky-theme-system .sky-weather-current-icon,
.sky-dashboard.sky-theme-dark .sky-captain-avatar-placeholder,
html[data-theme="dark"] .sky-dashboard.sky-theme-system .sky-captain-avatar-placeholder {
  background:
    radial-gradient(circle at 32% 22%, rgba(255,255,255,.15), transparent 30%),
    linear-gradient(145deg, #1a3a58, #0c2034) !important;
}

.sky-dashboard.sky-theme-dark .sky-calendar-future,
html[data-theme="dark"] .sky-dashboard.sky-theme-system .sky-calendar-future {
  opacity: .52;
}


/* ================= v10.3 READABLE HUD TYPOGRAPHY ================= */

/* The compact left column has enough unused space; scale its content by card width. */
.sky-hud-stack .sky-captain-card,
.sky-hud-stack .sky-countdown-card {
  container-type: inline-size;
}

.sky-hud-stack .sky-captain-copy {
  align-self: center;
}

.sky-hud-stack .sky-captain-kicker {
  font-size: clamp(.72rem, 3.05cqw, .88rem);
  letter-spacing: .075em;
}

.sky-hud-stack .sky-captain-name {
  margin-top: clamp(6px, 1.7cqw, 9px);
  font-size: clamp(1.24rem, 5.1cqw, 1.52rem);
  line-height: 1.12;
}

.sky-hud-stack .sky-captain-role {
  margin-top: clamp(4px, 1.25cqw, 7px);
  font-size: clamp(.74rem, 3.15cqw, .9rem);
  line-height: 1.42;
}

.sky-hud-stack .sky-captain-state {
  gap: 7px;
  margin-top: clamp(9px, 2.4cqw, 13px);
  padding: 5px 9px;
  font-size: clamp(.57rem, 2.45cqw, .7rem);
  letter-spacing: .065em;
}

.sky-hud-stack .sky-captain-state-dot {
  width: 7px;
  height: 7px;
}

/* Make the countdown event readable instead of leaving an empty left half. */
.sky-hud-stack .sky-countdown-event {
  max-width: 58%;
  font-size: clamp(.84rem, 3.75cqw, 1.02rem);
  font-weight: 850;
  line-height: 1.42;
  -webkit-line-clamp: 3;
}

.sky-hud-stack .sky-countdown-label {
  font-size: clamp(.48rem, 2.15cqw, .62rem);
  line-height: 1.25;
}

/* Weather card: increase all text in the two highlighted data bands. */
.sky-weather-current {
  justify-content: center;
}

.sky-weather-current-temp {
  font-size: clamp(1.95rem, 10.8cqw, 3rem);
  line-height: .98;
}

.sky-weather-current-temp span {
  font-size: clamp(.72rem, 3.4cqw, .98rem);
}

.sky-weather-current-desc {
  margin-top: clamp(5px, 1.5cqw, 8px);
  font-size: clamp(.72rem, 3.25cqw, .9rem);
  line-height: 1.3;
}

.sky-weather-rain {
  justify-content: center;
}

.sky-weather-rain-icon {
  width: clamp(29px, 8.6cqw, 39px);
  height: clamp(29px, 8.6cqw, 39px);
  font-size: clamp(.96rem, 4.7cqw, 1.24rem);
}

.sky-weather-rain strong {
  font-size: clamp(.72rem, 3.25cqw, .9rem);
  line-height: 1.34;
}

.sky-weather-rain div > span {
  margin-top: clamp(4px, 1.2cqw, 7px);
  font-size: clamp(.6rem, 2.65cqw, .74rem);
  line-height: 1.42;
}

/* The three-day forecast should use its available height, not look like tiny captions. */
.sky-weather-forecast-day {
  gap: clamp(2px, .7cqw, 5px);
}

.sky-weather-forecast-label {
  font-size: clamp(.6rem, 2.6cqw, .72rem);
  font-weight: 800;
}

.sky-weather-forecast-icon {
  margin: clamp(7px, 1.8cqw, 11px) 0;
  font-size: clamp(1.34rem, 6.6cqw, 1.9rem);
}

.sky-weather-forecast-temp {
  gap: clamp(5px, 1.35cqw, 8px);
  font-size: clamp(.62rem, 2.65cqw, .76rem);
}

.sky-weather-forecast-temp strong {
  font-size: clamp(.74rem, 3.2cqw, .92rem);
}

/* Preserve comfortable proportions on phones without overflowing the stacked cards. */
@media (max-width: 640px) {
  .sky-hud-stack .sky-captain-kicker {
    font-size: .75rem;
  }

  .sky-hud-stack .sky-captain-name {
    font-size: 1.3rem;
  }

  .sky-hud-stack .sky-captain-role {
    font-size: .78rem;
  }

  .sky-hud-stack .sky-captain-state {
    font-size: .6rem;
  }

  .sky-hud-stack .sky-countdown-event {
    max-width: 100%;
    font-size: .9rem;
  }

  .sky-weather-current-temp {
    font-size: clamp(2.2rem, 11vw, 3rem);
  }

  .sky-weather-current-desc,
  .sky-weather-rain strong {
    font-size: .78rem;
  }

  .sky-weather-rain div > span {
    font-size: .65rem;
  }

  .sky-weather-forecast-label {
    font-size: .64rem;
  }

  .sky-weather-forecast-icon {
    font-size: 1.45rem;
  }

  .sky-weather-forecast-temp {
    font-size: .67rem;
  }

  .sky-weather-forecast-temp strong {
    font-size: .8rem;
  }
}


/* ================= v10.5 HARMONIZED PRIMARY HUD ================= */

/* Unify title hierarchy across the non-calendar cards. */
.sky-captain-kicker,
.sky-countdown-title,
.sky-tags-title,
.sky-weather-title {
  font-size: clamp(.72rem, 2.75cqw, .82rem) !important;
  letter-spacing: .075em !important;
  line-height: 1.25;
}

.sky-countdown-subtitle,
.sky-tags-subtitle,
.sky-weather-location {
  margin-top: 4px;
  font-size: clamp(.65rem, 2.35cqw, .74rem) !important;
  line-height: 1.35;
}

/* ===== CAPTAIN STATUS ===== */
.sky-hud-stack .sky-captain-card {
  grid-template-columns: minmax(0, 1fr) clamp(74px, 20cqw, 88px);
  align-items: center;
  gap: clamp(12px, 3cqw, 18px);
  padding: clamp(15px, 3.6cqw, 20px);
}

.sky-hud-stack .sky-captain-copy {
  align-self: center;
}

.sky-hud-stack .sky-captain-avatar-frame {
  width: clamp(68px, 18cqw, 82px);
  height: clamp(68px, 18cqw, 82px);
}

.sky-hud-stack .sky-captain-name {
  margin-top: clamp(7px, 1.9cqw, 10px);
  font-size: clamp(1.28rem, 5.2cqw, 1.52rem);
  line-height: 1.08;
}

.sky-hud-stack .sky-captain-role {
  margin-top: clamp(5px, 1.4cqw, 8px);
  font-size: clamp(.76rem, 3.05cqw, .88rem);
  line-height: 1.35;
}

.sky-hud-stack .sky-captain-state {
  margin-top: clamp(10px, 2.5cqw, 14px);
  padding: 6px 10px;
  font-size: clamp(.58rem, 2.35cqw, .68rem);
}

/* ===== COUNTDOWN ROUTE ===== */
.sky-hud-stack .sky-countdown-card {
  padding: clamp(15px, 3.6cqw, 20px);
}

.sky-hud-stack .sky-countdown-body {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  align-items: center;
  gap: clamp(12px, 3.2cqw, 18px);
  padding: clamp(10px, 2.5cqw, 15px) 0;
}

.sky-hud-stack .sky-countdown-event {
  display: -webkit-box;
  max-width: none;
  overflow: hidden;
  font-size: clamp(.9rem, 3.65cqw, 1.05rem);
  line-height: 1.42;
  white-space: normal;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}

.sky-hud-stack .sky-countdown-main {
  align-items: flex-end;
  gap: 7px;
}

.sky-hud-stack .sky-countdown-number {
  font-size: clamp(2.25rem, 9cqw, 2.75rem);
  line-height: .92;
}

.sky-hud-stack .sky-countdown-label {
  max-width: 62px;
  padding-bottom: 3px;
  font-size: clamp(.52rem, 2.05cqw, .62rem);
  line-height: 1.2;
}

.sky-hud-stack .sky-countdown-footer {
  padding-top: 8px;
  font-size: clamp(.52rem, 1.95cqw, .62rem);
}

/* ===== TAG CONSTELLATION ===== */
.sky-tags-card {
  padding: clamp(16px, 3.4cqw, 20px);
}

.sky-tag-cloud {
  display: grid !important;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  align-content: center;
  align-items: stretch;
  gap: clamp(8px, 2cqw, 11px);
  margin-top: clamp(12px, 2.7cqw, 17px);
  padding: clamp(6px, 1.8cqw, 12px) 0;
}

.sky-tag-chip {
  width: 100%;
  min-width: 0;
  justify-content: space-between;
  gap: 8px;
  padding: clamp(8px, 2cqw, 11px) clamp(10px, 2.4cqw, 13px);
  box-sizing: border-box;
  font-size: clamp(.68rem, 2.6cqw, .78rem);
}

.sky-tag-count {
  min-width: clamp(21px, 5.8cqw, 25px);
  height: clamp(21px, 5.8cqw, 25px);
  font-size: clamp(.58rem, 2.15cqw, .67rem);
}

.sky-tags-footer {
  margin-top: 10px;
  padding-top: 11px;
  font-size: clamp(.61rem, 2.2cqw, .7rem);
}

/* ===== WEATHER ROUTE ===== */
.sky-weather-card {
  grid-template-rows:
    auto
    minmax(96px, 1fr)
    minmax(118px, 1.12fr)
    auto;
  gap: clamp(9px, 2.1cqw, 13px);
  padding: clamp(16px, 3.4cqw, 20px);
}

.sky-weather-current,
.sky-weather-rain {
  min-height: 0;
  padding: clamp(11px, 2.7cqw, 15px);
}

.sky-weather-current {
  justify-content: flex-start;
}

.sky-weather-current-icon {
  width: clamp(54px, 15.2cqw, 68px);
  height: clamp(54px, 15.2cqw, 68px);
  font-size: clamp(1.85rem, 7.8cqw, 2.35rem);
}

.sky-weather-current-temp {
  font-size: clamp(2rem, 9.8cqw, 2.75rem);
}

.sky-weather-current-temp span {
  font-size: clamp(.75rem, 3.1cqw, .95rem);
}

.sky-weather-current-desc {
  font-size: clamp(.74rem, 3cqw, .88rem);
}

.sky-weather-rain {
  align-items: flex-start;
  justify-content: center;
}

.sky-weather-rain-icon {
  width: clamp(31px, 8.5cqw, 38px);
  height: clamp(31px, 8.5cqw, 38px);
  margin-bottom: 5px;
  font-size: clamp(1rem, 4.5cqw, 1.22rem);
}

.sky-weather-rain strong {
  font-size: clamp(.74rem, 3cqw, .88rem);
}

.sky-weather-rain div > span {
  font-size: clamp(.61rem, 2.45cqw, .72rem);
  line-height: 1.4;
}

.sky-weather-forecast-grid {
  gap: clamp(7px, 1.8cqw, 10px);
}

.sky-weather-forecast-day {
  justify-content: center;
  padding: clamp(10px, 2.5cqw, 14px) 6px;
}

.sky-weather-forecast-label {
  font-size: clamp(.62rem, 2.35cqw, .72rem);
}

.sky-weather-forecast-icon {
  margin: clamp(7px, 1.7cqw, 10px) 0;
  font-size: clamp(1.35rem, 5.9cqw, 1.75rem);
}

.sky-weather-forecast-temp {
  font-size: clamp(.64rem, 2.4cqw, .74rem);
}

.sky-weather-forecast-temp strong {
  font-size: clamp(.76rem, 2.9cqw, .88rem);
}

.sky-weather-attribution {
  padding-top: 5px;
  font-size: clamp(.46rem, 1.7cqw, .52rem);
}

/* Tablet keeps the same visual hierarchy with slightly tighter spacing. */
@media (min-width: 641px) and (max-width: 959px) {
  .sky-tag-cloud {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .sky-hud-stack .sky-countdown-body {
    gap: 12px;
  }
}

/* Mobile: preserve larger readable type without creating horizontal overflow. */
@media (max-width: 640px) {
  .sky-captain-kicker,
  .sky-countdown-title,
  .sky-tags-title,
  .sky-weather-title {
    font-size: .75rem !important;
  }

  .sky-countdown-subtitle,
  .sky-tags-subtitle,
  .sky-weather-location {
    font-size: .68rem !important;
  }

  .sky-hud-stack .sky-countdown-body {
    display: flex;
    align-items: flex-start;
    flex-direction: column;
  }

  .sky-hud-stack .sky-countdown-number {
    font-size: 2.65rem;
  }

  .sky-tag-cloud {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .sky-tag-chip {
    font-size: .68rem;
  }

  .sky-weather-card {
    grid-template-rows: auto auto auto auto;
  }
}

@media (max-width: 390px) {
  .sky-tag-cloud {
    grid-template-columns: minmax(0, 1fr);
  }
}


/* ================= v10.6 UNIFIED ACTION BUTTONS + CENTERED RAIN ICON ================= */

/* Countdown / Tags / Weather header actions use the same visual dimensions.
   The former "查看更多" button is used as the size baseline. */
.sky-countdown-header > .sky-create-btn,
.sky-tags-header > .sky-create-btn,
.sky-weather-header > .sky-create-btn {
  display: inline-flex !important;
  width: 80px !important;
  min-width: 80px !important;
  height: 34px !important;
  min-height: 34px !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  padding: 0 12px !important;
  font-size: .72rem !important;
  font-weight: 700 !important;
  line-height: 1 !important;
  text-align: center !important;
  white-space: nowrap !important;
}

/* Center the umbrella glyph both geometrically and optically
   inside its pale-blue icon tile. */
.sky-weather-rain-icon {
  display: grid !important;
  align-items: center !important;
  justify-items: center !important;
  place-items: center !important;
  box-sizing: border-box !important;
  padding: 0 !important;
  line-height: 1 !important;
  text-align: center !important;
  text-indent: 0 !important;
}

.sky-weather-rain-icon::first-line {
  line-height: 1 !important;
}

/* Slight optical correction for the umbrella glyph's font metrics. */
.sky-weather-rain-icon {
  padding-top: 1px !important;
}

/* Mobile keeps the same three-button relationship, only slightly smaller. */
@media (max-width: 640px) {
  .sky-countdown-header > .sky-create-btn,
  .sky-tags-header > .sky-create-btn,
  .sky-weather-header > .sky-create-btn {
    width: 74px !important;
    min-width: 74px !important;
    height: 32px !important;
    min-height: 32px !important;
    padding: 0 10px !important;
    font-size: .68rem !important;
  }
}


/* ================= v10.6.1 COMPACT TAG HEADER + FULL-WIDTH EMPTY STATE ================= */

/*
Keep the original compact single-row header. The Widget subtitle is short
enough to remain beside the action button without reserving an empty row.
*/
.sky-tags-header {
  display: flex !important;
  align-items: flex-start !important;
  justify-content: space-between !important;
  gap: 14px !important;
}

.sky-tags-header > :first-child {
  display: block !important;
  min-width: 0 !important;
}

.sky-tags-subtitle {
  max-width: none !important;
  margin-top: 3px !important;
  line-height: 1.4 !important;
  white-space: nowrap !important;
  text-wrap: nowrap !important;
  word-break: normal !important;
  overflow-wrap: normal !important;
}

.sky-tags-header > .sky-create-btn {
  flex: 0 0 auto !important;
  align-self: flex-start !important;
}

/*
The Dashboard empty state remains full-width inside the two-column tag
cloud, so its copy does not wrap inside half of the card.
*/
.sky-tag-cloud > .sky-list-empty {
  grid-column: 1 / -1 !important;
  width: 100%;
  min-width: 0;
  max-width: none;
  align-self: stretch;
  justify-self: stretch;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 24px clamp(14px, 5cqw, 34px);
  line-height: 1.65;
  text-align: center;
  text-wrap: balance;
  word-break: normal;
  overflow-wrap: normal;
}

.sky-tag-cloud:has(> .sky-list-empty) {
  grid-template-columns: minmax(0, 1fr) !important;
}

@media (max-width: 560px) {
  .sky-tags-header {
    gap: 10px !important;
  }

  .sky-tags-subtitle {
    white-space: normal !important;
    text-wrap: pretty !important;
  }

  .sky-tag-cloud > .sky-list-empty {
    padding: 20px 12px;
    text-wrap: pretty;
  }
}


/* ================= v10.6.2 DYNAMIC TAG DETAIL-PAGE CHIPS ================= */

/*
Dashboard Tag Constellation intentionally keeps its equal two-column grid.

The Tags detail page uses a wrapping flex row. Each tag chip should size
to its own content so the number of chips per row adapts to tag length
and available width.
*/
.sky-tag-index-grid {
  display: flex !important;
  flex-wrap: wrap !important;
  align-items: flex-start !important;
  align-content: flex-start !important;
  justify-content: flex-start !important;
  gap: 10px !important;
}

.sky-tag-index-grid
> button.sky-tag-chip.sky-tag-chip-large {
  flex: 0 1 auto !important;
  width: auto !important;
  min-width: 0 !important;
  max-width: 100% !important;
  justify-content: flex-start !important;
  gap: 8px !important;
  white-space: nowrap !important;
}

.sky-tag-index-grid
> button.sky-tag-chip.sky-tag-chip-large
> .sky-tag-name {
  min-width: 0;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.sky-tag-index-grid
> button.sky-tag-chip.sky-tag-chip-large
> .sky-tag-count {
  flex: 0 0 auto;
}

/* Empty-state copy still occupies the complete Tags card. */
.sky-tag-index-grid > .sky-list-empty {
  flex: 1 0 100% !important;
  width: 100% !important;
}

@media (max-width: 560px) {
  .sky-tag-index-grid {
    gap: 8px !important;
  }

  .sky-tag-index-grid
  > button.sky-tag-chip.sky-tag-chip-large {
    max-width: 100% !important;
    padding: 8px 10px 8px 12px !important;
  }
}


/* ================= v10.7 TAG NAVIGATION + FONT FIX ================= */


/* Tag chips are real buttons so their click always invokes SilverBullet
   navigation instead of relying on the browser to interpret tag: as a URL. */
button.sky-tag-chip {
  appearance: none !important;
  -webkit-appearance: none !important;
  margin: 0 !important;
  border: 1px solid rgba(125,182,255,.22);
  background: rgba(255,255,255,.73);
  color: var(--sj-text, #2c4a6b);
  cursor: pointer;
  font-family:
    var(
      --sj-font-family,
      "LXGW WenKai Screen",
      "LXGW WenKai",
      "霞鹜文楷屏幕阅读版",
      "霞鹜文楷",
      sans-serif
    ) !important;
  font-style: normal !important;
  text-align: left;
}

button.sky-tag-chip .sky-tag-name,
button.sky-tag-chip .sky-tag-count {
  font-family: inherit !important;
}

button.sky-tag-chip:focus-visible {
  outline: 2px solid var(--sj-gold, #d4b16a);
  outline-offset: 2px;
}

button.sky-tag-chip:active {
  transform: translateY(0) scale(.985);
}


/* ================= v10.7.1 DYNAMIC REMAINING-HEIGHT TAG FIT ================= */

/*
Dashboard Tag Constellation:

- chips size to their own text;
- each row contains as many chips as its width allows;
- the cloud owns all space between header and statistics footer;
- overflow is clipped exactly at the footer divider;
- the Widget controller hides the first incomplete row and every row
  after it, so no chip is shown only partially.
*/
.sky-tags-card {
  display: flex !important;
  flex-direction: column !important;
  container-type: inline-size;
}

.sky-tags-card .sky-tag-cloud {
  display: flex !important;
  flex: 1 1 auto !important;
  flex-wrap: wrap !important;
  min-height: 0 !important;
  max-height: none !important;
  align-content: flex-start !important;
  align-items: flex-start !important;
  justify-content: flex-start !important;
  gap: 6px !important;
  box-sizing: border-box !important;
  width: 100% !important;
  margin-top: 12px !important;
  padding: 4px 0 !important;
  overflow: hidden !important;
  overflow: clip !important;
}

.sky-tags-card .sky-tag-cloud
> button.sky-tag-chip {
  display: inline-flex !important;
  flex: 0 1 auto !important;
  width: auto !important;
  min-width: 0 !important;
  max-width: min(100%, 190px) !important;
  height: 28px !important;
  min-height: 28px !important;
  max-height: 28px !important;
  align-items: center !important;
  justify-content: flex-start !important;
  box-sizing: border-box !important;
  gap: 5px !important;
  margin: 0 !important;
  padding: 0 7px 0 9px !important;
  border-radius: 999px !important;
  font-size: clamp(.58rem, 2.1cqw, .66rem) !important;
  line-height: 1 !important;
  white-space: nowrap !important;
}

.sky-tags-card .sky-tag-cloud
> button.sky-tag-chip[hidden] {
  display: none !important;
}

.sky-tags-card .sky-tag-cloud
> button.sky-tag-chip
> .sky-tag-name {
  display: block;
  min-width: 0;
  max-width: 15ch;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.sky-tags-card .sky-tag-cloud
> button.sky-tag-chip
> .sky-tag-count {
  display: grid !important;
  flex: 0 0 auto !important;
  min-width: 17px !important;
  width: auto !important;
  height: 17px !important;
  padding: 0 4px !important;
  place-items: center !important;
  font-size: .5rem !important;
  line-height: 1 !important;
}

/* The statistics divider remains fixed below the flexible tag area. */
.sky-tags-card .sky-tags-footer {
  flex: 0 0 auto !important;
  margin-top: 8px !important;
}

/* Empty state is centered in the complete remaining area. */
.sky-tags-card .sky-tag-cloud:has(> .sky-list-empty) {
  overflow: visible !important;
}

.sky-tags-card .sky-tag-cloud
> .sky-list-empty {
  min-height: 100%;
  padding: 18px 14px;
}

@media (max-width: 390px) {
  .sky-tags-card .sky-tag-cloud {
    gap: 5px !important;
  }

  .sky-tags-card .sky-tag-cloud
  > button.sky-tag-chip {
    max-width: 100% !important;
    height: 27px !important;
    min-height: 27px !important;
    max-height: 27px !important;
    padding-right: 6px !important;
    padding-left: 8px !important;
    font-size: .59rem !important;
  }
}


/* ================= v10.8 LAZY WEATHER LOADING ================= */


/* The invisible one-pixel image fires onload after the Widget is mounted. */
.sky-weather-lazy-trigger {
  position: absolute !important;
  width: 1px !important;
  height: 1px !important;
  overflow: hidden !important;
  opacity: 0 !important;
  pointer-events: none !important;
  inset: auto 0 0 auto !important;
}

/* Skeleton preserves the exact weather-card geometry, preventing layout jump. */
.sky-weather-loading-card {
  contain: layout paint;
}

.sky-weather-skeleton {
  position: relative;
  overflow: hidden;
  border-radius: 999px;
  background:
    color-mix(
      in srgb,
      var(--sj-blue, #7db6ff),
      transparent 88%
    );
}

.sky-weather-skeleton::after {
  content: "";
  position: absolute;
  inset: 0;
  transform: translateX(-110%);
  background:
    linear-gradient(
      90deg,
      transparent,
      rgba(255,255,255,.58),
      transparent
    );
  animation: sj-weather-shimmer 1.35s ease-in-out infinite;
}

@keyframes sj-weather-shimmer {
  100% {
    transform: translateX(110%);
  }
}

.sky-weather-skeleton-current-icon {
  width: clamp(54px, 15.2cqw, 68px);
  height: clamp(54px, 15.2cqw, 68px);
  flex: 0 0 auto;
  border-radius: clamp(16px, 4.4cqw, 21px);
}

.sky-weather-skeleton-temp {
  width: clamp(54px, 18cqw, 82px);
  height: clamp(24px, 7cqw, 34px);
}

.sky-weather-skeleton-desc {
  width: clamp(42px, 13cqw, 64px);
  height: 11px;
  margin-top: 9px;
}

.sky-weather-skeleton-rain {
  justify-content: center;
}

.sky-weather-skeleton-rain-icon {
  width: 34px;
  height: 34px;
  border-radius: 10px;
}

.sky-weather-skeleton-rain-copy {
  width: 84%;
  height: 28px;
  margin-top: 8px;
  border-radius: 8px;
}

.sky-weather-skeleton-day {
  pointer-events: none;
}

.sky-weather-skeleton-icon {
  width: 31px;
  height: 31px;
  margin: 9px auto;
  border-radius: 10px;
}

.sky-weather-skeleton-line {
  width: 58%;
  height: 10px;
  margin: 0 auto;
}

/* Cached data remains readable while a background refresh is running. */
.sky-weather-stale::after {
  content: "";
  position: absolute;
  top: 10px;
  right: 10px;
  width: 6px;
  height: 6px;
  border: 2px solid
    color-mix(
      in srgb,
      var(--sj-blue, #7db6ff),
      transparent 56%
    );
  border-top-color: var(--sj-gold, #d4b16a);
  border-radius: 999px;
  animation: sj-weather-spin .8s linear infinite;
}

@keyframes sj-weather-spin {
  to {
    transform: rotate(360deg);
  }
}

html[data-theme="dark"] .sky-weather-skeleton,
.sky-theme-dark .sky-weather-skeleton {
  background:
    color-mix(
      in srgb,
      var(--sj-blue, #78bfff),
      transparent 84%
    );
}

html[data-theme="dark"] .sky-weather-skeleton::after,
.sky-theme-dark .sky-weather-skeleton::after {
  background:
    linear-gradient(
      90deg,
      transparent,
      rgba(255,255,255,.10),
      transparent
    );
}

@media (prefers-reduced-motion: reduce) {
  .sky-weather-skeleton::after,
  .sky-weather-stale::after {
    animation: none;
  }
}





/* ================= v10.9.5 LARGER CENTERED LIST ACTIONS ================= */

.sky-dashboard {
  --sj-list-action-width: 104px;
  --sj-list-action-height: 38px;
  --sj-list-action-font-size: .90rem;
}

/*
All Dashboard list actions share one box, one label structure, and one
optical center:
- Recent Flight Log: 新建笔记
- Active Missions: 全部任务
- Journal / Project / Area / Archive: 新建笔记
*/
.sky-dashboard .sky-list-header > .sky-create-btn {
  display: inline-flex !important;
  flex: 0 0 var(--sj-list-action-width) !important;
  width: var(--sj-list-action-width) !important;
  min-width: var(--sj-list-action-width) !important;
  max-width: var(--sj-list-action-width) !important;
  height: var(--sj-list-action-height) !important;
  min-height: var(--sj-list-action-height) !important;
  max-height: var(--sj-list-action-height) !important;
  align-items: center !important;
  justify-content: center !important;
  gap: 5px !important;
  box-sizing: border-box !important;
  margin: 0 !important;
  padding: 0 10px !important;
  font-family: var(--sj-ui-font, sans-serif) !important;
  font-size: var(--sj-list-action-font-size) !important;
  font-weight: 700 !important;
  line-height: 1 !important;
  text-align: center !important;
  white-space: nowrap !important;
  vertical-align: middle !important;
}

/* Plus sign uses the full button height instead of sitting on a baseline. */
.sky-dashboard .sky-new-note-btn::before {
  content: "+";
  display: inline-flex !important;
  flex: 0 0 .86em !important;
  width: .86em !important;
  height: 100% !important;
  align-items: center !important;
  justify-content: center !important;
  color: currentColor;
  font-family: var(--sj-ui-font, sans-serif) !important;
  font-size: 1.02em !important;
  font-weight: 600 !important;
  line-height: 1 !important;
  transform: none !important;
}

/* Both 新建笔记 and 全部任务 now use this exact label wrapper. */
.sky-dashboard .sky-create-btn-label {
  display: inline-flex !important;
  height: 100% !important;
  min-height: 0 !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  padding: 0 !important;
  font: inherit !important;
  line-height: 1 !important;
  transform: translateY(.5px);
}

.sky-dashboard .sky-task-card .sky-list-header > .sky-create-btn {
  align-self: center !important;
}

@media (max-width: 560px) {
  .sky-dashboard {
    --sj-list-action-width: 98px;
    --sj-list-action-height: 36px;
    --sj-list-action-font-size: .84rem;
  }

  .sky-dashboard .sky-list-header > .sky-create-btn {
    gap: 4px !important;
    padding: 0 8px !important;
  }
}


/* ================= v10.9.6 CALENDAR TODAY EMOJI ================= */

/*
The current-month action uses a calendar emoji instead of the text “今”.
Keep the same compact circular button geometry as the month arrows.
*/
.sky-dashboard .sky-calendar-today-btn {
  width: clamp(26px, 7.2cqw, 32px) !important;
  min-width: clamp(26px, 7.2cqw, 32px) !important;
  max-width: clamp(26px, 7.2cqw, 32px) !important;
  padding: 0 !important;
  overflow: hidden !important;
  font-family:
    "Apple Color Emoji",
    "Segoe UI Emoji",
    "Noto Color Emoji",
    sans-serif !important;
}

.sky-dashboard .sky-calendar-today-icon {
  display: inline-flex !important;
  width: 100% !important;
  height: 100% !important;
  align-items: center !important;
  justify-content: center !important;
  box-sizing: border-box !important;
  font-family:
    "Apple Color Emoji",
    "Segoe UI Emoji",
    "Noto Color Emoji",
    sans-serif !important;
  font-size: clamp(.78rem, 3.2cqw, 1rem) !important;
  font-weight: 400 !important;
  line-height: 1 !important;
  transform: translateY(.02em);
}

.sky-dashboard .sky-calendar-today-btn:hover
.sky-calendar-today-icon {
  transform: translateY(-.02em) scale(1.06);
}

@media (max-width: 640px) {
  .sky-dashboard .sky-calendar-today-btn {
    width: 30px !important;
    min-width: 30px !important;
    max-width: 30px !important;
  }

  .sky-dashboard .sky-calendar-today-icon {
    font-size: .92rem !important;
  }
}


/* ================= v10.9.7 CIRCULAR AVATAR COVER MASK ================= */

/*
The frame remains responsible for the blue/gold halo.
The new inner mask alone clips the image, so the outer decorative rings
are not cut off.
*/
.sky-dashboard .sky-captain-avatar-mask {
  position: relative !important;
  display: block !important;
  width: 100% !important;
  height: 100% !important;
  min-width: 0 !important;
  min-height: 0 !important;
  box-sizing: border-box !important;
  overflow: hidden !important;
  border: 3px solid rgba(255, 255, 255, .95) !important;
  border-radius: 50% !important;
  background: #eef7ff !important;
  clip-path: circle(50% at 50% 50%) !important;
  isolation: isolate;
}

/*
Force the browser image to fill the complete circular mask while keeping
its intrinsic aspect ratio. Any excess is cropped around the center.
The tiny 1.03 scale prevents a pale seam at the clipping edge.
*/
.sky-dashboard img.sky-captain-avatar {
  position: absolute !important;
  inset: 0 !important;
  display: block !important;
  width: 100% !important;
  min-width: 100% !important;
  max-width: none !important;
  height: 100% !important;
  min-height: 100% !important;
  max-height: none !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
  background: transparent !important;
  object-fit: cover !important;
  object-position: 50% 50% !important;
  transform: scale(1.03) !important;
  transform-origin: 50% 50% !important;
}

/* Text fallback uses exactly the same visible circular diameter. */
.sky-dashboard .sky-captain-avatar-mask
.sky-captain-avatar-placeholder {
  display: grid !important;
  width: 100% !important;
  height: 100% !important;
  box-sizing: border-box !important;
  place-items: center !important;
  margin: 0 !important;
  padding: 0 !important;
  border: 0 !important;
  border-radius: 0 !important;
}

/* Neutralize the old border applied directly to image/placeholder. */
.sky-dashboard .sky-captain-avatar,
.sky-dashboard .sky-captain-avatar-placeholder {
  border: 0 !important;
}


/* ================= v10.9.11 MOBILE MENU GEOMETRY + CALENDAR TYPE ================= */

/*
Month and year remain visually secondary to the navigation arrows, but
are no longer undersized. Apply the same balanced type scale on desktop
and mobile while preserving the original touch targets.
*/
.sky-calendar-picker-btn,
.sky-calendar-year-btn {
  padding-inline: 8px !important;
  font-size: .58rem !important;
  letter-spacing: .012em !important;
}

/* Mobile AIRSHIP CONTROL PANEL labels remain comfortably readable. */
@media (max-width: 640px) {
  .sky-dashboard .sky-nav a {
    font-size: .88rem !important;
    line-height: 1.16 !important;
  }

  .sky-calendar-picker-btn,
  .sky-calendar-year-btn {
    padding-inline: 7px !important;
    font-size: .58rem !important;
  }

  /* Halve SilverBullet's original mobile side gutter. */
  #sb-top .main .inner .wrapper {
    padding-left: 10px !important;
    padding-right: 10px !important;
  }

  /*
  Closed state: the hamburger group itself is visually transparent, so
  the visible expander is exactly the same kind of button as the two
  controls to its left.

  Open state: the group becomes one regular rounded rectangle. It is not
  a capsule and does not alter the button geometry inside it.
  */
  #sb-top .wrapper > .sb-actions.hamburger,
  #sb-top .sb-actions.hamburger {
    position: relative !important;
    display: flex !important;
    box-sizing: border-box !important;
    flex: 0 0 46px !important;
    width: 46px !important;
    min-width: 46px !important;
    max-width: 46px !important;
    min-height: 36px !important;
    max-height: 36px !important;
    align-items: center !important;
    justify-content: flex-start !important;
    flex-direction: column !important;
    gap: 6px !important;
    margin: 0 !important;
    padding: 0 5px !important;
    overflow: hidden !important;
    overflow: clip !important;
    border: 0 !important;
    border-radius: 16px !important;
    background: transparent !important;
    box-shadow: none !important;
    backdrop-filter: none !important;
    -webkit-backdrop-filter: none !important;
    isolation: isolate;
    transition:
      max-height .24s cubic-bezier(.2,.78,.22,1),
      padding .2s ease,
      background .2s ease,
      box-shadow .2s ease !important;
  }

  #sb-top .sb-actions.hamburger::before {
    content: none !important;
    display: none !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger.open,
  #sb-top .wrapper > .sb-actions.hamburger.open:hover,
  #sb-top .sb-actions.hamburger.open,
  #sb-top .sb-actions.hamburger.open:hover {
    max-height: min(calc(100dvh - 76px), 430px) !important;
    padding: 7px 5px 7px !important;
    border-radius: 16px !important;
    background:
      linear-gradient(
        180deg,
        color-mix(in srgb, var(--top-background-color), white 4%),
        color-mix(in srgb, var(--top-background-color), var(--sj-blue) 7%)
      ) !important;
    box-shadow:
      inset 0 0 0 1px var(--sj-control-border),
      0 12px 28px rgba(41, 86, 126, .18) !important;
    backdrop-filter: blur(16px) saturate(1.08) !important;
    -webkit-backdrop-filter: blur(16px) saturate(1.08) !important;
  }

  /* Link wrappers use the same 36px rectangular track as direct buttons. */
  #sb-top .sb-actions.hamburger > a {
    display: flex !important;
    flex: 0 0 36px !important;
    width: 36px !important;
    min-width: 36px !important;
    max-width: 36px !important;
    height: 36px !important;
    min-height: 36px !important;
    max-height: 36px !important;
    align-items: center !important;
    justify-content: center !important;
    box-sizing: border-box !important;
    margin: 0 !important;
    padding: 0 !important;
    border-radius: 12px !important;
    text-decoration: none !important;
  }

  /*
  Every hamburger action now copies the two buttons on its left:
  36 × 36px, 12px corner radius, same blue/gold border and same surface.
  */
  #sb-top .sb-actions.hamburger > button,
  #sb-top .sb-actions.hamburger > a > button,
  #sb-top .sb-actions.hamburger button.expander {
    display: inline-flex !important;
    flex: 0 0 36px !important;
    width: 36px !important;
    min-width: 36px !important;
    max-width: 36px !important;
    height: 36px !important;
    min-height: 36px !important;
    max-height: 36px !important;
    align-items: center !important;
    justify-content: center !important;
    align-self: center !important;
    box-sizing: border-box !important;
    margin: 0 !important;
    padding: 0 !important;
    overflow: hidden !important;
    border: 1px solid var(--sj-control-border) !important;
    border-radius: 12px !important;
    background: var(--sj-control-background) !important;
    color: var(--sj-control-text) !important;
    line-height: 1 !important;
    text-align: center !important;
    box-shadow: none !important;
    transform: none !important;
    touch-action: manipulation !important;
  }

  #sb-top .sb-actions.hamburger > button:hover,
  #sb-top .sb-actions.hamburger > a > button:hover,
  #sb-top .sb-actions.hamburger button.expander:hover {
    border-color: var(--sj-control-border-hover) !important;
    background: var(--sj-control-background-hover) !important;
    color: var(--sj-blue-strong) !important;
    box-shadow: var(--sj-control-shadow) !important;
    transform: none !important;
  }

  #sb-top .sb-actions.hamburger :is(button, a > button) > svg {
    display: block !important;
    width: 17px !important;
    height: 17px !important;
    margin: 0 !important;
    transform: none !important;
  }

  /* Only the additional actions are hidden while the panel is collapsed. */
  #sb-top .sb-actions.hamburger button:not(.expander) {
    opacity: 0 !important;
    visibility: hidden !important;
    pointer-events: none !important;
    transform: none !important;
  }

  #sb-top .sb-actions.hamburger.open button:not(.expander),
  #sb-top .sb-actions.hamburger.open:hover button:not(.expander) {
    opacity: 1 !important;
    visibility: visible !important;
    pointer-events: auto !important;
    transform: none !important;
  }
}

@media (max-width: 380px) {
  .sky-dashboard .sky-nav a {
    font-size: .82rem !important;
  }

  .sky-calendar-picker-btn,
  .sky-calendar-year-btn {
    padding-inline: 6px !important;
    font-size: .56rem !important;
  }
}


/* ================= v10.9.10 PRESENTATION WIDGET CONTROLS ================= */

/*
Dashboard and section-index pages are presentation surfaces. Hide SilverBullet's
Lua Widget refresh/copy/edit button bar only when the rendered widget contains
one of these page roots. Other Lua widgets elsewhere in the Space keep their controls.
*/
#sb-main .cm-editor
.sb-lua-directive-block:has(.sky-dashboard)
.button-bar,
#sb-main .cm-editor
.sb-lua-directive-block:has(.sky-section-page)
.button-bar {
  display: none !important;
}

/* ================= v10.9.12 UNIFIED PRIMARY HUD HEADINGS ================= */

/*
All five primary HUD cards now share one title scale and one horizontal
start line. The original cards used different horizontal paddings
(roughly 15px / 16px / 18px), while the mobile calendar alone used 12px.
That made NAVIGATION ACTIVITY visibly sit farther left than the others.
*/
.sky-dashboard {
  --sj-hud-title-size: clamp(.74rem, 2.75cqw, .82rem);
  --sj-hud-title-letter-spacing: .075em;
  --sj-hud-title-line-height: 1.25;
  --sj-hud-title-gutter: 18px;
}

/* One title hierarchy for Captain, Countdown, Calendar, Tags and Weather. */
.sky-dashboard :is(
  .sky-captain-kicker,
  .sky-countdown-title,
  .sky-calendar-title,
  .sky-tags-title,
  .sky-weather-title
) {
  margin: 0 !important;
  padding: 0 !important;
  font-size: var(--sj-hud-title-size) !important;
  font-weight: 900 !important;
  line-height: var(--sj-hud-title-line-height) !important;
  letter-spacing: var(--sj-hud-title-letter-spacing) !important;
}

/* Remove the Captain-only 2px inset. */
.sky-dashboard .sky-captain-copy {
  padding-left: 0 !important;
}

/*
Keep each card's existing vertical padding and internal layout, but place
its header/content origin on the same horizontal guide.
*/
.sky-dashboard .sky-hud-stack .sky-captain-card,
.sky-dashboard .sky-hud-stack .sky-countdown-card,
.sky-dashboard .sky-calendar-card,
.sky-dashboard .sky-tags-card,
.sky-dashboard .sky-weather-card {
  padding-right: var(--sj-hud-title-gutter) !important;
  padding-left: var(--sj-hud-title-gutter) !important;
}

@media (max-width: 640px) {
  .sky-dashboard {
    --sj-hud-title-size: .76rem;
    --sj-hud-title-gutter: 16px;
  }

  /* Reassert after the older calendar-specific 16px 12px rule. */
  .sky-dashboard .sky-calendar-card {
    padding-right: var(--sj-hud-title-gutter) !important;
    padding-left: var(--sj-hud-title-gutter) !important;
  }
}
```

## 🎛️ 12｜移动端更多菜单与标题栏光学平衡

处理更多菜单的对称留白、锚定展开、可点击性、正常收起，以及标题栏左右视觉间距。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.30 SYMMETRIC MOBILE HAMBURGER PANEL PADDING
   The expanded panel now has equal 7px top and bottom inset,
   so the expander and final action sit symmetrically inside it.
   ========================================================= */


/* =========================================================
   v1.8.31 ANCHORED + CLICKABLE MOBILE HAMBURGER MENU
   - The expander button remains on its original title-bar baseline
   - The new top inset grows upward instead of pushing the button down
   - Overflowing menu actions receive a real interactive stacking layer
   ========================================================= */

@media (max-width: 640px) {
  /*
  Closed state starts at the original button position. In the open state
  the panel moves upward by exactly the same amount as its top padding.
  Therefore the expander's screen position is unchanged throughout:

    panel top  -7px  +  top padding 7px  =  button top 0px
  */
  #sb-top .wrapper > .sb-actions.hamburger,
  #sb-top .sb-actions.hamburger {
    top: 0 !important;
    z-index: 1001 !important;
    pointer-events: auto !important;
    transition:
      top .22s ease,
      padding .22s ease,
      max-height .24s cubic-bezier(.2,.78,.22,1),
      background .2s ease,
      box-shadow .2s ease !important;
  }

  #sb-top .wrapper > .sb-actions.hamburger.open,
  #sb-top .wrapper > .sb-actions.hamburger.open:hover,
  #sb-top .sb-actions.hamburger.open,
  #sb-top .sb-actions.hamburger.open:hover {
    top: -7px !important;
    height: auto !important;
    max-height: min(calc(100dvh - 69px), 430px) !important;
    padding: 7px 5px 7px !important;
    overflow: visible !important;
    pointer-events: auto !important;
    z-index: 1002 !important;
  }

  /*
  The title bar must remain the hit-testing layer above the editor while
  the menu extends below its normal 62px height. Without this, the menu
  can be visible but taps are intercepted by the editor canvas beneath it.
  */
  #sb-top {
    position: relative !important;
    z-index: 1000 !important;
    pointer-events: auto !important;
  }

  #sb-top > .main,
  #sb-top > .main > .inner,
  #sb-top > .main > .inner > .wrapper {
    position: relative !important;
    overflow: visible !important;
    pointer-events: auto !important;
  }

  /* Restore interaction on both direct-button and linked action paths. */
  #sb-top .sb-actions.hamburger.open > a,
  #sb-top .sb-actions.hamburger.open:hover > a,
  #sb-top .sb-actions.hamburger.open > button,
  #sb-top .sb-actions.hamburger.open:hover > button,
  #sb-top .sb-actions.hamburger.open > a > button,
  #sb-top .sb-actions.hamburger.open:hover > a > button {
    opacity: 1 !important;
    visibility: visible !important;
    pointer-events: auto !important;
  }

  #sb-top .sb-actions.hamburger.open > a {
    position: relative !important;
    z-index: 1 !important;
    cursor: pointer !important;
    touch-action: manipulation !important;
  }

  #sb-top .sb-actions.hamburger.open :is(button, a > button) {
    position: relative !important;
    z-index: 2 !important;
    cursor: pointer !important;
    touch-action: manipulation !important;
  }
}


/* =========================================================
   v1.8.39 MOBILE HAMBURGER DISMISS + CLICK HANDOFF FIX
   - Expanded appearance follows SilverBullet's real .open state
   - No sticky :hover or :focus-within fallback on touch screens
   - A pressed menu action temporarily keeps the panel open long
     enough for its click callback to run after the expander blurs
   ========================================================= */

@media (max-width: 640px) {
  /*
  Touch browsers may latch :hover, while the expander itself can retain
  focus after a second tap. Using either state as an open condition makes
  the panel impossible to dismiss. The closed state below therefore wins
  whenever SilverBullet has removed .open and no secondary action is
  currently being pressed.
  */
  #sb-top .wrapper > .sb-actions.hamburger:not(.open):not(
    :has(button:not(.expander):active)
  ),
  #sb-top .sb-actions.hamburger:not(.open):not(
    :has(button:not(.expander):active)
  ) {
    top: 0 !important;
    height: 36px !important;
    min-height: 36px !important;
    max-height: 36px !important;
    padding: 0 5px !important;
    overflow: hidden !important;
    overflow: clip !important;
    border-radius: 16px !important;
    background: transparent !important;
    box-shadow: none !important;
    backdrop-filter: none !important;
    -webkit-backdrop-filter: none !important;
    z-index: 1001 !important;
  }

  #sb-top .sb-actions.hamburger:not(.open):not(
    :has(button:not(.expander):active)
  ) button:not(.expander),
  #sb-top .sb-actions.hamburger:not(.open):not(
    :has(button:not(.expander):active)
  ) > a {
    opacity: 0 !important;
    visibility: hidden !important;
    pointer-events: none !important;
    transform: none !important;
  }

  /*
  SilverBullet removes .open in the currently focused menu button's blur
  handler. While a secondary action is physically pressed, :active keeps
  the visual/hit-test area expanded just until that action receives click.
  Once the press ends, the native blur state closes the panel normally.
  */
  #sb-top .wrapper > .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ),
  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) {
    top: -7px !important;
    height: auto !important;
    max-height: min(calc(100dvh - 69px), 430px) !important;
    padding: 7px 5px 7px !important;
    overflow: visible !important;
    pointer-events: auto !important;
    z-index: 1002 !important;
    border-radius: 16px !important;
    background:
      linear-gradient(
        180deg,
        color-mix(in srgb, var(--top-background-color), white 4%),
        color-mix(in srgb, var(--top-background-color), var(--sj-blue) 7%)
      ) !important;
    box-shadow:
      inset 0 0 0 1px var(--sj-control-border),
      0 12px 28px rgba(41, 86, 126, .18) !important;
    backdrop-filter: blur(16px) saturate(1.08) !important;
    -webkit-backdrop-filter: blur(16px) saturate(1.08) !important;
  }

  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) button:not(.expander),
  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) > a,
  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) > a > button {
    opacity: 1 !important;
    visibility: visible !important;
    pointer-events: auto !important;
    transform: none !important;
  }

  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) > a {
    position: relative !important;
    z-index: 3 !important;
    cursor: pointer !important;
    touch-action: manipulation !important;
  }

  #sb-top .sb-actions.hamburger:is(
    .open,
    :has(button:not(.expander):active)
  ) :is(button, a > button) {
    position: relative !important;
    z-index: 4 !important;
    cursor: pointer !important;
    touch-action: manipulation !important;
    -webkit-tap-highlight-color: transparent !important;
  }
}

/* =========================================================
   v1.8.33 MOBILE TOP-BAR OPTICAL BALANCE
   Shift the three right-side action buttons slightly right so the
   title-field left gutter visually matches the hamburger right gutter.
   ========================================================= */

@media (max-width: 640px) {
  /*
  Keep the title field's left edge unchanged. Only reduce the wrapper's
  right inset from 10px to 3px, moving the complete three-button action
  cluster 7px toward the screen edge. This matches the spacing measured
  from the supplied mobile screenshot without altering button gaps or
  expanded-menu geometry.
  */
  #sb-top .main .inner .wrapper {
    padding-left: 10px !important;
    padding-right: 3px !important;
  }
}
```

## 💾 13｜保存状态与 Page Decoration Prefix

移植 Zen 风格未保存指示器，并校正桌面端和移动端 pageDecoration.prefix 与标题框的视觉对齐。

```space-style
/* priority: 20 */

/* =========================================================
   v1.8.34 ZEN-STYLE SAVING INDICATOR
   SilverBullet applies .sb-unsaved while the current page has pending
   changes. CSS only visualizes that native state; it does not perform
   or verify the save operation itself.
   ========================================================= */

html {
  --sj-saving-ring-track:
    color-mix(in srgb, var(--sj-blue), transparent 62%);
  --sj-saving-ring-head: var(--sj-gold);
  --sj-saving-glow:
    color-mix(in srgb, var(--sj-gold), transparent 72%);
}

html[data-theme="dark"] {
  --sj-saving-ring-track:
    color-mix(in srgb, var(--sj-blue), transparent 54%);
  --sj-saving-ring-head: var(--sj-gold);
  --sj-saving-glow:
    color-mix(in srgb, var(--sj-gold), transparent 76%);
}

@keyframes sj-saving-title-breathe {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: .58;
  }
}

@keyframes sj-saving-shell-pulse {
  0%, 100% {
    border-color: var(--sj-border);
    box-shadow: none;
  }
  50% {
    border-color: var(--sj-gold);
    box-shadow:
      0 0 0 3px var(--sj-saving-glow),
      0 6px 18px rgba(41, 86, 126, .08);
  }
}

@keyframes sj-saving-ring-spin {
  to {
    transform: translateY(-50%) rotate(360deg);
  }
}

/*
Cover both known render paths:
1. .sb-unsaved is applied directly to #sb-current-page.
2. .sb-unsaved is applied to a descendant CodeMirror/title node.
*/
#sb-top #sb-current-page.sb-unsaved,
#sb-top #sb-current-page:has(.sb-unsaved) {
  position: relative !important;
  animation:
    sj-saving-shell-pulse 1.65s ease-in-out infinite !important;
}

/* Zen-style title flash, softened to remain readable. */
#sb-top #sb-current-page.sb-unsaved .cm-line,
#sb-top #sb-current-page:has(.sb-unsaved) .cm-line,
#sb-top #sb-current-page input.sb-page-name-editor.sb-unsaved {
  animation:
    sj-saving-title-breathe 1.65s ease-in-out infinite !important;
}

/* Reserve space so the saving ring never overlaps a long page name. */
#sb-top #sb-current-page.sb-unsaved input.sb-page-name-editor,
#sb-top #sb-current-page:has(.sb-unsaved) input.sb-page-name-editor,
#sb-top #sb-current-page.sb-unsaved .cm-content,
#sb-top #sb-current-page:has(.sb-unsaved) .cm-content {
  padding-right: 42px !important;
}

/* Blue/gold rotating indicator at the right edge of the title field. */
#sb-top #sb-current-page.sb-unsaved::after,
#sb-top #sb-current-page:has(.sb-unsaved)::after {
  content: "";
  position: absolute;
  top: 50%;
  right: 13px;
  z-index: 8;
  display: block;
  box-sizing: border-box;
  width: 16px;
  height: 16px;
  margin: 0;
  border: 2px solid var(--sj-saving-ring-track);
  border-top-color: var(--sj-saving-ring-head);
  border-right-color: var(--sj-blue-strong);
  border-radius: 50%;
  transform: translateY(-50%);
  transform-origin: 50% 50%;
  animation:
    sj-saving-ring-spin .82s linear infinite;
  pointer-events: none;
}

@media (max-width: 640px) {
  #sb-top #sb-current-page.sb-unsaved input.sb-page-name-editor,
  #sb-top #sb-current-page:has(.sb-unsaved) input.sb-page-name-editor,
  #sb-top #sb-current-page.sb-unsaved .cm-content,
  #sb-top #sb-current-page:has(.sb-unsaved) .cm-content {
    padding-right: 38px !important;
  }

  #sb-top #sb-current-page.sb-unsaved::after,
  #sb-top #sb-current-page:has(.sb-unsaved)::after {
    right: 11px;
    width: 15px;
    height: 15px;
  }
}

@media (prefers-reduced-motion: reduce) {
  #sb-top #sb-current-page.sb-unsaved,
  #sb-top #sb-current-page:has(.sb-unsaved),
  #sb-top #sb-current-page.sb-unsaved .cm-line,
  #sb-top #sb-current-page:has(.sb-unsaved) .cm-line,
  #sb-top #sb-current-page input.sb-page-name-editor.sb-unsaved,
  #sb-top #sb-current-page.sb-unsaved::after,
  #sb-top #sb-current-page:has(.sb-unsaved)::after {
    animation: none !important;
  }

  #sb-top #sb-current-page.sb-unsaved,
  #sb-top #sb-current-page:has(.sb-unsaved) {
    border-color: var(--sj-gold) !important;
    box-shadow:
      0 0 0 3px var(--sj-saving-glow) !important;
  }
}


/* =========================================================
   v1.8.35 PAGE PREFIX TITLE ALIGNMENT
   PageDecoration prefixes are rendered as a sibling before the title
   field. On desktop the themed title shell sits about 4px above the
   prefix and action-button track, so decorated pages receive a small
   optical correction without affecting undecorated pages or mobile.
   ========================================================= */

@media (min-width: 641px) {
  #sb-top .wrapper:has(
    > .sb-page-prefix:not(:empty)
  ) > #sb-current-page {
    position: relative !important;
    top: 4px !important;
  }

  /* Keep the emoji itself on the same 38px visual track. */
  #sb-top .wrapper > .sb-page-prefix:not(:empty) {
    display: inline-flex !important;
    flex: 0 0 auto !important;
    min-height: 38px !important;
    align-items: center !important;
    justify-content: center !important;
    align-self: flex-start !important;
    box-sizing: border-box !important;
    line-height: 1 !important;
  }
}


/* =========================================================
   v1.8.38 MOBILE PAGE PREFIX OPTICAL ALIGNMENT
   Emoji glyph metrics need only a very small optical lift on phones.
   Move the prefix up by 1px while leaving the title field and action
   buttons untouched.
   ========================================================= */

@media (max-width: 640px) {
  #sb-top .wrapper > .sb-page-prefix:not(:empty) {
    display: inline-flex !important;
    flex: 0 0 auto !important;
    min-height: 36px !important;
    align-items: center !important;
    justify-content: center !important;
    align-self: flex-start !important;
    box-sizing: border-box !important;
    margin: 0 !important;
    padding: 0 !important;
    line-height: 1 !important;
    transform: translateY(-1px) !important;
  }
}
```

---


## 🌐 14｜PWA 安全区域与浏览器系统栏动态取色

这一模块处理网页和已安装 PWA 之外的“系统外壳”区域：

- 网页模式下同步浏览器顶部状态栏与底部地址栏颜色；
- PWA 模式下让顶部、底部安全区域与当前主题保持一致；
- 亮暗模式切换后自动更新系统栏颜色；
- 给 iOS PWA 补充 `viewport-fit=cover` 与状态栏模式；
- 给浏览器声明正确的 `color-scheme`，避免系统控件使用错误明暗配色。

> [!note]
> 浏览器外壳颜色不是普通页面 CSS 的一部分，因此本模块由一个 `space-style` 块和一个很小的 `space-lua` 运行时共同组成。CSS 负责安全区域，Space Lua 负责更新页面 `<head>` 中的 meta 信息。

```space-style
/* priority: 20 */

/* =========================================================
   PWA SAFE AREAS + SYSTEM CHROME SURFACES
   ========================================================= */

html {
  /*
  Use solid colors here. Browser chrome and OS safe-area surfaces do not
  consistently support translucent gradients or color-mix results.
  */
  --sj-system-chrome-color: #f5faff;
  --sj-system-chrome-text: #294967;
  color-scheme: light;
}

html[data-theme="dark"] {
  --sj-system-chrome-color: #07121d;
  --sj-system-chrome-text: #e6f1fb;
  color-scheme: dark;
}

/*
The browser/PWA can expose pixels outside #sb-main. Keep every root
surface on the same solid color so those pixels never fall back to white.
*/
html,
body,
#sb-root {
  min-height: 100%;
  background-color: var(--sj-system-chrome-color) !important;
}

/*
The runtime adds .sj-standalone when launched as an installed PWA.
Use dynamic viewport height so the root follows mobile browser and
standalone viewport changes without leaving a contrasting bottom strip.
*/
html.sj-standalone,
html.sj-standalone body,
html.sj-standalone #sb-root {
  min-height: 100dvh;
  background-color: var(--sj-system-chrome-color) !important;
}

/*
Paint the iOS/Android safe areas explicitly. These layers are limited to
the OS-reserved insets and do not alter SilverBullet's content layout.
*/
@supports (padding: env(safe-area-inset-bottom)) {
  html.sj-standalone body::before,
  html.sj-standalone body::after {
    content: "";
    position: fixed;
    right: 0;
    left: 0;
    z-index: 2147483000;
    display: block;
    background: var(--sj-system-chrome-color);
    pointer-events: none;
  }

  html.sj-standalone body::before {
    top: 0;
    height: env(safe-area-inset-top);
  }

  html.sj-standalone body::after {
    bottom: 0;
    height: env(safe-area-inset-bottom);
  }
}

/*
When the virtual keyboard is open, keep the editor's own surfaces in
charge. The safe-area paint remains restricted to the actual OS inset.
*/
@media (max-width: 760px) {
  html,
  body,
  #sb-root {
    background-color: var(--sj-system-chrome-color) !important;
  }
}
```

```space-lua
-- priority: 20

-- =========================================================
-- SYSTEM CHROME META SYNCHRONIZER
-- Keeps browser/PWA chrome aligned with SilverBullet's theme.
-- =========================================================

sjSystemChrome = sjSystemChrome or {}

function sjSystemChrome.install()
  if js == nil or js.window == nil then
    return
  end

  js.window.eval([[
(function () {
  const controllerKey = "__sjSystemChromeController";

  if (
    window[controllerKey] &&
    typeof window[controllerKey].destroy === "function"
  ) {
    window[controllerKey].destroy();
  }

  const doc = document;
  const root = doc.documentElement;

  function ensureMeta(name) {
    let nodes = Array.from(
      doc.head.querySelectorAll('meta[name="' + name + '"]')
    );

    if (nodes.length === 0) {
      const node = doc.createElement("meta");
      node.setAttribute("name", name);
      doc.head.appendChild(node);
      nodes = [node];
    }

    return nodes;
  }

  function ensureViewportFitCover() {
    let viewport = doc.head.querySelector('meta[name="viewport"]');

    if (!viewport) {
      viewport = doc.createElement("meta");
      viewport.setAttribute("name", "viewport");
      viewport.setAttribute(
        "content",
        "width=device-width, initial-scale=1, viewport-fit=cover"
      );
      doc.head.appendChild(viewport);
      return;
    }

    const content = viewport.getAttribute("content") || "";

    if (!/viewport-fit\s*=\s*cover/i.test(content)) {
      viewport.setAttribute(
        "content",
        content.replace(/\s*,\s*$/, "") +
          (content.trim() ? ", " : "") +
          "viewport-fit=cover"
      );
    }
  }

  function isStandalone() {
    return (
      window.matchMedia("(display-mode: standalone)").matches ||
      window.navigator.standalone === true
    );
  }

  function currentMode() {
    const explicit = root.getAttribute("data-theme");

    if (explicit === "dark" || explicit === "light") {
      return explicit;
    }

    return window.matchMedia("(prefers-color-scheme: dark)").matches
      ? "dark"
      : "light";
  }

  function apply() {
    const mode = currentMode();
    const dark = mode === "dark";
    const color = dark ? "#07121d" : "#f5faff";

    root.classList.toggle("sj-standalone", isStandalone());
    root.style.setProperty("--sj-system-chrome-color", color);
    root.style.colorScheme = mode;

    if (doc.body) {
      doc.body.style.backgroundColor = color;
    }

    ensureMeta("theme-color").forEach(function (meta) {
      /*
      Browsers disagree about which matching theme-color node wins.
      Give every existing node the same current color.
      */
      meta.removeAttribute("media");
      meta.setAttribute("content", color);
    });

    ensureMeta("color-scheme").forEach(function (meta) {
      meta.setAttribute("content", mode);
    });

    ensureMeta("apple-mobile-web-app-status-bar-style").forEach(
      function (meta) {
        /*
        Apple only supports predefined status-bar styles, not arbitrary
        colors. Use dark icons on the light theme and a dark bar in dark
        mode, while the page safe-area supplies the surrounding color.
        */
        meta.setAttribute("content", dark ? "black" : "default");
      }
    );

    ensureViewportFitCover();
  }

  const themeObserver = new MutationObserver(function (records) {
    for (const record of records) {
      if (
        record.type === "attributes" &&
        (
          record.attributeName === "data-theme" ||
          record.attributeName === "class"
        )
      ) {
        apply();
        return;
      }
    }
  });

  themeObserver.observe(root, {
    attributes: true,
    attributeFilter: ["data-theme", "class"]
  });

  const schemeMedia = window.matchMedia(
    "(prefers-color-scheme: dark)"
  );
  const standaloneMedia = window.matchMedia(
    "(display-mode: standalone)"
  );

  function addMediaListener(media, listener) {
    if (typeof media.addEventListener === "function") {
      media.addEventListener("change", listener);
      return function () {
        media.removeEventListener("change", listener);
      };
    }

    media.addListener(listener);
    return function () {
      media.removeListener(listener);
    };
  }

  const removeSchemeListener = addMediaListener(
    schemeMedia,
    apply
  );
  const removeStandaloneListener = addMediaListener(
    standaloneMedia,
    apply
  );

  const readyListener = function () {
    apply();
  };

  window.addEventListener("pageshow", readyListener);
  window.addEventListener("focus", readyListener);

  apply();
  window.requestAnimationFrame(apply);
  window.setTimeout(apply, 250);

  window[controllerKey] = {
    destroy: function () {
      themeObserver.disconnect();
      removeSchemeListener();
      removeStandaloneListener();
      window.removeEventListener("pageshow", readyListener);
      window.removeEventListener("focus", readyListener);
    }
  };
})();
  ]])
end

sjSystemChrome.install()
```



## 🛠️ 维护说明

- 原生标签禁止使用 `#sb-main [class*="hashtag"]` 这类宽泛规则；它会在输入和 IME 组合状态下直接命中内部语法节点，造成同一标签在编辑前后尺寸和圆角不一致。普通与输入中的标签统一使用 8px 圆角和 2px × 6px 内边距。

- 首页标签云不设固定数量或固定行数。Widget 渲染全部过滤后标签，并按标签云实际剩余高度隐藏第一个放不下的完整行及其后内容；底部统计线始终保持可见。


- Dashboard 标签云继续使用等宽两列；Tags 板块页通过 `.sky-tag-index-grid > .sky-tag-chip-large` 按内容宽度自然换行，不要再对板块页标签设置 `width: 100%`。

- Dashboard 标签卡片保持紧凑单行标题区；Widget 副标题只保留“使用频率最高的标签集合”。空状态仍横跨标签网格全部列。


- Journal、Project、Area、Archive 和 Tasks 的空状态位于两列 Grid 中，必须使用 `grid-column: 1 / -1` 横跨整行；Tags 的空状态必须占满 Flex 整行，否则桌面宽度下提示文字会被限制在半列中异常换行。

- 围栏代码行使用不透明背景，因此包含代码块的编辑器会将 CodeMirror 原生 `.cm-selectionLayer` 提升到内容上方；不要再次把它强制设为负层级，也不要为此重写选区颜色或隐藏 `.cm-selectionBackground`。

- Frontmatter 折叠控制器只切换 `<html>` 上的 `.sj-frontmatter-collapsed`，不得直接修改 CodeMirror 的 `.cm-line` 或 Decoration 类名。
- 折叠状态下必须保留 opening fence 作为透明锚点，确保蓝色 `frontmatter` 角标始终可点击并恢复展开。

- 编辑器引用卡片只有一套规则：仅匹配带真实 QuoteMark Decoration 的行；禁止重新给 `.cm-editor blockquote` 或 `.cm-editor .sb-blockquote` 整块上背景。
- 引用行为本身由 SilverBullet 的 Markdown Enter 命令控制，主题只负责视觉，不再通过 MutationObserver 或 DOM 类修改干预编辑器。

- 引用卡片完全依赖 SilverBullet 原生 `.sb-blockquote-outside` 行 Decoration；不要再用 MutationObserver 给 `.cm-line` 增删类名。
- 在引用中按一次 Enter，SilverBullet 会原生续写 `>`；连续按两次 Enter 才会退出引用。这是编辑器行为，不是主题样式泄漏。

- 普通 Lua Widget 的 `.button-bar` 使用绝对定位覆盖在内容右上角；不要再改回 `position: relative` 或添加顶部外边距，否则工具栏会重新占据独立行。

- 字体完全使用系统字体栈，不需要上传字体文件、配置 CORS、设置 Nginx 字体目录或运行预载入脚本。

- 文本选区不包含任何自定义规则，完全使用 SilverBullet / CodeMirror 默认实现。

- 修改某项功能时，可直接定位到对应编号的 `space-style` 代码块。
- 多个块之间存在层叠覆盖关系，请保持当前顺序。
- 后方版本修正规则会覆盖前方基础规则，这是主题历史兼容逻辑的一部分。
- Dashboard 页面应仅保留 Space Lua 布局；Dashboard CSS 已集中在本文件第 11 区。

```text
╭────────────────────────────────────╮
│  RELINK FLIGHT SYSTEM · ACTIVE     │
│  THEME INDEX · SYNCHRONIZED        │
╰────────────────────────────────────╯
by Rawlkian
```
