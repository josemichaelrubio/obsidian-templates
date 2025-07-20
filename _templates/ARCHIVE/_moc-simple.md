---
created: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - MOC
  - index
type: MOC
aliases:
  - <% tp.file.title %> Map
  - <% tp.file.title %> Overview
related:
  - 
---

# <% tp.file.title %>
*Brief description of this domain/area*

## 🎯 Current Focus
> What's the main priority right now?

**Active Goal**: 
**Status**: 🟡 In Progress
**Next Action**: 

---

## 📁 Quick Links

### 📌 Pinned Resources
- [[Important Document 1]]
- [[Key Reference]]
- [[Main Project]]

### 📂 Subfolders
- 📁 **Subfolder 1** - Description
- 📁 **Subfolder 2** - Description  
- 📁 **Archive** - Completed/old items

---

## 🗺️ Content Map

### 🏃 Active Projects
- [[Project 1]] - Status
- [[Project 2]] - Status

### 📚 Resources & References  
- [[Resource 1]]
- [[Resource 2]]

### 💡 Ideas & Future Plans
- Idea 1
- Idea 2

---

## 📊 Quick Stats
- **Total Notes**: `$= dv.pages('"<% tp.file.folder %>"').length`
- **This Week**: `$= dv.pages('"<% tp.file.folder %>"').where(p => p.created >= dv.date("today").minus(dv.duration("7 days"))).length` new notes
- **Tasks**: `$= dv.pages('"<% tp.file.folder %>"').file.tasks.where(t => !t.completed).length` open

---

## 🔗 Related Systems
- [[Related MOC 1]]
- [[Related MOC 2]]
- [[00-COMMAND-CENTER|Command Center]]

---

## 📝 Quick Notes
*Temporary thoughts, reminders, or updates*

- 

---

*Last Updated: <% tp.date.now("YYYY-MM-DD") %>*