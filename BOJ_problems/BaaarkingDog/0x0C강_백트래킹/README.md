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

## 2021.03.02

### 15656 N과 M (7)

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
            print(state[i], end=' ')
        print()
        return
    for i in range(N):
        if not isused[i]:
            state[t] = nums[i]
            #isused[i] = 1
            BT(t+1)
            #isused[i] = 0

BT(0)
```

### 15657 N과 M (8)

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
        if t>0 and state[t-1]>nums[i]:
            continue
        if not isused[i]:
            state[t] = nums[i]
            #isused[i] = 1
            BT(t+1)
            #isused[i] = 0

BT(0)
```

### 15663 N과 M (9)

```
서로 다른 N개의 문자 중 M개를 선택하는 모든 경우를 출력, 단 동일한 경우를 출력하지는 않는다
수열을 정렬하고 활용하기에 이전 선택과 비교하여 해결 가능
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))
N = len(nums)

state = [0]*10
isused = [0]*10

states = []

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i], end=' ')
        print()
        return
    prev = -1 # 직전에 고른 수, 지역변수로 매번 초기화되어 첫 숫자 선택에는 영향을 주지 않음
    for i in range(N):
        if not isused[i] and prev != nums[i]: # 직전과 같은 수를 선택하지 않음
            state[t] = nums[i]
            prev = nums[i]
            isused[i] = 1
            BT(t+1)
            isused[i] = 0

BT(0)
```

### 15664 N과 M (10)

```
모든 경우 탐색: 백트래킹
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))

state = [0]*10
isused = [0]*10

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i], end=' ')
        print()
        return
    prev = -1
    for i in range(N):
        if t>0 and state[t-1]>nums[i]:
            continue
        if not isused[i] and prev!=nums[i]:
            state[t] = nums[i]
            prev = state[t]
            isused[i] = 1
            BT(t+1)
            isused[i] = 0
        
BT(0)
```

### 15665 N과 M (11)

```
모든 경우 탐색: 백트래킹
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))

state = [0]*M
isused = [0]*M

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i], end=' ')
        print()
        return
    prev = -1
    for i in range(N):
        if prev != nums[i]:
            state[t] = nums[i]
            prev = state[t]
            BT(t+1)
    
BT(0)
```

---

# 틀린 문제

## 21.03.02

### 15663 N과 M (9)

```
서로 다른 N개의 문자 중 M개를 선택하는 모든 경우를 출력, 단 동일한 경우를 출력하지는 않는다
수열을 정렬하고 활용하기에 이전 선택과 비교하여 해결 가능
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))
N = len(nums)

state = [0]*10
isused = [0]*10

states = []

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i], end=' ')
        print()
        return
    prev = -1 # 직전에 고른 수, 지역변수로 매번 초기화되어 첫 숫자 선택에는 영향을 주지 않음
    for i in range(N):
        if not isused[i] and prev != nums[i]: # 직전과 같은 수를 선택하지 않음
            state[t] = nums[i]
            prev = nums[i]
            isused[i] = 1
            BT(t+1)
            isused[i] = 0

BT(0)
```

### 15666 N과 M (12)

```
4 2
9 7 9 1
TC에서 7 7 출력이 안 나옴
```

```
N,M = map(int,input().split())
nums = sorted(list(map(int,input().split())))

state = [0]*N
isused = [0]*N

def BT(t):
    if t == M:
        for i in range(M):
            print(state[i], end=' ')
        print()
        return
    prev = -1
    for i in range(N):
        if t>0 and state[t]>nums[i]:
            continue
        if prev!=nums[i]:
            state[t] = nums[i]
            prev = state[t]
            #isused[i] = 1
            BT(t+1)
            #isused[i] = 0

BT(0)
```