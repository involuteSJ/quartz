---
CMDS: Frontend
type:
  - note
tags:
  - "#HTML"
  - "#Tag"
  - "#Form"
관련 문서:
  - "[[104.01 HTML]]"
category: problem
---
## 예상 문제
**1번**
다음 중 빈칸에 들어갈 말로 알맞게 짝지어진 것은?
```html
<!--1번-->
<select □□□□="cars" size="3">
	<!--2번-->
	<option □□□□="bmw" selected>BMW</option>
	<option □□□□="audi">Audi</option>
	<option □□□□="tesla">Tesla</option>
	<option □□□□="ford">Ford</option>
</select>
```
1. name - value
2. name - label
3. value - name
4. value - id

---
**2번**
다음 내용을 작성한 후 Submit 버튼을 클릭 시 시 서버가 받게 될 값은? (password - 1234)
![[Pasted image 20250303151421.png]]
```html
<form action="submit.php" method="POST">
  <input type="text" name="username" placeholder="Enter your name">
  <input type="password" name="pass" placeholder="Enter password">
  <input type="email" name="email" placeholder="Enter email">hb
  <label><input type="checkbox" name="hobby" value="reading"> Reading</label>
  <label><input type="checkbox" name="hobby" value="sports"> Sports</label>
  <label><input type="radio" name="gender" value="male"> Male</label>
  <label><input type="radio" name="gender" value="female"> Female</label>
  <input type="submit" value="Submit">
</form>
```

---
**3번**
a, b, c가 적절하게 짝지어진 것은?

|     |  1  |  2  |  3  |  4  |
|:---:|:---:|:---:|:---:|:---:|
|  a  | 10  | 20  |  <  |  <  |
|  b  | 50  |  <  | 60  | 70  |
|  c  | 80  | 90  | 100 |  ^  |

```html
<table>
	<tr>
		<th></th><th>1</th><th>2</th><th>3</th><th>4</th>
	</tr>
	<tr><!--a-->
		<td>a</td><td>10</td><td □□□□>20</td>
	</tr>
	<tr><!--b--><!--c-->
		<td>b</td><td □□□□>50</td><td>60</td><td □□□□>70</td>
	</tr>
	<tr>
		<td>c</td><td>80</td><td>90</td><td>100</td>
	</tr>
</table>
```
1. a : colspan="2" | b : colspan="1" | c : rowspan="1"
2. a : rowspan="2" | b : rowspan="1" | c : colspan="1"
3. a : colspan="3" | b : colspan="2" | c : rowspan="2"
4. a : rowspan="3" | b : rowspan="2" | c : colspan="2"

---
**4번**
a 태그와 form 태그의 차이점은?

---
**5번**
form 태그의 action과 method의 역할은?

---
**6번**
ol 태그와 ul 태그의 공통점과 차이점은?

---
**7번**
dt, dd, dl 태그의 역할은?
1. dt - 용어와 설명의 목록을 생성 / dd - 설명 목록의 용어를 정의 / dl - 용어에 대한 설명을 정의
2. dt - 설명 목록의 용어를 정의 / dd - 용어와 설명의 목록을 생성 / dl - 용어에 대한 설명을 정의
3. dt - 설명 목록의 용어를 정의 / dd - 용어에 대한 설명을 정의 / dl - 용어와 설명의 목록을 생성
4. dt - 용어와 설명의 목록을 생성 / dd - 용어에 대한 설명을 정의 / dl - 설명 목록의 용어를 정의

---
**8번**
빈칸에 들어갈 말로 알맞은 것은?
```html
<label for="□□□□">user: </label>
<input type="text" id="user" name="username" value="names" />
```
1. text
2. user
3. username
4. names

---
**9번**
다음중 시멘틱 태그가 아닌 것은?
1. header
2. navigation
3. section
4. aside
5. footer
6. article

---
**10번**
다음중 시멘틱 태그의 이름과 역할이 알맞게 짝지어진 것을 모두 고르면?
1. header - 해당 페이지의 제목만 가능하 일반적으로 로고, 메뉴, 검색 창 등과 함께 표시
2. nav - 문서를 연결하는 네비게이션 링크
3. article - 주제별 컨텐츠 영역을 표시하며 일반적으로 내부의 여러 개의 section을 포함
4. section - 실제 컨텐츠의 내용 등록
5. aside - 본문의 내용을 표시
6. footer - 문서 말미에 제작정보, 저작권 등의 정보 표시




## 답
1. name - value
	- select 태그의 name은 서버로 전송될 변수명
	- option 태그의 value는 선택 시 서버로 전송되는 값
	- 서버로 전송되는 값 -> cars = bmw
	- selected 태그 선택 시 해당 태그가 기본 선택 상태로 설정
	- form에서 사용하는 태그들은 name으로 변수명 설정 후 value로 값 지정
2. 답
	- username="홍길동"
	- pass="1234"
	- email="123\@naver.com"
	- hobby=\["reading","sports"\]
	- gender="male"
3. 3) a : colspan="3" | b : colspan="2" | c : rowspan="2"
	- colspan - 가로로 병합 / rowspan - 세로로 병합
	- 이때 병합되는 개수에 자기 자신도 포함
	- 추가로 thead, tbody, tfoot을 이용해서 헤더, 본문, 바닥글을 나눌 수 있음
	- caption 태그를 사용해 테이블 제목 설정 가능 - table 태그 안에 사용
4. 답
	- a
		- 하이퍼링크
		- 페이지 이동 - 내부 혹은 외부로
		- url을 클릭 시 브라우저가 해당 페이지를 요청 (get 방식만 가능)
		- \_self, \_blank로 문서를 여는 창이 현재 창이냐, 새창이냐 선택 가능
		- *ex) 페이지 간 이동, 다운로드 링크*
	- form
		- 사용자 데이터를 서버로 전송
		- get / post 선택 가능
		- *ex) 로그인, 회원가입, 검색 등*
5. action - 요청을 처리할 서버의 url / method - form 데이터 전송 방법 지정(get, post, dialog)
6. 답
	- ol - 순서가 있는 목록 생성 (ordered list)
	- ul - 순서가 없는 목록 생성 (unordered list)
	- 공통점 - 하위 목록으로 li 태그를 가짐
7. 3번
	- dl - 용어와 설명의 목록을 생성 (definition list)
	- dt - 설명 목록의 용어를 정의 (definition term)
	- dd - 용어에 대한 설명을 정의 (definition details)
8. 2번
	- label의 for 속성과 맞추고자 하는 태그의 id 속성이 일치해야 함
9. 2번
	- navigation -> nav
10. 2번, 6번
	- header - 반드시 페이지의 제목일 필요 없음
	- nav - **문서를 연결하는 네비게이션 링크 표시**
	- section - 주제별 컨텐츠 영역을 표시하며 일반적으로 내부에 여러 article 포함
	- article - 실제 컨텐츠의 내용 등록
	- aside - 본문 이외의 내용을 표시
	- footer - **문서 말미에 제작정보, 저작권 등의 정보 표시**