---
tags:
  - status/todo
  - work
date_created: 
date_modified: 2023-11-09
---

```dataviewjs
let tasks = dv.pages('"Work" or #work').file.tasks
let completedTasks = dv.pages('"Work" or #work').file.tasks.where(t => t.completed)
let incompletedTasks = dv.pages('"Work" or #work').file.tasks.where(t => !t.completed)
let percentCompleted = (completedTasks.length/tasks.length)*100
 
if (tasks.length > 0) {
  dv.el("div", `
 <progress value="${(completedTasks.length/tasks.length)*100}" max="100"></progress>
 <small>${Math.round((completedTasks.length/tasks.length)*100, 0)}% completed (${incompletedTasks.length} tasks remaining)</small>
 `)
}
```


>[!multi-column]
>> [!blank-container]
>> ## Open Tasks 📅
>> ```dataviewjs
>> dv.taskList(dv.pages('"Work" or #work').file.tasks
>> .where(t => !t.completed && t.status != "-" && !t.text.includes("@frank") &&
>> !t.text.includes("#task")
>> ))
>> ```
>
>> [!blank-container]
>> ## This Weeks Tasks 📅
>> ```dataviewjs
>> const today = new Date();
>> const startOfWeek = new Date(today.getFullYear(), today.getMonth(), today.getDate() - today.getDay());
>> const endOfWeek = new Date(today.getFullYear(), today.getMonth(), today.getDate() - today.getDay() + 6);
>> dv.taskList(dv.pages('"Work" or #work').where(p => p.file.ctime >= startOfWeek && p.file.ctime <= endOfWeek).file.tasks)
>> ```

```dataviewjs
const today = new Date();
const startOfWeek = new Date(today.getFullYear(), today.getMonth(), today.getDate() - today.getDay());
const endOfWeek = new Date(today.getFullYear(), today.getMonth(), today.getDate() - today.getDay() + 6);

dv.taskList(dv.pages('"Work" or #work').where(p => p.file.ctime >= startOfWeek && p.file.ctime <= endOfWeek).file.tasks)
  
```

