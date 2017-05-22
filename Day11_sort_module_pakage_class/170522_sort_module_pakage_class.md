#python 알고리즘, 모듈-패키지, 클래스, 버블정렬
17.05.22 김영광

* python 선택정렬
* 모듈
* 패키지
* 클래스
* 버블정렬

<br>

##python 선택정렬

```python

def selection_sort(ori_list):
    
    #주어진 길이
    ori_len = len(ori_list)
    
    #리스트 길이 -1 번만큼 순회, 각 인덱스는 i에 지정
    for i in range(ori_len-1):
        print('{}번째 loop입니다'.format(i+1))
        cur_min_index = i
        print('현재 최소값은 {} 인덱스는 {} 입니다.'.format(ori_list[cur_min_index],cur_min_index+1))
       
        #loop 내부에서 매 loop마다 리스트길이 - i(상위 인덱스)만큼 순회
        for j in range(i+1, ori_len):
            if ori_list[cur_min_index] > ori_list[j]:
                cur_min_index = j
                print('{}번째 index의 {}값이 기존값보다 더 작아서 저장합니다.'.format(
                    cur_min_index+1, ori_list[cur_min_index]))

        ori_list[i], ori_list[cur_min_index] = ori_list[cur_min_index], ori_list[i] #파이써닉!
        print(list)

selection_sort(list)
print(list)

```
###작동원리
1. 주어진 리스트 중에 최솟값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체한다(패스(pass)).
3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.

###시간복잡도
 n개의 주어진 리스트를 이와 같은 방법으로 정렬하는 데에는 Θ(n2) 만큼의 시간이 걸린다.[O 엔제곱]

<br>

##모듈
파이썬 파일 각각을 서로 불러오고 기능을 파일별로 나누는 기능

###모듈 불러오기(import)

```python
>shop.py

def buy_item():
    print('Buy item!')

buy_item()
```

```python
>game.py

def play_game():
    print('Play game!')

play_game()
```

```python
>lol.py(main)

import game
import shop

print('= Turn on game =')
game.play_game()
shop.buy_item()
```

import를 이용하여 lol.py는 shop.py에 정의된 함수와 game.py의 정의된 함수를 사용할 수 있다.



###모듈의 전역변수 활용하기
```__name__```은 모듈의 이름을 나타내는함수 다음과 같이 활용 가능!

```python
def buy_item():
    print('Buy item!')

if __name__ == '__main__':
    buy_item()
```
메인 모듈, 즉 모듈이 직접 실행되는 때에는, 다시 말해 자신이 import된 때에는 buy_item함수를 실행하지 않는다. 모듈로서 불려갈 때에는 저 함수가 호출되지 않는다.

###모듈 불러오는 다른 방법들
```from 모듈명 * 을 사용해 모듈 내 모든 식별자 (변수, 함수) import```
```from을 사용해 모듈의 함수를 직접 import```

<br>


##패키지만들기
``` brew install tree``` 설치 확인!
커맨드 라인에 ```	tree``` 입력 후 파일 구조 잘 생성되는 지 확인!

패키지는 모듈들을 모아 둔 특별한 폴더를 뜻한다. (일반적인 폴더와는 다르다)
폴더를 패키지로 만들면 계층 구조를 가질 수 있으며, 모듈들을 해당 패키지에 모을 수 있는 역할을 한다.
패키지를 만들 때는 패키지로 사용할 폴더에 ```__init__.py```파일을 넣어주면, 해당 폴더는 패키지로 취급된다. (비어있어도 무관하다)

```
├── func
│   ├── __init__.py
│   ├── game.py
│   └── shop.py
└── lol.py
```

```__init__.py```생성하기
```touch __init__.py```

### 패키지 불러오기

```python
from functions.game import play_game
from functions.shop import buy_item
from friends.chat import send_message

~~~
```
> functions 폴더 패키지 안에 game 모듈 불러오기  
> functions 폴더 패키지 안에 shop 모듈 불러오기   
> friends 폴더 패키지 안에 chat 모듈 불러오기     

<br>


##클래스
클래스는 객체를 만들기 위한 틀이다. (현실에 비유할 경우, 붕어빵과 붕어빵 틀이라고 생각하는것이 일반적이다)

객체의 메서드를 정의할 때, 첫 번째 인수는 항상 **self**이다. **self**에는 메서드를 호출하는 객체 자신이 자동으로 전달된다.
이렇게 self가 자동으로 호출되는 이유는 클래스의 메서드를 사용할 때 어떤 객체가 해당 메서드를 사용하고 있는지 알 수 있도록 하기 위해서이다. 또한 이렇게 하나의 메서드를 여러 객체가 공유할 수 있다.

속성이나 메서드에 접근할 때는 ```객체.속성명``` 또는 ```객체.메서드명``` 을 사용한다.


클래스가 저장된 파일

```python
class Shop:
    description = 'Python shop class'
    def __init__(self, name, shop_type, address):
        self.name = name
        self.shop_type = shop_type
        self.address = address

    def shop_info(self):
        print('상점이름: {}'.format(self.name))
        print('   Shop Type: {}'.format(self.shop_type))
        print('   Address : {}'.format(self.address))
        print('-----------------------------')

    def chage_type(self, shop_type):
        self.shop_type = shop_type

    @classmethod
    def change_description(cls, description):
        cls.description = description

    @staticmethod
    def print_type():
        print('hello') 
```
 
 
위의 클래스파일을 사용하는 파일

```python
from class_sample import Shop

lotteria = Shop('Lotteria', 'fastfood', '서울시 영등포구 타임스퀘어')
cu = Shop('CU', 'convinent store', '서울시 강남구 신사동')

lotteria.shop_info()
cu.shop_info()
```

출력결과

```
상점이름: Lotteria
   Shop Type: pc방
   Address : 서울시 영등포구 타임스퀘어
-----------------------------
상점이름: CU
   Shop Type: convinent store
   Address : 서울시 강남구 신사동
-----------------------------
```

### 인스턴스 메서드
주로 사용하는 메서드(클래스 안에 정의된 함수 대부분)

### 클래스 메서드
클래스 속성에 대해 동작하는 메서드, 호출주체 자체가 클래스임.
클래스메서드는 ```@classmethod 데코레이터```를 붙여 선언하며, 첫 번째 인자의 이름은 관용적으로 cls를 사용한다.

###스태틱 메서드 
클래스나 인스턴스에 영향을 주지 않을 목적으로 만들어내는 메서드
스태틱메서드는 ```@staticmethod 데코레이터```를 붙여 선언한다.

---
<br><br><br>

##버블 정렬(거품 정렬)
거품 정렬(Bubble sort)은 두 인접한 원소를 검사하여 정렬하는 방법이다. 시간 복잡도가 {\displaystyle O(n^{2})} O(n^{2})로 상당히 느리지만, 코드가 단순하기 때문에 자주 사용된다. 원소의 이동이 거품이 수면으로 올라오는 듯한 모습을 보이기 때문에 지어진 이름이다.

<img src="https://upload.wikimedia.org/wikipedia/commons/3/37/Bubble_sort_animation.gif">

**핵심은 인접한 두개 원소끼리 서로 비교해가면서 교체한다는 것이다**

!개인적인 생각 => 여러개 CPU에 동시에 할당할 수 있다면 상당히 빠른 알고리즘이 될 것 같다.(mult-tasking을 지원하는 환경에서 쉽고 빠르게 구현 가능 할 것.)

###구현
7개 숫자 거품정렬 예제

```python
def bubbleSort(list):
    length = len(list)-1
    print('정렬대상: {}'.format(list))
    for i in range(length):
        print('{}번째 진행상황: {}'.format(i+1, list))
        for j in range(length-i):
            if list[j] > list[j+1]:
                list[j], list[j+1] = list[j+1], list[j]
            print('  세부 진행 상황: {}'.format(list))

    return list


list = [5,4,2,6,7,1,3]

result = bubbleSort(list)

print('정렬완료 {}'.format(result))
```

```python
정렬대상: [5, 4, 2, 6, 7, 1, 3]
1번째 진행상황: [5, 4, 2, 6, 7, 1, 3]
  세부 진행 상황: ['4, 5', 2, 6, 7, 1, 3]
  세부 진행 상황: [4, '2, 5', 6, 7, 1, 3]
  세부 진행 상황: [4, 2, '5, 6', 7, 1, 3]
  세부 진행 상황: [4, 2, 5, '6, 7', 1, 3]
  세부 진행 상황: [4, 2, 5, 6, '1, 7', 3]
  세부 진행 상황: [4, 2, 5, 6, 1, '3, 7'] #7이 제일 뒤로 옴
2번째 진행상황: ['4, 2', 5, 6, 1, 3, 7]
  세부 진행 상황: ['2, 4', 5, 6, 1, 3, 7]
  세부 진행 상황: [2, '4, 5', 6, 1, 3, 7]
  세부 진행 상황: [2, 4, '5, 6', 1, 3, 7]
  세부 진행 상황: [2, 4, 5, '1, 6', 3, 7]
  세부 진행 상황: [2, 4, 5, 1, '3, 6', 7] #6이 그다음 뒤로 옴
3번째 진행상황: [2, 4, 5, 1, 3, 6, 7]
  세부 진행 상황: [2, 4, 5, 1, 3, 6, 7]
  세부 진행 상황: [2, 4, 5, 1, 3, 6, 7]
  세부 진행 상황: [2, 4, 1, 5, 3, 6, 7]
  세부 진행 상황: [2, 4, 1, 3, 5, 6, 7] #5가 그다음 뒤로 옴
4번째 진행상황: [2, 4, 1, 3, 5, 6, 7]
  세부 진행 상황: [2, 4, 1, 3, 5, 6, 7]
  세부 진행 상황: [2, 1, 4, 3, 5, 6, 7]
  세부 진행 상황: [2, 1, 3, 4, 5, 6, 7]
5번째 진행상황: [2, 1, 3, 4, 5, 6, 7]
  세부 진행 상황: [1, 2, 3, 4, 5, 6, 7]
  세부 진행 상황: [1, 2, 3, 4, 5, 6, 7]
6번째 진행상황: [1, 2, 3, 4, 5, 6, 7]
  세부 진행 상황: [1, 2, 3, 4, 5, 6, 7]
정렬완료 [1, 2, 3, 4, 5, 6, 7]
```

인접한 것 두개씩 정렬된다.








 




