# Copilot Instructions for PM Study Platform

## Project Overview

This is a **project management education platform** delivering interactive HTML-based study guides for PMP/PMBOK exam preparation. The site contains 4 major sections covering PM fundamentals, PMBOK 10 knowledge areas, organizational structures, and process groups—all in Traditional Chinese with pedagogical metaphors (e.g., restaurant operations, mountain climbing, space missions).

**Key Characteristic**: Each guide uses thematic analogies + interactive tabs (metaphor → core concepts → quizzes/flashcards) to make complex PM theory relatable.

## Architecture & Content Structure

### Directory Organization
- **`01-pm-intro/`**: Foundational PM concepts (Project vs Operations, PM evolution from PMBOK v6→v7)
- **`02-PM_Voyage_Guide/`**: High-level concepts (EEF/OPA assets, organizational structures, PM roles)
- **`03pm_process_groups_study_tool/`**: Detailed coverage of 5 process groups (Initiating → Planning → Executing → Monitoring → Closing)
- **`04PMBOK_Interactive_Tutor/`**: Deep-dive into 10 knowledge areas with domain-specific study guides
- **`index.html`**: Master navigation hub linking all sections

### Content Patterns

Each guide follows this tab structure:
```
1. 觀念比喻 (Metaphor Tab)
   - Real-world analogy explaining the PM concept
   - Metaphor stays consistent within a guide
   
2. 核心重點 / 計畫書解剖 (Core Concepts Tab)
   - Flashcard-based interactive cards
   - Flip-card animation reveals answer on click
   - Key terms, definitions, ITTO patterns
   
3. 模擬測驗 / 情境模擬考題 (Quiz Tab)
   - Multiple-choice questions with explanations
   - Tests recall and application
```

## Technical Conventions

### Tech Stack
- **Framework**: Vanilla HTML5 + CSS + JavaScript (NO build process)
- **UI Libraries**: 
  - Tailwind CSS (cdn) for styling
  - React 18 + Babel (cdn) for interactive components in newer guides
  - Chart.js (cdn) for data visualization
  - Font Awesome 6 (cdn) for icons
- **Deployment**: Static GitHub Pages (`/.github/workflows/static.yml`)

### File Naming
- `{TopicName}_{StudyGuide|Interactive_Tutor|Study_Tool|Dojo}.html` (PascalCase for topics)
- Master hub files: `{section_name}.html` 
- Supporting guides: `01Topic.html`, `02Topic.html` (numbered prefixes)

### Code Patterns

**Metaphor System**:
Each guide embeds a central metaphor object:
```javascript
// Example: Project Charter guide uses "Royal Charter" metaphor
const metaphor = {
  sponsor: "國王 (King) - issues charter",
  pm: "船長 (Captain) - receives authorization",
  charter: "特許狀 (Royal Charter) - source of authority"
}
```

**Flip-Card Pattern** (Used universally):
```html
<div class="flip-card" onclick="flipCard(this)">
  <div class="flip-card-inner">
    <div class="flip-card-front">Question/Term</div>
    <div class="flip-card-back">Answer/Definition</div>
  </div>
</div>
<!-- CSS: transform: rotateY(180deg) on hover/click -->
```

**Tab Navigation** (Vanilla JS):
```javascript
function switchTab(tabName) {
  // Hide all tabs
  document.querySelectorAll('[id^="content-"]').forEach(el => el.classList.add('hidden'));
  // Show selected tab
  document.getElementById(`content-${tabName}`).classList.remove('hidden');
  // Update active button styling
}
```

**Quiz Question Object Structure**:
```javascript
const questions = [
  {
    question: "Question text",
    options: [
      { text: "Option A", correct: true },
      { text: "Option B", correct: false }
    ],
    explanation: "Why this answer is correct..."
  }
]
```

## Critical Content Patterns

### PMBOK Framework References
- **10 Knowledge Areas** (not 9): Integration, Scope, Schedule, Cost, Quality, Resource, Communication, Risk, Procurement, Stakeholder
- **5 Process Groups**: Initiating → Planning → Executing → Monitoring & Controlling → Closing
- **ITTO Model**: Inputs → Tools & Techniques → Outputs (referenced in deeper guides)
- **Version Awareness**: Guides distinguish PMBOK v6 (process-heavy) vs v7 (principle-based, value-driven)

### Pedagogical Metaphors (Keep Consistent)
- **Project Charter**: "Royal Charter authorizing a ship captain"
- **Project Management**: "Restaurant operations" or "Film production"  
- **OPA/EEF**: "Mountain climbing equipment" (internal vs external resources)
- **Org Structures** (Functional→Matrix→Projectized): "From borrowed employees → shared authority → independent film crew"

### PMBOK v6 vs v7 Distinction
- **v6**: 5 process groups + 10 knowledge areas + 49 processes (rigid framework)
- **v7**: 12 Principles + 8 Performance Domains + Tailoring concept (flexible, value-focused)
- Guides emphasize this shift from "recipe-like" to "adaptive" PM philosophy

## Development Workflow

### No Build Process
- Edit HTML/CSS/JS directly in files
- Changes deploy immediately via GitHub Pages (`static.yml` watches root)
- Test locally by opening HTML in browser

### Adding New Guides
1. Create `{TopicName}_{GuideType}.html` in appropriate directory
2. Follow tab structure: metaphor → concepts → quiz
3. Include flip-card CSS + flip-card onclick handlers
4. Link from parent hub's navigation (e.g., `PMBOK_Interactive_Tutor.html`)
5. Optionally add entry to `index.html` master nav

### Consistency Checklist
- [ ] Traditional Chinese (zh-TW) throughout
- [ ] Tailwind CDN + Font Awesome CDN linked in `<head>`
- [ ] Language metadata: `<html lang="zh-TW">`
- [ ] Tab animation: `@keyframes fadeIn` with `animate-fade-in` class
- [ ] Metaphor explicitly stated in header or first section
- [ ] Quiz includes `explanation` field for every question
- [ ] "考試記憶點" (exam memory tips) callout included where relevant

## Common AI Tasks

**When updating existing guides**:
- Preserve metaphor consistency—don't invent new analogies
- Keep flip-card onClick logic unchanged
- Maintain tab structure (don't reorder tabs)
- Update quiz explanations, not question logic

**When creating new guides**:
- Start with metaphor first (how does PMBOK concept map to real life?)
- Build flashcards from PMBOK official definitions
- Generate quiz questions testing concept application, not memorization
- Always include "為什麼？" (Why?) in explanations

**When fixing content errors**:
- Distinguish PMBOK v6 vs v7 if relevant
- Cross-check against official PMBOK terminology
- Preserve exam-prep voice (practical, memory-aid focused)

## Key Files for Reference

- [PM Intro Hub](01-pm-intro/pm-intro.html) - Entry point for newcomers; shows Project vs Ops distinction
- [PMBOK Interactive Tutor](04PMBOK_Interactive_Tutor/PMBOK_Interactive_Tutor.html) - Dashboard of 10 knowledge areas with metaphor-driven intro
- [Project Charter Guide](04PMBOK_Interactive_Tutor/01Project_Integration_Management_Study_Guide/01Project_Charter_Interactive_Guide.html) - Exemplar of flip-card + metaphor pattern
- [Org Structures Guide](02-PM_Voyage_Guide/03PM_Organizational_Structures_Study_Guide.html) - Shows React-based interactive guide pattern
