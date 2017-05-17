#2017.05.09 화
- HTML Tag (emmet 연습하기)
	- 테이블 요소 학습
	- Form 요소 학습
- 클래스와 아이디 속성 (뒤에 CSS와 연결되는 부분) 학습
- CSS 사용법 학습
- CSS 선택자 학습

###환경설정
오늘은 필요하지 않았음

--

###HTML Tag 본격 공부하기
- 어제까지 배운 Tag들

	```html
	<ol></ol> : 순서가 있는 목록
	<li>
	<li>
	<ul></ul> : 순서가 없는 목록
	<dt>
	<dd>
	......
	```
	이들도 여러 타입과 옵션을 부여할 수 있다는 것 외에는 별다른 것이 없었음

- table 만들기(테이블 요소 학습)
	html 에서 테이블을 만드는 것은, 표를 그린다고 생각하기 보단 각 블록을 서로 레고처럼 위에서부터 조립한다고 생각하는 것이 더 직관적이다.
	
	```html
	테이블 예시 (3*3 일반적인 표)
	
	<table> 
	    <tr>
	      <th>이름</th>
	      <th>나이</th>
	      <th>점수</th>
	    </tr>
	    <tr>
	      <td>철수</td>
	      <td>19</td>
	      <td>90</td>
	    </tr>
	    <tr>
	      <td>영희</td>
	      <td>18</td>
	      <td>70</td>
	    </tr>
	</table>
	```
	- 행병합(가로 끼리 병합)
		```
		<td colsapn = "2"></td>
		```<br>
		같은 행의 두칸을 병합
	- 열병합(세로 끼리 병합)
		```
		<td rowsapn = "2"></td>
		```<br>
		같은 열의 두칸을 병합

	---

	- 행의 구조화
	
	```	
	<thead> (table head의 준말) : 한번만 선언 가능
	<tbody> : 여러번 중복 선언 가능
	<tfoot> : 한번만 선언 가능
	```
- Form 요소 학습
	- GET 방식으로 전달하기 : URL이 그대로 노출
	- POST 방식으로 전달하기	: URL에 노출되는 것을 방지할 수 있음.(다른 변수를 통해서 전달 가능)
	
	---
	
	- input Tags

	```html
	<form action="">
	  <input type="text" name="usename"><br>
	  <input type="password" name="password"><br>
	  <input type="radio" name="radio"><br>
	  <input type="checkbox" name="checkbox"><br>
	  <input type="button"><br>
	  <input type="file" name="file"><br>
	  <input type="sumit"><br>
	  <input type="reset"><br>
	  <input type="hidden" name="hidden" value="hiddenValue"><br>
	<br>
	  <input type="radio" name="radio-name" value="a">
	  <input type="radio" name="radio-name" value="b">
	  <input type="sumit" value="전송">
	</form>
	```
	input type에는 여러 종류가 있다. 추가적인 종류를 알고 싶다면 참조 >> <a href="https://www.w3schools.com/tags/att_input_type.asp">Input Tag의 가용한 type 더 알아보기</a>
	
	- label Tag
	
	```html
	  <label for="username">Username</label>
	  <input type="text" id="username">
	```
	레이블은 말그대로 레이블인데, 위와 같이 별도로 표현하는 것이 추후 관리하기에 좋음.
	
	- select tag
	
	드롭다운 선택 아이콘을 만들어 주는 테그
		
	```html
	<form action="">
	<select name="numver" id="">
	  <option value="1">First</option>
	  <option value="2">Second</option>
	  <option value="3">Third</option>
	  <option value="4">Fourth</option>
	</select>
	</form>
	```
	
	select에 multiple & size 속성이 있는데 유용하지 않으므로 PASS
	
	- optgroup tag
		
	select요소 내의 옵션들을 그룹핑해주는 방법

	```html
	<form action="optgroup-select" id="">
	<select>
	  <optgroup lable="Fruits">
	    <option value="apple">Apple</option>
	    <option value="banana">Banana</option>
	    <option value="orange">Orange</option>
	  </optgroup>
	  <optgroup lable="Colors">
	    <option value="red">Red</option>
	    <option value="blue">Blue</option>
	    <option value="green">Green</option>
	  </optgroup>
	</select>
	</form>
	```
		
	- button tag
		버튼은 input 테그 안에서도 만들 수 있지만 아래와 같이 만드는 것이 관리에 유용하다
		
	```html
	<form action="">
	  <button type="sumit">button</button>
	  <button type="reset">2buton</button>
	  <button type="button">3buttond</button>
	</form>
	```
	각 타입별로 다른 기능을 수행하는 버튼들임
	
	- fieldset, legend tag
		
	```html
	<form action="">
	  <fieldset>
	    <legend>Login</legend>
	    <label>username:<input for="text"></label>
	    <label>password:<input for="password"></label>
	  </fieldset>
	</form>
	```
	웹에 특정한 area를 지정하여 박스를 만들고, legend 테그로 제목을 부여한다.

--

###id와 class
각 tag들을 그룹핑하거나 각 tag간 구분이 필요할 경우 id나 class를 부여할 수 있다.
일반적으로 id는 #으로, class는 .으로 표현된다.(emmet에서 이런식으로 표현 됨, 내가 어제 이해 못했던 부분)

id는 페이지에서 딱 한번만 선언 가능하고 class는 여러번 사용 가능하다. **따라서 두 속성이 겹칠때에는 id의 속성이 우선권을 가진다.**

--

###색상
inline으로 넣지말고 CSS를 적극 활용하자

색상은 다음과 같이 #을 붙인 후 번호로 입력 된다.

```html
#ff0099
```
RGB순으로 16진수 2자리 즉  0~255.0~255.0~255의 색 조합으로 해당 색을 표현한다.
<a href="http://www.color-hex.com/">색의 관한 추가정보 </a>

---

###CSS

- 외부 스타일 시트 사용하기(External Style Sheet)

Doc.html의 head에 다음과 같이 link tag 추가

```html
<head>
<link rel="stylesheet" href="css/external.css">
</head>
```
.css/external.css의 내용

```html
#index-title{
  font-size: 20px;
  font-weight: bold;
  color: #ff9822;
}
#index-content{
  color: #999000
}
.section{
  color: #333;
  margin-bottom: 40px;
}
p.section-title{
  font-size: 28px;
  color: Blue;
}
p.section-content{
  font-size: 13px;
  line-height: 13px;
  color: #999;
}
```

다시 Doc.html의 body 부분에서 적용

```html
<h3 id="index-title" class="title">Lorem ipsum dolor sit amet.</h3>
<p id="index-content">Lorem ipsum dolor sit amet.</p>

<div class="section">
  <p class="section-title">Lorem ipsum dolor sit amet.</p>
  <p class="section-content">Lorem ipsum dolor sit amet.</p>
</div>
<div class="section">
  <p class="section-title">Lorem ipsum dolor sit.</p>
  <p class="section-content">Lorem ipsum dolor.</p>
</div>
```
이렇게 하면 css파일에서 지정된 양식으로 body내용의 style이 변경된다.


####반드시 알고가야할 Cascading

나는 이를 낙수 현상으로 번역하고자 한다. 물이 흐를 때 여러 장애물을 피해서 구석구석 흐르는 것처럼...

CSS 상에 각각의 id나 class에 여러가지로 양식이 지정될 수 있는데, 문제는 이 양식들이 html문서의 body에서 동시에 적용되었을 경우에 어떤 양식을 우선적으로 적용할 것인가 하는 이슈가 있다.

우선순위는 다음과 같다
1. Inline (인라인 스타일)2. ID Selector (ID 선택자)3. Class Selector (클래스 선택자)4. TAG Selector (태그 선택자)

**Ref. 만약 ID.class 선택자라면 ID 선택자보다 우선한다.**

---

#### 크롬 개발자 도구
option + command + I

debuging, consol 창 활용하기





		
