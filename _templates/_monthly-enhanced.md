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
parent-goals: []
child-goals: []
primary-focus: ""
key-projects: []
completion-status: ""
---
# <% moment(tp.file.title, "YYYY-MM").format("MMMM YYYY") %> Monthly Plan

## Goal Hierarchy

### Parent Annual Goals
```dataview
LIST
FROM "06-ROUTINES/Yearly"
WHERE contains(child-goals, this.file.link)
```

### Parent Quarterly Goals
```dataview
LIST  
FROM "06-ROUTINES/Quarterly"
WHERE contains(child-goals, this.file.link)
```

## References
### This Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").format("YYYY") %>]]

### This Quarter  
[[06-ROUTINES/Quarterly/<% moment(tp.file.title, "YYYY-MM").format("YYYY-[Q]Q") %>]]

### Last Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").subtract(1, 'months').format("YYYY-MM") %>]]

### Next Month
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").add(1, 'months').format("YYYY-MM") %>]]

## Monthly Theme
*What's the main focus for this month?*


## Monthly Goals

### Goals Supporting Annual Objectives
*Break down yearly goals into monthly actions*

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

### Project Milestones This Month
```dataview
TABLE 
    tags as "Type",
    file.mtime as "Last Updated"
FROM "01-PROJECTS"
WHERE contains(monthly-milestones, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT file.mtime DESC
```

### Area Maintenance Goals
```dataview
LIST
FROM "02-AREAS"
WHERE contains(monthly-focus, this.file.link) AND !contains(file.folder, "ARCHIVE")
```

## Weekly Breakdown
```dataview
TABLE 
    length(file.tasks.completed) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(file.tasks.completed) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Weekly"
WHERE contains(parent-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
SORT date ASC
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
    tR += `| ${link} |\n`; //  <--  Only the link and the separators
}
%>

## Habit & Routine Tracking
### Daily Habits This Month
- [ ] 
- [ ] 
- [ ] 

### Weekly Routines
- [ ] 
- [ ] 

## Project & Area Integration
### Active Projects This Month
```dataview
LIST
FROM "01-PROJECTS"
WHERE !contains(file.folder, "ARCHIVE") AND !contains(file.folder, "COMPLETED")
WHERE startswith(file.name, "00-") AND file.name != "00-PROJECTS"
SORT file.mtime DESC
LIMIT 5
```

### Areas Needing Focus
```dataview
LIST  
FROM "02-AREAS"
WHERE !contains(file.folder, "ARCHIVE")
WHERE startswith(file.name, "00-") AND file.name != "00-AREAS"
SORT file.mtime DESC
LIMIT 5
```

## Notes 
- 

## Monthly Review
### Mind Dump
- 

### Highlights
- 

### Challenges Faced
- 

### Lessons Learned
- 

### Goal Achievement Summary
- **Goals Completed**: __ / __ (__%)
- **Key Projects Advanced**: 
- **Habits Maintained**: 
- **Major Win**: 
- **Learning**: 

### Next Month Planning
- **Carry Forward Goals**: 
- **New Focus Areas**: 
- **Habit Adjustments**: 