---
title: "파이썬 참조와 튜플추가 "
toc: tru
toc_label: "파이썬 참조와 튜플"
categories:
  - Python
---


---

# 1. 주소 참조
```python
a= [1,2,3]
b=a
```

# 2. 값 참조
```python
a=[1,2,3]
b = a[:]
c = copy(a)
```
# 3. 튜플 값 추가하기
```python
a = (1, 2, 3)
a = a + (4,)
print(a)
```
