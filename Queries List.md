# The List of potential queries for the Related Notes base
This short note lists potential Obsidian Bases queries that you can include use to build your own deterministic note discovery engine. I'll be using "this note" as a convention of the main file the queries below will be returing the results against. In Obsidian Bases, this is normally represented by `this.file` element.

- `file.links.contains(this.file)` - list any files that contain this note in their links (backlinks).
- `file.backlinks.contains(this.file)` - lists all the notes this note links to (outgoing links).
- `file.fullname.contains(this.file.name)` - lists notes that contain this note's name in their filename.
- `file.tags.filter(this.file.tags.contains(value)).length >= 2` - the 2-tag overlap rule. If a note shares at least **2** tags with this note, it shows up in the results
- `this.file.links.length > 1 && file.links.filter(this.file.links.contains(value)).length == this.file.links.length` - lists all the notes that share **all** the outgoing links with this note. Has to be more than 1 link in common. You can set it to a higher number if you actively use links. If a note links to 3 other links, this query returns all the other notes that link **at least** to the same 3 notes.
- `this.aliases != null && list(this.aliases).filter(file.name.contains(value)).length > 0` - lists all the notes that contain this file's aliases in their filenames. Works very well with people, company vocabulary, scientific concepts, etc
- `author != null && list(this.author).filter(author.contains(value)).length > 0` - lists all the documents or articles authored by the same author.
- `project != null && project == this.project` - lists all the notes that belong to the same project.

Take this as a foundation, learn the logic of queries, and mix and match for your case what 'relevant notes' actually mean in your vault.
