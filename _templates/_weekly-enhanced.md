---
date: <% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>
tags:
  - weekly
  - Routine
  - Todo
related:
  - "[[00-Weekly]]"
---
# Weekly Notes - Week <% moment(tp.file.title, "YYYY-[W]WW").format("WW, YYYY") %>

## References
### This Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-MM") %>]]
### Last Week
[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").subtract(1, 'weeks').format("YYYY-[W]WW") %>]]
### Next Week
[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").add(1, 'weeks').format("YYYY-[W]WW") %>]]

## Weekly Planning

### Weekly Goals
- [ ] 

### Project Focus This Week
```dataview
LIST
FROM "01-PROJECTS"
WHERE !contains(file.folder, "ARCHIVE") AND !contains(file.folder, "COMPLETED")
WHERE startswith(file.name, "00-") AND file.name != "00-PROJECTS"
GROUP BY file.folder
SORT file.mtime DESC
```

### Open Tasks From Projects
```dataview
TASK
FROM "01-PROJECTS" OR "02-AREAS"
WHERE !completed AND !regexmatch(file.folder, "(?i)archive")
WHERE due >= date(<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>) AND due <= date(<% moment(tp.file.title, "YYYY-[W]WW").endOf('week').format("YYYY-MM-DD") %>) OR !due
SORT priority DESC, due ASC
LIMIT 10
```

## Daily Tracker

| Day           | Note                                                                                                                | Top Priority |
| :------------ | :------------------------------------------------------------------------------------------------------------------ | :----------: |
| **Sunday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>]]                |              |
| **Monday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(1, 'days').format("YYYY-MM-DD") %>]] |              |
| **Tuesday**   | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(2, 'days').format("YYYY-MM-DD") %>]] |              |
| **Wednesday** | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(3, 'days').format("YYYY-MM-DD") %>]] |              |
| **Thursday**  | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(4, 'days').format("YYYY-MM-DD") %>]] |              |
| **Friday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(5, 'days').format("YYYY-MM-DD") %>]] |              |
| **Saturday**  | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(6, 'days').format("YYYY-MM-DD") %>]] |              |

## Weekly Performance Review

### Goal Completion Trend
```dataview
TABLE 
    file.link AS "Week",
    length(file.tasks.completed) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(file.tasks.completed) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Weekly"
WHERE file.name != "00-Weekly" AND !regexmatch(file.folder, "(?i)archive")
SORT date DESC
LIMIT 6
```

### Recent Project Activity
```dataview
TABLE 
  choice(file.mtime > date(today) - dur(7 days), "🔥 This Week", 
    choice(file.mtime > date(today) - dur(14 days), "📅 Recent", "💤 Older")) as "Activity",
  file.mtime as "Last Updated"
FROM "01-PROJECTS"
WHERE !contains(file.folder, "ARCHIVE") AND !contains(file.folder, "COMPLETED")
WHERE file.name != "00-PROJECTS"
SORT file.mtime DESC
LIMIT 8
```

## Notes
- 

## Weekly Review
### Mind Dump
- 

### Highlights
- 

### Challenges Faced
- 

### Lessons Learned
- 

### Key Metrics
- **Goals Completed**: __ / __ (__%)
- **Project Focus**: 
- **Energy Level**: __ / 10
- **Key Win**: 
- **Area for Improvement**: 

### Next Week Planning
- **Top 3 Priorities**: 
  1. 
  2. 
  3. 
- **Project Focus**: 
- **Time Allocation**: 