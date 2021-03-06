---
title: "파이썬 클래스, 모듈, 패키지, 예외처리 "
toc: tru
toc_label: "클래스, 모듈, 패키지, 예외처리"
categories:
  - Python
---

---


# 1. if \_\_name__ == "\_\_main__":

: `__name__`변수는 `모듈의 이름`이 저장되는 변수

> 모듈로 import되어 사용되는가? 현재 파일이 엔트리 포인트(최상위 코드 실행 시작점)로 사용되는가

```python
# mod01.py
def add(a,b):
    return a+b
def sub(a,b):
    return a-b

if __name__ == "__main__":
    print(add(1, 4))
    print(sub(4, 2))
```

```python
# mod01_use.py
# import mod01

# print("10 + 20 = {}".format(mod01.add(10,20)))
# print("10 - 20 = {}".format(mod01.sub(10,20)))

from mod01 import add, sub
print("10 + 20 = {}".format(add(10,20)))
print("10 - 20 = {}".format(sub(10,20)))
```



# 2. 변수와 클래스, 함수를 포함한 모듈

```python
# mod02.py
# 변수
PI = 3.141592

# 클래스
class Math:
    def solv(self, r):
        return PI*(r**2)

# 함수
def add(a,b):
    return a+b
```

---

```python
# mod02_use.py
import mod02

print(mod02.PI)
circle_area = mod02.Math()
print(circle_area.solv(5))
print(mod02.Math().solv(5))
print(mod02.add(10,20))
```

# 3. 패키지

: `__init__.py`파일을 디렉토리 안에 만듦 (3.3버전 후부터는 없어도 인식)

```python
import game.graphic.render
game.graphic.render.render_test()

from game.sound.echo import echo_test
echo_test()

from game.play import run
run.run_test()
```


# 4. 예외만들기

: `raise`

```python
class UserException(Exception):
    def __init__(self):
        self.message = "사용자 정의 예외입니다."
    def get_message(self):
        return self.message
    def __str__(self):
        return self.message

def exception_f(nick):
    if nick == "바보":
        raise UserException()
    print(nick)

try:
    exception_f("천사")
    exception_f("바보")
    exception_f("천재")
except UserException as e:
    print(e.get_message())
    # __str__ 호출
    print(e)
```
