---
date: <% moment(tp.file.title, "YYYY-[Q]Q").startOf('quarter').format("YYYY-MM-DD") %>
tags:
  - quarterly
  - Routine
  - Todo
related:
  - "[[00-Quarterly]]"
goal-type: quarterly
goal-horizon: 3-months
parent-goals: <%*
// Auto-link to yearly plan for this quarter
const quarterForParent = moment(tp.file.title, "YYYY-[Q]Q");
const parentYear = quarterForParent.year();
tR += `["[[06-ROUTINES/Yearly/${parentYear}]]"]`;
%>
child-goals: <%*
// Auto-generate child-goals for monthly notes in this quarter
const quarterForChildren = moment(tp.file.title, "YYYY-[Q]Q");
const childYear = quarterForChildren.year();
const childQuarterNumber = quarterForChildren.quarter();
const startMonth = (childQuarterNumber - 1) * 3; // 0, 3, 6, 9 (0-indexed)
const monthlyGoals = [];
for (let i = 0; i < 3; i++) {
    const monthIndex = startMonth + i;
    const monthMoment = moment().year(childYear).month(monthIndex);
    monthlyGoals.push(`"[[06-ROUTINES/Monthly/${monthMoment.format("YYYY-MM")}]]"`);
}
tR += `[${monthlyGoals.join(', ')}]`;
%>
primary-goals: ""
key-projects: <%*
// Auto-link to active projects starting with 00-
const fs = require('fs');
const path = require('path');
const projectsPath = path.join(app.vault.adapter.basePath, '01-PROJECTS');
const activeProjects = [];

try {
    const files = fs.readdirSync(projectsPath, { withFileTypes: true });
    for (const file of files) {
        if (file.isFile() && file.name.startsWith('00-') && file.name.endsWith('.md')) {
            const projectName = file.name.replace('.md', '');
            activeProjects.push(`"[[01-PROJECTS/${projectName}]]"`);
        }
    }
} catch (error) {
    // Fallback if directory reading fails
}

tR += activeProjects.length > 0 ? `[${activeProjects.join(', ')}]` : '[]';
%>
completion-status: ""
---
# <% moment(tp.file.title, "YYYY-[Q]Q").format("[Q]Q YYYY") %> Quarterly Plan

## References

### This Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY-[Q]Q").format("YYYY") %>]]

### Last Quarter
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-[Q]Q").subtract(1, 'quarters').format("YYYY-[Q]Q") %>]]

### Next Quarter
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-[Q]Q").add(1, 'quarters').format("YYYY-[Q]Q") %>]]

## Monthly Breakdown
```dataview
TABLE 
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Monthly"
WHERE contains(parent-goals, this.file.link) 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name ASC
```

## Monthly Tracker
| Months this Quarter |
| :------------------ |
<%*
const quarter = moment(tp.file.title, "YYYY-[Q]Q");
const year = quarter.year();
const tableQuarterNumber = quarter.quarter();
const tableStartMonth = (tableQuarterNumber - 1) * 3;

function generateMonthLink(year, month) {
  const monthMoment = moment().year(year).month(month);
  return `[[06-ROUTINES/Monthly/${monthMoment.format("YYYY-MM")}]]`;
}

for(let i = 0; i < 3; i++){
  const monthIndex = tableStartMonth + i;
  tR += `| ${generateMonthLink(year, monthIndex)} |\n`;
}
%>

## Quarterly Theme
*What's the main focus for this quarter?*
- 

## Quarterly Goals

#### 🎯 Career & Professional
- [[00-MOC-CAREER|00-Career]]:
	- [ ] 
- [[00-MCCS]]:
	- [ ] 

#### 💪 [[00-MEDICAL]] & [[00-FITNESS]]
- [[04-Current Training Program]]/ [[02-USAPL NATIONALS]]:
	- [ ] 
- Other:
	- [ ] 

#### 💍 Relationships & Personal: [[00-Social]]
- [[Victoria Owens Rubio]]:
	- [ ] 
- Family:
	- [ ] 
- Friends:
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
- [ ] Purchase Budget:

#### Other
- 

## Big Picture Tasks

### <% moment(tp.file.title, "YYYY-[Q]Q").format("YYYY") %> Goals:
> [!info]- Yearly Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Yearly"
> WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-[Q]Q").format("YYYY") %>")
>   AND !completed
> SORT priority DESC, text ASC
> ```

## Project Tasks
```tasks
not done
(path includes 01-PROJECTS) OR (path includes 02-AREAS)
(due after <% moment(tp.file.title, "YYYY-[Q]Q").startOf('quarter').subtract(1, 'days').format("YYYY-MM-DD") %>) AND (due before <% moment(tp.file.title, "YYYY-[Q]Q").endOf('quarter').add(1, 'days').format("YYYY-MM-DD") %>)
sort by priority reverse
limit 20
```

## Recent Activity

### Goal Completion Trend of Previous Quarters
```dataview
TABLE 
    file.link AS "Quarter",
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Quarterly"
WHERE file.name != "00-Quarterly" 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name DESC
LIMIT 4
```

### Recent [[00-PROJECTS]] Activity
```dataview
TABLE file.mtime as "Last Updated" 
FROM "01-PROJECTS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-PROJECTS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-[Q]Q").startOf('quarter').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-[Q]Q").endOf('quarter').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```

### Recent [[00-AREAS]] Activity
```dataview 
TABLE file.mtime as "Last Updated" 
FROM "02-AREAS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-AREAS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-[Q]Q").startOf('quarter').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-[Q]Q").endOf('quarter').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```

## Notes
- 

## Quarterly Review

### Mind Dump
- 