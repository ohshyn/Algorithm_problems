# 맞은 문제

## 21.01.15

### 1926 그림

```
BFS 활용1: 맵의 모든 위치 탐방하기.
```

```
from collections import deque

def main():
    R,C = map(int, input().split())
    board = [list(map(int, input().split())) for _ in range(R)]
    
    cnt = 0
    max_size = 0
    for r in range(R):
        for c in range(C):
            if board[r][c] == 1:
                cnt += 1
                cur_size = 0
                
                q = deque([(r,c)])
                board[r][c] =  -1
                while q:
                    dr = [-1,1,0,0]
                    dc = [0,0,-1,1] # 상하좌우
                
                    cr,cc = q.popleft()
                    cur_size += 1
                    
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        
                        if not(0<=nr<R) or not(0<=nc<C):
                            continue
                        if board[nr][nc] != 1:
                            continue
                        q.append((nr,nc))
                        board[nr][nc] = -1
                max_size = max(max_size,cur_size)
    print(cnt)
    print(max_size)
    
    
main()
```

### 2178 미로 탐색

```
BFS 활용2: 하나의 시작점에서의 모든 지점으로의 최소 거리 구하기.
```

```
from collections import deque


def main():
    R,C = map(int, input().split())
    maze = [list(map(int, list(input()))) for _ in range(R)]
    dist = [[-1]*C for _ in range(R)]
    
    q = deque([(0,0)])
    maze[0][0] = -1
    dist[0][0] = 0
    while q:
        cr,cc = q.popleft()
        
        dr=[-1,1,0,0]
        dc=[0,0,-1,1]
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if maze[nr][nc] != 1:
                continue
            q.append((nr,nc))
            maze[nr][nc] = -1
            dist[nr][nc] = dist[cr][cc]+1
            
            if (nr,nc) == (R-1,C-1):
                return dist[nr][nc] + 1
    
    
print(main())
```

### 7576 토마토

```
BFS 활용3: 여러 시작점에서 모든 지점으로의 최소 거리 구하기.
```

```
from collections import deque

def main():
    C,R = map(int, input().split())
    tomatos = [list(map(int,input().split())) for _ in range(R)]
    days = [[-1 for _ in range(C)] for _ in range(R)] # -1: 아직 안익음
    
    max_day = 0
    
    q = deque()
    for r in range(R):
        for c in range(C):
            if tomatos[r][c] == 1:
                q.append((r,c))
                tomatos[r][c] = -1
                days[r][c] = 0

                
    while q:
        cr,cc = q.popleft()
        dr=[-1,1,0,0]
        dc=[0,0,-1,1] # 상하좌우
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if tomatos[nr][nc] != 0:
                continue
            q.append((nr,nc))
            tomatos[nr][nc] = -1
            days[nr][nc] = days[cr][cc] + 1
            max_day = max(max_day, days[nr][nc])
    for r in range(R):
        for c in range(C):
            if tomatos[r][c] == 0:
                return -1
    else:
        return max_day
    
    
print(main())
```

### 7569 토마토

```
BFS 활용4: 3차원에서의 BFS, 여러 시작점에서 모든 지점으로의 최소 거리 구하기.
```

```
from collections import deque

def main():
    C,R,H = map(int, input().split())
    tomatos = [[list(map(int, input().split())) for _ in range(R)] for _ in range(H)]
    days = [[[-1 for _ in range(C)] for _ in range(R)] for _ in range(H)]
    
    q = deque()
    for h in range(H):
        for r in range(R):
            for c in range(C):
                if tomatos[h][r][c] == 1:
                    q.append((h,r,c))
                    tomatos[h][r][c] = -1
                    days[h][r][c] = 0
    
    max_day = 0
    while q:
        ch,cr,cc = q.popleft()
        dh = [-1,1,0,0,0,0] 
        dr = [0,0,-1,1,0,0]
        dc = [0,0,0,0,-1,1]
        for i in range(6):
            nh,nr,nc = ch+dh[i],cr+dr[i],cc+dc[i]
            if not(0<=nh<H) or not(0<=nr<R) or not(0<=nc<C):
                continue
            if tomatos[nh][nr][nc] != 0:
                continue
            q.append((nh,nr,nc))
            tomatos[nh][nr][nc] = -1
            days[nh][nr][nc] = days[ch][cr][cc]+1
            
            max_day = max(max_day, days[nh][nr][nc])
    
    for h in range(H):
        for r in range(R):
            for c in range(C):
                if tomatos[h][r][c] == 0:
                    return -1
    else:
        return max_day


print(main())
```

### 1697 숨바꼭질

```
BFS 활용6: 1차원에서의 BFS.
BFS 적용 범위에 대해 고민해볼 필요가 있는 문제.
```

```
from collections import deque

def main():
    N,K = map(int, input().split())
    board = [-1 for _ in range(100001)] # idx를 1부터 시작하기 위해서 +1
    
    q = deque([N])
    board[N] = 0
    while q:
        c = q.popleft()
        if c == K:
            return board[c]
        d = [-1,+1,+c]
        for i in range(3):
            n = c+d[i]
            if not(0<=n<100001):
                continue
            if board[n] >= 0:
                continue
            q.append(n)
            board[n] = board[c]+1
            
    

print(main())
```

### 1012 유기농 배추

```
BFS 활용1: 시작 지점에서 연결된 모든 지점 탐방
```

```
from collections import deque

def main():
    T = int(input())
    for t in range(T):
        C,R,K = map(int, input().split())
        
        ground = [[0 for _ in range(C)] for _ in range(R)]
        for _ in range(K):
            c,r = map(int, input().split())
            ground[r][c] = 1
        
        cnt = 0
        for r in range(R):
            for c in range(C):
                if ground[r][c] == 1:
                    cnt += 1
                    # BFS
                    q = deque([(r,c)])
                    ground[r][c] = -1 # 방문표시
                    
                    while q:
                        cr,cc = q.popleft()
                        dr = [-1,1,0,0]
                        dc = [0,0,-1,1]
                        for i in range(4):
                            nr,nc = cr+dr[i],cc+dc[i]
                            if not(0<=nr<R) or not(0<=nc<C):
                                continue
                            if ground[nr][nc] != 1:
                                continue
                            q.append((nr,nc))
                            ground[nr][nc] = -1
        print(cnt)
        
main()
```

---

# 틀린 문제

## 21.01.15

### 4179 불!

```
BFS 활용5: 하나는 다른 BFS에 종속적이고 나머지 하나는 독립적인 서로다른 BFS.
```

```
from collections import deque

def main():
    R,C = map(int, input().split())
    maze = [list(input()) for _ in range(R)]
    j_pos,f_pos = (),() 
    for r in range(R):
        for c in range(C):
            if maze[r][c] == 'J':
                j_pos = (r,c)
            elif maze[r][c] == 'F':
                f_pos = (r,c)
    
    dr = [-1,1,0,0]
    dc = [0,0,-1,1]
    # 불의 전파 시간 파악
    f_times = [[-1 for _ in range(C)] for _ in range(R)]
    q = deque([f_pos])
    f_times[f_pos[0]][f_pos[1]] = 0
    while q:
        cr,cc = q.popleft()
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if maze[nr][nc] == '#' or f_times[nr][nc] >= 0:
                continue
            f_times[nr][nc] = f_times[cr][cc]+1
            q.append((nr,nc))
    # 지훈이의 이동시간 파악
    j_times = [[-1 for _ in range(C)] for _ in range(R)]
    q.append(j_pos)
    j_times[j_pos[0]][j_pos[1]] = 0
    while q:
        cr,cc = q.popleft()
        if cr in [0,R-1] or cc in [0,C-1]: # 처음부터 가장자리에 있는 경우
            return j_times[cr][cc] + 1
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C): # maze 범위를 벗어남은 곧 탈출
                return j_times[cr][cc] + 1
            if maze[nr][nc] == '#' or j_times[nr][nc] >= 0:
                continue
            if f_times[nr][nc] != -1 and j_times[cr][cc]+1>=f_times[nr][nc]:
                continue
            q.append((nr,nc))
            j_times[nr][nc] = j_times[cr][cc]+1
    return 'IMPOSSIBLE'


print(main())
```