---
tags:
  - mentoring
  - tracking
cssclasses:
  - cards
  - table-wide
---

## 🎯 Pages Needing Content

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

## 📊 Progress by Category

```dataview
TABLE WITHOUT ID
  key as "Category",
  "<progress value='" + round(100 - (length(rows) / 5 * 100)) + "' max='100'></progress><br>" + round(100 - (length(rows) / 5 * 100)) + "% completed (" + (5 - length(rows)) + "/5)" as "Progress"
FROM "Mentoring"
WHERE contains(tags, "todo")
GROUP BY file.folder
SORT key
```

## ✅ Completed Pages

```dataviewjs
const completedPages = dv.pages('"Mentoring"')
  .where(p => p.file.name != "TODO Tracker" && (!p.tags || !p.tags.includes("todo")))
  .sort(p => [p.file.folder, p.file.name]);

dv.table(["Page", "Category"],
  completedPages.map(p => [
    "✅ " + p.file.link,
    p.file.folder
  ])
);
```

---

### 📈 Quick Stats

- **Total pages**: `$= dv.pages('"Mentoring"').where(p => p.file.name != "TODO Tracker").length`
- **TODO pages**: `$= dv.pages().where(p => p.tags && p.tags.includes("todo")).length`
- **Completed**: `$= dv.pages('"Mentoring"').where(p => p.file.name != "TODO Tracker" && (!p.tags || !p.tags.includes("todo"))).length`