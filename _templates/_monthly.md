---
date: <% moment(tp.file.title, "YYYY-[W]WW").startOf('month').format("YYYY-MM-DD") %>
tags:
  - monthly
  - Routine
  - Todo
related:
  - "[[00-Monthly]]"
---
# Monthly Notes
## References:
###  This Year: 
[[06-ROUTINES/Yearly/<% moment(tp.file.title, "YYYY").format("YYYY") %>]]
### Last Month: 
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").subtract(1, 'months').format("YYYY-MM") %>]]
### Next Month: 
[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-MM").add(1, 'months').format("YYYY-MM") %>]]
## Monthly Goals
- [ ] 
## Weekly Tracker

| Week |
| :--- |
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

