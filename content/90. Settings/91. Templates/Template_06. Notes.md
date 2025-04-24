---
CMDS: 
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
type:
- note
tags: 
관련 문서: 
category:
---
<% await tp.file.move("/10. Permanent Notes/11. Connect/" + tp.file.title) %>
# <% tp.file.title %>
