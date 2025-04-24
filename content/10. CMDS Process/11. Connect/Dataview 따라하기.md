```dataview
LIST
FROM ""
WHERE category="index"
```
#### 나만의 도서관 만들기
```dataview
table without id
	"![|60]("+cover_url+")" as cover,
	link(file.link, title) as Title,
	join(list(status,  myRate)) as Status
from #book
```


