---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - Routine
  - Todo
related:
  - "[[00-Daily]]"
---
# Daily Notes - <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D, YYYY") %>
| Direction    | Date                                                                                                             | Link                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 📅 This Week | <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %> | [[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]] |
| ◀️ Yesterday | <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>                               | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>]]                                |
| ▶️ Tomorrow  | <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>                                    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>]]                                     |
## Todoist
### Tasks
```todoist
filter: "today | overdue"
```
### Completed
Ctrl + P (Command Palette)
%% TCT_TEMPLATED_START <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %> 20:00 %%

%% TCT_TEMPLATED_END <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %> 19:59 %%
## Notes
- 