---
layout: post
title:  "백준_1463"
type: "DP"
algorithm: true
text: true
date:   2021-04-15
author: "Jiwoo Lee"
comments: true
---

<br><br>
<hr>
<font size="2em" color="green">2021.04.15</font>
## 1로 만들기
정수 X에 사용할 수 있는 연산은 다음과 같이 `세 가지` 이다.<br>
1. X가 3으로 나누어 떨어지면, 3으로 나눈다.<br>
2. X가 2로 나누어 떨어지면, 2로 나눈다.<br>
3. 1을 뺀다.<br>

정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다.<br>
연산을 사용하는 횟수의 최솟값을 출력하시오.<br><br>

- 입력 조건<br>
-- 첫째 줄에 1보다 크거나 같고, 10^6보다 작거나 같은 정수 N이 주어진다.<br>

- 출력 조건<br>
-- 첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

<br>

```python
/**
* min(-1한 경우, 2로 나눈 경우, 3으로 나눈 경우) + 1(횟수)
*/

n = int(input())
d = [0,0,1,1]

for i in range(4, n+1):
    d.append(d[i-1]+1)
  
    if i%2 == 0:
        d[i] = min(d[i//2]+1, d[i])
    if i%3 == 0:
        d[i] = min(d[i//3]+1, d[i])

print(d[n])
```
<br>
<hr>
