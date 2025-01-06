---
cssclasses:
  - dashboard
banner: "![[Pasted image 20250104201310.png]]"
banner_y: 0.18
---
## ⚙️ **DASHBOARD**

#### 🎓 Kuliah 
---
Jadwal Kuliah

Tugas
```dataview
TABLE MataKuliah as "Mata Kuliah", Selesai, Deadline, Catatan
from "01 - Kuliah" AND #kuliah/tugas
WHERE Selesai = false
SORT Deadline
```
#### 🏆 Tracker
---
##### **🥤 Hydration**

```contributionGraph
title: ""
graphType: default
dateRangeValue: 12
dateRangeType: FIXED_DATE_RANGE
startOfWeek: 0
showCellRuleIndicators: true
titleStyle:
  textAlign: left
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#daily"
  dateField:
    type: PAGE_PROPERTY
    value: date
  filters: []
  countField:
    type: PAGE_PROPERTY
    value: Liter
fillTheScreen: false
enableMainContainerShadow: false
cellStyleRules:
  - id: Ocean_a
    color: "#8dd1e2"
    min: "2"
    max: "4"
  - id: Ocean_b
    color: "#63a1be"
    min: "4"
    max: "6"
  - id: Ocean_c
    color: "#376d93"
    min: "6"
    max: "8"
  - id: Ocean_d
    color: "#012f60"
    min: "8"
    max: 9999
fromDate: 2025-01-01
toDate: 2025-12-31

```
##### **💸 Financial**
```contributionGraph
title: ""
graphType: default
dateRangeValue: 180
dateRangeType: FIXED_DATE_RANGE
startOfWeek: 0
showCellRuleIndicators: true
titleStyle:
  textAlign: left
  fontSize: 15px
  fontWeight: normal
dataSource:
  type: PAGE
  value: "#daily"
  dateField: {}
  countField:
    type: PAGE_PROPERTY
    value: Pengeluaran
fillTheScreen: false
enableMainContainerShadow: false
fromDate: 2025-01-01
toDate: 2025-12-31
cellStyleRules: []

```
#### 🗓️ Acara
---
```dataview
TABLE date as "Tanggal", startTime as "Jam" 
from "07 - Daily/Events" AND #event 
WHERE completed = false
```
#### Vault Info
---
- 🗄️ Recent file updates `$=dv.list(dv.pages('').sort(f=>f.file.mtime.ts,"desc").limit(4).file.link)`
- 🔖 Tagged: favorite `$=dv.list(dv.pages('#favorite').sort(f=>f.file.name,"desc").limit(4).file.link)`
- 〽️ Stats
    - File Count: `$=dv.pages().length`
    - Personal recipes: `$=dv.pages('"Family/Recipes"').length`