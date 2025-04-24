(#) 개수만큼 헤딩
(---) 줄 만들기
(\*\*) Bold (단축키 : ctrl + B)
(\~\~) 취소선
(\*) 기울이기

---
#### Unordered List
- \- 기호를 통해 작성
- ctrl + shift를 통해 위, 아래로 이동 가능

---
#### Task Box
\- \[x\] 를 통해 task box 생성 가능
- ctrl + L 을 이용하여 task box 생성 가능

---
#### Code Block
\` 기호를 통해 inline code 생성 가능
`인라인 코드`

\` 기호를 3번 사용하면 Code Block 생성

```java
public hello {
	public static void main(String[] args) {
		System.out.println("Hello");
	}
}
```

code 혹은 복사해야 편한 내용들은 code block을 활용해서 복사를 하면 편하게 사용 가능

---
#### External Link
\[표기할 링크\]\(실제 링크\)
이미지나 영상을 참조시킬때는 대괄호 앞에 ! 기호를 붙여서 임베딩 가능

#### Internal Link
\[\[내부 파일에 접근할 때 사용\]\] 
- 나중에 정리가 필요한 내용은 제목만 만들어 놓은 뒤, 나중에 문서 편집 가능
- 파일끼리 관계를 맺을 때 사용

---
#### Footnote
\[\^내용] 기호를 통해 각주 추가 가능

---
### Quotes and Callouts

#### Blockquote
\> 기호를 통해 quotes 생성 가능

> 안녕하세요
> 반갑습니다

\[\!내용\] 기호를 통해 Callouts 생성 가능

> [!note]
>오늘 날씨가 좋네요
>하늘이 맑아요

>[!quote]
>누군가 이런 말을 했다
>>다른 내용
>>두번째 줄


---
#### Tables
\| number \| name \|
\| \-\-\-\-\-\-\-\- \| \-\-\-\-\-\- \|
\| 내용 1 \| 내용 2 \|

| number | name |
| ------ | ---- |
| 내용 1   | 내용 2 |

---

### Mathematical Equations (LaTeX)
#### Inline Math
\$ 와 \$ 사이에 내용 넣을 경우 수학적 기호로 표기

$E = mc^2$

#### Display Math
\$\$ 와 \$\$ 내부에 사용하는 경우 블럭 형태로 사용 가능

$$
\frac{\partial f}{ \partial x} = 2\sqrt{a}x
$$

---
#### Highlight
\=\= 와 \=\= 사이에 넣은 내용은 하이라이트 기능 적용
==hello==
