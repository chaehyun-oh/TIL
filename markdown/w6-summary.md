# 6주차 summary

## 2차원 리스트의 회전

```python
matrix = [
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9]
]

n = 3
rotated_matrix = [[0] * n for _ in range(n)]

for i in range(n):
	for j in range(n):
			rotated_matrix[i][j] = matrix[j][n-i-1]
#왼쪽 90도 회전

for i in range(n):
	for j in range(n):
			rotated_matrix[i][j] = matrix[n-j-1][j]
#오른쪽 90도 회전

#[n-i-1] == 길이 - 인덱스 - 1 (인덱스처럼 만들기 위해 -1)
```

### 무식하게 풀기(Brute-force)

: 가장 원시적으로 푸는 방식, 전부 다 해보는 방식, 가장 단순한 풀이 기법, 효율성은 낮음

: 모든 경우의 수를 탐색해서 문제를 해결하는 방식

```python
#예시 백준 블랙잭
for i in range(n - 2):
	for j in range(i + 1, n - 1):
		for k in range(j + 1, n):
			total = cards[i] + cards[j] + cards[k]

			if max_total < total <= m:
				max_total = total
			if total == m:
				max_total = total
```

### 델타 탐색(Delta Search)

: (0,0)에서부터 이차원 리스트의 모든 원소를 순회하며 각 지점에서 상하좌우에 위치한 다른 지점을 조회, 이동 하는 방식

델타 설정 > 델타 순회 > 경계값 확인

```python
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]
#행을 X로 열을 y로 표현

for i in range(4)
	nx = x + dx[i]
	ny = y + dy[i]

#범위를 벗어나지 않으면 갱신
if 0 <= nx < 3 and 0 <= ny < 3:
	x = nx
	y = ny
print(x, y)

#--------------

delta = [(-1, 0), (0, 1), (1, 0), (0, -1)]
#파이썬에서만 가능한 방식 - 튜플 더하기
# (x, y) = (1, 3) + (4, 5) >> 가능

for i in range(4):
	for j in range(4):
		for d in delta:
			print(i + d[0], j + d[1])
			nx = x + d[0]
```

## 그래프의 표현

-   인접 행렬(Adjacent matrix): 두 정점을 연결하는 간선이 없으면 0 있으면 1을 가지는 행렬로 표현

    ```python
    n = 5 #정점 개수
    m = 5 #간선 개수

    graph = [[0] * n for _ in range(n)]

    for _ in range(m):
    	v1, v2 = map(int, input().split())
    	graph[v1][v2] = 1
    	graph[v2][v1] = 1

    ```

-   인접 리스트(Adjecent list): 리스트를 통해 각 정점에 대한 인점 정접들을 순차적으로 표현(딕셔너리, 리스트)

    ```python
    n = 5 #정점 개수
    m = 5 #간선 개수

    graph = [[] for _ in range(n)]

    for _ in range(m):
        v1, v2 = map(int, input().split())
        graph[v1].append(v2)
        graph[v2].append(v1)

    ```

### DFS 동작 과정

DFS하기 전 탐색을 위한 그래프가 필요함 > 그래프는 인접 행렬 or 인접 리스트로 표현 가능

각 정점을 방문했는지 여부 판별할 체크 리스트 필요 > visited 리스트 생성하여 기본값 False로 놓고 각 정점의 방문 여부를 체크

DFS 사이클

-   현재 정점 방문 처리
-   인접한 모든 정점 확인
-   방문하지 않은 인접 정점으로 이동

<반복문을 이용한 DFS>

```python
visited = [False] * n

def dfs(startV):
	stack = [startV]
	visited[startV] = True

	while stack:
		cur = stack.pop()

		for adj in graph[cur]:
			if not visited[adj]:
				visited[adj] = True
				stack.append(adj)
```
