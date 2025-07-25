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

## Goal Hierarchy

### Parent 5-Year Goals
```dataview
LIST
FROM "06-ROUTINES/5-Year"
WHERE contains(child-goals, this.file.link)
```

### Supporting Life Goals  
```dataview
LIST
FROM "06-ROUTINES/Life"
WHERE contains(child-goals, child-goals)
```
-- Update uptop
## Reference Navigation
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

## Annual Theme & Focus
### Primary Focus Area
*What is the main theme for this year?*


### Core Intention
*What do you want this year to be about?*


## Yearly Goals & Projects

### Goal Categories

#### 🎯 Career & Professional
- [ ] 

#### 💪 Health & Fitness  
- [ ] 

#### 💍 Relationships & Personal
- [ ] 

#### 🧠 Learning & Growth
- [ ] 

#### 🎨 Creative & Passion Projects
- [ ] 

#### 💰 Financial & Security
- [ ] 

## Supporting Projects
```dataview
TABLE 
    tags as "Type",
    created as "Started"
FROM "01-PROJECTS"
WHERE contains(supporting-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT created DESC
```

## Quarterly Breakdown
```dataview
TABLE 
    primary-goals as "Focus",
    key-projects as "Projects",
    completion-status as "Status"
FROM "06-ROUTINES/Quarterly"
WHERE contains(parent-goals, this.file.link)
SORT date ASC
```

## Quarterly Tracker
| Quarter | Focus Area | Key Projects | Status |
| :------ | :--------- | :----------- | :----: |
<%*
const year = moment(tp.file.title, "YYYY").year();

function generateQuarterLink(quarter) {
    const startDate = moment().year(year).quarter(quarter).startOf('quarter');
    return `[[06-ROUTINES/Quarterly/${startDate.format("YYYY-[Q]Q")}]]`;
}

let tableRows = "";
for (let q = 1; q <= 4; q++) {
    tableRows += `| ${generateQuarterLink(q)} |  |  |  |\n`;
}

tR += tableRows;
%>

## Monthly Goal Rollup
```dataview
TABLE 
    length(file.tasks.completed) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(file.tasks.completed) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %",
    primary-focus as "Focus"
FROM "06-ROUTINES/Monthly"
WHERE contains(parent-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT date DESC
LIMIT 12
```

## Areas & Habits Integration
### Key Areas This Year
```dataview
LIST
FROM "02-AREAS"
WHERE contains(strategic-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
```

### Habits to Build/Maintain
- [ ] 
- [ ] 
- [ ] 

## Progress Tracking
### Current Progress (Mid-Year Review)
*How are you doing on your annual goals?*


### Key Wins So Far
- 

### Areas Needing Attention  
- 

### Course Corrections Needed
- 

## Yearly Review 
### Mind Dump
- 

### Major Highlights
- 

### Major Challenges Faced
- 

### Major Lessons Learned
- 

### Areas for Growth
- 

### Success Metrics Achieved
- 

### Goals to Carry Forward
- 