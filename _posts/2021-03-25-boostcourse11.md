---
title: "210325-파이썬 기본 문법"
toc: tru
toc_label: "파이썬 기본 문법"
categories:
  - Python
---


---



> 도서 `이것이 코딩테스트다`에 나온 파이썬 문법  일부 정리

# 1. 자료형

## round() 함수

- 2진수 체계에서는 실수 정보를 표현하는 `정확도에 한계`가 있음
- 소수점 값끼리 비교할 때 사용

```python
round(0.5666, 2)
```

>0.57


## - 리스트 슬라이싱

- 리스트에서 연속적인 원소를 가져올 때 사용

```python
lista = [ 1, 2, 3, 4, 5, 6 ]
print(lista[1:3])
```

>[2, 3]



## - 리스트 컴프리헨션

- 리스트 초기화 할 때 사용

```python
array = [ i * i for i in range(10) if i % 2 == 1]
print(array)
```

> [1, 9, 25, 49, 81]

---

```python
array = [i for i in range(1, 10)]
print(array)
```

>[1, 2, 3, 4, 5, 6, 7, 8, 9]

---

```python
n = 3
m = 2
array = [[0] * m for _ in range(n)]
print(array)
```

> [[0, 0], [0, 0], [0,0]]


## - 튜플 자료형

- 튜플은 한 번 선언 된 후 `변경 할 수 없음`
- 그래프 알고리즘 구현 시 사용

```python
tuple = (1, 2, 3, 4, 5, 6)
print(tuple)
```

> (1, 2, 3, 4, 5, 6)



## - 사전 자료형

- 키(key)와 값(value) `쌍을 데이터`로 갖음
- O(1)의 시간으로 처리할 수 있어서 리스트보다 빠르게 동작

```python
data = dict()
data['하나'] = 1
data['둘'] = 2
data['셋'] = 3
print(data)
```

> {'하나': 1, '둘': 2, '셋': 3}


## - 집합 자료형

- `중복을 허용하지 않고 순서가 없음`
- 특정 데이터가 앞서 나왔는지에 대한 여부를 확인할때 사용

```
dataA = set([1, 1, 2, 2, 3, 3, 4, 4, 5, 5])
print(dataA)

dataB = {1, 1, 2, 2, 3, 3, 4, 4, 5, 5}
print (dataB)
```

> {1, 2, 3, 4, 5}
> {1, 2, 3, 4, 5}


---



#  2. 함수

## - 파이썬에서 함수의 구조

```python
def 함수명(매개변수):
		실행할 소스코드
		return 반환 값
```

## - global 키워드

- 함수 밖의 변수 데이터를 변경하는 경우 사용

```python
a = 0

def func():
	global a
	a += 1

for i in range(10):
	func()

print(a)
```

> 10

## - 람다 표현식

- 함수를 간단하게 작성하여 적용할 수 있음

```python
def add(a, b):
	return a + b
print(add(1, 2))

print((lambda a, b: a + b)(1, 2))
```


---




# 3. 입출력

## -  input()

- 내장함수이며 기본적인 입력방법
- 한 줄의 문자열을 입력 받음

```python
str = input()
num = int(input())
```


### input().split()

- 내장함수이며 문자열을 특정 구분자로 나눔

```python
data = list(map(int, input().split()))
n, m ,k = map(int, input().split())
```

## - sys.stdin.readline()

- 데이터를 반복적으로 입력받을 때 사용
- rstrip()은 readline() 입력 후 줄바꿈 기호를 제거해줌

```python
import sys
str =  sys.stdin.readline().rstrip()
```

## - f-string

- python 3.6이상의 버전에서 사용
- `자료형 변환 없이` 사용 가능

```python
answer = 5
print(f"정답은 {answer}입니다.")
```

>정답은 5입니다.


---



# 4. _(언더바)

- 반복 수행시 변수의 값을 무시할 때 사용



---




# 5. 들여쓰기

- 파이썬에서 들여쓰기는 `스페이스바 4번`이 표준

