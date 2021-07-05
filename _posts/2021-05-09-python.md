---
title: "파이썬 런타임 에러 (RecursionError)"
toc: tru
toc_label: "RecursionError"
categories:
  - Python
---


---

# 런타임 에러 (RecursionError)

: 프로그램이 비정상적으로 종료된 경우

## 1. 파이썬에서 발생한 이유

> Python이 정한 최대 재귀 깊이보다 재귀의 깊이가 더 깊어질 때 발생

## 2 .해결 방법

1. 재귀함수를 사용하지 않고 `반복문` 사용
2. sys.setrecursionlimit()을 사용하여 최대 재귀 깊이 변경
```python
import sys
sys.setrecursionlimit(10**9)
```
- 재귀의 깊이가 서버를 감당 할 수 없는 경우 `Segmentation fault`가 발생
- 최대 깊이 제한을 너무 적게 해도 `RecursionError`가 발생
