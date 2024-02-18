
---
address: ['Home: -', 'Work: Company']
birthday: YYYY-MM-DD
date_created: 2024-02-18
date_modified: 2024-02-18
document_type: contact
email: ['sample.contact@email.com']
first_name: Sample
last_name: Contact
phone: ['Mobile: +49 123 45678']
tags: contact
---
# ![[profile-picture-placeholder.jpg | rounded-full | 64x64]] `$=dv.span(dv.current().file.frontmatter.first_name)` `$=dv.span(dv.current().file.frontmatter.last_name)`
```dataviewjs
dv.span("**✉ Email**<br/>")
for(let email of dv.current().file.frontmatter.email){dv.span(`${email}<br>`)}
```

```dataviewjs
dv.span("**📱 Phone**<br/>")
for(let phone of dv.current().file.frontmatter.phone){dv.span(`${phone}<br>`)}
```

**🌐 Websites**


## Details