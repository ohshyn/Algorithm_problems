# 맞은 문제

## 21.01.12

### 10866 덱

```
deque 기본 활용
```

```
from sys import stdin
from collections import deque

def main():
    dq = deque()
    
    for i in range(int(stdin.readline())):
        cmd = stdin.readline().split()
        if cmd[0] == 'push_front':
            dq.appendleft(int(cmd[1]))
        elif cmd[0] == 'push_back':
            dq.append(int(cmd[1]))
        elif cmd[0] == 'pop_front':
            if dq:
                print(dq.popleft())
            else:
                print(-1)
        elif cmd[0] == 'pop_back':
            if dq:
                print(dq.pop())
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
        else: # back
            if dq:
                print(dq[-1])
            else:
                print(-1)
    
main()
```
---

# 틀린 문제

## 21.01.14

### 1021 회전하는 큐

### 5430 AC