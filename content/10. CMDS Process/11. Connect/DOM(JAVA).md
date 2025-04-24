---
CMDS: Java
type:
  - note
tags:
  - "#DOM"
상위 문서: "[[101.01 Object-Oriented Concepts]]"
category: content
---
## DOM

문서를 완전히 메모리에 로딩 후 필요한 내용 찾기

- Dom Tree
	- 문서를 구성하는 모든 요소를 Node로 구성
	- 태그들은 root 노드를 시작으로 부모- 자식의 관계 구성
-  XML 파싱

```java
public class BoxOfficeDomParser implements BoxOfficeParser {
	private static BoxOfficeDomParser parser = new BoxOfficeDomParser();
	public static BoxOfficeDomParser getParser() {
		return parser;
	}

	private BoxOfficeDomParser() {}
	private List<BoxOffice> list = new ArrayList<>();

	@Override
	public List<BoxOffice> getBoxOffice(InputStream resource) {
		try {
			DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
			DocumentBuilder builder = factory.newDocumentBuilder();
			Document doc = builder.parse(resource);
			Element root = doc.getDocumentElement();
			parse(root);
		} catch (IOException | ParseConfigurationException | SAXException e) {
			e.printStackTrace
		}
		return list;
	}

	private void parse(Element root) {
		NodeList boxOffice = root.getElementsByTagName("dailyBoxOffice");
		for(int i=0; i<boxOffices.getLength(); i++) {
			Node child = boxOffices.item(i);
			list.add(getBoxOffice(child));
		}
	}

	private BoxOffice getBoxOffice(Node node) {
		NodeList childes = node.getChildNodes();
		int rank = -1, audiAcc = -1;
		String name = child.getNodeName();
		String content = child.getTextContent();
		if(name.equals("rank")) {
			rank = Integer.parseInt(content);
		} else if(name.equals("audiAcc")) {
			audiAcc = Integer.parseInt(content);
		} else if(name.equals("movieNm")) {
			movieNm = content;
		} else if(name.equals("openDt")) {
			openDt = content;
		}
	}
}

```