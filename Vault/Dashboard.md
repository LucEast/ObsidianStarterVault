---
banner: "![[banner-dashboard.jpg]]"
banner_title: Home
banner_icon: 🏠
tags:
- " #dashboard"
alias: homepage
include_in_navbar: true
navbar_name: Dashboard
---

```dataviewjs
let navbar = [];
let loadingMessage = dv.el("span", "**Loading navigation...**", {attr: {style: "font-size:13px; color:gray"}});

let allPages = dv.pages("#dashboard").sort(page => page.file.folder, "asc");
let filteredPages = allPages.filter(p => 
    p.file.tags.values.includes("#dashboard") && p?.include_in_navbar == true
);

for(let page of filteredPages){
    let navItem = '';
    let navName = 'Untitled';
    let navLink = '';

    if(page.navbar_name === undefined){
        navName = page.file.name;
    } else {
        navName = page.navbar_name;
    }
    navLink = page.file.path;

    // Format the nav  item link
    if(dv.current().file.path === page.file.path){
        navItem = `**[[${navLink}|${navName}]]**`
    } else {
        navItem = `[[${navLink}|${navName}]]`
    }

    navbar.push(navItem)
}

dv.paragraph(navbar.join(' | '))

if(filteredPages.values.length > 0){
    loadingMessage.remove();
}
```
# Dashboard
>[!multi-column]
>>[!blank-container]
>>## 🏠  Navigation
>>[[Concept Board|💡  Concept Board →]]
>>[[Journal Dashboard|📘 Journal →]]
>>[[Learning Dashboard|🎓  Learning →]]
>>[[!Notes Dashboard|🗒️  Notes →]]
>>[[Projects/Projects|📐  Projects →]]
>>[[Personal Dashboard|🔒  Personal →]]
>>[[Resources Dashboard|ℹ️  Resources →]]
>>[[Spaces Dashboard|📦  Spaces →]]
>>[[Work Home|💼 Work Dashboard → ]]
>
>>[!blank-container]
>>## 📐  Projects (`$=dv.pages('"Projects" and #project').length`)
>>```dataviewjs
>>let projectList = [];
>>let projects = dv.pages('"Projects" and #dashboard and !#projects');
>>projects = projects.filter(obj => obj.is_active === true);
>>for(let i=0; i<projects.length; i++){
>>	projectList.push(`[[${projects[i].file.path}|${projects[i].file.path.split('/')[projects[i].file.path.split('/').length-2]} →]]`)
>>}
>>dv.list(projectList)
>>```
>
>> [!blank-container]
>> ## Open Tasks 📅
>> ```dataviewjs
>> dv.taskList(dv.pages('-"Templates" and -"Work" and -#work').file.tasks
>> .where(t => !t.completed && t.status != "-" && !t.text.includes("@frank") &&
>> !t.text.includes("#task")
>> ))
>> ```
### ✏️  Recently Changed
```dataviewjs
function converteTime(time){
	// Convert from ms to minutes
	let convertedTime = ""
	time = time/60000; // time in minutes

	if(time < 60){
		convertedTime = `${Math.ceil(time)} minutes ago`;
	} else if (time < 1440){
		convertedTime = `${Math.ceil(time/60)} hours ago`
	} else {
		convertedTime = `${Math.ceil(time/1440)} days ago`
	}	
	return convertedTime
}

for (let group of dv.pages('!"_data_"').sort(k => k.file.mtime, 'desc').limit(10).groupBy(p => p.page)) {
	dv.table(["Name", "Date Modified", "Mentions", ""], 
		group.rows
			.sort(k => k.file.mtime, 'desc')
			.map(k => [
			k.file.link, 
			converteTime(Date.now()-k.file.mtime),
			k.file.inlinks.length,
			`<small>[[${k.file.path}|View →]]</small>`
			]))}
```

**Stats**
Number of files: `$=dv.pages('!"_data_"').length`
Number of notes: `$=dv.pages('"Notes" and !#dashboard').length`
Number of concepts: `$=dv.pages('"Concept Board" and !#dashboard').length`

---
```dataviewjs
let navbar = [];
let loadingMessage = dv.el("span", "**Loading navigation...**", {attr: {style: "font-size:13px; color:gray"}});

let allPages = dv.pages("#dashboard").sort(page => page.file.folder, "asc");
let filteredPages = allPages.filter(p => 
    p.file.tags.values.includes("#dashboard") && p?.include_in_navbar == true
);

for(let page of filteredPages){
    let navItem = '';
    let navName = 'Untitled';
    let navLink = '';

    if(page.navbar_name === undefined){
        navName = page.file.name;
    } else {
        navName = page.navbar_name;
    }
    navLink = page.file.path;

    // Format the nav  item link
    if(dv.current().file.path === page.file.path){
        navItem = `**[[${navLink}|${navName}]]**`
    } else {
        navItem = `[[${navLink}|${navName}]]`
    }

    navbar.push(navItem)
}

dv.paragraph(navbar.join(' | '))

if(filteredPages.values.length > 0){
    loadingMessage.remove();
}
```
