---
date: <% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>
tags:
  - weekly
  - Routine
  - Todo
related:
  - "[[00-Weekly]]"
goal-type: weekly
goal-horizon: 1-week
parent-goals: <%*
// Auto-link to monthly note that contains this week
const weekDate = moment(tp.file.title, "YYYY-[W]WW");
const monthlyNote = weekDate.format("YYYY-MM");
tR += `["[[06-ROUTINES/Monthly/${monthlyNote}]]"]`;
%>
child-goals: <%*
// Auto-generate child-goals for daily notes in this week
const weekStart = moment(tp.file.title, "YYYY-[W]WW").startOf('week');
const dailyGoals = [];
for (let i = 0; i < 7; i++) {
    const dayMoment = weekStart.clone().add(i, 'days');
    dailyGoals.push(`"[[06-ROUTINES/Daily/${dayMoment.format("YYYY-MM-DD")}]]"`);
}
tR += `[${dailyGoals.join(', ')}]`;
%>
---
# Weekly Notes - Week <% moment(tp.file.title, "YYYY-[W]WW").format("WW, YYYY") %>

## References
### This Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-MM") %>]]
### Last Week
[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").subtract(1, 'weeks').format("YYYY-[W]WW") %>]]
### Next Week
[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").add(1, 'weeks').format("YYYY-[W]WW") %>]]
### Days:

| Day           | Note                                                                                                                |
| :------------ | :------------------------------------------------------------------------------------------------------------------ |
| **Sunday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>]]                |
| **Monday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(1, 'days').format("YYYY-MM-DD") %>]] |
| **Tuesday**   | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(2, 'days').format("YYYY-MM-DD") %>]] |
| **Wednesday** | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(3, 'days').format("YYYY-MM-DD") %>]] |
| **Thursday**  | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(4, 'days').format("YYYY-MM-DD") %>]] |
| **Friday**    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(5, 'days').format("YYYY-MM-DD") %>]] |
| **Saturday**  | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(6, 'days').format("YYYY-MM-DD") %>]] |

## Weekly Goals
#### 🎯 Career & Professional
- [[00-MOC-CAREER|00-Career]]:
	- [ ] 
- [[00-MCCS]]:
	- [ ] 
#### 💪 [[00-MEDICAL]] & [[00-FITNESS]]
- [[04-Current Training Program]]/ [[02-USAPL NATIONALS]]:
	- [ ] 
- Other:
	- [ ] Adderall intake this week:
#### 💍 Relationships & Personal: [[00-Social]]
- [[Victoria Owens Rubio]]:
	- [ ] 
- Family:
	- [ ] 
- Friends:
	- [ ] 
- Gatherings:
	- [ ] 
- Other:
	- [ ] 
#### 🧠 Learning & Growth
- [[00-2026 Spring]]
	- [ ] 
- [[00-MSAI]]
	- [ ] 
- [[00-BOOKS]]
	- [ ] 
- Other:
	- [ ] 
#### 🎨 Creative & Passion Projects
- [[00-UBUNTU]]:
	- [ ] 
- [[00-WEBSITE]]:
	- [ ] 
- Creating Art:
	- [ ] 
- Other:
	- [ ] 
#### 💰 Financial & Security
- Debts & Credit Paid off:
	- [ ] 
-  [ ] Purchase Budget:
#### Other
- 
## Big Picture Tasks
### <% moment(tp.file.title, "YYYY-[W]WW").format("MMMM YYYY") %> Goals:
> [!info]- Monthly Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Monthly"
> WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-MM") %>")
>   AND !completed
> SORT priority DESC, text ASC
> ```

### <% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-[Q]Q") %> Goals:

> [!info]- Quarterly Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Quarterly"
> WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-[Q]Q") %>")
> AND !completed
> SORT priority DESC, text ASC
> ```

## Project Tasks
```tasks
not done
(path includes 01-PROJECTS) OR (path includes 02-AREAS)
(due after <% moment(tp.file.title, "YYYY-[W]WW").startOf('week').subtract(1, 'days').format("YYYY-MM-DD") %>) AND (due before <% moment(tp.file.title, "YYYY-[W]WW").endOf('week').add(1, 'days').format("YYYY-MM-DD") %>)
sort by priority reverse
limit 10
```

## Recent Activity

### Goal Completion Trend of the Previous 6 weeks
```dataview
TABLE 
    file.link AS "Week",
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Weekly"
WHERE file.name != "00-Weekly" AND !contains(file.folder, "ARCHIVE")
SORT file.name DESC
LIMIT 6
```

### Recent [[00-PROJECTS]] Activity
```dataview
TABLE file.mtime as "Last Updated" 
FROM "01-PROJECTS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-PROJECTS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(7, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```
### Recent [[00-AREAS]] Activity
```dataview 
TABLE file.mtime as "Last Updated" 
FROM "02-AREAS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-AREAS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').add(7, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```

## Notes
- 

### Mind Dump
- 