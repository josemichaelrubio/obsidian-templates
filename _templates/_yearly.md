---
date: <% moment(tp.file.title, "YYYY").startOf('year').format("YYYY-MM-DD") %>
tags:
  - yearly
  - Routine
  - Todo
related:
  - "[[00-Yearly]]"
---
# Yearly Notes

## Reference

### Current 5-Year Plan

### Last Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").subtract(1, 'years').format("YYYY") %>]]
###  Next Year
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").add(1, 'years').format("YYYY") %>]]

## Yearly Goals & Projects

- [ ] 
## Quarterly Tracker
| Quarter                                   |
| :---------------------------------------- |
<%*
const year = moment(tp.file.title, "YYYY").year();

function generateQuarterLink(quarter) {
    const startDate = moment().year(year).quarter(quarter).startOf('quarter');
    return `[[06_ROUTINES/Quarterly/${startDate.format("YYYY-[Q]Q")}]]`;
}

let tableRows = "";
for (let q = 1; q <= 4; q++) {
    tableRows += `| ${generateQuarterLink(q)} |\n`;
}

tR += tableRows;
%>
## Notes
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
