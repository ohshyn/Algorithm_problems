# 맞은 문제

## 21.02.11

### XXXX CCCC

```
설명
```

```
코드
```
---

# 틀린 문제

## 21.02.11

### 1629 곱셈

```
귀납적인 사고로 구현하는 것이 재귀
재귀는 Base Condition(종료조건)이 반드시 존재하고 모든 입력은 Base Condition으로 귀결해야함
```

```
def mul(A,B,C):
    if B==1:
        return A%C
    val = mul(A,B//2,C)
    val = val*val%C
    if B%2 == 0:
        return val
    return val*A%C

def main():
    A,B,C = map(int,input().split())
    return mul(A,B,C)
    
print(main())
```

### 11729 하노이 탑 이동 순서

```
재귀함수 구상 순서를 연습하자
```

```
# 1. 함수의 정의
## func(N): 일반적인 재귀함수의 프로토타입, 하노이탑에서는 탑의 이동을 확인해야하기에 불가능
def func(t1, t2, N): # 원판 N개를 t1기둥에서 t2기둥으로 옮기는 방법을 출력하는 함수
    # 2. Base Condition
    if N == 1:
        print(t1,t2)
        return
    # 3. 재귀 식
    func(t1,6-t1-t2,N-1) # N-1개 원판을 t1에서 6-t1-t2로 옮긴다
    print(t1,t2) # N번 원판을 t1에서 t2로 옮긴다
    func(6-t1-t2,t2,N-1) # N-1개 원판을 6-t1-t2에서 t2로 옮긴다
    

def main():
    N = int(input())
    print(2**N-1) # 하노이탑의 일반항, 일반적인 재귀 문제에서는 물어보지 않음
    func(1,3,N)
    
main()
```

### 1074 Z

```
재귀함수를 사용해야하는 문제유형에 익숙해지자
```

```
# 1. 함수의 정의
def func(N,r,c): # 2^N X 2^N 배열에서 (r,c)를 방문하는 순서를 반환하는 함수
    # 2. base condition
    if N == 0:
        return 0 # N이 0일 때 return 0
    # 3. 재귀 식
    half = 2**(N-1)
    if r<half and c<half:
        return func(N-1,r,c)
    if r<half and c>=half:
        return half*half + func(N-1,r,c-half)
    if r>=half and c<half:
        return 2*half*half + func(N-1,r-half,c)
    return 3*half*half + func(N-1,r-half,c-half)
    
def main():
    N,r,c = map(int,input().split())
    print(func(N,r,c))
    
main()
```