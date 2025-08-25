- **Web site**는 여러 개의 Web page가 모인 것
- **Web Page**는 HTML (구조), CSS (스타일링) 등의 웹 기술을 이용해서 만들어진, 웹사이트를 구성하는 하나의 요소

# HTML (HyperText Markup Language)
웹 페이지의 **의미**와 **구조**를 정의하는 언어

## HyperText
웹 페이지를 다른 페이지로 연결하는 링크 - 참조 - 비선형성, 상호연결성, 사용자 주도적 탐색

## Markup Language
태그 등을 이용하여 문서나 데이터의 **구조**를 명시하는 언어
ex) HTML, Markdown

---

## HTML의 구조
- `<!DOCTYPE html>`
해당 문서가 html로 문서라는 것을 나타냄
- `<html></hmtl>`
전체 페이지의 콘텐츠를 포함
- `<title></title>`
브라우저 탭 및 즐겨찾기 시 표시되는 제목으로 사용
- `<head></head>`
문서와 관련된 설정, 설명과 컴퓨터가 식별하는 메타데이터
- `<body></body>`
문서의 내용, 표시되는 모든 콘텐츠 작성. 한 문서에 한개의 body 요소만 존재
- `<p></p>` 
텍스트 문단 만듦
- `<a></a>`
다른 페이지로 이동시키는 하이퍼링크 태그
- `<img></img>`
src에 지정된 그림을 보여주는 태크, 닫는 태그가 없음
ex) `<img src ="images/sample/n=pn" alt = "t샘플 이미지">`

## HTML Attributes (속성)
요소 설정, 동작 조절 위해서
`p class= "editor-note">My cat is very grumpy</p>`에서 `class= "editor-note"` 부분 !

## HTML Text Structure
텍스트 구조와 의미를 제공하고있는것
- Heading & Paragraphs
`h1~6, p `
- Lists
`ol, ul, li`
- Emphasis & Importance
`em, strong`