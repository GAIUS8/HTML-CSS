#2017.05.08.월
- HTML 기본 설정
- HTML 문법 일부

##ATOM - html 환경 설정
route> Atom > Preference > +Install > 'emmet' pakage 설치

##emmet
html 문서의 자동완성 기능을 담당한다. <br>
<a href="https://docs.emmet.io/">공식문서[https://docs.emmet.io/]</a><br>

###emmet 기능 살펴보기
####Nesting Operators(중첩 연산자)
- 하위 Tag를 tree구조로 펼치기
	
	Input
	
	~~~html
	div>ul>li [tab]
	~~~
	
	Result 
	
	```html
	<div>
 	 <ul>
		<li></li>
	 </ul>
	</div>
	```

- Tag들을 병렬로 설계
	
	Input
	
	```html
	div+p+bq [tab]
	```
	Result
	
	```html
	<div></div>
	<p></p>
	<blockquote></blockquote>
	```
- tree구조와 병렬구조의 동시 응용

	Input
	
	```html
	div+div>p>span+em
	```
	
	Result
	
	```html
	<div></div>
	<div>
  		<p><span></span><em></em></p>
	</div>
	```
	
- 등반오퍼레이터(climb-up operater)라는데( ^ 요표시)

	Input
	
	```html
	div+div>p>span+em^bq
	```
	
	Result
	
	```html
	<div></div>
	<div>
		<p><span></span><em></em></p>
	<blockquote></blockquote>
	</div>
	
	테그하나만 점프한 모습.
	```

	Input2
	
	```html
	div+div>p>span+em^^^bq
	```
	
	Result2
	
	```html
	<div></div>
	<div>
		<p><span></span><em></em></p>
	</div>
	<blockquote></blockquote>

	테그 세번 점프해서 완전히 밖으로 나온 모습.(사실 두번만 점프해도 같은 결과)
	```
- 	곱배기 기능

	Input
	
	```html
	ul>li*5
	```
	
	Result
	
	```html
	<ul>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
		<li></li>
	</ul>	
	```

- Grouping(그룹핑)

	Input
	
	```html
	div>(header>ul>li*2>a)+footer>p
	```
	
	Result
	
	```html
	<div>
   	 <header>
   	     <ul>
   	         <li><a href=""></a></li>
   	         <li><a href=""></a></li>
   	     </ul>
   	 </header>
   	 <footer>
   	     <p></p>
   	 </footer>
	</div>
	```
	
	---
	*만약 위의 예제에서 그룹핑을 안할경우(괄호를 없앨 경우)
	
	Input
	
	```html
	div>header>ul>li*2>a+footer>p
	```
	
	Result
	
	```html
	<div>
		<header>
			<ul>
				<li>
					<a href=""></a>
					<footer>
						<p></p>
					</footer>
				</li>
				<li>
					<a href=""></a>
					<footer>
						<p></p>
					</footer>
				</li>
			</ul>
		</header>
	</div>
	요래됨 <li>가 두개 만들어 지는데, <li>는 및에 자식들을 가지고 있으니 자식들까지 싸그리 복사됨.
	```
	
- tree + Grouping + 곱배기 혼합 사용

	Input
	
	```html
	(div>dl>(dt+dd)*3)+footer>p
	```
	
	Result
	
	```html
	<div>
		<dl>
			<dt></dt>
			<dd></dd>
			<dt></dt>
			<dd></dd>
			<dt></dt>
			<dd></dd>
		</dl>
	</div>
	<footer>
		<p></p>
	</footer>
	```

####Attribute operators(속성 연산자)
- ID & CLASS 이건 CSS를 배워야 할것같다.. 뭔말인지 모르겠음.
- Custom attributes

	```html
	td[title="Hello world!" colspan=3]
	```

	outputs
	
	```html
	<td title="Hello world!" colspan="3"></td>
	```
	
	You can place as many attributes as you like inside square brackets.
	You don’t have to specify attribute values: td[colspan title] will produce <td 	colspan="" title=""> with tabstops inside each empty attribute (if your editor 	supports them).
	You can use single or double quotes for quoting attribute values.
	You don’t need to quote values if they don’t contain spaces: td[title=hello 	colspan=3] will work.

- Item numbering (숫자 붙이기)
	
	Input	
	
	```html
	ul>li.item$$$*5
	*달라($)표시의 개수가 표현 숫자의 자릿수
	```
	Result
	
	```html
	<ul>
    	<li class="item001"></li>
    	<li class="item002"></li>
    	<li class="item003"></li>
    	<li class="item004"></li>
    	<li class="item005"></li>
	</ul>
	```

- 숫자 붙이는데 범위를 지정하거나 역순으로 부여하기

	Input	
	
	```html
	ul>li.item$@-*5
	*골뱅이(@)부터 달라($)까지 마이너스 붙은건 역순 0*5 이건 5>=x>0의 범의를 뜻함(역순이므로)
	```
	Result
	
	```html
	<ul>
   	 	<li class="item5"></li>
   	 	<li class="item4"></li>
   	 	<li class="item3"></li>
   	 	<li class="item2"></li>
   	 	<li class="item1"></li>
	</ul>
	```

	---
	Input2	
	
	```html
	ul>li.item$@3*5
	*골뱅이(@)부터 달라($)까지, 여기선 3부터 5개
	```
	Result2
	
	```html
    <ul>
    	<li class="item3"></li>
     	<li class="item4"></li>
     	<li class="item5"></li>
     	<li class="item6"></li>
     	<li class="item7"></li>
    </ul>
	```

- tag 안에 text 넣기
	
	Input
	
	```html
	a{Click me}
	```
	
	Result
	
	```html
	<a href="">Click me</a>
	
	tag 사이에 text가 들어간다
	```

	---
	여전히 다른 문법과도 잘 적용된다
	
	Input
	
	```html
	p>{Click }+a{here}+{ to continue}
	```
	
	Result
	
	```html
	<p>Click <a href="">here</a> to continue</p>
	```	
	---
	Input2
	
	```html
	p{Click }+a{here}+{ to continue}
	```
	
	Result2
	
	```html
	<p>Click </p>
	<a href="">here</a> to continue
	```	












