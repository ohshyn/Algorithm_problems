# 맞은 문제

## 21.01.12

### 18258 큐 2

```
파이썬의 리스트는 인자 삭제 시 뒤 원소를 재배치한다: O(n).
deque 활용 기초.
```

```
from sys import stdin
from collections import deque

def main():
    n = int(stdin.readline())
    
    dq = deque()
    for i in range(n):
        cmd = stdin.readline().split()
        if cmd[0] == 'push':
            dq.append(int(cmd[1]))
        elif cmd[0] == 'pop':
            if dq:
                print(dq.popleft())
            else:
                print(-1)
        elif cmd[0] == 'size':
            print(len(dq))
        elif cmd[0] == 'empty':
            if dq:
                print(0)
            else:
                print(1)
        elif cmd[0] == 'front':
            if dq:
                print(dq[0])
            else:
                print(-1)
        elif cmd[0] == 'back':
            if dq:
                print(dq[-1])
            else:
                print(-1)

main()
```

---


# 틀린 문제

