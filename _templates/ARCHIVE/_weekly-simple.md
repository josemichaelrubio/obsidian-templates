---
date: <% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>
tags:
  - weekly
  - review
week-rating: 
top-win: 
next-week-focus: 
related:
  - "[[00-Weekly]]"
---

# Week <% moment(tp.file.title, "YYYY-[W]WW").format("WW") %> Review
*<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("MMM D") %> - <% moment(tp.file.title, "YYYY-[W]WW").endOf('week').format("MMM D, YYYY") %>*

<div style="display: flex; justify-content: space-between; padding: 10px; background: #f3f4f6; border-radius: 10px; margin-bottom: 20px;">
<span>[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").subtract(1, 'week').format("YYYY-[W]WW") %>|← Last Week]]</span>
<span>[[06-ROUTINES/Monthly/<% moment(tp.file.title, "YYYY-[W]WW").format("YYYY-MM") %>|📅 <% moment(tp.file.title, "YYYY-[W]WW").format("MMMM YYYY") %>]]</span>
<span>[[06-ROUTINES/Weekly/<% moment(tp.file.title, "YYYY-[W]WW").add(1, 'week').format("YYYY-[W]WW") %>|Next Week →]]</span>
</div>

## 📊 Week at a Glance

```dataviewjs
// Visual week summary
const weekStart = dv.date("<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>");
const days = [];
let totalHours = 0;
let daysTracked = 0;

for (let i = 0; i < 7; i++) {
    const date = weekStart.plus(dv.duration(`${i} days`));
    const dateStr = date.toFormat("yyyy-MM-dd");
    const page = dv.page(`06-ROUTINES/Daily/${dateStr}`);
    
    if (page) {
        const ai = page["ai-hours"] || 0;
        const ubuntu = page["ubuntu-hours"] || 0;
        const website = page["website-hours"] || 0;
        const total = ai + ubuntu + website;
        totalHours += total;
        if (total > 0) daysTracked++;
        
        days.push({
            date: date.toFormat("EEE"),
            hours: total,
            mood: page.mood || "—",
            energy: page.energy || "—"
        });
    } else {
        days.push({
            date: date.toFormat("EEE"),
            hours: 0,
            mood: "—",
            energy: "—"
        });
    }
}

dv.el("div", `
<div style="background: #f9fafb; padding: 20px; border-radius: 10px; margin-bottom: 20px;">
    <div style="display: grid; grid-template-columns: repeat(7, 1fr); gap: 10px; text-align: center;">
        ${days.map(day => `
            <div>
                <div style="font-weight: bold;">${day.date}</div>
                <div style="font-size: 1.5em; margin: 10px 0;">${day.hours}h</div>
                <div style="font-size: 0.8em;">
                    ⚡${day.energy} 😊${day.mood}
                </div>
            </div>
        `).join('')}
    </div>
    <div style="margin-top: 20px; padding-top: 20px; border-top: 1px solid #e5e7eb; text-align: center;">
        <strong>Total Hours: ${totalHours}</strong> | 
        <strong>Days Tracked: ${daysTracked}/7</strong> | 
        <strong>Daily Average: ${(totalHours / 7).toFixed(1)}h</strong>
    </div>
</div>
`);
```

## 🎯 Domain Balance

```dataviewjs
// Calculate domain totals for the week
const weekStart = dv.date("<% moment(tp.file.title, "YYYY-[W]WW").startOf('week').format("YYYY-MM-DD") %>");
let aiTotal = 0, ubuntuTotal = 0, websiteTotal = 0;

for (let i = 0; i < 7; i++) {
    const date = weekStart.plus(dv.duration(`${i} days`));
    const page = dv.page(`06-ROUTINES/Daily/${date.toFormat("yyyy-MM-dd")}`);
    if (page) {
        aiTotal += page["ai-hours"] || 0;
        ubuntuTotal += page["ubuntu-hours"] || 0;
        websiteTotal += page["website-hours"] || 0;
    }
}

const total = aiTotal + ubuntuTotal + websiteTotal;

if (total > 0) {
    dv.el("div", `
<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin-bottom: 20px;">
    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; border-radius: 10px; color: white; text-align: center;">
        <div style="font-size: 1.5em;">🚀</div>
        <div style="font-size: 2em; margin: 10px 0;">${aiTotal}h</div>
        <div>AI Career</div>
    </div>
    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); padding: 20px; border-radius: 10px; color: white; text-align: center;">
        <div style="font-size: 1.5em;">🎬</div>
        <div style="font-size: 2em; margin: 10px 0;">${ubuntuTotal}h</div>
        <div>Ubuntu</div>
    </div>
    <div style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); padding: 20px; border-radius: 10px; color: white; text-align: center;">
        <div style="font-size: 1.5em;">🌐</div>
        <div style="font-size: 2em; margin: 10px 0;">${websiteTotal}h</div>
        <div>Website</div>
    </div>
</div>
    `);
}
```

## 🏆 Week Highlights

### Top 3 Wins
1. **🥇** 
2. **🥈** 
3. **🥉** 

### Challenges Faced
- 

### Key Learnings
- 

---

## 📈 Progress Check

### Career
- **What moved forward**: 
- **Still pending**: 

### Education  
- **Completed**: 
- **Next up**: 

### Personal Projects
- **Ubuntu progress**: 
- **Website updates**: 

---

## 🎯 Next Week Planning

### Week <% moment(tp.file.title, "YYYY-[W]WW").add(1, 'week').format("WW") %> Focus Areas

**Primary Focus**: 

**Top 3 Priorities**:
1. 
2. 
3. 

**Time Allocation Target**:
- 🚀 AI: __ hours
- 🎬 Ubuntu: __ hours
- 🌐 Website: __ hours

---

## 💭 Reflection

**Week Rating**: `/10`

**What worked well**: 

**What to improve**: 

**Grateful for**: 

---

*[[00-Weekly|Weekly Hub]] • [[00-COMMAND-CENTER|Command Center]]*