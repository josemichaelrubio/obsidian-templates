---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - 5-year
  - long-term
  - planning
related:
  - "[[00-5Year]]"
goal-type: strategic
goal-horizon: 5-year
parent-goals: []
child-goals: []
---
# 5-Year Plan: <% tp.file.title %>

## Parent Life Goals
```dataview
LIST
FROM "06-ROUTINES/Life"
WHERE contains(child-goals, this.file.link)
```

## Strategic Focus Areas
*What are the 3-5 major themes for these 5 years?*

### 1. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 

### 2. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 

### 3. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 

## Year-by-Year Breakdown
```dataview
TABLE 
    primary-focus as "Focus",
    key-projects as "Key Projects",
    goal-progress as "Progress"
FROM "06-ROUTINES/Yearly"
WHERE contains(parent-goals, this.file.link)
SORT date ASC
```

## Supporting Annual Goals
```dataview
LIST
FROM "06-ROUTINES/Yearly"
WHERE contains(parent-goals, this.file.link)
GROUP BY primary-focus
SORT date ASC
```

## Connected PARA Elements

### Primary Projects
*Which major projects support these 5-year goals?*
```dataview
LIST
FROM "01-PROJECTS"
WHERE contains(supporting-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
```

### Key Areas
*Which ongoing areas are critical to these goals?*
```dataview
LIST
FROM "02-AREAS"
WHERE contains(strategic-goals, this.file.link) AND !contains(file.folder, "ARCHIVE")
```

## Progress Review
### Current Status
*Where are you in year __ of this 5-year plan?*


### Major Milestones Achieved
- 

### Course Corrections Needed
- 

### Key Lessons Learned
- 