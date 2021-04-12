
---
title: "알고리즘 기초"
toc: tru
toc_label: "알고리즘 기초"
categories:
  - Algorithm
---


---
# 스택

한쪽 방향으로만 자료를 넣고 뺄 수 있는 자료구조

> Last In First Out (LIFO)

- push: 스택에 자료를 넣는 연산
- pop: 스택에서 자료를 빼는 연산
- top: 스택의 가장 위에 있는 자료를 보는 연산
- empty: 스택이 비어있는지 아닌지를 알아보는 연산
- size: 스택에 저장되어있는 자료의 개수를 알아보는 연산

---

# 큐

한쪽 끝에서만 자료를 넣고 다른 한쪽 끝에서만 뺄 수 있는 자료구조

> First In Frist Out (FIFO)

- push: 큐에 자료를 넣는 연산
- pop: 큐에서 자료를 빼는 연산
- front: 큐의 가장 앞에 있는 자료를 보는 연산
- back: 큐의 가장 뒤에 있는 자료를 보는 연산
- empty: 큐가 비어있는지 아닌지를 알아보는 연산
- size: 큐에 저장되어있는 자료의 개수를 알아보는 연산


---

# 덱

양 끝에서만 자료를 넣고 양 끝에서 뺄 수 있는 자료구조

- push_front: 덱의 앞에 자료를 넣는 연산
- push_back: 덱의 뒤에 자료를 넣는 연산
- pop_front: 덱의 앞에서 자료를 빼는 연산
- pop_back: 덱의 두에서 자료를 빼는 연산
- front: 덱의 가장 앞에 있는 자료를 보는 연산
- back: 덱의 가장 뒤에 있는 자료를 보는 연산


---


# 최대 공약수(GreatestCommonDivisor)

## 유클리드 호제법(Euclidean algorithm)

a를 b로 나눈 나머지를 r이라고 했을 때
> GCD(a, b) = GCD(b, r)
r이 0이면 그 때 b가 최대 공약수이다.


---

# 최소공배수(LeastCommonMultiple)

## 최소공배수 구하기

두 수 a, b의 최대공약수를 g라고 했을 때,
> 최소공배수 = g * (a/g) * (b/g)


---


# 소수(PrimeNumber)

## 에라토스테네스의 체(SieveofEratosthenes)

1. 2부터 N까지의 수 중 가장 작은 수를 찾는다.

2. 그 수가 소수면 그 수의 배수를 지운다.

3. 반복

> 안쪽 for문의 j는 N의 크기에 따라 i*i 또는 i*2로 바꿈


---
