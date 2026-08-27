# {{date:dddd, DD MMMM}}

```base
filters:
  and:
    - and:
        - todo != NULL
    - or:
        - due == date(this.file.name)
        - file.links.contains(this.file)
        - file.fullname.containsAny(this.file.name)
formulas:
  completion: if(todo == true,"completed","still open")
properties:
  file.name:
    displayName: task description
views:
  - type: table
    name: Tasks related to this day exactly
    groupBy:
      property: formula.completion
      direction: DESC
    order:
      - todo
      - file.name
      - due
      - formula.completion
    sort:
      - property: file.fullname
        direction: ASC
    columnSize:
      file.name: 484
      note.due: 187

```

```base
filters:
  and:
    - or:
        - todo != NULL
    - or:
        - due < date(this.file.name)
    - todo == false
formulas:
  overdue: today() - due
properties:
  file.name:
    displayName: task description
views:
  - type: table
    name: Overdue tasks
    order:
      - todo
      - file.name
      - formula.overdue
      - due
    sort: []
    columnSize:
      file.name: 386
      formula.overdue: 103
      note.due: 183
```

```base
filters:
  and:
    - or:
        - due == date(this.file.name)
        - created == date(this.file.name)
        - published == date(this.file.name)
        - file.name.contains(this.file.name)
    - todo == null
views:
  - type: cards
    name: Related notes
    order:
      - file.name
      - file.backlinks
    cardSize: 450
```
