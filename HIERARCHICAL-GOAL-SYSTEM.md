# Hierarchical Goal Decomposition System

This document explains the goal hierarchy system implemented in your Obsidian vault.

## System Overview

```
Life Goals → 5-Year Plans → Yearly Goals → Quarterly Goals → Monthly Goals → Weekly Goals → Daily Tasks
```

Each level automatically references and feeds into the next, creating a seamless goal decomposition from lifetime aspirations down to daily actions.

## Template Structure & YAML Schema

### Core YAML Fields for Goal Tracking
All goal templates include these standardized fields:

```yaml
goal-type: [life|strategic|annual|quarterly|monthly|weekly|daily]
goal-horizon: [lifetime|5-year|1-year|quarterly|1-month|1-week|1-day]
parent-goals: [list of links to higher-level goals]
child-goals: [list of links to lower-level goals]
primary-focus: "Main theme or area"
key-projects: [list of supporting project links]
goal-progress: "Status description"
completion-status: "Current state"
```

### Template Hierarchy

#### 1. Life Goals Template (`_life-goals.md`)
- **Purpose**: Lifetime aspirations and ultimate outcomes
- **Horizon**: Lifetime
- **Key Features**: 
  - Success criteria definition
  - Connection to supporting 5-year plans
  - Annual progress reviews
  - PARA area connections

#### 2. 5-Year Plan Template (`_5-year-enhanced.md`)  
- **Purpose**: Strategic planning and major life themes
- **Horizon**: 5 years
- **Key Features**:
  - 3-5 strategic focus areas
  - Year-by-year breakdown
  - Project and area integration
  - Progress tracking

#### 3. Yearly Plan Template (`_yearly-enhanced.md`)
- **Purpose**: Annual objectives and themes  
- **Horizon**: 1 year
- **Key Features**:
  - Annual theme setting
  - Goal categories (Career, Health, Relationships, etc.)
  - Quarterly tracking
  - Monthly goal rollup
  - Areas and habits integration

#### 4. Monthly Plan Template (`_monthly-enhanced.md`)
- **Purpose**: Monthly focus and project milestones
- **Horizon**: 1 month  
- **Key Features**:
  - Monthly theme
  - Goal breakdown by category
  - Weekly tracking
  - Project milestone tracking
  - Area maintenance goals

#### 5. Enhanced Weekly Template (`_weekly-enhanced.md`)
- **Purpose**: Weekly planning and review
- **Horizon**: 1 week
- **Key Features**:
  - Project focus identification
  - Task due tracking
  - Performance trends
  - Project activity monitoring

#### 6. Enhanced Daily Template (`_daily-enhanced.md`)
- **Purpose**: Daily execution and habits
- **Horizon**: 1 day
- **Key Features**:
  - Goal hierarchy context
  - Weekly/monthly goal visibility
  - Priority alignment
  - Habit tracking

## Automated Cross-References

### Upward References (Child → Parent)
Templates automatically show higher-level goals:

```dataview
# Shows parent 5-year goals in yearly template
LIST
FROM "06-ROUTINES/5-Year Plan" 
WHERE contains(child-goals, this.file.link)
```

### Downward References (Parent → Child)  
Templates automatically show supporting lower-level goals:

```dataview  
# Shows supporting quarterly goals in yearly template
LIST
FROM "06-ROUTINES/Quarterly"
WHERE contains(parent-goals, this.file.link)
```

### Cross-Level Integration
Templates show relevant information from multiple levels:

```dataview
# Daily template shows this week's incomplete goals  
LIST
FROM "06-ROUTINES/Weekly"
WHERE contains(file.name, "current-week-format")
FLATTEN file.tasks as tasks
WHERE tasks.text AND !tasks.completed
```

## PARA System Integration

### Projects Connection
Goals connect to active projects through metadata:

```yaml
# In project frontmatter
supporting-goals: ["[[Annual Goal]]", "[[5-Year Plan]]"]

# In goal frontmatter  
key-projects: ["[[Project A]]", "[[Project B]]"]
```

### Areas Integration  
Areas link to strategic goals:

```yaml
# In areas frontmatter
strategic-goals: ["[[5-Year Plan]]", "[[Life Goal]]"]

# In goal frontmatter
related-areas: ["[[Career Area]]", "[[Health Area]]"]
```

## Implementation Workflow

### Setting Up the Hierarchy

1. **Define Life Goals**: Start with 3-7 major life aspirations
2. **Create 5-Year Plans**: Break life goals into 5-year strategic themes  
3. **Set Annual Goals**: Derive yearly objectives from 5-year plans
4. **Plan Quarters**: Break annual goals into quarterly milestones
5. **Set Monthly Focus**: Identify monthly themes and project milestones
6. **Weekly Planning**: Align weekly goals with monthly themes
7. **Daily Execution**: Connect daily priorities to weekly goals

### Maintaining the System

1. **Daily**: Check hierarchy context, set aligned priorities
2. **Weekly**: Review goal progress, plan next week
3. **Monthly**: Assess goal completion, adjust focus areas  
4. **Quarterly**: Evaluate annual progress, course-correct
5. **Yearly**: Assess life goal progress, set new annual themes
6. **5-Yearly**: Major life assessment and strategic pivots

## Query Examples

### Goal Completion Tracking
```dataview
TABLE 
    goal-progress as "Progress",
    completion-status as "Status", 
    length(child-goals) as "Supporting Goals"
FROM "06-ROUTINES"
WHERE goal-type
SORT goal-horizon DESC
```

### Cross-Level Goal Alignment  
```dataview
TABLE
    file.link as "Goal",
    goal-type as "Level",
    parent-goals as "Supports",
    child-goals as "Supported By"
FROM "06-ROUTINES" 
WHERE contains(goal-type, "annual") OR contains(goal-type, "monthly")
```

### Project-Goal Integration
```dataview
TABLE
    supporting-goals as "Supports Goals",
    tags as "Type",
    created as "Started"
FROM "01-PROJECTS"  
WHERE supporting-goals AND !contains(file.folder, "ARCHIVE")
```

## Benefits of This System

1. **Automatic Alignment**: Daily actions visibly connect to life goals
2. **Progress Visibility**: Each level shows progress toward higher-level objectives  
3. **Context Preservation**: Never lose sight of why you're doing something
4. **Systematic Review**: Built-in review cycles at appropriate intervals
5. **PARA Integration**: Goals and projects work together seamlessly
6. **Flexible Structure**: Can add/modify goals at any level without breaking the system

## Troubleshooting

### Common Issues
- **Broken Links**: Use consistent naming conventions for goal files
- **Missing Cross-References**: Ensure `parent-goals` and `child-goals` arrays are populated
- **Query Failures**: Check that YAML frontmatter follows the schema
- **Archive Pollution**: Use `!contains(file.folder, "ARCHIVE")` in all queries

### Maintenance Tasks  
- Monthly: Review and update goal cross-references
- Quarterly: Audit goal hierarchy for completeness
- Annually: Clean up completed goals and archive old plans