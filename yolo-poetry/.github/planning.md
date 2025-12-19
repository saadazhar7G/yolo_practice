# Feature Planning Instructions

## Planning Phase Principles

### 1. Code Analysis First
- Always examine existing code structure before planning
- Identify relevant files, patterns, and dependencies
- Understand current architecture and conventions

### 2. Difficulty Assessment
After initial analysis, provide difficulty rating:
- **EASY**: Simple changes, isolated scope, clear path forward
- **MEDIUM**: Multiple files, some complexity, moderate dependencies
- **HARD**: Complex logic, architectural changes, significant refactoring

### 3. Interactive Planning Process
- Ask targeted follow-up questions one at a time
- Focus on clarifying requirements, constraints, and preferences
- Don't assume - verify understanding before proceeding

### 4. Step-by-Step Planning
Move through planning incrementally:
1. Understand the feature requirement
2. Analyze impact on existing code
3. Identify affected components
4. Outline high-level approach
5. Break down into concrete steps
6. Confirm plan with user

### 5. Concise Communication
- Keep explanations brief and focused
- Use bullet points for clarity
- Avoid verbose descriptions
- Get to the point quickly

### 6. Planning Output Format

```
## Feature: [Feature Name]
**Difficulty**: [EASY/MEDIUM/HARD]

**Analysis**:
- [Key finding 1]
- [Key finding 2]

**Questions**:
- [Question 1]?
- [Question 2]?

**Proposed Approach**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Files to Modify**:
- `file1.py` - [reason]
- `file2.py` - [reason]
```

## Execution Phase Transition

Once planning is complete and approved:
1. Confirm: "Plan approved. Starting implementation."
2. Switch to execution mode
3. Implement changes step by step
4. Test each step before proceeding
5. Provide brief progress updates

### Execution Guidelines
- Implement one logical unit at a time
- Run tests/validation after each step
- Keep user informed of progress
- Ask for input if uncertainty arises
- Don't rush - methodical is better than fast

## Example Flow

**User**: "Add logging to the application"

**Agent**: 
```
Analyzing codebase...

**Difficulty**: MEDIUM

Found 3 modules without logging. Current structure uses no logging framework.

Questions:
- Which logging level do you need (INFO, DEBUG, WARNING)?
- Console output, file, or both?
- Any specific modules to prioritize?
```

**User**: "INFO level, file output, focus on main module"

**Agent**:
```
Plan:
1. Add logging dependency (poetry add)
2. Create logging config in main module
3. Add INFO-level logs at key points
4. Configure file output to logs/app.log

Proceed with implementation?
```

**User**: "Yes"

**Agent**: "Plan approved. Starting implementation." [begins execution]
