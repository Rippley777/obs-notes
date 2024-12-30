- Install the **Dataview Plugin** for powerful note querying.
- Create dynamic lists or tables using note metadata. Example:

```dataview
table file.mtime as "Last Modified"
from "Projects"
where contains(tags, "active")
sort file.mtime desc
