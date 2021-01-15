# 맞은 문제

---

# 틀린 문제

## 21.01.12

### 2493 탑

```
스택은 LIFO(선입후출)을 활용하기 위함임을 잊지말자!
```

```
def communication(towers):
    st = [] # 수신 가능한 타워를 저장하는 스택
    ans = [] # 각 타워의 수신타워 인덱스를 저장
    
    for i,t in enumerate(towers):
        while st:
            if st[-1][1] <= t: # t보다 작은 타워는 더 이상 이후의 타워를 수신 할 수 없음
                st.pop()
            else: # 수신 조건
                ans.append(st[-1][0]+1)
                break
        if not st: # 처음에는 수신 가능한 st이 없음
            ans.append(0)
        st.append((i,t)) # 앞으로 수신 가능한 타워에 타워를 추가
    return ans
    

def main():
    n = int(input()) # 탑 개수
    towers = list(map(int, input().split()))
    
    print(*communication(towers))
    
main()
```

### 2493 옥상정원

```
스택의 관점에서 문제를 푸는 연습!
```

```
def banchmarking(buildings):
    # st top에 위치한 빌딩이 i번째 빌딩 보다 작거나 같으면 i번째 빌딩을 볼수 없으므로 높을때 까지 pop
    # i번쨰 빌딩을 push
    # i번째 빌딩을 제외한 나머지 빌딩이 옥상을 볼 수 있으니 결과에 st크기-1 을 더함
    
    st = []
    ans = 0
    for i,b in enumerate(buildings):
        while st and st[-1] <= b:
            st.pop()
        st.append(b)
        ans += (len(st)-1)
    return ans

def main():
    n = int(input())
    buildings = [int(input()) for i in range(n)]

    print(banchmarking(buildings))


main()
```
