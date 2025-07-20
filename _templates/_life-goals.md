---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - life-goals
  - long-term
related:
  - "[[00-Life]]"
goal-type: life
goal-horizon: lifetime
---
# Life Goal: <% tp.file.title %>

## Goal Statement
*What is the ultimate outcome you want to achieve in your lifetime?*


## Why This Matters
*Deep personal significance and impact*


## Success Criteria
*How will you know when you've achieved this life goal?*
- [ ] 
- [ ] 
- [ ] 

## Supporting 5-Year Goals
```dataview
LIST
FROM "06-ROUTINES/5 Year"
WHERE contains(parent-goals, this.file.link)
```

## Related Areas
*Which PARA areas does this connect to?*
- [[02-AREAS/]]

## Progress Tracking
### Current Status
*Where are you now relative to this goal?*


### Key Milestones Achieved
- 

### Next Major Milestone
*What's the next big step?*


## Annual Reviews
```dataview
TABLE 
    goal-progress as "Progress",
    key-milestone as "Key Milestone"
FROM "06-ROUTINES/Yearly"
WHERE contains(parent-goals, this.file.link)
SORT date DESC
LIMIT 5
```