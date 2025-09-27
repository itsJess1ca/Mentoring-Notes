---
tags:
  - mentoring
  - tracking
cssclasses:
  - cards
  - table-wide
---
## ✅ Completed Pages

```dataviewjs
const completedPages = dv.pages()
  .where(p => !["TODO Tracker", "CLAUDE", "README"].includes(p.file.name) && (!p.tags || !p.tags.includes("todo")))
  .sort(p => [p.file.folder, p.file.name]);

dv.table(["Page", "Category"],
  completedPages.map(p => [
    "✅ " + p.file.link,
    p.file.folder
  ])
);
```

---

## 📊 Progress by Category

```dataviewjs
// Get all files by folder (both completed and todo)
const allFilesByFolder = dv.pages()
  .where(p => !["TODO Tracker", "CLAUDE", "README"].includes(p.file.name))
  .groupBy(p => p.file.folder);

// Get todo files by folder
const todoFilesByFolder = dv.pages()
  .where(p => p.tags && p.tags.includes("todo"))
  .groupBy(p => p.file.folder);

// Create progress calculation
const progressData = [];
for (let folderGroup of allFilesByFolder) {
  const folder = folderGroup.key;
  const totalFiles = folderGroup.rows.length;
  const todoGroup = todoFilesByFolder.find(g => g.key === folder);
  const todoFiles = todoGroup ? todoGroup.rows.length : 0;
  const completedFiles = totalFiles - todoFiles;
  const progressPercent = totalFiles > 0 ? Math.round((completedFiles / totalFiles) * 100) : 100;

  progressData.push([
    folder,
    `<progress value='${progressPercent}' max='100'></progress><br>${progressPercent}% completed (${completedFiles}/${totalFiles})`
  ]);
}

dv.table(["Category", "Progress"], progressData.sort());
```

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
---
### 📈 Quick Stats

- **Total pages**: `$= dv.pages('"Mentoring"').where(p => p.file.name != "TODO Tracker").length`
- **TODO pages**: `$= dv.pages().where(p => p.tags && p.tags.includes("todo")).length`
- **Completed**: `$= dv.pages('"Mentoring"').where(p => p.file.name != "TODO Tracker" && (!p.tags || !p.tags.includes("todo"))).length`