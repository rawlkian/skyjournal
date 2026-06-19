```space-lua
sj = sj or {}

function sj.dashboard()
  return widget.htmlBlock(
    dom.div {
      class = sj.themeRootClass("sky-dashboard"),

      -- HERO
      sj.hero(),

      -- PRIMARY HUD
      dom.div {
        class = "sky-grid sky-dashboard-block",
        dom.div {
          class = "sky-hud-panel sky-hud-stack-panel",
          dom.div {
            class = "sky-hud-stack",
            sj.captain(),
            sj.countdown()
          }
        },
        dom.div {
          class = "sky-hud-panel sky-hud-calendar-panel",
          sj.calendarActivity()
        },
        dom.div {
          class = "sky-hud-panel sky-hud-tags-panel",
          sj.tagsCard()
        },
        dom.div {
          class = "sky-hud-panel sky-hud-weather-panel",
          sj.weather()
        }
      },

      -- NAV PANEL
      sj.quickNav(),

      -- LIVE OVERVIEW
      dom.div {
        class = "sky-section-heading",
        dom.span { "✦ LIVE NAVIGATION DATA ✦" },
        dom.small { "Recent notes and active missions" }
      },
      dom.div {
        class = "sky-overview-grid",
        sj.recentNotes(),
        sj.openTasks()
      },

      -- PARA KNOWLEDGE DECK
      dom.div {
        class = "sky-section-heading",
        dom.span { "✦ KNOWLEDGE DECK ✦" },
        dom.small { "Journal · Project · Area · Archive" }
      },
      dom.div {
        class = "sky-para-grid",
        sj.journalList(),
        sj.projectList(),
        sj.areaList(),
        sj.archiveList()
      },

      -- FOOTER
      sj.footer()
    }
  )
end
```
