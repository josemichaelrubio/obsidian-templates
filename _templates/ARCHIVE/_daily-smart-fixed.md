---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - routine
  - smart-template
  - auto-analysis
energy: 
mood: 
focus-domain: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "AI Career" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "Website Development" : "Review & Planning" %>
ai-hours: 0
ubuntu-hours: 0
website-hours: 0
study-hours: 0
wedding-tasks: 0
achievement: 
challenge: 
tomorrow-priority: 
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

## 🤖 **AI-Generated Daily Strategy**

**Today's Smart Focus:** <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🚀 AI Career Development" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🎬 Ubuntu Creative Work" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🌐 Website Development" : "📋 Review & Planning" %>

**Optimal Time Allocation:**
<% 
const dayNum = moment(tp.file.title, "YYYY-MM-DD").format("d");
const isAIDay = dayNum == "1" || dayNum == "4";
const isUbuntuDay = dayNum == "2" || dayNum == "5"; 
const isWebsiteDay = dayNum == "3";
%>
<% if (isAIDay) { %>
- 🚀 **AI Career Focus**: 2-3 hours (primary domain day)
- 🎬 **Ubuntu Creative**: 30-60 minutes (maintain momentum) 
- 🌐 **Website Development**: 30-60 minutes (steady progress)
<% } else if (isUbuntuDay) { %>
- 🎬 **Ubuntu Creative Focus**: 1.5-2 hours (primary domain day)
- 🚀 **AI Career**: 60-90 minutes (maintain learning)
- 🌐 **Website Development**: 30-60 minutes (steady progress)
<% } else if (isWebsiteDay) { %>
- 🌐 **Website Development Focus**: 2-3 hours (primary domain day)
- 🚀 **AI Career**: 60-90 minutes (maintain learning)
- 🎬 **Ubuntu Creative**: 30-60 minutes (creative flow)
<% } else { %>
- 📋 **Review & Planning**: Equal time across all domains
- 🚀 **AI Career**: 60-90 minutes (light maintenance)
- 🎬 **Ubuntu Creative**: 60-90 minutes (creative restoration)
- 🌐 **Website Development**: 60-90 minutes (technical review)
<% } %>

**Recommended Start Time:** <% isAIDay ? "9:00 AM (peak focus for AI learning)" : isUbuntuDay ? "2:00 PM (creative energy peak)" : isWebsiteDay ? "10:00 AM (technical work optimal)" : "Variable based on energy" %>

---

## 📊 **Yesterday's Performance Check**
```dataview
TABLE 
  ai-hours as "🚀 AI", 
  ubuntu-hours as "🎬 Ubuntu", 
  website-hours as "🌐 Website",
  (ai-hours + ubuntu-hours + website-hours) as "📊 Total",
  choice(energy, energy + "/10", "Not Set") as "⚡ Energy",
  choice(mood, mood + "/10", "Not Set") as "😊 Mood"
FROM "06-ROUTINES/Daily"
WHERE file.name = dateformat(date(today) - dur(1 day), "yyyy-MM-dd")
LIMIT 1
```

---

## 🎯 **Smart Priority Tasks**

### **🚀 AI Career Development** <% isAIDay ? "*PRIMARY FOCUS TODAY*" : "" %>
```dataview
TASK
FROM "02-AREAS/Career" OR "01-PROJECTS"
WHERE contains(tags, "ai-career") OR contains(tags, "ai") OR contains(tags, "ml")
WHERE !completed
SORT priority ASC, due ASC
LIMIT 4
```

**Today's AI Session Goals:**
- [ ] **Learning Block**: Course/tutorial progress (Target: <% isAIDay ? "2+ hours" : "60-90 min" %>)
- [ ] **Practice/Project**: Hands-on coding work
- [ ] **Portfolio Development**: Document or showcase progress
- [ ] **Community Engagement**: Networking or learning from others

### **🎬 Ubuntu Screenplay Development** <% isUbuntuDay ? "*PRIMARY FOCUS TODAY*" : "" %>
```dataview
TASK
FROM "01-PROJECTS/Screenwriting/Ubuntu"
WHERE !completed
SORT priority ASC, due ASC  
LIMIT 4
```

**Today's Creative Session Goals:**
- [ ] **Character Development**: Expand profiles and motivations (Target: <% isUbuntuDay ? "1-2 hours" : "30-60 min" %>)
- [ ] **Story Structure**: Work on plot progression
- [ ] **Ubuntu Theme**: Deepen philosophical elements  
- [ ] **Writing Session**: Actual script/scene development

### **🌐 Website Development** <% isWebsiteDay ? "*PRIMARY FOCUS TODAY*" : "" %>
```dataview
TASK
FROM "01-PROJECTS/josemichaelrubio.com"
WHERE !completed
SORT priority ASC, due ASC
LIMIT 4
```

**Today's Development Goals:**
- [ ] **Technical Work**: Coding/development progress (Target: <% isWebsiteDay ? "2+ hours" : "30-60 min" %>)
- [ ] **Content Creation**: Write/refine site content
- [ ] **Design Refinement**: Visual/UX improvements
- [ ] **Portfolio Integration**: Showcase AI and creative work

### **📚 Maintenance & Supporting Tasks**
```dataview
TASK
FROM "02-AREAS/Grad_School" OR "01-PROJECTS/Wedding" OR "02-AREAS"
WHERE !completed AND !contains(tags, "ai-career") AND !contains(file.path, "Ubuntu") AND !contains(file.path, "josemichaelrubio")
SORT priority ASC, due ASC
LIMIT 3
```

---

## 📈 **Live Progress Tracking**
*Update throughout the day - feeds your dynamic dashboard*

### **Domain Time Investment**
**🚀 AI Career Hours:** _(update as you work)_
**🎬 Ubuntu Creative Hours:** _(update as you work)_  
**🌐 Website Development Hours:** _(update as you work)_
**📚 Study/Admin Hours:** _(grad school, wedding, etc.)_

### **Auto-Calculated Daily Metrics**
- **Total Productive Hours:** `= ai-hours + ubuntu-hours + website-hours + study-hours`
- **Primary Domain Progress:** `= choice(focus-domain = "AI Career", ai-hours, choice(focus-domain = "Ubuntu Creative", ubuntu-hours, choice(focus-domain = "Website Development", website-hours, (ai-hours + ubuntu-hours + website-hours) / 3)))`
- **Daily Goal Achievement:** `= round((ai-hours + ubuntu-hours + website-hours) / 5 * 100)`% (Target: 5+ productive hours)
- **Domain Balance:** AI `= round(ai-hours / (ai-hours + ubuntu-hours + website-hours + 0.1) * 100)`% | Ubuntu `= round(ubuntu-hours / (ai-hours + ubuntu-hours + website-hours + 0.1) * 100)`% | Website `= round(website-hours / (ai-hours + ubuntu-hours + website-hours + 0.1) * 100)`%

---

## 🌟 **Daily Reflection & Intelligence**

### **Energy & Experience Tracking**
**Energy Level (1-10):** _(How energized do you feel overall?)_
**Mood/Motivation (1-10):** _(How positive and motivated are you?)_
**Focus Quality:** `= choice(focus-domain = "AI Career" AND ai-hours > 0, "🎯 On Target", choice(focus-domain = "Ubuntu Creative" AND ubuntu-hours > 0, "🎯 On Target", choice(focus-domain = "Website Development" AND website-hours > 0, "🎯 On Target", "🔄 Mixed Focus")))`

### **Achievement & Challenge Capture** 
**Today's Biggest Win:**
- 

**Challenge Encountered:**
- 

**Breakthrough/Insight:**
- 

**Tomorrow's AI-Suggested Priority:** 
<% 
const tomorrowDay = moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("d");
const tomorrowIsMon = tomorrowDay == "1";
const tomorrowIsTue = tomorrowDay == "2";
const tomorrowIsWed = tomorrowDay == "3";
const tomorrowIsThu = tomorrowDay == "4";
const tomorrowIsFri = tomorrowDay == "5";
%>
<% if (tomorrowIsMon || tomorrowIsThu) { %>
🚀 **AI Career Focus** - Leverage momentum from today's work
<% } else if (tomorrowIsTue || tomorrowIsFri) { %>  
🎬 **Ubuntu Creative Focus** - Channel today's insights into creative work
<% } else if (tomorrowIsWed) { %>
🌐 **Website Development Focus** - Build on today's technical progress  
<% } else { %>
📋 **Review & Integration** - Synthesize this week's cross-domain learnings
<% } %>

---

## 🔮 **Smart Next-Day Preview**

### **Tomorrow's Auto-Generated Plan**
**Date:** <% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("dddd, MMMM D, YYYY") %>
**Suggested Primary Focus:** <% tomorrowIsMon || tomorrowIsThu ? "🚀 AI Career Development" : tomorrowIsTue || tomorrowIsFri ? "🎬 Ubuntu Creative Work" : tomorrowIsWed ? "🌐 Website Development" : "📋 Review & Planning" %>
**Optimal Start Time:** <% tomorrowIsMon || tomorrowIsThu ? "9:00 AM" : tomorrowIsTue || tomorrowIsFri ? "2:00 PM" : tomorrowIsWed ? "10:00 AM" : "Flexible" %>

**Preparation for Tomorrow:**
- [ ] Set up workspace for tomorrow's primary domain
- [ ] Review relevant materials/resources  
- [ ] Clear any obstacles for tomorrow's focus time
- [ ] Set intention for tomorrow's key achievement

---

## 📝 **Notes & Ideas**
*Your original note-taking space - enhanced with context*

**Cross-Domain Connections:** _(How did today's work in different areas inform each other?)_
- 

**Random Thoughts & Ideas:**
- 

**Meeting Notes/Communications:**
- 

**Learning Captures:**
- 

---

## 🔄 **Weekly Context & Integration**
```dataview
TABLE 
  ai-hours as "🚀 AI",
  ubuntu-hours as "🎬 Ubuntu", 
  website-hours as "🌐 Website",
  (ai-hours + ubuntu-hours + website-hours) as "📊 Total",
  focus-domain as "🎯 Focus"
FROM "06-ROUTINES/Daily"
WHERE date >= date(today) - dur(6 days) AND date <= date(today)
SORT date DESC
```

---

*🤖 This smart template adapts to your patterns and feeds your dynamic dashboard*
*Ready to make tomorrow even more productive and aligned!*