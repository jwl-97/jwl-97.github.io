---
layout: post
title:  "백준_9095"
type: "DP"
algorithm: true
text: true
date:   2021-04-22
author: "Jiwoo Lee"
comments: true
---

<br><br>
<hr>
<font size="2em" color="green">2021.04.22</font>
## 1, 2, 3 더하기
정수 4를 1, 2, 3의 합으로 나타내는 방법은 총 7가지가 있다. 합을 나타낼 때는 수를 1개 이상 사용해야 한다.<br>
1+1+1+1<br>
1+1+2<br>
1+2+1<br>
2+1+1<br>
2+2<br>
1+3<br>
3+1<br>

정수 n이 주어졌을 때, n을 1, 2, 3의 합으로 나타내는 방법의 수를 구하는 프로그램을 작성하시오.<br><br>

- 입력 조건<br>
-- 첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 정수 n이 주어진다. n은 양수이며 11보다 작다.<br>

- 출력 조건<br>
-- 각 테스트 케이스마다, n을 1, 2, 3의 합으로 나타내는 방법의 수를 출력한다.

<br>

```python
/**
* n = 1     1    
*     2     2    
*     3     4
*     4     7
*
* d[n] = d[n-3] + d[n-2] + d[n-1]
*/

T = int(input())

d = [1, 2, 4]

for i in range (3, 10):
  d.append(d[i-3] + d[i-2] + d[i-1])

for i in range(T):
  n = int(input())
  print(d[n-1])
```
<br>
<hr>
