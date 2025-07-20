---
created: 2025-07-20
tags:
  - guide
  - documentation
  - workflow
type: Guide
aliases:
  - Simplified Workflow Guide
  - Quick Start Guide
  - System Documentation
---

# 🚀 Simplified Workflow Guide
*Your streamlined Obsidian system - powerful yet simple*

## 📋 Overview

I've created a simplified system that maintains all the power of your complex workflows while being much easier to use daily. Here's what's new:

### 🎯 New Dashboards
1. **[[00-COMMAND-CENTER]]** - Your main visual dashboard
2. **[[00-PROGRESS-TRACKER 1]]** - Long-term progress visualization
3. **[[00-TASK-CENTRAL]]** - All tasks in one beautiful view

### 📝 Simplified Templates
1. **`_daily-simple`** - Streamlined daily notes (80% faster to fill out)
2. **`_weekly-simple`** - Visual weekly reviews with automatic calculations
3. **`_quick-capture`** - Instant note capture for ideas
4. **`_moc-simple`** - Easy MOC creation and maintenance

---

## 🎨 Visual Improvements

### Color Coding System
- 🚀 **Purple** = AI/Career (Monday, Thursday focus)
- 🎬 **Pink** = Ubuntu Creative (Tuesday, Friday focus)
- 🌐 **Blue** = Website Development (Wednesday focus)
- 📋 **Orange** = Review & Planning (Weekends)

### Progress Indicators
- ✅ **Green** = On track / Good progress
- 🟡 **Yellow** = Needs attention / Medium priority
- 🔴 **Red** = Urgent / Behind schedule
- 🔵 **Blue** = Information / Neutral

---

## 🚀 Quick Start Daily Workflow

### Morning (2 minutes)
1. Open **[[00-COMMAND-CENTER]]**
2. Click "Create Today's Note"
3. Fill in your 3 priorities
4. Check the suggested focus domain

### During the Day (10 seconds per update)
- Update hour counts as you work
- Add notes in the quick notes section
- Check off completed tasks

### Evening (3 minutes)
1. Rate your energy and mood (1-10)
2. Write one win and one challenge
3. Add any key learnings
4. Save and close

---

## 📊 Weekly Review Process (10 minutes)

### Every Sunday
1. Open **[[00-COMMAND-CENTER]]**
2. Click "Weekly Review"
3. The template auto-calculates:
   - Daily averages
   - Domain balance
   - Total productive hours
4. Just fill in:
   - Top 3 wins
   - Main challenges
   - Next week's focus
   - Week rating (1-10)

---

## ⚡ Quick Capture Methods

### For Ideas
```
Cmd/Ctrl + N → "quick-" → Enter
Type your idea → Save to 98-QUICK
Process later during weekly review
```

### For Tasks
Add directly to daily note:
- `- [ ] 🔴 Urgent task`
- `- [ ] 🟡 Important task`
- `- [ ] 🟢 Nice to have`

### For Resources
Drag and drop into appropriate folder
Add basic tags, process details later

---

## 📈 Understanding Your Dashboards

### Command Center Features
- **Quick Stats**: Live metrics at a glance
- **Focus Balance**: Visual progress bars
- **Activity Heatmap**: 7-day productivity view
- **Quick Actions**: One-click navigation

### Progress Tracker Features
- **Goal Progress**: Visual percentage bars
- **Monthly Trends**: Productivity graphs
- **Achievement Timeline**: Visual milestone tracking
- **Success Metrics**: Consistency and balance scores

### Task Central Features
- **Priority Matrix**: 4-quadrant task organization
- **Domain Grouping**: Tasks by life area
- **Task Statistics**: Completion rates and trends
- **Quick Templates**: Copy-paste task formats

---

## 🛠️ Customization Tips

### Adjusting Focus Days
In daily template, modify the focus calculation:
```javascript
// Current: Mon/Thu = AI, Tue/Fri = Ubuntu, Wed = Website
// Change to your preference in the template
```

### Adding New Domains
1. Create new folder in 01-PROJECTS or 02-AREAS
2. Create MOC using `_moc-simple` template
3. Add to Command Center's "Quick Domain Access"

### Changing Colors
Find and replace gradient values:
- Purple gradient: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- Pink gradient: `linear-gradient(135deg, #f093fb 0%, #f5576c 100%)`
- Blue gradient: `linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)`

---

## 🔧 Troubleshooting

### Dataview Not Working?
1. Enable Dataview in Community Plugins
2. Turn on JavaScript queries in Dataview settings
3. Refresh/restart Obsidian

### Templates Not Inserting?
1. Set template folder to `99-META/_templates` in Templater settings
2. Assign hotkeys for quick insertion
3. Use Templater (not core Templates plugin)

### Calculations Showing NaN?
- Ensure time values are numbers (not "2h" but just "2")
- Check that daily notes have proper frontmatter
- Initialize values to 0 in templates

---

## 🎯 Best Practices

### Daily Success Tips
1. **Be Consistent**: Even 1 minute daily > sporadic long sessions
2. **Track Honestly**: Real data = real insights
3. **Focus Deeply**: One domain at a time
4. **Celebrate Wins**: Record them to stay motivated

### Weekly Success Tips
1. **Review on Same Day**: Consistency builds habit
2. **Be Brief**: Quality > Quantity in reflections
3. **Plan Realistically**: Better to exceed than fall short
4. **Look for Patterns**: What times/days are most productive?

### System Maintenance
- **Monthly**: Archive completed projects
- **Quarterly**: Review and adjust templates
- **Yearly**: Major system evaluation

---

## 🚦 Migration Path

### From Complex to Simple
1. **Keep Both**: Run parallel for 1 week
2. **Compare**: See which provides better insights
3. **Adjust**: Modify simple templates as needed
4. **Switch**: When comfortable, archive complex versions

### Gradual Adoption
- **Week 1**: Just use Command Center
- **Week 2**: Add simple daily template
- **Week 3**: Try weekly review
- **Week 4**: Full system adoption

---

## 📚 Additional Resources

### Useful Hotkeys to Set
- `Cmd/Ctrl + D`: Create daily note
- `Cmd/Ctrl + W`: Open weekly review
- `Cmd/Ctrl + T`: Open task central
- `Cmd/Ctrl + Q`: Quick capture

### Recommended Plugins
- **Dataview**: Powers all dashboards (Required)
- **Templater**: For templates (Required)
- **Calendar**: Visual date navigation
- **Hotkeys++**: Extended keyboard shortcuts

### Workflow Videos
Consider recording yourself doing:
1. Morning routine (2 min)
2. Weekly review (10 min)
3. Month-end analysis (15 min)

---

## 💡 Remember

> "The best system is the one you actually use."

Your simplified workflow maintains all the power of complex tracking while being sustainable and enjoyable to use daily.

---

*Questions? Check [[99-META/]] for more documentation*
*[[00-COMMAND-CENTER|Back to Command Center]]*