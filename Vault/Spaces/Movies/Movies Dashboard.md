---
tags:
  - dashboard
  - mediaDB/tv/series
  - mediaDB/tv/movies
description: list of all movies and series
cssclasses:
  - cards
  - cards-cover
  - cards-2-3
  - table-max
  - narrow-tables
---

[[Games Dashboard|Spaces]] / **[[Movies Dashboard|Movies]]**
# Movies/Series
Collection of movies and series.
Movies/Series watched: `$= dv.pages('"Spaces/Movies/Entries" and !#dashboard').where(page => page.watched ==true).length`
Total number of movies/series: `$= dv.pages('"Spaces/Movies/Entries" and !#dashboard').length`

**Add a new movie**

```meta-bind-button
label: + Add Movie
hidden: false
class: ""
tooltip: ""
id: ""
style: default
actions:
  - type: command
    command: obsidian-media-db-plugin:open-media-db-search-modal-with-movie
```

```meta-bind-button
label: + Add Series
hidden: false
class: ""
tooltip: ""
id: ""
style: default
actions:
  - type: command
    command: obsidian-media-db-plugin:open-media-db-search-modal-with-series
```

**Table of movies**
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
	"by " + director as Director,
	"⭐ " + scoreImdb as "⭐ IMDB",
	rating
from #mediaDB/tv/movies or #mediaDB/tv/series  
where image != null and file.name != "movie template"
```

---
[[Games Dashboard|Spaces]] / **[[Movies Dashboard|Movies]]**