# 코드 작성 팁

파이썬은 일반적으로 myStyle 보다는 my_style 이런식으로 많이 사용하는 거 같다

# 내장 함수

## zip()
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
## 접두어, 접미사 체크

```
>>> "hello world".startwith('hello')
True
>>> "hello wolrd".endswith('hello')
False

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