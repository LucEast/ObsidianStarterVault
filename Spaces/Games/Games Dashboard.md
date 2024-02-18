---
tags:
  - dashboard
  - mediaDB/game
description: list of all games
cssclasses: []
---

[[Games Dashboard|Spaces]] / **[[Games Dashboard|Games]]**
Games
Collection of Games.
Games played: `$= dv.pages('"Spaces/Games/Entries" and !#dashboard').where(page => page.played ==true).length`
Total number of movies/series: `$= dv.pages('"Spaces/Games/Entries" and !#dashboard').length`

**Add a new game

```meta-bind-button
label: + Add Game
hidden: false
class: ""
tooltip: ""
id: ""
style: default
actions:
  - type: command
    command: obsidian-media-db-plugin:open-media-db-search-modal-with-game
```

**Table of games**
```dataviewjs
for (let group of dv.pages('"Spaces/Books" and !#dashboard').groupBy(p => p.book)) {
	dv.table(["Cover", "Title", "Category", "Status"], 
		group.rows 
			.sort(k => k.file.ctime, 'desc')
			.map(k => [
			("![|100](" + k['cover'] + ")"),
			k.file.link, 
			k['category'],
			k['status']
			]))}
```
```dataview
table without id 
	("![](" + image + ")") as Image,
	file.link as Title,
	string(year) as Year, 
	genres as Genres,
	played as Played,
	onlineRating
from #mediaDB/game 
where image != null and file.name != "game template"
```

---
[[Games Dashboard|Spaces]] / **[[Games Dashboard|Games]]**