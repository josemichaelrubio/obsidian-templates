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
child-goals: <%*
// Auto-generate child-goals for yearly notes in this 5-year range
const childTitle = tp.file.title;
const childMatch = childTitle.match(/(\d{4})-(\d{4})/);
if (childMatch) {
    const startYear = parseInt(childMatch[1]);
    const endYear = parseInt(childMatch[2]);
    const yearlyGoals = [];
    for (let year = startYear; year <= endYear; year++) {
        yearlyGoals.push(`"[[06-ROUTINES/Yearly/${year}]]"`);
    }
    tR += `[${yearlyGoals.join(', ')}]`;
} else {
    tR += '[]';
}
%>
---
# 5-Year Plan: <% tp.file.title %>

## References

### Life Goals
[[06-ROUTINES/Life/00-Life Goals]]

### Previous 5-Year
<%*
const prevTitle = tp.file.title;
const prevMatch = prevTitle.match(/(\d{4})-(\d{4})/);
if (prevMatch) {
    const startYear = parseInt(prevMatch[1]);
    const prevStart = startYear - 5;
    const prevEnd = startYear - 1;
    tR += `[[06-ROUTINES/5-Year/${prevStart}-${prevEnd}]]`;
} else {
    tR += '[[06-ROUTINES/5-Year/]]';
}
%>

### Next 5-Year
<%*
const nextTitle = tp.file.title;
const nextMatch = nextTitle.match(/(\d{4})-(\d{4})/);
if (nextMatch) {
    const endYear = parseInt(nextMatch[2]);
    const nextStart = endYear + 1;
    const nextEnd = endYear + 5;
    tR += `[[06-ROUTINES/5-Year/${nextStart}-${nextEnd}]]`;
} else {
    tR += '[[06-ROUTINES/5-Year/]]';
}
%>

## Yearly Breakdown
```dataview
TABLE 
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Goals",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Yearly"
WHERE contains(parent-goals, this.file.link) 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name ASC
```

## Yearly Tracker
| Years this 5-Year |
| :---------------- |
<%*
const trackerTitle = tp.file.title;
const trackerMatch = trackerTitle.match(/(\d{4})-(\d{4})/);
if (trackerMatch) {
    const startYear = parseInt(trackerMatch[1]);
    const endYear = parseInt(trackerMatch[2]);
    for (let year = startYear; year <= endYear; year++) {
        tR += `| [[06-ROUTINES/Yearly/${year}]] |\n`;
    }
} else {
    tR += '| No years found |\n';
}
%>

## 5-Year Theme
*What's the main focus for this 5-year period?*
- 

## Strategic Focus Areas

### 1. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 
**Tasks:**
- [ ] 

### 2. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 
**Tasks:**
- [ ] 

### 3. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 
**Tasks:**
- [ ] 

### 4. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 
**Tasks:**
- [ ] 

### 5. 
**Target Outcome:** 
**Why Important:** 
**Success Metrics:** 
**Tasks:**
- [ ] 

## Big Picture Tasks

### Life Goals:
> [!info]- Life Goals
> ```dataview
> TASK
> FROM "06-ROUTINES/Life"
> WHERE !completed
> SORT priority DESC, text ASC
> ```

## Recent Activity

### Goal Completion Trend of Years in This 5-Year
```dataview
TABLE 
    file.link AS "Year",
    length(filter(file.tasks, (t) => t.completed)) + " / " + length(file.tasks) AS "Tasks",
    choice(length(file.tasks) > 0, 
        round((length(filter(file.tasks, (t) => t.completed)) / length(file.tasks)) * 100, 0) + "%", 
        "No goals") AS "Completion %"
FROM "06-ROUTINES/Yearly"
WHERE contains(parent-goals, this.file.link) 
  AND !contains(file.folder, "ARCHIVE")
SORT file.name ASC
```

## Notes
- 

## 5-Year Review

### Mind Dump
- 

### Highlights
- 

### Challenges Faced
- 

### Lessons Learned
-