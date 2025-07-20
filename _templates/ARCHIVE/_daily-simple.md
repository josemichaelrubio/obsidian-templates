---
date: <% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD") %>
tags:
  - daily
  - routine
energy: 
mood: 
focus: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🚀 AI" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🎬 Ubuntu" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🌐 Website" : "📋 Review" %>
ai-hours: 0
ubuntu-hours: 0
website-hours: 0
win: 
challenge: 
related:
  - "[[00-Daily]]"
---

# <% moment(tp.file.title, "YYYY-MM-DD").format("dddd, MMMM D") %>

<div style="display: flex; justify-content: space-between; padding: 10px; background: #f3f4f6; border-radius: 10px; margin-bottom: 20px;">
<span>[[<% moment(tp.file.title, "YYYY-MM-DD").subtract(1, 'days').format("YYYY-MM-DD") %>|← Yesterday]]</span>
<span>[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-MM-DD").format("YYYY-[W]WW") %>|📅 Week <% moment(tp.file.title, "YYYY-MM-DD").format("WW") %>]]</span>
<span>[[<% moment(tp.file.title, "YYYY-MM-DD").add(1, 'days').format("YYYY-MM-DD") %>|Tomorrow →]]</span>
</div>

## 🎯 Today's Focus: <% moment(tp.file.title, "YYYY-MM-DD").format("d") == "1" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "4" ? "🚀 AI Career" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "2" || moment(tp.file.title, "YYYY-MM-DD").format("d") == "5" ? "🎬 Ubuntu Creative" : moment(tp.file.title, "YYYY-MM-DD").format("d") == "3" ? "🌐 Website Development" : "📋 Review & Planning" %>

### 🔥 Three Key Priorities
1. 
2. 
3. 

---

## ⏰ Time Tracking
*Just update the numbers as you work*

- **🚀 AI Career**: `0` hours
- **🎬 Ubuntu**: `0` hours  
- **🌐 Website**: `0` hours

---

## 📝 Quick Notes
*Brain dump throughout the day*



---

## 🌟 End of Day

**⚡ Energy**: `/10`
**😊 Mood**: `/10`

**🏆 Today's Win**: 

**🤔 Challenge**: 

**💡 Key Learning**: 

---

## 📋 Tasks
- [ ] 

---

*[[00-Daily|Daily Hub]] • [[00-COMMAND-CENTER|Command Center]]*