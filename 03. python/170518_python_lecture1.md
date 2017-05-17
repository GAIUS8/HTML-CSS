#python 입문 - 17.05.18

##가상환경 설치 및 설정하기

### pyenv
* 맥  
`brew install pyenv`  
`brew install pyenv-virtualenv`

### 기본 셸 변경

### zsh
<http://theyearlyprophet.com/love-your-terminal.html>  

```
brew install zsh zsh-completions
curl -L http://install.ohmyz.sh | sh
chsh -s `which zsh`
```

> **`chsh: /usr/local/bin/zsh: non-standard shell` 오류 발생할 경우**
> 
> ```
> sudo vim /etc/shells
> 맨 아래에 `which zsh`했을때의 결과를 추가 후 저장
> ```

> **현재 shell 확인법**  
> echo $SHELL

### pyenv 설정

* 설치 후 pyenv관련 설정을 shell설정에 추가  
	* 맥 `vi ~/.zshrc`
	* 리눅스 	`vim ~/.zshrc`

> 맥
> 
```
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

#### 파이썬 설치 전 필요 패키지 설치

<https://github.com/yyuu/pyenv/wiki/Common-build-problems>

#### 파이썬 셸 관련 설정 (macOS)

> 셸에서 방향키 관련 이슈 해결을 위한 유틸리티 설치

관련 유틸리티 설치 (readline, xz)

```
brew install readline xz
```


##가상환경 사용법

`pyenv install 3.5.3`. 가상환경에 사용할 파이썬 버전 설치

임의(여기서는 fc-python)의 이름의 가상환경 설정
`pyenv virtualenv <version> <env_name>`
> `pyenv virtualenv 3.5.3 fc-python` 입력
> 

#### 사용할 폴더로 이동
```
cd projects
mkdir python
cd python
```

#### local에 가상환경 지정
`pyenv local fc-python`


#### 가상환경 지우기
`pyenv uninstall <env_name>`

## iPython

기본 파이썬 셸보다 다양한 기능을 사용할 수 있도록 해주는 셸을 제공해줌

## iPython 설치

`pip install ipython`

커맨드라인에서 `ipython`실행

-

#### vi 단축키

`shift + g` : 가장 아래로  
`shift + a` : 현재 줄에서 가장 마지막으로


## 변수

###기본 용어 해설
- 할당 : = 할당이라는 것은 같은 주소를 공유하여 같은 값을 가지게 하는 것. 결과값이 같아지므로 같아진 것처럼 보이는 효과가 있다. 변경되는 값이 서로 연동된다.
- 같은지 비교 : == 조건문에서 비교 연산자로 많이 사용

####내장함수 id()
: 해당변수가 저장되어 있는 위치를 나타내준다(주소를 가져옴)

####내장함수 type()
: 인자의 속성 및 type을 확인하는 함수

####python의 자료형
* int
* char
* float
* list
* dict
* tuple
* ......

#### 예약어

아래 예약어들은 파이썬 구문을 정의하는데 사용되기 때문에 변수로 사용할 수 없다.

False, class, finally, is, return,  
None, continue, for, lambda, try,  
True, def, from, nonlocal, while,  
and, del, global, not, with,  
as, elif, if, or, yield,  
assert, else, import, pass,    
break, except, in, raise


## 정수 및 부동소수점
### 사칙연산의 우선순위를 따름(괄호가 더 우선)
### 진수 2진수0b 8진수0o 16진수0x
### 형변환

##문자열
### 따옴표 사용 '' '' ' '
### python에서는 문자열 더하기 가능
### 형변환 str
### 이스케이프 문자 (\) - 특수기능 내장
이스케이프 문자|설명
---|---
\a	| 비프음 발생
\t	| 탭(tab)
\n	| 줄바꿈
\\	| \\(역슬래시) 입력
\\'	| 작은따옴표(') 입력
\\"	| 큰따옴표(") 입력

### 문자열 인덱스 연산 가능(자리수가 몇번째인지를 기준으로 리스트처럼 인덱스로 한자씩 불러오기 가능)

## 슬라이스 연산

**[start:end:step]** 형식을 사용한다.

- [:] 
	- 처음부터 끝까지
- [start:]
	- start오프셋부터 마지막까지
- [:end]
	- 처음부터 end오프셋까지
- [start:end]
	- start오프셋부터 end오프셋까지
- [start:end:step]
	- start오프셋부터 end오프셋까지, step만큼씩 뛰어넘은 부분


#### 내장함수 len()
:해당 인자의 길이를 반환함

#### string method 인 split()
: 문자열을 공백이나 (,) 콤마등의 기준으로 나눠서 각 단어 혹은 문자를 리스트 집합으로 반환해줌.

#### sting method 인 join()
: 공백이나 , 등을 기준으로 문자열 리스트를 결합해줌


### 대소문자 다루기

```python
>>> lux = 'lux, the Lady of Luminosity'
>>> lux.capitalize()
'Lux, the lady of luminosity'
>>> lux.title()
'Lux, The Lady Of Luminosity'
>>> lux.upper()
'LUX, THE LADY OF LUMINOSITY'
>>> lux.lower()
'lux, the lady of luminosity'
>>> lux.swapcase()
'LUX, THE lADY OF lUMINOSITY'
```

### 공식문서

[Text Sequence - String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

### 문자열 포맷

#### 새 스타일 ({}, format)

```
{}.format(변수)
```

----

# 시퀀스 타입

파이썬에 내장된 시퀀스 타입에는 문자열, 리스트, 튜플이 있다. 

## 리스트

```
>>> empty_list1 = []
>>> empty_list2 = list()
>>> sample_list = ['a', 'b', 'c', 'd']
>>> sample_list2 = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
```

내부 메서드로는 append() - 추가, extend() - 확장 등이 있다.

.insert(offset)

del

.remove()

.pop()

.index()

.count()

.sorted()

sort(list)

#### 리스트 복사 (copy)
: 복사는 할당이랑은 다른 개념 (=은 표시는 할당을 의미 - 주소를 공유한다)

- copy함수 : 새로운 리스트를 만들어 낸다(주소값이 다름)
- list함수 : 새로운 리스트를 만들어 낸다
- 슬라이스 연산[:] : 역시 새로운 리스트를 만들어 낸다.

**할당과 복사를 헷갈리지 않도록 주의한다.

## 튜플

튜플은 리스트와 비슷하나, 정의 후 내부 항목의 삭제나 수정이 불가능하다.

empty_tuple = ()

#### 튜플을 사용하는 이유

- 리스트보다 적은 메모리 사용
- 정의후에는 변하지 않는 내부 값



## 딕셔너리(dictionary)

Key-Value형태로 항목을 가지는 자료구조.

empty_dict1 = {}

empty_dict2 = dict()


#### 형변환

**dict** 함수를 사용, 두 값의 시퀀스(리스트 또는 튜플)을 딕셔너리로 변환 한다.

```python
>>> sample = [[1,2], [3,4], [5,6]]
>>> dict(sample)
>>> 
{1: 2, 3: 4, 5: 6}
```

key로 값 호출하기

결합하기 update

삭제 del

전체 삭제 clear

in으로 키 검색

#### 키 또는 값 얻기

**keys()**  
모든 키 얻기

**values()**  
모든 값 얻기

**items()**  
모든 키-값 얻기 (튜플로 반환)

#### 복사

**copy()**  

## 셋(Set)

셋은 키만 있는 딕셔너리와 같으며, 중복된 값이 존재할 수 없다.

#### 셋 생성

```python
>>> empty_set = set()
>>> champions = {'lux', 'ahri', 'ezreal'}
```

#### 형변환

문자열, 리스트, 튜플, 딕셔너리를 셋으로 변환할 수 있으며, 중복된 값이 사라진다.

#### 집합 연산

연산자|설명
---|---
\|	|	합집합(Union)
&	|	교집합(Intersection)
\-	|	차집합(Difference)
^	|	대칭차집합(Exclusive)
<=	|	부분집합(Subset)
<	|	진부분집합(Proper subset)
\>=	|	상위집합(Superset)
\>	|	진상위집합(Proper superset)



# 제어문

## if, elif, else(조건문)

if와 else는 조건이 참인지 거짓인지 판단하는 파이썬 선언문(Statement)이며, elif는 else내의 if를 중첩해야 할 때 사용한다.

```
if 조건:
	조건이 참일 경우
else:
	조건이 거짓일 경우
```

```
if 조건1:
	조건1이 참일 경우
elif 조건2:
	조건1은 거짓이나, 조건2가 참일 경우
else:
	조건1,2가 모두 거짓일 경우
```

comprehesion
```
print("Good") if a > 90 else print("nomal") if a>70 else print("bed")
```


## for문 (조건에 따른 순회)

#### 기본형태

시퀀스형 데이터를 순회하고자 할 때 사용한다.

```
for 항목 in 순회가능(iterable)객체:
   <항목을 사용한 코드>
```

iterable한 객체에는 문자열, 튜플, 딕셔너리, 셋 등이 있다.

break

continue

else(break가 작동 했는지 확인)

#### 여러 시퀀스 동시순회 (zip)
```
>>> fruits = ['apple', 'banana', 'melon']
>>> colors = ['red', 'yellow', 'green', 'purple']
>>> for fruit, color in zip(fruits, colors):
...   print('fruit:', fruit, ' color:', color)
... 
fruit: apple  color: red
fruit: banana  color: yellow
fruit: melon  color: green
```

zip으로 묶은 시퀀스들 중, 가장 짧은 시퀀스가 완료되면 순회가 종료된다.

zip을 사용하면 여러 시퀀스로부터 튜플을 만들 수 있다.

```
>>> list(zip(fruits, colors))
```

#### 숫자 시퀀스 생성 (range)

range()함수는 특정 범위의 숫자 스트림 데이터를 반환한다.

```
range(start, stop, step)
```

zip과 마찬가지로, iterable한 객체를 반환하며, 따라서 for문을 순회할 수 있다.


#### C언어의 for문과 다른점
else 기능이 있다
c언어는 몇번을 돌릴지 지정하는데, python에서는 몇번째꺼까지 할지 정한다(시퀀셜한 모든 것이 다 되는 이점)



