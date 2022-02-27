---
layout: post
title: input()과 sys.stdin.readline()의 차이
categories: Python Algorithm
tags: Python Algorithm
---
​	코딩 테스트에 있어서, 반복문으로 입력을 여러줄 받아야하는 경우 단순히 input()을 이용하면 시간 초과가 발생할 수 있다.

따라서 입력을 빠르게 받기위한 방법으로 sys.stdin.readline()을 이용한다. 아래 문제를 참고해보도록 하자.

![img](https://k.kakaocdn.net/dn/ddxkR1/btrmnneW6Sv/FxvXGiQEaAKL1Fc7RfF381/img.png)

​	위의 문제에서 볼 수 있는 것처럼 여러 줄의 입력을 받아야하는 경우, input()을 이용하지 말고 sys.stdin.readline() 함수를 이용하도록 해보자.

```python
import sys	# sys 라이브러리 import
n = int(input())
for i in range(n):
  a, b = map(int, sys.stdin.readline().split())
  print(a+b)
```

혹은 다음과 같은 방식으로 input을 sys.stdin.readline으로 새롭게 정의하여 input을 계속 이용해도 된다.

```python
import sys
input = sys.stdin.readline
n = int(input())
for i in range(n):
  a, b = map(int, input().split())
  print(a+b)
```

​	그런데 한가지 주의해야할 것은, sys.stdin.readline을 이용할 때 개행문자('\n')도 함께 포함되어 입력되기 때문에 만약 개행문자를 없애야 하는 상황이라면 sys.stdin.readline().rstrip()을 이용하여 개행문자를 없애도록 해야한다. 위의 예에서는 int 형으로 변경하는 과정에서 개행문자가 없어지기 때문에 따로 rstrip을 해주지 않아도 된다. 하지만 다음과 같이 문자열을 받아오는 경우에는 주의하도록 하자.

<img width="573" alt="스크린샷 2022-02-27 오후 8 24 42" src="https://user-images.githubusercontent.com/96689787/155880502-cd956262-8727-4116-b303-80f2c8524cfc.png" style="zoom:50%;"/>

위와 같은 입력을 2차원 리스트로 받아오기 위해서 다음과 같이 코드를 작성할 수 있다.

```python
from sys import stdin
input = stdin.readline

n, m = map(int, input().split())
Board = [list(input().rstrip()) for _ in range(n)]
#result = [['#', '#', '#', '#', '#'], ['#', '.', '.', 'B', '#'], ['#', '.', '#', '.', '#'], ['#', 'R', 'O', '.', '#'], ['#', '#', '#', '#', '#']]
```

하지만 만약 여기서 rstrip을 쓰지 않았다면 다음과 같은 결과가 나온다.

```python
from sys import stdin
input = stdin.readline

n, m = map(int, input().split())
Board = [list(input()) for _ in range(n)]
#result = [['#', '#', '#', '#', '#', '\n'], ['#', '.', '.', 'B', '#', '\n'], ['#', '.', '#', '.', '#', '\n'], ['#', 'R', 'O', '.', '#', '\n'], ['#', '#', '#', '#', '#', '\n']]
```

따라서, 만약 sys.stdin.readline을 이용하게 된다면 개행문자 꼭 고려해야 한다.
