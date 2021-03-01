# 맞은 문제

## 21.03.01

### 15649 N과 M (1)

```
백트래킹: 상태공간을 DFS 탐방하며 모든 가능한 경우를 확인하는 탐색방법
```

```
N,M = map(int,input().split()) # 입력
arr = [0] * 10 # 수열을 담는 리스트
isused = [0] * 10 # 특정 수의 사용 여부를 나타내는 리스트

def back_tracking(t):
    if t == M: # 재귀함수의 base condition
        for i in range(M):
            print(arr[i],end=' ')
        print()
        return
    for i in range(1,N+1):
        if not isused[i]:
            arr[t] = i
            isused[i] = 1
            back_tracking(t+1)
            isused[i] = 0 # i번째를 사용하는 모든 재귀가 끝난 상황, 다시 사용하지 않는 경우를 고려해줘야 함
        
back_tracking(0)
```

### 15650 N과 M (2)

```
백트래킹 + 조건: 기본 백트래킹 골자에 if 조건의 경우 continue로 가지치기
```

```
N,M = map(int, input().split())
l = [0]*10
isused = [0]*10


def back_tracking(t):
    if t == M:
        for i in range(M):
            print(l[i],end=' ')
        print()
        return
    for i in range(1,N+1):
        if i!=0 and l[t-1]>=i:
            continue
        if not isused[i]:
            l[t] = i
            isused[i] = 1
            back_tracking(t+1)
            isused[i] = 0

back_tracking(0)
```

### 15651 N과 M (3)

```
백트래킹 + 조건: 기본 백트래킹 골자에 if 조건의 경우 continue로 가지치기
```

```
N,M = map(int,input().split())
state = [0]*10
isused = [0]*10

def BT(t):
    if t==M:
        for i in range(M):
            print(state[i],end=' ')
        print()
        return
    for i in range(1,N+1):
        if not isused[i]:
            state[t] = i
            #isused[t] = 1
            BT(t+1)
            #isused[t] = 0
            
BT(0)
```

### 15652 N과 M (4)

```
백트래킹 + 조건: 기본 백트래킹 골자에 if 조건의 경우 continue로 가지치기
```

```
N,M = map(int,input().split())
state = [0]*10
isused = [0]*10

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i],end=' ')
        print()
        return
    for i in range(1,N+1):
        if i!=0 and state[t-1]>i:
            continue
        if not isused[i]:
            state[t] = i
            #isused[i] = 1
            BT(t+1)
            #isused[i] = 0
            
BT(0)
```

### 15654 N과 M (5)

```
백트래킹 + 조건: 기본 백트래킹 골자에 if 조건의 경우 continue로 가지치기
```

```
N,M = map(int,input().split())
state = [0] * 10
isused = [0] * 10
cands = sorted(list(map(int,input().split())))

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i],end=' ')
        print()
        return
    for i in range(N):
        if not isused[i]:
            state[t] = cands[i]
            isused[i] = 1
            BT(t+1)
            isused[i] = 0
            
BT(0)
```

### 15655 N과 M (6)

```
백트래킹 + 조건: 기본 백트래킹 골자에 if 조건의 경우 continue로 가지치기
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))
state = [0]*10
isused = [0]*10

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i],end=' ')
        print()
        return
    
    for i in range(N):
        if t!=0 and state[t-1]>nums[i]:
            continue
        if not isused[i]:
            state[t] = nums[i]
            isused[i] = 1
            BT(t+1)
            isused[i] = 0

BT(0)
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