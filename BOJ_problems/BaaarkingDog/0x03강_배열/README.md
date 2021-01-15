# 맞은 문제

---

# 틀린 문제

## 21.01.12

### 3723 두수의합

```
루프 회수를 줄이기 위해 두 개의 인덱스를 제어.
```

```
n = int(input())
a = sorted(list(map(int, input().split())))
x = int(input())


i,j = 0,n-1
cnt = 0
while i < j:
    s =  a[i]+a[j]
    
    if s == x:
        i += 1
        j -= 1
        cnt += 1
    elif s > x:
        j -= 1
    else:
        i += 1

print(cnt)
```