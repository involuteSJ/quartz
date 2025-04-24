---
CMDS: Java
type:
  - note
tags:
  - "#SAX"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
category: content
---
## SAX - Simple API for XML
- #### XML 파싱
	- 파싱
		- 문서에서 필요한 정보를 얻기 위해 태그를 구별하고 내용을 추출
		- SAX parse - 문서를 읽으면서 이벤트 기반으로 처리
		- DOM parser - 문서를 읽고 문서 구조를 자료구조에 저장하여 탐색
	- SAX - 빠르고 한번에 처리, 다양한 탐색의 어려움
	- DOM - 다양한 탐색, 느리고 큰 문서 처리의 어려움
- #### 동작 방식
	- 문서를 읽다가 발생하는 이벤트 기반으로 문서 처리
	- ![[00. Inbox/03. Excalidraw/sax|sax]]
- #### DTO \(Data Transfer Object\)
	- 계층간 데이터 교환을 위해 사용되는 객체
	- 필요한 데이터만 캡슐화
	- ##### 작성 방법
		- 필요한 속성을 private하게 선언
		- Getter / Setter로 encapsulation 처리
		- Default constructor
		- 필요에 따라 toString(), hashCode(), equals() 재정의
		- 데이터 변환 로직
- #### VO \(Value Object\)
	- 주로 도메인 모델의 값 자체를 표현하기 위해 사용. 필요에 따라 비즈니스 로직 포함
	- 생성 시점에 설정된 값을 변경할 수 없는 불변 객체
	- 동일한 값이면 서로 같다
- #### Record 클래스
	- 불변 객체를 간단하고 명료하게 정의 가능
	- DTO, VO를 구현할 때 유용
	- 특징
		- 불변성 - 객체 생성 이후 변경 불가 : 모든 필드가 final
		- 간결성 - 변수 선언 외에 필요한 코드는 컴파일 시점에 자동 생성
	- 제한사항
		- record를 묵시적으로 상속받았기 때문에 다른 클래스 상속 불가
- #### Handler
```java
public interface BoxOfficeParser {
	public abstract List<BoxOffice> getBoxOffice(InputStream resource);
}

public class BoxOfficeSaxParser extends DefaultHandler implements BoxOfficeParser {
	public List<BoxOffice> getBoxOffice(InputStream resource) {
		try {
			SAXParserFactory factory = SAXParserFactory.newInstance();
			SAXParser parser = factory.newSAXParser();
			parser.parse(resource, this);
		} catch(IOException | SAXException | ParserConfigurationException e) {
			e.printStackTrace();
		}
		return list;
	}
}

@Override
public void startDocument() throws SAXException {
	System.out.println("문서 시작");
}

@Override
public void characters(char[] ch, int start, int length) throws SAXException {
	 this.content = String.valueOf(ch, start, length);
 }

@Override
public void endElement(String uri, String localName, String qName) throws SAXException {
	if(qName.equals("rank")) {
		this.rank = Integer.parseInt(content);
	} else if(qName.equals("movieNm")) {
		this.movieNm = content;
	} else if(qName.equals("openDt")) {
		this.openDt = content;
	} else if(qName.equals("audiAcc")) {
		this.audiAcc = Integer.parseInt(content);
	} else if(qName.equals("dailyBoxOffice")) {
		this.dailyBoxOffice = new BoxOffice(rank, movieNm, openDt, audiAcc);
	}
}
 ```
