---
created: <% tp.file.creation_date() %>
aliases: 
tags:
  - DailyNote
author:
  - 곽승준
source: 
type:
  - note
index:
  - "[[🏷 Daily Notes]]"
CMDS:
---
# <% tp.file.title %>

## [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %> |◀︎]] <% tp.file.title %> [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %> |▶︎]]


## Schedule
#### Event
- 

#### 1. 내가 해야 할 일 (목표 설정)
> 오늘의 주요 목표 (반드시 `#goal` 태그를 붙여주세요.)
- [ ] #goal 📅 <% tp.date.now("YYYY-MM-DD") %>

---

#### 완료
```tasks
tag includes #goal
done
due on {{date:YYYY-MM-DD}}
sort by done
```

---

#### 미완료
```tasks
tag includes #goal
not done
due before tomorrow
sort by priority
```


#### Daily Quote
<% tp.web.daily_quote() %>

## Note-taking

#### Created Today

```dataview
list
from ""
where file.cday = date(this.file.name) and !contains(file.folder, "00. Inbox/01. Daily Notes")
```

#### Modified Today

```dataview
list
from ""
where file.mday = date(this.file.name)
and !contains(file.folder, "00. Inbox/01. Daily Notes")
and file.cday != date(this.file.name)
```
