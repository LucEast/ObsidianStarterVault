---
document_type: dashboard
tags:
  - dashboard
---

# Journal Entries
Explore your collection of journal entries.

```meta-bind-button
label: + Add work journal
hidden: false
class: ""
tooltip: ""
id: ""
style: default
actions:
  - type: command
    command: quickadd:choice:0e01a20b-5cab-4964-b8c0-0de1752922af

```

**Table of journal entries**
```dataviewjs
for (let group of dv.pages('"Work/OWL-IT/Journal" and !#dashboard').groupBy(p => p.entry)) {
	dv.table(["Entry", "Significant event"], 
		group.rows 
			.sort(k => k.name, 'desc')
			.map(k => [
			k.file.link,
			k['event']
			]))}
```
`$="<small>Number of entries: " + dv.pages('"Work/OWL-IT/Journal/Entries"').length+"</small>"`

```tasks 
done this week
group by done
(path includes Work) OR (tags includes work)
short mode
```


```tasks 
done last week
group by done
(path includes Work) OR (tags includes work)
short mode
```
