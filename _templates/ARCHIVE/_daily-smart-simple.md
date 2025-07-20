---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - routine
  - smart-template
energy: 
mood: 
ai-hours: 0
ubuntu-hours: 0
website-hours: 0
study-hours: 0
achievement: 
challenge: 
related:
  - "[[00-Daily]]"
---

# Daily Notes - <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D, YYYY") %>

## 🗓️ Navigation
| Direction    | Date                                                                                                             | Link                                                                                                                                    |
| ------------ | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| 📅 This Week | <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %> | [[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY") %>-W<% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]] |
| ◀️ Yesterday | <% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>                               | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>]]                                |
| ▶️ Tomorrow  | <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>                                    | [[06-ROUTINES/Daily/<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>]]                                     |

---

## 🤖 **Smart Daily Strategy**

**Today's Focus:** <% moment(tp.file.title, "YYYY-MM-DD").format("dddd") %>

**Recommended Schedule:**
- **Morning (9-11 AM):** <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" ? "🚀 AI Career Learning (Primary)" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" ? "🚀 AI Career Learning" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🌐 Website Development (Primary)" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🚀 AI Career Learning (Primary)" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🚀 AI Career Learning" : "📋 Weekly Planning" %>

- **Afternoon (2-4 PM):** <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" ? "🎬 Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" ? "🎬 Ubuntu Creative (Primary)" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🚀 AI Career Learning" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🎬 Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🎬 Ubuntu Creative (Primary)" : "🔄 Review & Reflect" %>

- **Evening (6-8 PM):** <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" ? "🌐 Website Development" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" ? "🌐 Website Development" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🎬 Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🌐 Website Development" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🌐 Website Development" : "📚 Study/Admin" %>

---

## 📊 **Yesterday's Performance**
```dataview
TABLE 
  ai-hours as "🚀 AI", 
  ubuntu-hours as "🎬 Ubuntu", 
  website-hours as "🌐 Website",
  (ai-hours + ubuntu-hours + website-hours) as "📊 Total",
  choice(energy, energy + "/10", "❓") as "⚡ Energy"
FROM "06-ROUTINES/Daily"
WHERE file.name = dateformat(date(today) - dur(1 day), "yyyy-MM-dd")
LIMIT 1
```

---

## 🎯 **Priority Tasks Today**

### 🚀 **AI Career Development**
```dataview
TASK
FROM "02-AREAS/Career" OR "01-PROJECTS"
WHERE contains(tags, "ai-career") OR contains(tags, "ai") OR contains(tags, "ml")
WHERE !completed
SORT priority ASC, due ASC
LIMIT 3
```

**Focus Areas:**
- [ ] Learning/Course Progress: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "2+ hours (Primary Day)" : "1 hour" %>
- [ ] Hands-on Practice/Coding
- [ ] Portfolio/Project Development
- [ ] AI Community Engagement

### 🎬 **Ubuntu Screenplay**
```dataview
TASK
FROM "01-PROJECTS/Screenwriting/Ubuntu"
WHERE !completed
SORT priority ASC, due ASC
LIMIT 3
```

**Creative Goals:**
- [ ] Character Development: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "1.5+ hours (Primary Day)" : "45 min" %>
- [ ] Story Structure Work
- [ ] Ubuntu Philosophy Research
- [ ] Actual Writing/Scene Work

### 🌐 **Website Development**
```dataview
TASK
FROM "01-PROJECTS/josemichaelrubio.com"
WHERE !completed
SORT priority ASC, due ASC
LIMIT 3
```

**Development Tasks:**
- [ ] Technical/Coding Work: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "2+ hours (Primary Day)" : "45 min" %>
- [ ] Content Creation
- [ ] Design/UX Improvements
- [ ] Portfolio Integration

### 📚 **Supporting Tasks**
```dataview
TASK
FROM "02-AREAS/Grad_School" OR "01-PROJECTS/Wedding"
WHERE !completed
SORT priority ASC, due ASC
LIMIT 2
```

---

## 📈 **Live Progress Tracking**

### **Domain Hours** *(Update throughout the day)*
- **🚀 AI Career:** _____ hours
- **🎬 Ubuntu Creative:** _____ hours  
- **🌐 Website Development:** _____ hours
- **📚 Study/Admin:** _____ hours

### **Daily Metrics** *(Auto-calculated in dashboard)*
- **Total Productive Hours:** `= ai-hours + ubuntu-hours + website-hours + study-hours`
- **Goal Progress:** `= round((ai-hours + ubuntu-hours + website-hours) / 5 * 100)`% (Target: 5+ hours)
- **Primary Domain Success:** <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "AI Career focus achieved if 2+ hours" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "Ubuntu focus achieved if 1.5+ hours" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "Website focus achieved if 2+ hours" : "Balanced day achieved if 4+ total hours" %>

---

## 🌟 **Daily Reflection**

### **Energy & Mood**
- **Energy Level (1-10):** _____
- **Mood/Motivation (1-10):** _____
- **Focus Quality:** _____

### **Wins & Challenges**
**Today's Biggest Achievement:**
- 

**Challenge Faced:**
- 

**Key Insight/Learning:**
- 

### **Tomorrow's Priority**
**Suggested Focus:** <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "1" ? "🚀 AI Career Development - Start week strong" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "2" ? "🎬 Ubuntu Creative - Tuesday creative flow" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "3" ? "🌐 Website Development - Midweek technical focus" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "4" ? "🚀 AI Career Development - Thursday momentum" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "5" ? "🎬 Ubuntu Creative - Friday creative energy" : "📋 Weekend planning and review" %>

---

## 📝 **Notes & Ideas**

### **Cross-Domain Connections**
*(How did today's work in different areas connect?)*
- 

### **Random Thoughts**
- 

### **Meeting Notes**
- 

### **Learning Captures**
- 

---

## 🔄 **This Week's Context**
```dataview
TABLE 
  file.link as "Day",
  ai-hours as "🚀 AI",
  ubuntu-hours as "🎬 Ubuntu", 
  website-hours as "🌐 Website",
  (ai-hours + ubuntu-hours + website-hours) as "📊 Total"
FROM "06-ROUTINES/Daily"
WHERE date >= date(today) - dur(6 days) AND date <= date(today)
SORT date DESC
```

**Week Progress:**
- **🚀 AI Career Total:** `= sum(extract(this.ai-hours, 0)) + sum(extract(this.ai-hours, 1)) + sum(extract(this.ai-hours, 2)) + sum(extract(this.ai-hours, 3)) + sum(extract(this.ai-hours, 4)) + sum(extract(this.ai-hours, 5)) + sum(extract(this.ai-hours, 6))` hours
- **🎬 Ubuntu Total:** `= sum(extract(this.ubuntu-hours, 0)) + sum(extract(this.ubuntu-hours, 1)) + sum(extract(this.ubuntu-hours, 2)) + sum(extract(this.ubuntu-hours, 3)) + sum(extract(this.ubuntu-hours, 4)) + sum(extract(this.ubuntu-hours, 5)) + sum(extract(this.ubuntu-hours, 6))` hours
- **🌐 Website Total:** `= sum(extract(this.website-hours, 0)) + sum(extract(this.website-hours, 1)) + sum(extract(this.website-hours, 2)) + sum(extract(this.website-hours, 3)) + sum(extract(this.website-hours, 4)) + sum(extract(this.website-hours, 5)) + sum(extract(this.website-hours, 6))` hours

---

*🤖 Smart template feeds your dynamic dashboard with live data*  
*Tomorrow: <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("dddd") %> will focus on <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "4" ? "AI Career" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "5" ? "Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d") == "3" ? "Website Development" : "Planning & Review" %>*