---
date: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
tags:
  - yearly
  - Routine
  - Todo
related:
  - "[[00-Yearly]]"
goal-type: annual
goal-horizon: 1-year
parent-goals: <%*
// Auto-link to 5-year that contains this year
const currentYear = moment(tp.file.title, "YYYY").year();
const fiveYearStart = Math.floor((currentYear - 2025) / 5) * 5 + 2025;
const fiveYearEnd = fiveYearStart + 4;
tR += `["[[06-ROUTINES/5-Year/${fiveYearStart}-${fiveYearEnd}]]"]`;
%>
child-goals: <%*
// Auto-generate child-goals for quarterly notes in this year
const yearForQuarters = moment(tp.file.title, "YYYY").year();
const quarterlyGoals = [];
for (let q = 1; q <= 4; q++) {
    quarterlyGoals.push(`"[[06-ROUTINES/Quarterly/${yearForQuarters}-Q${q}]]"`);
}
tR += `[${quarterlyGoals.join(', ')}]`;
%>
primary-focus: ""
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
goal-progress: ""
---
# <% tp.file.title %> Annual Plan

## References

### Current 5-Year
<%*
const currentYearNav = moment(tp.file.title, "YYYY").year();
const fiveYearStartNav = Math.floor((currentYearNav - 2025) / 5) * 5 + 2025;
const fiveYearEndNav = fiveYearStartNav + 4;
tR += `[[06-ROUTINES/5-Year/${fiveYearStartNav}-${fiveYearEndNav}]]`;
%>

### Last Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").subtract(1, 'years').format("YYYY") %>]]

### Next Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").add(1, 'years').format("YYYY") %>]]

## Quarterly Breakdown
```dataview
TABLE 
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Quarterly"
WHERE contains(parent-goals, this.file.link) 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name ASC
```

## Quarterly Tracker
| Quarters this Year |
| :----------------- |
<%*
const year = moment(tp.file.title, "YYYY").year();

function generateQuarterLink(quarter) {
    const startDate = moment().year(year).quarter(quarter).startOf('quarter');
    return `[[06-ROUTINES/Quarterly/${startDate.format("YYYY-[Q]Q")}]]`;
}

for (let q = 1; q <= 4; q++) {
    tR += `| ${generateQuarterLink(q)} |\n`;
}
%>

## Annual Theme
*What's the main focus for this year?*
- 

## Yearly Goals

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

### 5-Year Goals:
> [!info]- 5-Year Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/5-Year"
> WHERE contains(child-goals, this.file.link)
>   AND !completed
> SORT priority DESC, text ASC
> ```

## Project Tasks
```tasks
not done
(path includes 01-PROJECTS) OR (path includes 02-AREAS)
(due after <% moment(tp.file.title, "YYYY").startOf('year').subtract(1, 'days').format("YYYY-MM-DD") %>) AND (due before <% moment(tp.file.title, "YYYY").endOf('year').add(1, 'days').format("YYYY-MM-DD") %>)
sort by priority reverse
limit 25
```

## Recent Activity

### Goal Completion Trend of Previous Years
```dataview
TABLE 
    file.link AS "Year",
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Yearly"
WHERE file.name != "00-Yearly" 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name DESC
LIMIT 5
```

### Recent [[00-PROJECTS]] Activity
```dataview
TABLE file.mtime as "Last Updated" 
FROM "01-PROJECTS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-PROJECTS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY").endOf('year').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
LIMIT 10
```

### Recent [[00-AREAS]] Activity
```dataview 
TABLE file.mtime as "Last Updated" 
FROM "02-AREAS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-AREAS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY").endOf('year').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
LIMIT 10
```

## Notes
- 

## Yearly Review

### Mind Dump
- 

### Highlights
- 

### Challenges Faced
- 

### Lessons Learned
- 