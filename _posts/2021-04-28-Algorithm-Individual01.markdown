---
layout: post
title:  "A* (A-star) 알고리즘"
date:   2021-04-28
last_modified_at: 2021-04-28
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

**파이썬을 이용한 A* 알고리즘 구현**

<br/>

```python
class Node:
    def __init__(self, parent=None, Position=None):
        self.parent = parent    # 이전 노드
        self.position = position    # 현재 위치
        
        self.f = 0
        self.g = 0
        self.h = 0
```

<br/>

F=G+H

- F = 출발지점에서 목적지까지의 총 cost 합
- G = 현재 노드에서 출발 지점까지의 총 cost 합
- H = Heuristic, 현재 노드에서 목적지까지의 추정 거리

<br/>

G(x)

G = 현재 노드에서 출발 지점까지의 총 cost , 현재 노드 = node(2), 출발 지점에서 2 cost만큼 떨어져 있다.
(parent 노드는 당연히 node(1)) 따라서, 현재 노드(2)는 아래와 같이 표현된다.

```python
node(2).g = 2
```

<br/>

H(x)

H = Heuristic, 현재 노드에서 목적지까지의 추정 거리

현재 노드 = node(2)에서 목적지까지의 거리를 추정해보자 (현재 노드부터 1이라고 가정)

5 cost만큼 오른쪽으로 가서, 위로 3 cost만큼 가면 목적지 노드가 있다.

node(2).h = 5^2 + 3^2 = 34 (피타고라스)

<br/>

```python
def heuristic(node, goal, D=1, D2=2 ** 0.5):
    dx = abs(node.position[0] - goal.position[0])
    dy = abs(node.position[1] - goal.position[1])
    return D * (dx + dy) + (D2 - 2 * D) * min(dx, dy)
    
...
child.h = heuristic(child, endNode)
...
```

<br/>

F(x)

F = 출발 지점에서 목적지까지의 총 cost 합. 이제 현재 노드 (node(2))의 G값과 H값을 더해보면,
node(2).f = node(2).g + node(2).h = 2+34 = 36

<br/>

의사코드

```python
/* A* 특징
1. openList와 closeList라는 보조 데이터를 사용한다.
2. F = G + H 를 매번 노드를 생성할 때마다 계산한다.
3. openList에는 현재 노드에서 갈 수 있는 노드를 전부 추가해서 F,G,H를 계산한다.
    openList에 중복된 노드가 있다면, F값이 제일 작은 노드로 바꾼다.
    
4. closeList에는 openList에서 F값이 가장 작은 노드를 추가시킨다.
*/

openList.add(startNode)  # openList는 시작 노드로 init

while openList is not empty:
    # 현재 노드 = openList에서 F 값 가장 작은 것
    currentNode <- node in openList having the lowest F value
    openList.remove(currentNode)  # openList에서 현재 노드 제거
    closeList.add(currentNode)  # closeList에 현재 노드 추가
    
    if goalNode is currentNode:
        currentNode.parent.position 계속 추가 후
        경로 출력 후 종료
        
    children <- currentNode와 인접한 모든 노드 추가
    
    for each child in children:
        if child in closeList:
            continue
        
        child.g = currentNode.g + child와 currentNode 거리(1)
        child.h = child와 목적지까지의 거리
        child.f = child.g + child.h
        
        # child가 openList에 있고, child의 g 값이 openList에 중복된 노드 g값과 같으면
        # 다른 자식 불러오기
        if child in openList and child.g > openNode.g in openList:
            continue
            
        openList.add(child)
```

<br/>

파이썬 코드

```python
# Time Complexity는 H에 따라 다르다.
# O(b^d), where d = depth, b = 각 노드의 하위 요소 수
# heapque를 이용하면 길을 출력할 때 reverse를 안해도 됨

class Node:
    def __init__(self, parent=None, position=None):
        self.parent = parent
        self.position = position

        self.g = 0
        self.h = 0
        self.f = 0

    def __eq__(self, other):
        return self.position == other.position

def heuristic(node, goal, D=1, D2=2 ** 0.5):  # Diagonal Distance
    dx = abs(node.position[0] - goal.position[0])
    dy = abs(node.position[1] - goal.position[1])
    return D * (dx + dy) + (D2 - 2 * D) * min(dx, dy)


def aStar(maze, start, end):
    # startNode와 endNode 초기화
    startNode = Node(None, start)
    endNode = Node(None, end)

    # openList, closedList 초기화
    openList = []
    closedList = []

    # openList에 시작 노드 추가
    openList.append(startNode)

    # endNode를 찾을 때까지 실행
    while openList:

        # 현재 노드 지정
        currentNode = openList[0]
        currentIdx = 0

        # 이미 같은 노드가 openList에 있고, f 값이 더 크면
        # currentNode를 openList안에 있는 값으로 교체
        for index, item in enumerate(openList):
            if item.f < currentNode.f:
                currentNode = item
                currentIdx = index

        # openList에서 제거하고 closedList에 추가
        openList.pop(currentIdx)
        closedList.append(currentNode)

        # 현재 노드가 목적지면 current.position 추가하고
        # current의 부모로 이동
        if currentNode == endNode:
            path = []
            current = currentNode
            while current is not None:
                # maze 길을 표시하려면 주석 해제
                # x, y = current.position
                # maze[x][y] = 7 
                path.append(current.position)
                current = current.parent
            return path[::-1]  # reverse

        children = []
        # 인접한 xy좌표 전부
        for newPosition in [(0, -1), (0, 1), (-1, 0), (1, 0), (-1, -1), (-1, 1), (1, -1), (1, 1)]:

            # 노드 위치 업데이트
            nodePosition = (
                currentNode.position[0] + newPosition[0],  # X
                currentNode.position[1] + newPosition[1])  # Y
                
            # 미로 maze index 범위 안에 있어야함
            within_range_criteria = [
                nodePosition[0] > (len(maze) - 1),
                nodePosition[0] < 0,
                nodePosition[1] > (len(maze[len(maze) - 1]) - 1),
                nodePosition[1] < 0,
            ]

            if any(within_range_criteria):  # 하나라도 true면 범위 밖임
                continue

            # 장애물이 있으면 다른 위치 불러오기
            if maze[nodePosition[0]][nodePosition[1]] != 0:
                continue

            new_node = Node(currentNode, nodePosition)
            children.append(new_node)

        # 자식들 모두 loop
        for child in children:

            # 자식이 closedList에 있으면 continue
            if child in closedList:
                continue

            # f, g, h값 업데이트
            child.g = currentNode.g + 1
            child.h = ((child.position[0] - endNode.position[0]) **
                       2) + ((child.position[1] - endNode.position[1]) ** 2)
            # child.h = heuristic(child, endNode) 다른 휴리스틱
            # print("position:", child.position) 거리 추정 값 보기
            # print("from child to goal:", child.h)
            
            child.f = child.g + child.h

            # 자식이 openList에 있으고, g값이 더 크면 continue
            if len([openNode for openNode in openList
                    if child == openNode and child.g > openNode.g]) > 0:
                continue
                    
            openList.append(child)


def main():
    # 1은 장애물
    maze = [[0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]

    start = (0, 0)
    end = (7, 6)

    path = aStar(maze, start, end)
    print(path)


if __name__ == '__main__':
    main()
    # [(0, 0), (1, 1), (2, 2), (3, 3), (4, 3), (5, 4), (6, 5), (7, 6)]
```

<br/>

출처

[A-star 알고리즘 설명](https://choiseokwon.tistory.com/210)