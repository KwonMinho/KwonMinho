
# 자주 쓰는 python 문법 

### int 나누기
```python
5/3 => type float
5//3 => type int
```


### Map과 함께 사용하여 입력받기
```
a,b = map(int, input().split())
```
### swap 방식
```python
a,b = b,a 
```

### slice
```python

# 1 리스트에서 현재 index 삭제
arr[:index]+arr[index+1:]

# 2 마지막 인덱스 제거
a = a[:-1]

```

### zip()
zip() 함수는 여러 개의 순회 가능한(iterable) 객체를 인자로 받고, 
각 객체가 담고 있는 원소를 터플의 형태로 차례로 접근할 수 있는 반복자(iterator)를 반환합니다.

```
>>> numbers = [1, 2, 3]
>>> letters = ["A", "B", "C"]
>>> for t1, t2 in zip(numbers, letters):
      print((t1,t2))

```
```
(1, 'A')
(2, 'B')
(3, 'C')
```


# 그 외
## heapq

```python
import heapq

heap =[]
heapq.heappush(heap,1)
print(heap)  # [1]
heapq.heappush(heap,2)
print(heap) #[1,2]


## 기존리스트를 heap으로 변환
_list = [1,2,3,4,5]
heapq.heapify(_list)

# pop
heapq.heappop(heap)

```


# 모르는 문법 메모

2**2 => 2 제곱

'a'*50 ==> 'aaaaaaaaaaaaaaaaaa.....aaaaaaaaaaaaaaaaaaaa'

a[-1] <- 마지막 인덱스 접근

a+b :리스트 끼리 더하기

a*3 :리스트 반복하기

del a[1]:리스트에서 요소 삭제

a.index(targetValue): 타켓value의 위치 반환

a.insert(addIndex, value): addIndex 위치에, value를 삽입

a.pop(): 맨 마지막에 있는 요소꺼내기(꺼내고 삭제됨)

a.count(target): 리스트에서 포함된 요소 target의 개수세기

a.extend([4, 5])는 a += [4, 5]와 동일하다.

## copy
a is b : 같은 객체인지비교

### copy하는 방법

```
1. [:] 
a = [1,2,3]
b = a[:]

2. copy module

from copy import copy
a = [1, 2, 3]
b = copy(a)

```

## list 내포하기

```
a = [1,2,3,4]
# 1,2,3,4 중 짝수에만 3을 곱하는 것
result = [num*3 for num in a if num% 2 ==0]

[표현식 for 항목 in 반복 개체 if 조건문]
```

## 튜플

**튜플의 항목 값은 변화가 불가능하다. 따라서 프로그램이 실행되는 동안 그 값이 항상 변하지 않기를 바란다거나 값이 바뀔까 걱정하고 싶지 않다면 주저하지 말고 튜플을 사용해야 한다. **

튜플(tuple)은 몇 가지 점을 제외하곤 리스트와 거의 비슷하며 리스트와 다른 점은 다음과 같다.

- 리스트는 [ ]으로 둘러싸지만 튜플은 ( )으로 둘러싼다.
- 리스트는 그 값의 생성, 삭제, 수정이 가능하지만 튜플은 그 값을 바꿀 수 없다.

t2 = (1,)처럼 단지 1개의 요소만을 가질 때는 요소 뒤에 콤마(,)를 반드시 붙여야 한다는 것과
t4 = 1, 2, 3처럼 괄호( )를 생략해도 무방하다는 점이다.


## dict(해시맵)
- Key 리스트 만들기(keys)
- Value 리스트 만들기(values)
- Key, Value 쌍 얻기(items) --> 튜플로 반환
- Key: Value 쌍 모두 지우기(clear)
- Key로 Value얻기(get)
- 해당 Key가 딕셔너리 안에 있는지 조사하기(in)

## 집합 자료형

```
s2 = set('hello')
{'e','h','l','o'}
```

- 중복을 허용하지 않는다
- 순서가 없다

만약 set 자료형에 저장된 값을 인덱싱으로 접근하려면 다음과 같이 리스트나 튜플로 변환한후 해야 한다.

※ 중복을 허용하지 않는 set의 특징은 자료형의 중복을 제거하기 위한 필터 역할로 종종 사용하기도 한다.

```python
s1 = set([1,2,3])
l1 = list(s1)

#차집합
s1-s2
#합집합
s1+s2
#교집합
s1 & s2

#값 1개 추가하기
s1.add(4)

#여러 개 추가하기
s1.update([4,5,6])

#특정 값 제거하기
s1.remove(2)

```
## 불 자료형

```
값	   |참 or 거짓
"python"	참
""	      거짓
[1, 2, 3]	참
[] 	      거짓
() 	      거짓
{}	      거짓
1	      참
0	      거짓
None	      거짓
```

# 제너레이터

필요할 때마다 객체를 생성하여 던져주는 역할.

생성한 객체들은 메모리에 보관하지 않는다.

재너레이터는 한번 실행하면 끝

- 메모리 절약
- 수행 시간 절약

# 코드 스타일
파이썬은 일반적으로 myStyle 보다는 my_style 이런식으로 많이 사용하는 거 같다

# sort dict by key

```
python version 
>>> x = {1: 2, 3: 4, 4: 3, 2: 1, 0: 0}
>>> {k: v for k, v in sorted(x.items(), key=lambda item: item[1])}
{0: 0, 2: 1, 1: 2, 4: 3, 3: 4}
```

# 내장 함수


```

## 접두어, 접미사 체크

```
>>> "hello world".startwith('hello')
True
>>> "hello wolrd".endswith('hello')
False

```


## dict 초기화

```
from collections import defaultdict

_dict = defaultdict(lambda:0)
```

## itemgetter()?

```
from operator import itemgetter

dict_item = {}

#dict.items()는 튜플값으로 리턴
sorted_list_item = [
      key for key, value in sorted(dict_item.items(), key=itemgetter(1), reverse=True )
]


```


# (), [], [[]], {}의 이해

- 튜플<->리스트의 차이는 튜플은 한번 생성한 이후에는 요소를 변경하거나 삭제할 수 없다.

- 세트 <-> (리스트,튜플)와는 다르게 데이터를 중복해서 쓸 수 없다.

```python
s1=[1,2,3,4] #this is a list in python. 
s2=(1,2,3) #this is a tuple. 
s3=s1[1:] #this take the list elements starting from index 1 to end element. 
s4=[[1,2],[1]] #this is a list of list
s5={1,2,3,4} #this is a Set
s6={80:"국어", 85: "수학", 90:"물리"}
```

# 파이썬특정 기준으로 정렬 key, function,repr 메소드

파이썬 정렬 함수는 
*list.sort()*, *sorted()* 가 있다.

### sorting 할때 key 값을 기준으로 정렬
```python
sorted("This is a test string".split(), key=str.lower)
```

### 복잡한 객체를 정렬할 때 사용
```python
 student_tuples = [
...     ('john', 'A', 15),
...     ('jane', 'B', 12),
...     ('dave', 'B', 10),
... ]

sorted(student_tuples, key=lambda student: student[2])
```


# lambda 함수
파이썬에서 "lambda" 는 런타임에 생성해서 사용할 수 있는 익명 함수

간단한 기능을 일반적인 함수와 같이 정의해두고 쓰는 것이 아니고 
필요한 곳에서 즉시 사용하고 버림

```python
plus = lambda x, y: x + y

result = plus(20, 30)

print(result)
```

# enumerate 함수

```python
for i, val in enumerate(arr[1:]):
```

# 삼항 연산자

```python
op = 2 if cnt==-1 else 5
```