
# Complete Guide: Hierarchical Goal System

*Your Life Goals → Daily Actions Automation System*

## What We Built

You now have a **complete hierarchical goal decomposition system** that automatically connects your life aspirations to daily actions. This system replaces manual goal tracking with intelligent automation that shows relevant context at every level.

### System Architecture

```
Life Goals (Lifetime aspirations)
    ↓ automatically feeds into
5-Year Plans (Strategic themes)
    ↓ automatically feeds into  
Yearly Goals (Annual objectives)
    ↓ automatically feeds into
Quarterly Plans (3-month milestones)
    ↓ automatically feeds into
Monthly Plans (Monthly themes & projects)
    ↓ automatically feeds into
Weekly Goals (Weekly priorities)
    ↓ automatically feeds into
Daily Tasks (Daily execution)
```

**Key Innovation**: Each level automatically shows relevant goals from levels above and tracks progress toward levels below through YAML metadata and Dataview queries.

## How to Use the System

### 1. Start at the Top: Life Goals

**Location**: `06-ROUTINES/Life/`  
**Template**: `_life-goals.md`

**When to Use**: Define your 3-7 major lifetime aspirations (like "Win 3 Oscars", "Start successful company")

**How to Use**:
1. Create new file in `06-ROUTINES/Life/` folder
2. Template auto-applies with sections for:
   - Goal statement and why it matters
   - Success criteria checklist
   - Supporting 5-year goals (auto-populated)
   - Progress tracking across years

**Example**:
```yaml
---
goal-type: life
goal-horizon: lifetime
related: ["[[00-Life]]"]
---
# Life Goal: Win Academy Award for Best Screenplay

## Goal Statement
Win an Academy Award for Best Original Screenplay for a feature film I wrote.

## Why This Matters
Recognition of creative achievement and contribution to cinema...
```

### 2. Create Strategic Themes: 5-Year Plans

**Location**: `06-ROUTINES/5-Year Plan/`  
**Template**: `_5-year-enhanced.md`

**When to Use**: Break life goals into 5-year strategic themes

**How to Use**:
1. Create file like `2025-2030.md` 
2. Fill in 3-5 major themes for these 5 years
3. Connect to life goals via YAML metadata

**Key Features**:
- Shows parent life goals automatically
- Year-by-year breakdown table
- PARA integration (connects projects/areas)
- Progress tracking

**YAML Connection**:
```yaml
parent-goals: ["[[Life Goal - Win Academy Award]]"]
child-goals: ["[[2025]]", "[[2026]]", "[[2027]]"]
```

### 3. Set Annual Objectives: Yearly Goals

**Location**: `06-ROUTINES/Yearly/`  
**Template**: `_yearly-enhanced.md`

**When to Use**: Each January or when planning your year

**How to Use**:
1. Create file like `2025.md`
2. Set annual theme and primary focus
3. Break into 6 goal categories
4. Connect to 5-year plan in YAML

**Goal Categories**:
- 🎯 Career & Professional
- 💪 Health & Fitness  
- 💍 Relationships & Personal
- 🧠 Learning & Growth
- 🎨 Creative & Passion Projects
- 💰 Financial & Security

**Smart Features**:
- Quarterly tracker with auto-generated links
- Monthly goal rollup with completion %
- Supporting projects auto-listed
- Key areas integration

### 4. Plan Quarterly Milestones

**Location**: `06-ROUTINES/Quarterly/`  
**Template**: `_quarterly-enhanced.md`

**When to Use**: Every quarter (January, April, July, October)

**How to Use**:
1. Create file like `2025-Q1.md`
2. Set quarterly theme and focus
3. Break annual goals into quarterly milestones
4. Connect to yearly goals in YAML

**Key Features**:
- Shows parent annual/5-year goals
- Monthly tracker with completion rates
- Project focus integration
- Progress tracking mid-quarter

### 5. Focus Monthly: Monthly Plans

**Location**: `06-ROUTINES/Monthly/`  
**Template**: `_monthly-enhanced.md`

**When to Use**: First of each month

**How to Use**:
1. Template auto-applies for files like `2025-07.md`
2. Set monthly theme in `primary-focus` YAML field
3. Break quarterly goals into monthly actions
4. Review weekly breakdown automatically generated

**Critical YAML Field**:
```yaml
primary-focus: "Wedding prep and AWS certification"
```
*This shows up automatically in daily notes*

**Smart Features**:
- Auto-generated weekly tracker
- Project milestone tracking  
- Area maintenance goals
- Habit and routine tracking

### 6. Execute Weekly: Weekly Goals

**Location**: `06-ROUTINES/Weekly/`  
**Template**: `_weekly-enhanced.md`

**When to Use**: Weekly planning (Sunday/Monday)

**How to Use**:
1. Template auto-applies for files like `2025-W30.md`
2. Set weekly goals as checkable tasks
3. Review project focus automatically shown
4. Plan daily priorities in tracker table

**Key Features**:
- Active projects grouped by folder
- Open tasks filtered by due dates
- Goal completion trend analysis
- Recent project activity tracking

**Important**: Weekly goals you add here automatically appear in daily notes as actionable tasks.

### 7. Daily Execution

**Location**: `06-ROUTINES/Daily/`  
**Template**: `_daily-enhanced.md`

**When to Use**: Every day

**Auto-Generated Content**:
- **This Week's Goals**: Shows incomplete tasks from current week
- **This Month's Focus**: Shows monthly theme from YAML
- **Active Projects**: Current project status
- **Outstanding Tasks**: Due today or overdue

**Manual Planning Sections**:
- Top 3 Priorities (aligned with weekly/monthly)
- Project time blocks
- Daily habits checklist
- End of day review

## YAML Metadata System

### Core Schema
Every goal file includes these fields:

```yaml
goal-type: [life|strategic|annual|quarterly|monthly|weekly|daily]
goal-horizon: [lifetime|5-year|1-year|quarterly|1-month|1-week|1-day]
parent-goals: ["[[Parent Goal]]"]      # Links up the hierarchy
child-goals: ["[[Child Goal]]"]        # Links down the hierarchy
primary-focus: "Theme or focus area"   # Shows in lower levels
key-projects: ["[[Project A]]"]        # PARA integration
goal-progress: "Status description"    # Progress tracking
```

### How Connections Work

**Upward Connection** (Child → Parent):
```yaml
# In 2025.md (yearly file)
parent-goals: ["[[2025-2030]]", "[[Life Goal - Win Academy Award]]"]
```

**Downward Connection** (Parent → Child):
```yaml
# In 2025-2030.md (5-year file)  
child-goals: ["[[2025]]", "[[2026]]", "[[2027]]"]
```

**Dataview Magic**: Templates automatically query these connections:
```dataview
# Shows parent goals automatically
LIST FROM "06-ROUTINES/5-Year Plan" 
WHERE contains(child-goals, this.file.link)
```

## PARA System Integration

### Projects Connect to Goals
```yaml
# In project frontmatter
supporting-goals: ["[[2025]]", "[[Life Goal - Win Academy Award]]"]

# In goal frontmatter
key-projects: ["[[00-UBUNTU]]", "[[00-WEBSITE]]"]
```

### Areas Connect to Strategy
```yaml
# In area frontmatter  
strategic-goals: ["[[2025-2030]]"]

# In goal frontmatter
related-areas: ["[[00-Career]]", "[[00-Screenwriting]]"]
```

## Annual Review Integration

### Historical Continuity
Your `_annual-review.md` template connects to archived reviews:

**What It Does**:
- 28-question self-analysis (from Think and Grow Rich)
- Goal achievement analysis with completion rates
- Project outcomes tracking
- Multi-year pattern recognition
- Integration with historical reviews in 97-ARCHIVES

**When to Use**: End of each year for comprehensive reflection

## Workflow Recommendations

### Weekly Workflow
1. **Sunday Planning**: Review weekly template, set weekly goals
2. **Daily Check-in**: Review daily template goals context each morning  
3. **Friday Review**: Complete weekly review sections, plan next week

### Monthly Workflow  
1. **Month Start**: Set `primary-focus` in monthly file
2. **Mid-Month**: Review progress via monthly queries
3. **Month End**: Complete monthly review, carry forward goals

### Quarterly Workflow
1. **Quarter Start**: Break annual goals into quarterly milestones
2. **Mid-Quarter**: Review progress and course-correct
3. **Quarter End**: Assess goal achievement, plan next quarter

### Annual Workflow
1. **Year Start**: Connect yearly goals to 5-year plan
2. **Mid-Year**: Review progress via yearly template
3. **Year End**: Complete comprehensive annual review

## Advanced Features

### Automatic Archive Filtering
All queries exclude ARCHIVE folders:
```dataview
WHERE !contains(file.folder, "ARCHIVE")
```
*Keeps historical data separate from active planning*

### Smart Task Display  
Templates show actual tasks, not just links:
```dataview
TASK FROM "06-ROUTINES/Weekly"
WHERE contains(file.name, "2025-W30")
WHERE !completed
```

### Project Activity Tracking
Visual indicators for project momentum:
```dataview
choice(file.mtime > date(today) - dur(7 days), "🔥 This Week", 
  choice(file.mtime > date(today) - dur(30 days), "📅 Recent", "💤 Older"))
```

### Goal Completion Analytics
Automatic percentage tracking:
```dataview
round((length(file.tasks.completed) / length(file.tasks)) * 100, 0) + "%"
```

## Troubleshooting

### Common Issues

**Goals not showing up in daily notes**:
- Check YAML connections in parent files
- Ensure `parent-goals`/`child-goals` arrays are populated
- Verify file names match exactly (case-sensitive)

**Archive items appearing in queries**:
- All queries should include `!contains(file.folder, "ARCHIVE")`
- Move completed items to ARCHIVE folders

**Broken template links**:
- Use consistent naming: `YYYY.md`, `YYYY-MM.md`, `YYYY-WXX.md`  
- Check Templater folder configuration matches enhanced templates

### Maintenance Tasks

**Monthly**:
- Review goal cross-references for accuracy
- Update project supporting-goals connections
- Clean up completed tasks

**Quarterly**:
- Audit hierarchy completeness  
- Archive completed projects
- Update 5-year plan progress

**Annually**:
- Complete comprehensive annual review
- Update life goals if needed
- Archive old planning files

## System Benefits

### Automated Context
- Daily notes show relevant weekly/monthly context
- No manual copying between levels
- Always see why you're doing something

### Progress Visibility  
- Goal completion rates across all levels
- Project momentum tracking
- Multi-year pattern recognition

### Systematic Planning
- Built-in review cycles at appropriate intervals
- Structured templates prevent missed areas
- Historical continuity with archived reviews

### PARA Integration
- Projects and goals work together seamlessly
- Areas connect to strategic objectives
- Resources organized by goal support

## Getting the Most from Your System

### Pro Tips

1. **Start Small**: Don't try to fill everything at once. Start with current year and quarter.

2. **Weekly Discipline**: The system works best with consistent weekly planning and review.

3. **YAML First**: Always fill in YAML metadata - that's what powers the automation.

4. **Project Connection**: Connect every project to supporting goals for full integration.

5. **Review Rhythms**: Stick to the review cycles - they compound over time.

6. **Archive Discipline**: Move completed items to ARCHIVE folders to keep queries clean.

### Success Indicators

**You'll know it's working when**:
- Daily notes show relevant context without manual work
- You can trace daily tasks back to life goals
- Weekly planning connects to monthly themes
- Annual reviews show clear progress patterns
- Projects automatically support strategic goals

---

*This system replaces manual goal tracking with intelligent automation. Your life goals now automatically cascade to daily actions, and your daily work visibly contributes to lifetime aspirations.*

**Created**: 2025-07-20  
**System Status**: Fully Operational  
**Templates**: 8 Enhanced Templates + Historical Integration  
**Automation**: Complete YAML + Dataview Integration