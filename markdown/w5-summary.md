# 5주차 summary

## 알고리즘 -2

### 스택

: 데이터를 한쪽에서만 넣고 빼는 자료구조, LIFO(Last in First out, 후입선출) 방식

-   push, pop
-   뒤집기, 되돌리기, 되돌아가기
-   마무리 되지 않은 일을 임시 저장 (괄호 매칭, 함수 호출, 백트래킹, DFS깊이 우선 탐색)
-   파이썬은 리스트로 스택을 간편하게 사용할 수 있음 (append, pop)

### 큐

:한 쪽 끝에서 데이터를 넣고 다른 한 쪽에서만 데이터를 뺄 수 있는 자료구조, FIFO (First in First out, 선입선출) 방식

-   dequeue, enqueue
-   덱 (Deque, Double-Ended Queue) 자료구조: 양 방향 삽입, 삭제가 자유로운 큐
    -   양방향 삽입, 추출이 모두 큐보다 빠름(appendleft, popleft, append, pop)
    -   데이터의 삽입, 추출이 많을 때 시간 단축 가능

### 힙(Heap)

우선순위 큐: 순서가 아닌 우선순위 기준으로 우선순위가 높은 데이터가 먼저 나감

우선순위 큐를 구현하는 하나의 방법으로써의 힙

힙의 시간복잡도: O(logN)

힙의 특징

-   최대값, 최소값을 빠르게 찾아내도록 만들어진 데이터 구조
-   완전 이진 트리의 형태로 느슨한 정렬 상태를 지속적으로 유지
-   힙 트리에서는 중복 값을 허용

파이썬 heapq 모듈

-   Minheap(최소 힙)으로 구현되어 있음 (가장 작은 값이 먼저 옴)
-   삽입, 삭제, 수정, 조회 연산의 속도가 리스트보다 빠르다.

메서드

-   heapq.heapify(): heap으로 만들기
-   heapq.heappop(heap): heap의 가장 앞의 값(최소값)을 제거
-   heapq.heappush(heap, value): heap에 해당 값이 최소값이면 가장 앞에 추가, 아니면 다른곳에 추가(명확하게는 랜덤배치는 아님 - 트리구조)

### 셋 (set)

셋은 수학에서의 집합을 나타내는 데이터 구조로 python에서는 기본적으로 내장되어 있음

셋의 연산: add(), remove(), +, -, &, ^

셋의 사용 케이스

-   데이터의 중복이 없어야 할 때 (고유값들로 이뤄진 데이터가 필요할 때)
-   정수가 아닌 데이터의 삽입, 삭제, 탐색이 빈번히 필요할 때

### 이차원 리스트

이차원 리스트: 리스트를 원소로 가지는 리스트 _(2차원으로 펼쳐서 생각하는게 중요)_

```python
matrix = [
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9]
]
```

### 특정 값으로 초기화 된 이차원 리스트 만들기

-   반복문으로 작성 1

```python
#100 X 100 이차원 리스트 만들기
matrix = []

for _ in range(100):
	matrix.append([0] * 100) # => [0,0,0, ...0] 원소 100개의 리스트
#pprint 쓰면 이차원 리스트를 편하게 볼 수 있음
```

-   반복문으로 작성 2

```python
n = 4 #행
m = 3 #열

matrix = []

for _ in range(n):
	matrix.append([0] * m)
```

-   리스트 컴프리헨션으로 작성

```python
matrix = [[0] * 10 for _ in range(10)]

n = 4
m = 3
matrix = [[0] * m for _ in range(n)] #각각 다른 요소m개 * n

matrix2 = [[0] * m] * n # 위의 이차원 리스트와 다름 이건 같은 요소m * n
matrix2[0][0] = 1 #따라서 이렇게 하게 되면 모든 행의 첫 요소가 1로 변경 됨
```

### 행렬 입력 받기

```python
# 3*3 입력받기
matrix = [list(map(int, input().split()) for _ in range(3)]

n, m = map(int, input().split())
matrix = [list(map(int, input().split()) for _ in range(n)]

```

### 순회

-   인덱스를 통해 각각 출력
-   이중 for 문을 이용한 행 우선 순회 & 열 우선 순회

```python
matrix = [
	[1, 2, 3, 4],
	[5, 6, 7, 8],
	[9, 0, 1, 2],
]

for i in range(3):
	for j in range(4)
		print(matrix[i][j], end='')
	print()

for i in range(4):
	for j in range(3)
		print(matrix[j][i], end='')
	print()

#총합 구하기
total = sum(map(sum, matrix))

```

## 전치

전치 행렬: 기존 행렬의 행과 열을 맞바꾸는 것

열 우선 순회 = 전치
