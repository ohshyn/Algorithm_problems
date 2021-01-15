# 맞은 문제

## 21.01.12

### 5397 키로거

```
리스트값을 특정 위치 기준으로 좌, 우 나누어 관리할 때, 두 스택을 활용해보자.
```

```
def key_logger(l):
    l_st = []
    r_st = []
    
    for c in l:
        if c == '<':
            if l_st:
                r_st.append(l_st.pop())
        elif c == '>':
            if r_st:
                l_st.append(r_st.pop())
        elif c == '-':
            if l_st:
                l_st.pop()
        else:
            l_st.append(c)
    return ''.join(l_st + r_st[::-1])
    

def main():
    n = int(input())
    for _ in range(n):
        l = input()
        print(key_logger(l))
    
main()
```

---

# 틀린 문제