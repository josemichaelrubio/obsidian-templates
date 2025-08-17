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
parent-goals: <%*
// Auto-link to weekly note that contains this day
const dailyDate = moment(tp.file.title, "YYYY-MM-DD");
const weeklyNote = dailyDate.format("YYYY-[W]WW");
tR += `["[[06-ROUTINES/Weekly/${weeklyNote}]]"]`;
%>
---
# Daily Notes - <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D, YYYY") %>

| Direction    | Date                                                                                                             | Link                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 📅 This Week | <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %> | [[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]] |
| ◀️ Yesterday | <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>                               | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>]]                                |
| ▶️ Tomorrow  | <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>                                    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>]]                                     |
## Notes
- 

## Morning Affirmations (Napoleon Hill Method)
*Read aloud with emotion and belief*
```dataview
LIST daily-affirmation
FROM "03-RESOURCES/Self-Help"
```

## Goal Hierarchy Context
### This Week's Goals  
```dataview
TASK
FROM "06-ROUTINES/Weekly"
WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-[W]WW") %>")
WHERE !completed
```

### This Month's Focus
```dataview
LIST primary-focus
FROM "06-ROUTINES/Monthly"  
WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM") %>")
```

#### Today's Goal Contributions
```dataview
TASK
FROM "06-ROUTINES/Daily"
WHERE file.name = "<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>"
WHERE !completed
```

## Today's Focus
### Top 3 Priorities
*Aligned with weekly and monthly goals*
- [ ] ⬆️ 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] 🔼 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] 🔼 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 

### Project Time Blocks
- [ ] 🎬 **Screenwriting**: ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] 💍 **Wedding**: ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] 🎓 **Learning**: ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] 💻 **Development**: ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 📅 <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 

### Daily Habits
- [ ] Morning routine 🔁 every day ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] Exercise session 🔁 every day 🔼 ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
- [ ] Evening review 🔁 every day ⏳ <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 
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
//WHERE contains(tags, "screenwriting") OR contains(tags, "wedding") OR 
//contains(tags,"certification")
WHERE !contains(file.folder, "COMPLETED")
SORT created DESC
LIMIT 10
```

## Outstanding Tasks
```dataview
TASK
FROM 
"06-ROUTINES/Daily"
WHERE !completed
WHERE !contains(file.folder, "ARCHIVE")
WHERE due >= date(today) OR !due
SORT priority DESC, due ASC
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
LIMIT 10
```

## End of Day Review
### Completed
```tasks
done on <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
sort by done
```

### Today's Persistence Practice (Napoleon Hill)
*What obstacles did you overcome today?*
- 

*How did you maintain faith in your goals?*
- 

## Evening Visualization (Think and Grow Rich)
*Practice before sleep - see yourself in possession of your goals*
```dataview
LIST visualization-statement  
FROM "03-RESOURCES/Self-Help"
```

### Tomorrow's Prep
- 