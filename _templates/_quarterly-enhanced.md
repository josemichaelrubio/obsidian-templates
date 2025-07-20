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
parent-goals: []
child-goals: []
primary-goals: ""
key-projects: []
completion-status: ""
---
# <% moment(tp.file.title, "YYYY-[Q]Q").format("[Q]Q YYYY") %> Quarterly Plan

## Goal Hierarchy

### Parent Annual Goals
```dataview
LIST
FROM "06-ROUTINES/Yearly"
WHERE contains(child-goals, this.file.link)
```

### Parent 5-Year Goals
```dataview
LIST
FROM "06-ROUTINES/5-Year Plan"
WHERE contains(child-goals, this.file.link)
```

## References
### This Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY-[Q]Q").format("YYYY") %>]]

### Last Quarter
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-[Q]Q").subtract(1, 'quarters').format("YYYY-[Q]Q") %>]]

### Next Quarter
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-[Q]Q").add(1, 'quarters').format("YYYY-[Q]Q") %>]]

## Quarterly Theme & Focus
### Primary Focus Area
*What is the main theme for this quarter?*


### Key Outcomes
*What do you want to achieve by the end of this quarter?*


## Quarterly Goals

### Goals Supporting Annual Objectives
*Break down yearly goals into quarterly milestones*

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

## Project Focus This Quarter
```dataview
TABLE 
    tags as "Type",
    file.mtime as "Last Updated"
FROM "01-PROJECTS"
WHERE contains(quarterly-focus, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT file.mtime DESC
```

## Monthly Breakdown
```dataview
TABLE 
    primary-focus as "Focus",
    length(file.tasks.completed) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(file.tasks.completed) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Monthly"
WHERE contains(parent-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT date ASC
```

## Monthly Tracker
| Month | Focus Area | Key Projects | Status |
| :---- | :--------- | :----------- | :----: |
<%*
const quarter = moment(tp.file.title, "YYYY-[Q]Q");
const year = quarter.year();
const quarterNumber = quarter.quarter();
const startMonth = (quarterNumber - 1) * 3; // 0, 3, 6, 9 (0-indexed)

function generateMonthLink(year, month) {
  const monthMoment = moment().year(year).month(month);
  return `[[06-ROUTINES/Monthly/${monthMoment.format("YYYY-MM")}]]`;
}

let tableRows = "";
for(let i = 0; i < 3; i++){
  const monthIndex = startMonth + i;
  tableRows += `| ${generateMonthLink(year, monthIndex)} |  |  |  |\n`
}

tR += tableRows;
%>

## Areas & Projects Integration
### Key Areas This Quarter
```dataview
LIST
FROM "02-AREAS"
WHERE contains(quarterly-focus, this.file.link) AND !contains(file.folder, "ARCHIVE")
```

### Major Projects This Quarter
```dataview
LIST
FROM "01-PROJECTS"
WHERE contains(quarterly-milestones, this.file.link) AND !contains(file.folder, "ARCHIVE")
WHERE startswith(file.name, "00-") AND file.name != "00-PROJECTS"
```

## Progress Tracking
### Mid-Quarter Review
*How are you progressing toward quarterly goals?*


### Key Wins This Quarter
- 

### Challenges Encountered
- 

### Course Corrections Needed
- 

## Quarterly Review
### Mind Dump
- 

### Major Highlights
- 

### Major Challenges Faced
- 

### Major Lessons Learned
- 

### Goal Achievement Summary
- **Goals Completed**: __ / __ (__%)
- **Key Projects Advanced**: 
- **Major Milestone Reached**: 
- **Biggest Win**: 
- **Key Learning**: 

### Next Quarter Planning
- **Goals to Carry Forward**: 
- **New Focus Areas**: 
- **Habit Changes**: 
- **Project Priorities**: 