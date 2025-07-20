---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
  - annual-review
  - reflection
  - assessment
related:
  - "[[00-Yearly]]"
review-year: <% moment(tp.file.title).format("YYYY") %>
goal-achievement-rate: ""
key-breakthrough: ""
major-challenge: ""
---
# <% moment(tp.file.title).format("YYYY") %> Annual Review

## Executive Summary
### Year Theme
*What was this year about?*


### Overall Assessment
- **Goal Achievement Rate**: __% (__/__ goals completed)
- **Key Breakthrough**: 
- **Major Challenge Overcome**: 
- **Biggest Learning**: 

## Goal Achievement Analysis

### Life Goals Progress
```dataview
TABLE 
    goal-progress as "Progress This Year",
    key-milestone as "Milestone Reached"
FROM "06-ROUTINES/Life"
WHERE contains(annual-reviews, this.file.link)
```

### Annual Goal Completion
```dataview
TASK
FROM "06-ROUTINES/Yearly"
WHERE contains(file.name, "<% moment(tp.file.title).format("YYYY") %>")
```

### Project Outcomes
```dataview
TABLE 
    tags as "Type",
    choice(contains(tags, "completed"), "✅ Completed", 
      choice(contains(tags, "paused"), "⏸️ Paused", 
      choice(contains(tags, "archived"), "📦 Archived", "🔄 Active"))) as "Status",
    created as "Started"
FROM "01-PROJECTS"
WHERE contains(string(file.frontmatter), "<% moment(tp.file.title).format("YYYY") %>") OR contains(file.path, "<% moment(tp.file.title).format("YYYY") %>")
SORT created DESC
```

## Self-Analysis Questionnaire
*Based on Think and Grow Rich - 28 Key Questions*

### Goal Achievement & Vision
1. **Did I attain the goal I established as my objective for this year?** 
   - [ ] Yes [ ] Partially [ ] No
   - **Details**: 

2. **Did I deliver service of the best possible quality, or could I have improved any part of it?**
   - **Assessment**: 

3. **Did I deliver service in the greatest possible quantity?**
   - **Assessment**: 

### Personal Conduct & Efficiency  
4. **Has my conduct been influenced by personal efficiency?**
   - **Assessment**: 

5. **Have my personal habits been above reproach?** 
   - **Assessment**: 

6. **How much time did I devote to unprofitable effort that could have been better used?**
   - **Assessment**: 

### Financial & Resource Management
7. **How did I manage my finances this year?**
   - **Income Growth**: 
   - **Savings Rate**: 
   - **Investment Progress**: 

8. **What resources did I waste that could have been better allocated?**
   - **Assessment**: 

### Relationships & Social 
9. **How have my relationships evolved this year?**
   - **Family**: 
   - **Professional**: 
   - **Personal**: 

10. **What service did I render that was helpful to others?**
    - **Assessment**: 

### Personal Growth & Learning
11. **What new knowledge or skills did I acquire?**
    - **Professional Skills**: 
    - **Personal Development**: 
    - **Creative Abilities**: 

12. **What are my three most damaging weaknesses? What am I doing to correct them?**
    - **Weakness 1**: 
    - **Weakness 2**: 
    - **Weakness 3**: 

## Historical Context & Legacy Data
### Previous Year Comparison
```dataview
TABLE 
    review-year as "Year",
    goal-achievement-rate as "Goal Rate",
    key-breakthrough as "Key Win",
    major-challenge as "Main Challenge"
FROM "97-ARCHIVES"
WHERE contains(tags, "annual-review")
SORT review-year DESC
LIMIT 5
```

### Multi-Year Patterns
#### Consistent Strengths
*What do you consistently do well year after year?*
- 

#### Recurring Challenges  
*What patterns keep appearing that need addressing?*
- 

#### Evolution Trends
*How have you grown and changed over the years?*
- 

## Detailed Category Assessment

### 🎯 Career & Professional
#### Achievements
- 

#### Challenges
- 

#### Growth Areas
- 

### 💪 Health & Fitness
#### Achievements  
- 

#### Challenges
- 

#### Health Metrics
- **Physical Condition**: 
- **Mental Health**: 
- **Energy Levels**: 

### 💍 Relationships & Personal
#### Achievements
- 

#### Areas for Growth
- 

### 🧠 Learning & Growth
#### New Skills Acquired
- 

#### Knowledge Areas Expanded
- 

#### Certifications/Education
- 

### 🎨 Creative & Passion Projects
#### Creative Outputs
- 

#### Artistic Development
- 

### 💰 Financial & Security
#### Financial Metrics
- **Net Worth Change**: 
- **Savings Rate**: 
- **Investment Performance**: 

#### Financial Discipline
- 

## Fear Assessment & Mental Obstacles
### Current Fears Audit
*What fears held you back this year?*
- 

### Mental Blocks Overcome
- 

### Confidence Areas Gained
- 

### Areas Still Needing Courage
- 

## Lessons Learned & Wisdom Gained

### Top 5 Lessons This Year
1. 
2. 
3. 
4. 
5. 

### Failures That Became Learning
- 

### Unexpected Discoveries
- 

### Mindset Shifts
- 

## Looking Forward

### Momentum to Carry Forward  
*What's working that should continue?*
- 

### Systems to Modify
*What needs adjustment?*
- 

### New Areas to Explore
*What's calling to you for next year?*
- 

### Legacy Impact
*How did this year contribute to your life goals?*
- 

## Integration with Goal System

### Life Goal Progress Assessment
```dataview
LIST
FROM "06-ROUTINES/Life"  
WHERE contains(progress-years, "<% moment(tp.file.title).format("YYYY") %>")
```

### 5-Year Plan Milestone Status
```dataview
LIST
FROM "06-ROUTINES/5-Year Plan"
WHERE contains(milestone-years, "<% moment(tp.file.title).format("YYYY") %>")
```

### Seeds for Next Year
*Based on this year's learnings, what should next year focus on?*

#### Top 3 Priority Areas
1. 
2. 
3. 

#### Habits to Build/Continue
- 

#### Relationships to Nurture
- 

#### Skills to Develop
- 

## Archive References
### Related Annual Reviews
```dataview
LIST
FROM "97-ARCHIVES"
WHERE contains(tags, "annual-review") OR contains(file.name, "Review") OR contains(file.name, "Assessment")
SORT file.name DESC
LIMIT 10
```

### Historical Goal Documents
```dataview  
LIST
FROM "97-ARCHIVES"
WHERE contains(file.name, "Goal") OR contains(file.name, "Plan") OR contains(tags, "planning")
SORT file.name DESC
LIMIT 10
```

---
*Review completed on: <% tp.date.now("YYYY-MM-DD") %>*