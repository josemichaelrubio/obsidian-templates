---
tags:
  - quarterly
  - Routine
  - Todo
type: quarterly
related:
  - "[[00-Quarterly]]"
---
# Quarterly Notes

Year: [[06_ROUTINES/Yearly/2000]]

Last Quarter: [[06_ROUTINES/Quarterly/1999-Q4]]

Next Quarter: [[06_ROUTINES/Quarterly/2000-Q2]]

## Quarter in Review

### Main Goals for the Quarter

*   

### Highlights

*   What were the best moments of this quarter?

### Challenges Faced

*   What obstacles did you encounter this quarter?

### Lessons Learned

*   What did you learn this quarter?

## Monthly Tracker

| Month                           | Note                                                                                                                 |
| :------------------------------ | :------------------------------------------------------------------------------------------------------------------- |
| [[06_ROUTINES/Monthly/2000-01]] | Overview of the month, linking to weekly notes within. Consider adding a brief summary after the month is completed. |
| [[06_ROUTINES/Monthly/2000-02]] | Overview of the month, linking to weekly notes within. Consider adding a brief summary after the month is completed. |
| [[06_ROUTINES/Monthly/2000-03]] | Overview of the month, linking to weekly notes within. Consider adding a brief summary after the month is completed. |

| Month                                     |
| :---------------------------------------- |
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
  tableRows += `| ${generateMonthLink(year, monthIndex)} |\n`
}

tR += tableRows;

%>
## Quarterly Tasks

### Work/Studies

- [ ] 

### Personal

- [ ] 

### Projects

- [ ] 

## Notes

*   Any other notes or reflections for the quarter