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

## 21.01.18

### 2583 영역 구하기

```
BFS 활용: 모든 영역을 탐방하며 특정 영역의 크기 확인.
좌표의 환산.
```

```
from collections import deque


def main():
    R,C,K = map(int, input().split())
    board = [[0 for _ in range(C)] for _ in range(R)]
    for _ in range(K):
        x1,y1,x2,y2 = map(int, input().split())
        for r in range(R-y2, R-y1): # r
            for c in range(x1, x2): # c
                board[r][c] = 1
    
    cnt = 0
    sizes = []
    for r in range(R):
        for c in range(C):
            if board[r][c] == 0:
                cnt += 1
                q = deque([(r,c)])
                board[r][c] = -1
                cur_size = 0
                while q:
                    cr,cc = q.popleft()
                    cur_size += 1
                    dr,dc = [-1,1,0,0],[0,0,-1,1]
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        if not(0<=nr<R) or not(0<=nc<C):
                            continue
                        if board[nr][nc] != 0:
                            continue
                        q.append((nr,nc))
                        board[nr][nc] = -1
                sizes.append(cur_size)
    print(cnt)
    print(*sorted(sizes))
    
    
main()
```

### 2667 단지번호붙이기

```
BFS 활용: 영역 개수 구하기, 영역 별 크기 구하기.
```

```
from collections import deque


def main():
    N = int(input())
    board = []
    for r in range(N):
        board.append(list(map(int, list(input()))))
    
    cnts = []
    for r in range(N):
        for c in range(N):
            if board[r][c] == 1:
                cur_cnt = 0
                q = deque([(r,c)])
                board[r][c] = -1
                while q:
                    cr,cc = q.popleft()
                    cur_cnt += 1
                    dr,dc = [-1,1,0,0],[0,0,-1,1]
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        if not(0<=nr<N) or not(0<=nc<N):
                            continue
                        if board[nr][nc] != 1:
                            continue
                        q.append((nr,nc))
                        board[nr][nc] = -1
                cnts.append(cur_cnt)
    print(len(cnts))
    for cnt in sorted(cnts):
        print(cnt)


main()
```

### 7562 나이트의 이동

```
BFS 활용: 출발 좌표에서 목적 좌표까지 몇 번의 규칙을 적용해야하는지 확인.
```

```
from collections import deque


def main():
    T = int(input())
    
    steps = []
    for _ in range(T):
        L = int(input())
        fr,fc = map(int, input().split())
        tr,tc = map(int, input().split())
        
        board = [[0 for _ in range(L)] for _ in range(L)]
        q = deque([(fr,fc)])
        board[fr][fc] = 1
        
        while q:
            cr,cc = q.popleft()
            if (cr,cc) == (tr,tc):
                steps.append(board[cr][cc]-1)
                break
            dr,dc = [-1,-2,-2,-1,1,2,2,1],[-2,-1,1,2,-2,-1,1,2]
            for i in range(8):
                nr,nc = cr+dr[i],cc+dc[i]
                if not(0<=nr<L) or not(0<=nc<L):
                    continue
                if board[nr][nc] != 0:
                    continue
                q.append((nr,nc))
                board[nr][nc] = board[cr][cc] + 1
    for step in steps:
        print(step)
    

main()
```

## 21.01.19

### 2468 안전 영역

```
조건에 따라 변하는 데이터 + BFS 기초
```

```
from collections import deque


def flood(heights, N, h):
    board = [[0 if heights[r][c]<=h else heights[r][c] for c in range(N)] for r in range(N)]
    
    island_cnt = 0
    for r in range(N):
        for c in range(N):
            if board[r][c] != 0:
                island_cnt += 1
                q = deque([(r,c)])
                board[r][c] = 0
                while q:
                    cr,cc = q.popleft()
                    dr,dc = [-1,1,0,0],[0,0,-1,1]
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        if not(0<=nr<N) or not(0<=nc<N):
                            continue
                        if board[nr][nc] <= 0:
                            continue
                        q.append((nr,nc))
                        board[nr][nc] = 0
    return island_cnt
    

def main():
    N = int(input())
    heights = [list(map(int, input().split())) for _ in range(N)]
    
    max_height = 0
    for r in range(N):
        for c in range(N):
            max_height = max(max_height, heights[r][c])
    #print(max_height)
    
    max_cnts = 0
    for h in range(max_height + 1):
        max_cnts = max(max_cnts, flood(heights, N, h))
    print(max_cnts)


main()
```

### 2573 빙산

```
BFS 알고리즘 구현 활용: 사방탐색, 기초 BFS
```

```
def melting(heights, R,C):
    cnts_0s = [[0 for _ in range(C)] for _ in range(R)]
    for r in range(R):
        for c in range(C):
            if heights[r][c] != 0:
                dr,dc = [-1,1,0,0],[0,0,-1,1]
                cnt_0s = 0
                for i in range(4):
                    nr,nc = r+dr[i],c+dc[i]
                    if not(0<=nr<R) or not(0<=nc<C):
                        continue
                    if heights[nr][nc] == 0:
                        cnt_0s += 1
                cnts_0s[r][c] = cnt_0s
    return [[heights[r][c] - cnts_0s[r][c] if heights[r][c] - cnts_0s[r][c] >= 0 else 0 for c in range(C)] for r in range(R)]
    
from collections import deque
def counting(heights, R,C):
    cnt = 0
    board = [[heights[r][c] for c in range(C)] for r in range(R)]
    for r in range(R):
        for c in range(C):
            if board[r][c] != 0:
                cnt += 1
                q = deque([(r,c)])
                board[r][c] = 0
                while q:
                    cr,cc = q.popleft()
                    dr,dc = [-1,1,0,0],[0,0,-1,1]
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        if not(0<=nr<R) or not(0<=nc<C):
                            continue
                        if board[nr][nc] <= 0:
                            continue
                        q.append((nr,nc))
                        board[nr][nc] = 0
    return cnt

def is_melt_all(heights, R,C):
    cnt_0 = 0
    for r in range(R):
        cnt_0 += heights[r].count(0)
    return cnt_0 == R*C

def main():
    R,C = map(int, input().split())
    heights = [list(map(int, input().split())) for _ in range(R)]
    year = 0
    while True:
        heights = melting(heights, R,C)
        cnt = counting(heights, R,C)
        year += 1
        
        if cnt >= 2:
            return year
        if is_melt_all(heights,R,C):
            return 0

print(main())
```

## 21.01.20

### 2146 다리 만들기

```
BFS 활용
```

```
from collections import deque
from itertools import combinations

def get_poss(board, N):
    poss = []
    visited = [[0 for _ in range(N)] for _ in range(N)]
    for r in range(N):
        for c in range(N):
            if board[r][c] == 1 and visited[r][c] != 1:
                q = deque([(r,c)])
                visited[r][c] = 1
                pos = [(r,c)]
                while q:
                    cr,cc = q.popleft()
                    dr,dc = [-1,1,0,0],[0,0,-1,1]
                    for i in range(4):
                        nr,nc = cr+dr[i],cc+dc[i]
                        if not(0<=nr<N) or not(0<=nc<N):
                            continue
                        if board[nr][nc] != 1:
                            continue
                        if visited[nr][nc] == 1:
                            continue
                        q.append((nr,nc))
                        visited[nr][nc] = 1
                        pos.append((nr,nc))
                poss.append(pos)
    return poss

def main():
    N = int(input())
    board = [list(map(int,input().split())) for _ in range(N)]
    
    # 섬의 좌표들을 구하자
    poss = get_poss(board, N)
    # 각 쌍의 섬 좌표에서 최소치를 구하며 비교
    bridge_len = N*N
    island_cnt = len(poss)
    
    for comb in combinations(range(island_cnt),2):
        i,j = comb
        for k in range(len(poss[i])):
            for l in range(len(poss[j])):
                cur_len = abs(poss[i][k][0]-poss[j][l][0]) + abs(poss[i][k][1]-poss[j][l][1])
                bridge_len = min(bridge_len, cur_len)
    print(bridge_len-1)

main()
```

### 5014 스타트링크

```
1차원 BFS
```

```
from collections import deque

def main():
    HEIGHT,FROM,TO,UP,DOWN = map(int, input().split())
    building = [-1 for _ in range(HEIGHT+1)]
    
    q = deque([FROM])
    building[FROM] = 0
    while q:
        c = q.popleft()
        if c == TO:
            return building[c]
        d = [+UP, -DOWN]
        for i in range(2):
            n = c+d[i]
            if not(1<=n<HEIGHT+1):
                continue
            if building[n] != -1:
                continue
            q.append(n)
            building[n] = building[c]+1
    else:
        return 'use the stairs'

print(main())
```

### 6593 상범 빌딩

```
3차원 BFS
```

```
from collections import deque
def main():
    while True:
        H,R,C = map(int,input().split())
        if (H,R,C) == (0,0,0):
            break
        building = []
        for h in range(H):
            row = []
            for r in range(R):
                row.append(list(input()))
            building.append(row)
            input() # 공백
        pos_S,pos_E = (),()
        for h in range(H):
            for r in range(R):
                for c in range(C):
                    if building[h][r][c] == 'S':
                        pos_S = (h,r,c)
                    elif building[h][r][c] == 'E':
                        pos_E = (h,r,c)
        q = deque([pos_S])
        building[pos_S[0]][pos_S[1]][pos_S[2]] = str(0)
        while q:
            ch,cr,cc = q.popleft()
            if (ch,cr,cc) == pos_E:
                print('Escaped in ' + building[ch][cr][cc] + ' minute(s).')
                break
            dh,dr,dc = [-1,1,0,0,0,0],[0,0,-1,1,0,0],[0,0,0,0,-1,1]
            for i in range(6):
                nh,nr,nc = ch+dh[i],cr+dr[i],cc+dc[i]
                if not(0<=nh<H) or not(0<=nr<R) or not(0<=nc<C):
                    continue
                if building[nh][nr][nc] not in ['.','E']:
                    continue
                q.append((nh,nr,nc))
                building[nh][nr][nc] = str(int(building[ch][cr][cc])+1)
        else:
            print('Trapped!')

main()
```

## 21.01.21

### 13549 숨바꼭질 3

```
1차원 BFS 활용: 서로 다른 가중치로 탐색
```

```
from collections import deque
def main():
    FROM,TO = map(int, input().split())
    board = [-1 for _ in range(100001)]
    q = deque([FROM])
    board[FROM] = 0
    while q:
        c = q.popleft()
        if c == TO:
            return board[c]
        d = [2*c, c-1, c+1]
        for i in range(3):
            n = d[i]
            if not(0<=n<100001):
                continue
            if board[n] != -1:
                continue
            q.append(n)
            board[n] = board[c] if i==0 else board[c]+1 


print(main())
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

## 21.01.19

### 2206 벽 부수고 이동하기

```
맵의 형태를 바꿔가며 BFS
```

```
from collections import deque


def BFS(maze,cand,R,C):
    board = [[maze[r][c] for c in range(C)] for r in range(R)]
    board[cand[0]][cand[1]] = 0
    
    q = deque([(0,0)])
    while q:
        cr,cc = q.popleft()
        if (cr,cc) == (R-1,C-1):
            return board[cr][cc]+1
        dr,dc = [-1,1,0,0],[0,0,-1,1]
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if board[nr][nc] != 0:
                continue
            q.append((nr,nc))
            board[nr][nc] = board[cr][cc] + 1
    else:
        return -1
    

def main():
    R,C = map(int, input().split())
    maze = [list(map(int, list(input()))) for _ in range(R)]
    
    cands = []
    for r in range(R):
        for c in range(C):
            if maze[r][c] == 1:
                cands.append((r,c))
    min_dist = R*C
    for cand in cands:
        cur_dist = BFS(maze, cand, R,C)
        if cur_dist != -1:
            min_dist = min(min_dist, cur_dist)
            break
    else:
        min_dist = -1
    print(min_dist)
    
    
main()
```

### 5427 불

```
서로 다른 BFS 중 하나만 종속적일 때: 각각 BFS를 구하여 해결
메모리 초과로 실패
```

```
from collections import deque
def main():
    T = int(input())
    for t in range(T):
        C,R = map(int,input().split())
        maze = [list(input()) for _ in range(R)]
        pos_p, pos_f = (),[]
        time_p, time_f = [[0 for _ in range(C)] for _ in range(R)],[[0 for _ in range(C)] for _ in range(R)]
        
        for r in range(R):
            for c in range(C):
                if maze[r][c] == '@':
                    pos_p = (r,c)
                elif maze[r][c] == '*':
                    pos_f.append((r,c))
        
        q_f = deque(pos_f)
        while q_f:
            cr,cc = q_f.popleft()
            dr,dc = [-1,1,0,0],[0,0,-1,1]
            for i in range(4):
                nr,nc = cr+dr[i],cc+dc[i]
                if not(0<=nr<R) or not(0<=nc<C):
                    continue
                if maze[nr][nc] in ('#', '*'):
                    continue
                if time_f[nr][nc] != 0:
                    continue
                q_f.append((nr,nc))
                time_f[nr][nc] = time_f[cr][cc] + 1
        # for r in range(R):
        #     print(time_f[r])
        # print()
        EXIT = False
        q_p = deque([pos_p])
        while q_p:
            cr,cc = q_p.popleft()
            dr,dc = [-1,1,0,0],[0,0,-1,1]
            for i in range(4):
                nr,nc = cr+dr[i],cc+dc[i]
                if not(0<=nr<R) or not(0<=nc<C):
                    EXIT = True
                    print(time_p[cr][cc] + 1)
                    break
                if maze[nr][nc] in ['#', '*']:
                    continue
                if time_p[cr][cc]+1 >= time_f[nr][nc]:
                    continue
                q_p.append((nr,nc))
                time_p[nr][nc] = time_p[cr][cc] + 1
        if not EXIT:
            print('IMPOSSIBLE')

main()
```

## 21.01.21

### 1600 말이 되고픈 원숭이

```
한 객체에 서로 다른 이동 형태의 BFS
```

```
from collections import deque
def main():
    # 하나의 객체가 다른 이동이 가능한 경우의 BFS
    K = int(input())
    C,R = map(int,input().split())
    board = [list(map(int, input().split())) for _ in range(R)]
    visit = [[[0 for _ in range(K+1)] for _ in range(C)] for _ in range(R)] # K+1 차원으로 말과 원숭이의 이동을 다른 차원에서 관리
    q = deque()
    
    def horse(cr,cc,ch):
        dr,dc = [-1,-2,-2,-1,1,2,2,1],[-2,-1,1,2,-2,-1,1,2]
        for i in range(8):
            nr,nc,nh = cr+dr[i],cc+dc[i],ch+1
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if board[nr][nc] != 0:
                continue
            if visit[nr][nc][nh] != 0:
                continue
            visit[nr][nc][nh] = visit[nr][nc][ch]+1 # 말의 BFS는 원숭이와 다른 차원에서 관리
            q.append((nr,nc,nh))
    
    def monkey(cr,cc,ch):
        dr,dc = [-1,1,0,0],[0,0,-1,1]
        for i in range(4):
            nr,nc = cr+dr[i],cc+dc[i]
            if not(0<=nr<R) or not(0<=nc<C):
                continue
            if board[nr][nc] != 0:
                continue
            if visit[nr][nc][ch] != 0:
                continue
            visit[nr][nc][ch] = visit[nr][nc][ch]+1
            q.append((nr,nc,ch))
    
    def BFS():
        q.append((0,0,0))
        board[0][0] = 1
        while q:
            cr,cc,ch = q.popleft()
            if (cr,cc) == (R-1,C-1):
                print(board[cr][cc][ch]-1)
                break
            if ch < k:
                horse(cr,cc,ch)
                monkey(cr,cc,ch)
            elif ch == l:
                monkey(cr,cc,ch)
        else:
            print(-1)
    
    BFS()
        
main()
```

### 3197 백조의 호수

```
BFS 활용
시간 초과: 얼음 녹이는 과정에서 개선이 필요
```

```
from collections import deque
def main():
    R,C = map(int,input().split())
    lake = [list(input()) for _ in range(R)]
    # 한 백조의 위치에서 시작한 BFS 중 또 다른 백조를 만나면 끝
    pos_swan = ()
    for r in range(R):
        for c in range(C):
            if lake[r][c] == 'L':
                pos_swan = (r,c)
    
    def BFS():
        q = deque([pos_swan])
        visited = [[0 for _ in range(C)] for _ in range(R)]
        visited[pos_swan[0]][pos_swan[1]] = 1
        while q:
            cr,cc = q.popleft()
            dr,dc = [-1,1,0,0],[0,0,-1,1]
            for i in range(4):
                nr,nc = cr+dr[i],cc+dc[i]
                if not(0<=nr<R) or not(0<=nc<C):
                    continue
                if lake[nr][nc] not in ['.','L']:
                    continue
                if visited[nr][nc] != 0:
                    continue
                if lake[nr][nc] == 'L':
                    return False # 다른 백조를 만나면 루프 종료
                q.append((nr,nc))
                visited[nr][nc] = 1
        return True
    
    def melting():
        water_cnt = [[0 for _ in range(C)] for _ in range(R)]
        for r in range(R):
            for c in range(C):
                cnt = 0
                dr,dc = [-1,1,0,0],[0,0,-1,1]
                for i in range(4):
                    nr,nc = r+dr[i],c+dc[i]
                    if not(0<=nr<R) or not(0<=nc<C):
                        continue
                    if lake[nr][nc] == '.':
                        cnt += 1
                water_cnt[r][c] = cnt
        for r in range(R):
            for c in range(C):
                if lake[r][c] == 'X' and water_cnt[r][c] > 0:
                    lake[r][c] = '.'
    
    days = 0
    while BFS():
        # 백조가 못 만나면 얼음이 녹고 다음날에 대해 판단
        melting()
        days += 1
    print(days)


main()
```