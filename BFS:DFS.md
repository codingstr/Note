# 그래프의 표현 방식

<img src="/Users/family/Documents/coding/Alorithm/Note/images/BFS:DFS 1.png" alt="BFS:DFS 1" style="zoom: 25%;" />

**인접 행렬 Adjacency Matrix**

* 2차원 배열에 각 노드가 연결된 형태를 기록함

* 연결되지 않은 노드끼리의 비용은 무한의 비용이라고 작성함. 실제 코드에서는 999999999등의 값으로 초기화함

* 모든 관계를 저장하므로 노드 개수가 많을수록 메모리가 낭비됨

* 특정한 노드가 연결되어 있는지에 대한 정보를 얻는 속도가 비교적 빠름

* ex )

  ```python
  INF = 999999999
  graph = [
  	[0, 7, 5],
  	[7, 0, INF],
  	[5, INF, 0]
  ]
  ```

**인접 리스트 Adjacency LIst**

- 모든 노드에 연결된 노드에 대한 정보를 차례대로 연결하여 저장함
- 연결된 정보만을 저장하기 때문에 메모리를 효율적으로 사용함
- 특정한 노드가 연결되어 있는지에 대한 정보를 얻는 속도가 비교적 느림
- ex )

```python
graph = [[] for _ in range(3)]
graph[0].append((1, 7))
graph[0].append((2, 5))
graph[1].append((0, 7))
graph[2].append(0, 5)
# graph == [ [ (1, 7), (2, 5) ], [ (0, 7) ], [ (0, 5) ] ]
```



# DFS : Depth First Search / 깊이 우선 탐색

<img src="/Users/family/Documents/coding/Alorithm/Note/images/BFS:DFS 2.png" alt="BFS:DFS 2" style="zoom: 25%;" />

 ### DFS의 동작 과정

```css
1. 탐색 시작 노드를 스택에 삽입, 방문 처리
2. 스택 최상단 노드의 방문하지 않은 인접 노드를 스택에 삽입, 방문 처리. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 제거
3. 2.를 수행할 수 없을 때까지 반복
```

* 1 → 2 → 7 → 6 → 8 → 3 → 4 → 5
* 스택 자료구조에 기초함
* 구현 시에는 재귀함수를 이용해 구현
* O(N)

### DFS 예제

```python
def dfs(graph, v, visited) :
     # 현재 노드를 방문 처리
     visited[v] = True
     print(v, end=' ')
     # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
     for i in graph[v] :
         if not visited[i] :
             dfs(graph, i, visited)

# 각 노드가 연결된 정보를 2차원 리스트 자료형으로 표현
graph = [
    [], 
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]
# 각 노드가 방문된 정보를 리스트 자료형으로 표현
visited = [False]*9
# 정의된 DFS 함수 호출
dfs(graph, 1, visited)
```



# BFS : Breadth First Search / 너비 우선 탐색

<img src="/Users/family/Documents/coding/Alorithm/Note/images/BFS:DFS 2.png" alt="BFS:DFS 2" style="zoom: 25%;" />

### BFS의 동작 과정

```css
1. 탐색 시작 노드를 큐에 삽입, 방문 처리
2. 큐에서 노드를 꺼내 방문하지 않은 인접 노드를 모두 큐에 삽입, 방문 처리
3. 2.를 수행할 수 없을 때까지 반복
```

- 1 → 2 → 3 → 7 → 4 → 5 → 6 → 8
- 큐 자료구조에 기초함
- 구현 시에는 deque 라이브러리를 이용해 구현
- O(N)

### BFS 예제

```python
from collections import deque

def bfs(graph, start, visited) :
    queue = deque([start])
    visited[start] = True
    # queue가 빌 때까지 반복
    while queue :
        # pop
        v = queue.popleft()
        print(v, end = ' ')
        # 인접한 모든 노드 방문 처리
        for i in graph[v] :
            if not visited[i] :
                queue.append(i)
                visited[i] = True

# 각 노드가 연결된 정보를 2차원 리스트 자료형으로 표현
graph = [
    [], 
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

visited = [False]*9
bfs(graph, 1, visited)
```

|      |   DFS    |     BFS     |
| :--: | :------: | :---------: |
| 원리 |   스택   |     큐      |
| 구현 | 재귀함수 | 큐 자료구조 |

