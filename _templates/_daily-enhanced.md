---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - Routine
  - Todo
related:
  - "[[00-Daily]]"
goal-type: daily
goal-horizon: 1-day
parent-goals: []
---
# Daily Notes - <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D, YYYY") %>

| Direction    | Date                                                                                                             | Link                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 📅 This Week | <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %> | [[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]] |
| ◀️ Yesterday | <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>                               | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>]]                                |
| ▶️ Tomorrow  | <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>                                    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>]]                                     |
## Notes
- 

## Goal Hierarchy Context
### This Week's Goals  
```dataview
TASK
FROM "06-ROUTINES/Weekly"
WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-[W]WW") %>")
WHERE !completed
LIMIT 5
```

### This Month's Focus
```dataview
LIST primary-focus
FROM "06-ROUTINES/Monthly"  
WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM") %>")
LIMIT 1
```

## Today's Focus
### Top 3 Priorities
*Aligned with weekly and monthly goals*
1. 
2. 
3. 

### Project Time Blocks
- 🎬 **Screenwriting**: 
- 💍 **Wedding**: 
- 🎓 **Learning**: 
- 💻 **Development**: 

### Daily Habits
- [ ] 
- [ ] 
- [ ] 
## Today's Active Projects
```dataview
LIST
FROM "01-PROJECTS"
WHERE !contains(file.folder, "COMPLETED") AND !contains(file.folder, "ARCHIVE")
WHERE startswith(file.name, "00-") AND file.name != "00-PROJECTS"
GROUP BY file.folder
SORT file.mtime DESC
```

## Current Project Focus Areas
```dataview
TABLE WITHOUT ID
  file.link as "Project",
  tags as "Type",
  created as "Started"
FROM "01-PROJECTS"
WHERE contains(tags, "screenwriting") OR contains(tags, "wedding") OR contains(tags, "certification")
WHERE !contains(file.folder, "COMPLETED")
SORT created DESC
LIMIT 5
```

## Outstanding Tasks
```dataview
TASK
FROM "01-PROJECTS" OR "02-AREAS" OR "06-ROUTINES/Daily"
WHERE !completed
WHERE !contains(file.folder, "ARCHIVE")
WHERE due >= date(today) OR !due
SORT priority DESC, due ASC
LIMIT 8
```

## Recent Project Activity
```dataview
TABLE 
  choice(file.mtime > date(today) - dur(7 days), "🔥 This Week", 
    choice(file.mtime > date(today) - dur(30 days), "📅 This Month", "💤 Older")) as "Activity",
  file.mtime as "Last Updated"
FROM "01-PROJECTS"
WHERE !contains(file.folder, "COMPLETED") AND !contains(file.folder, "ARCHIVE")
WHERE file.name != "00-PROJECTS"
SORT file.mtime DESC
LIMIT 5
```

## End of Day Review
### Completed
- 

### Tomorrow's Prep
- 