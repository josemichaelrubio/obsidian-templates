---
date: <% moment(tp.file.title, "YYYY-MM").startOf('month').format("YYYY-MM-DD") %>
tags:
  - monthly
  - Routine
  - Todo
related:
  - "[[00-Monthly]]"
goal-type: monthly
goal-horizon: 1-month
parent-goals: <%*
// Auto-link to quarterly note that contains this month
const monthDate = moment(tp.file.title, "YYYY-MM");
const quarterlyNote = monthDate.format("YYYY-[Q]Q");
tR += `["[[06-ROUTINES/Quarterly/${quarterlyNote}]]"]`;
%>
child-goals: <%*
// Auto-generate child-goals for weekly notes in this month
const monthStart = moment(tp.file.title, "YYYY-MM").startOf('month');
const monthEnd = moment(tp.file.title, "YYYY-MM").endOf('month');
const weeklyGoals = [];

// Find all weeks that overlap with this month
let currentWeek = monthStart.clone().startOf('week');
while (currentWeek.isSameOrBefore(monthEnd, 'week')) {
    weeklyGoals.push(`"[[06-ROUTINES/Weekly/${currentWeek.format("YYYY-[W]WW")}]]"`);
    currentWeek.add(1, 'week');
}
tR += `[${weeklyGoals.join(', ')}]`;
%>
primary-focus: 
  - 
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
# <% moment(tp.file.title, "YYYY-MM").format("MMMM YYYY") %> Monthly Plan

## References

### This Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").format("YYYY") %>]]

### This Quarter  
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-MM").format("YYYY-[Q]Q") %>]]

### Last Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").subtract(1, 'months').format("YYYY-MM") %>]]

### Next Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").add(1, 'months').format("YYYY-MM") %>]]

## Weekly Breakdown
```dataview
TABLE 
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Weekly"
WHERE contains(parent-goals, this.file.link) 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name ASC
```

## Weekly Tracker
| Weeks this Month |
| :--------------- |
<%*
// Get the current month and year from the file title
const currentMonth = moment(tp.file.title, "YYYY-MM");
const year = currentMonth.year();
const month = currentMonth.month(); // Month is 0-indexed (0 = January, 11 = December)

// Function to generate the week link
function generateWeekLink(year, week) {
    const weekMoment = moment().year(year).week(week);
    // VERY IMPORTANT: Check if the week actually belongs to the current month.
    if (weekMoment.month() === month) {
        return `[[06-ROUTINES/Weekly/${weekMoment.format("YYYY-[W]WW")}]]`;
    }
    return null; // Return null if the week is not in the current month
}

// Generate potential week links (weeks 1 to 53, to cover all possibilities)
const weekLinks = [];
for (let week = 1; week <= 53; week++) {
    const link = generateWeekLink(year, week);
    if (link) {
        weekLinks.push(link);
    }
}

// Handle the edge case for week 53 of the previous year/ week 1 of next year.
const firstWeek = moment(tp.file.title, "YYYY-MM").startOf('month').week();
const lastWeek = moment(tp.file.title, "YYYY-MM").endOf('month').week();

if(firstWeek > 51){
  const linkPreviousYear = generateWeekLink(year - 1, firstWeek);
      if (linkPreviousYear) {
          weekLinks.unshift(linkPreviousYear); //Adds to beggining
      }
}
if(lastWeek == 1){
  const linkNextYear = generateWeekLink(year + 1, lastWeek)
    if (linkNextYear){
      weekLinks.push(linkNextYear)
    }
}

// Output the table rows
for (const link of weekLinks) {
    tR += `| ${link} |\n`;
}
%>

## Monthly Theme
*What's the main focus for this month?*

## Monthly Goals

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

### <% moment(tp.file.title, "YYYY-MM").format("YYYY-[Q]Q") %> Goals:
> [!info]- Quarterly Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Quarterly"
> WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM").format("YYYY-[Q]Q") %>")
>   AND !completed
> SORT priority DESC, text ASC
> ```

### <% moment(tp.file.title, "YYYY-MM").format("YYYY") %> Goals:
> [!info]- Yearly Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Yearly"
> WHERE contains(file.name, "<% moment(tp.file.title, "YYYY-MM").format("YYYY") %>")
>   AND !completed
> SORT priority DESC, text ASC
> ```

## Project Tasks
```tasks
not done
(path includes 01-PROJECTS) OR (path includes 02-AREAS)
(due after <% moment(tp.file.title, "YYYY-MM").startOf('month').subtract(1, 'days').format("YYYY-MM-DD") %>) AND (due before <% moment(tp.file.title, "YYYY-MM").endOf('month').add(1, 'days').format("YYYY-MM-DD") %>)
sort by priority reverse
limit 15
```

## Recent Activity

### Goal Completion Trend of Previous Weeks
```dataview
TABLE 
    file.link AS "Week",
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Weekly"
WHERE file.name != "00-Weekly" 
  AND !contains(file.folder, "ARCHIVE")
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
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-MM").startOf('month').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-MM").endOf('month').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```

### Recent [[00-AREAS]] Activity
```dataview 
TABLE file.mtime as "Last Updated" 
FROM "02-AREAS" 
WHERE !contains(file.folder, "ARCHIVE") 
  AND !contains(file.folder, "COMPLETED") 
  AND file.name != "00-AREAS" 
  AND file.mtime >= date(<% moment(tp.file.title, "YYYY-MM").startOf('month').format("YYYY-MM-DD") %>) 
  AND file.mtime < date(<% moment(tp.file.title, "YYYY-MM").endOf('month').add(1, 'days').format("YYYY-MM-DD") %>) 
SORT file.mtime DESC
```

## Notes
- 

## Monthly Review

### Mind Dump
-