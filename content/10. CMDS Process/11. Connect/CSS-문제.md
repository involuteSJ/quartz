---
CMDS: Frontend
type:
  - note
tags:
  - "#CSS"
관련 문서:
  - "[[104.02 CSS]]"
category: problem
---

# 태그 선택 연습 문제
**1번**
각 문서와 주석으로 옳지 않은 것은?
1. html - \<\!-- --\>
2. css - //
3. css - /\* \*/
4. javascript - //
5. javascript - /\* \*/

---
**2번**
스타일 적용 방법으로 옳지 않은 것은?
1. 인라인 스타일 - 개별 태그에 style="property:value;" 형태로 지정
2. 내부 스타일 - 일반적으로 body 태그 내에 \<style\> 태그를 사용하여 작성
3. 외부 스타일 - 외부에 별도 .css 파일을 만들어 link 태그를 통해 사용
4. 외부 스타일 - @import 방식을 통해 다른 css 파일 내부에서 사용하며 해당 태그 상단에위치해야 함

---
**3번**
p태그의 색상이 변하는 원인으로 알맞은 것은?
```html
<div>yellow</div>
<div id="div">blue</div>
<div class="div">green</div>
<div name="div">red</div>
<p class="div" name="div">this is black</p>
```
1.
```css
div {
	color: yellow;
}
```
2.
```css
#div {
	color: blue;
}
```
3.
```css
.div {
	color: green;
}
```
4.
```css
div[name="div"] {
	color: red;
}
```

---
**4번**
사용자가 input 태그를 누르고 있는 동안 테두리를 노란색으로 바꾸려고 할 때 올바른 선택자는?
```css
/*1번*/
input:hover {
	border: 1px solid yellow;
}
/*2번*/
input:visited {
	border: 1px solid yellow;
}
/*3번*/
input:focus {
	border: 1px solid yellow;
}
/*4번*/
input:active {
	border: 1px solid yellow;
}
```

---
**5번**
ul 태그 내의 li 선택자 중 짝수번째 선택자만 색상을 파란색으로 바꾸려고 할 때 올바른 선택자는?
```css
/*1번*/
ul>li:nth-child(2n) {
	color: blue;
}
/*2번*/
ul>li:nth-element(2n) {
	color: blue;
}
/*3번*/
ul>li:nth-type(2n) {
	color: blue;
}
/*4번*/
ul>li:nth-of-type(2n+1) {
	color: blue;
}
```

---
**6번**
아래 내용을 적용한 html 파일에서 content1과 content2 사이의 간격을 a, content2과 content3 사이의 간격을 b, content 3과 content 4 사이의 간격을 c라고 할 때 a, b, c의 값을 구하시오 
```html
<head>
	<style>
		#content1 {
			margin: 10px;
			border: 0px;
			padding: 10px;
		}
		#content2 {
			margin: 5px;
			border: 0px;
			padding: 5px;
		}
		#content3 {
			margin: 3px;
			border: 0px;
			padding:3px;
		}
		#content4 {
			margin: 1px;
			border: 0px;
			padding: 1px;
		}
	</style>
</head>
<body>
	<span id="content1">content1</span><span id="content2">content2</span>
	<div id="content3">content3</div>
	<div id="content4">content4</div>
</body>
```
1. a : 30px / b : 26px / c : 8px
2. a : 30px / b : 6px / c : 7px
3. a : 25px / 26px / 8px
4. a : 25px / 6px / 7px

---
**7번**
아래 내용을 적용한 html 파일에서 content1과 content2 사이의 간격을 a, content2과 content3 사이의 간격을 b, content 3과 content 4 사이의 간격을 c라고 할 때 a, b, c의 값을 구하시오 
```html
<head>
	<style>
		#content1 {
			margin: 10px;
			border: 0px;
			padding: 10px;
		}
		#content2 {
			margin: 5px;
			border: 0px;
			padding: 5px;
		}
		#content3 {
			display: inline-block;
			margin: 3px;
			border: 0px;
			padding:3px;
		}
		#content4 {
			margin: 1px;
			border: 0px;
			padding: 1px;
		}
	</style>
</head>
<body>
	<span id="content1">content1</span><span id="content2">content2</span>
	<div id="content3">content3</div>
	<div id="content4">content4</div>
</body>
```
1. a : 30px / b : 16px / c : 8px
2. a : 30px / b : 16px / c : 7px
3. a : 25px / b : 13px / c : 8px
4. a : 25px / b : 13px / c : 7px

---
**8번**
id가 div 인 태그를 flex 레이아웃으로 설정하고, 주축을 세로, 공간이 부족하면 다음줄로 넘기고 주축을 가운데 정렬, 교차축을 space-between으로 설정하시오
```css
#div {
	display: □□□□;
	flex-direction: □□□□;
	flex-wrap: □□□□;
	justify-content: □□□□;
	align-content: □□□□;
}
```

---
**9번**
일반적인 문서 흐름에 따라 배치하고, 다른 위치 속성에 영향을 받지 않는 배치 방법은?
1. static
2. relative
3. fixed
4. absolute

---
**10번**
요소의 배치 기준이 static이 아닌 조상 요소인 배치 방법은?
1. static
2. relative
3. fixed
4. absolute

---
**11번**
요소를 뷰포트 기준으로 특정 위치에 고정시키는 배치 방법은?
1. static
2. relative
3. fixed
4. absolute

---
**12번**
일단 요소를 static하게 배치 후 자신의 원래 위치에서 이동하여 배치하는 방법은?
1. static
2. relative
3. fixed
4. absolute

---
**13번**
다음 중 모바일 설정을 위해 사용할 미디어 쿼리로 올바른 것은?
1. @media (min-width: 769px) { }
2. @media (max-width: 768px) { }
3. @media (minimum-scale: 5) { }
4. @media (maximum-scale: 5) { }
# 답
1. 2번
	- css에는 // 주석이 없음
2. 2번
	- body -> head
3. 3번
	- p태그의 class도 div 이므로 .div 선택자 사용시 초록색으로 변함
4. 4번
	- hover - 마우스를 올리면
	- visited - 한번 이상 방문한 링크
	- focus - 포커스가 되면
	- active - 마우스로 누르고 있는 동안
5. 1번
6. 2번
	- span과 span 사이에 margin 병합이 발생하지 않음 -> a=30
	- span과 block 사이에 margin 병합이 발생하지 않음
	- 근데 span은 상하 margin, padding이 적용되지 않음(실제로는 가지고 있음) -> b=6
	- block과 block 사이에 margin 병합이 발생 -> c=7
7. 1번
	- block과 inline-block / span과 inline-block 사이에 margin 병합이 발생하지 않음
	- + float의 경우 margin 병합이 발생하지 않음
8. 답
	- flex
	- column
	- wrap
	- center
	- space-between
9. 1번
10. 4번
11. 3번
12. 2번
13. 1번
	- 0-480 : 모바일
	- 481-768 : 테블릿
	- 769-1280 : 작은 랩탑
	- 1280- : 데스크톱