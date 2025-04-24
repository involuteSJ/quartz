---
<%* let num = tp.file.title.match(/\d+/)?.[0]; -%>
<%* let site = tp.system.suggester(["백준", "프로그래머스", "SWEA"], ["BOJ", "PGM", "SWEA"]) -%>
CMDS: CodingTest
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
Algorithm Site: <% site %>
tags:
  - "#CodingTest"
관련 문서:
  - "[[103.02 Related Problems]]"
문제 링크:
  - https://www.acmicpc.net/problem/<% num %>
category: coding_test
---
<% await tp.file.move("/30. Permanent Notes/" + tp.file.title) %>
# \<% tp.file.title %>

## 문제 분석



## 문제 해결 아이디어


## 코드
```java

```

## 시간 복잡도


## 느낀점