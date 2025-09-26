# CLAUDE Configuration & Documentation

This file tracks configurations, commands, and features available for this Obsidian vault using the Minimal theme.

## Vault Purpose & Intent

**Primary Purpose:** Personal knowledge management and mentoring resource hub

**Target Audience:**
- Personal reference for career development and technical growth
- Resource to share with developers I'm mentoring
- Knowledge base for common mentoring scenarios and advice

**Content Strategy:**
- Practical, actionable advice over theoretical concepts
- Real-world examples and strategies
- Structured progression from junior to senior developer topics
- Both technical and soft skill development

**Usage Patterns:**
- Quick reference during mentoring conversations
- Structured guidance for mentees working independently
- Personal reflection and career planning
- Resource sharing with other mentors

## Current Setup

**Vault:** Jess' Notes
**Theme:** Minimal for Obsidian
**Location:** `C:\Users\Jess\Documents\Jess' Notes`

## Active CSS Snippets

### mentoring-tracker.css
Location: `.obsidian/snippets/mentoring-tracker.css`

```css
/* Fix emoji + link line breaks in dataview tables - keep emoji with filename */
.dataview.table-view-table .internal-link {
  white-space: nowrap !important;
  display: inline !important;
}

/* But allow the cell itself to wrap when text is too long */
.dataview.table-view-table td {
  white-space: normal !important;
  word-wrap: break-word;
}

/* Cards layout - keep emoji attached but allow wrapping */
.cards .dataview.table-view-table td:first-child {
  min-width: 210px;
}
```

## Project Structure

```
Mentoring/
├── Career Development/
│   ├── One-on-ones.md (todo)
│   ├── Goal Setting.md (todo)
│   ├── Performance Review Preparation.md (todo)
│   ├── Promotion Roadmaps.md (todo)
│   └── Career Pivoting.md (todo)
├── Technical Growth/
│   ├── Code Review Best Practices.md (todo)
│   ├── Technical Presentations.md (todo)
│   ├── Learning New Technologies.md (todo)
│   ├── Portfolio and GitHub.md (todo)
│   └── Open Source Contribution.md (todo)
├── Workplace Skills/
│   ├── Communication Strategies.md (todo)
│   ├── Meeting Facilitation.md (todo)
│   ├── Feedback Skills.md (todo)
│   ├── Conflict Resolution.md (todo)
│   └── Time Management.md (todo)
├── Industry Knowledge/
│   ├── Company Structures.md (todo)
│   ├── Networking Strategies.md (todo)
│   ├── Conference Participation.md (todo)
│   ├── Side Projects Balance.md (todo)
│   └── Remote Work Best Practices.md (todo)
├── Specific Challenges/
│   ├── Imposter Syndrome.md (todo)
│   ├── Difficult Colleagues.md (todo)
│   ├── Work-Life Balance.md (todo)
│   ├── Burnout Prevention.md (todo)
│   └── Company Transitions.md (todo)
├── Interview Advice/
│   └── General Advice.md (completed)
├── Brag Doc.md (completed)
└── 📋 Mentoring Notes TODO Tracker.md
```

## Minimal Theme Features Available

### Cards
- **CSS Classes:** `cards`, `list-cards`
- **Modifiers:** `table-100`, `table-max`, `table-wide`, `cards-align-bottom`, `cards-cover`
- **Aspect Ratios:** `cards-16-9`, `cards-1-1`, `cards-2-1`, `cards-2-3`
- **Columns:** `cards-cols-1` to `cards-cols-8`

### Progress Bars
- **HTML:** `<progress value="50" max="100"></progress>`
- **Colors:** Automatically use color scheme
- **Dataview Integration:** Compatible with DataviewJS

### Tables
- **CSS Classes:** `table-100`, `table-max`, `table-wide`, `table-nowrap`, `table-wrap`
- **Settings:** Trim Dataview columns, maximum column width

### Images
- **CSS Classes:** `img-grid`, `img-100`, `img-max`, `img-wide`
- **Filters:** `#blend`, `#circle`, `#invert`, `#invertW`, `#outline`
- **Features:** Image grids, block width control

### Block Width
- **Classes:** `table-100`, `table-max`, `table-wide`, `iframe-100`, `iframe-max`, `iframe-wide`

### Checklists
- **Alternate Checkboxes:** `[ ]`, `[/]`, `[x]`, `[-]`, `[>]`, `[<]`, `[?]`, `[!]`, `[*]`, etc.
- **Color Integration:** Uses color scheme

### Code Blocks
- **Color Schemes:** Compatible with syntax highlighting
- **Style Settings:** Customizable via plugin

### Embeds
- **CSS Classes:** `embed-strict`, `embed-underline`
- **Features:** Strict embeds for seamless transclusion

## Tag System

### Core Tags
- `mentoring` - All mentoring-related content
- `todo` - Files that need content completion
- `tracking` - Progress tracking files

### Category Tags
- `career-development` - Career growth topics
- `technical-growth` - Technical skill development
- `workplace-skills` - Professional skills
- `industry-knowledge` - Industry insights
- `specific-challenges` - Common workplace challenges

### Specific Tags
- `interviews`, `salary`, `negotiation`, `coding-challenges`
- `bragdoc`, `self-promotion`, `performance`
- `communication`, `feedback`, `conflict-resolution`
- `networking`, `remote-work`, `work-life-balance`
- `mental-health`, `career-change`

## Dataview Queries

### Current Working Patterns

**TODO Pages:**
```dataviewjs
const todoPages = dv.pages().where(p => p.tags && p.tags.includes("todo"))
  .sort(p => [p.file.folder, p.file.name]);

dv.table(["Page", "Category", "Modified"],
  todoPages.map(p => [
    "📝 " + p.file.link,
    p.file.folder,
    dv.date(p.file.mtime).toFormat("MMM dd")
  ])
);
```

**Progress by Category:**
```dataview
TABLE WITHOUT ID
  key as "Category",
  "<progress value='" + round(100 - (length(rows) / 5 * 100)) + "' max='100'></progress><br>" + round(100 - (length(rows) / 5 * 100)) + "% completed (" + (5 - length(rows)) + "/5)" as "Progress"
FROM "Mentoring"
WHERE contains(tags, "todo")
GROUP BY file.folder
SORT key
```

## Commands to Remember

### Lint/Typecheck
- Check README or search codebase for proper commands
- Common patterns: `npm run lint`, `npm run typecheck`, `ruff`

### Git Workflow
- Always run git status and git diff before committing
- Use descriptive commit messages
- End commits with: 🤖 Generated with [Claude Code](https://claude.ai/code)

## Notes

- All TODO files are tagged with `todo` for easy tracking
- CSS snippet handles emoji + filename display issues
- Progress bars use 5 files per category assumption
- Cards layout active on TODO tracker
- DataviewJS preferred over regular Dataview for complex queries