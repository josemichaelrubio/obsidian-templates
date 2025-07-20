---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - Routine
  - Todo
related:
  - "[[00-Daily]]"
---
# Daily Notes - <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D, YYYY") %>

| Direction    | Date                                                                                                             | Link                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 📅 This Week | <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %> | [[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]] |
| ◀️ Yesterday | <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>                               | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>]]                                |
| ▶️ Tomorrow  | <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>                                    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>]]                                     |

## Today's Active Projects 
```dataview
LIST 
FROM "01-PROJECTS"
WHERE !contains(file.folder, "COMPLETED") AND !contains(file.folder, "ARCHIVE")
WHERE file.name != "00-PROJECTS"
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

## Notes
- 

## Today's Focus
### Top 3 Priorities
1. 
2. 
3. 

### Project Time Blocks
- 🎬 **Screenwriting**: 
- 💍 **Wedding**: 
- 🎓 **Learning**: 
- 💻 **Development**: 

## End of Day Review
### Completed
- 

### Tomorrow's Prep
- 