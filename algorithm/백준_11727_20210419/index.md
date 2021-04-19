---
layout: post
title:  "백준_11727"
type: "DP"
algorithm: true
text: true
date:   2021-04-19
author: "Jiwoo Lee"
comments: true
---

<br><br>
<hr>
<font size="2em" color="green">2021.04.19</font>
## 2×n 타일링 2
2×n 직사각형을 1×2, 2×1과 2×2 타일로 채우는 방법의 수를 구하는 프로그램을 작성하시오.<br><br>

- 입력 조건<br>
-- 첫째 줄에 n이 주어진다.<br>

- 출력 조건<br>
-- 첫째 줄에 2×n 크기의 직사각형을 채우는 방법의 수를 10,007로 나눈 나머지를 출력한다.

<br>

```python
/**
* n = 1     1     |
*     2     3     || , =, ㅁ
*     3     5     |||, =|, |=, ㅁ|, |ㅁ
*     4     11    ||||, ||=, |=|, =||, ==, ||ㅁ, |ㅁ|, ㅁ||, ㅁㅁ, ㅁ=, =ㅁ
*
* d[n] = d[n-2] * 2 + d[n-1]
*/

n = int(input())

d = [1, 3, 5]

for i in range(3, n):
  d.append(d[i-2] * 2 + d[i-1])

print(d[n-1] % 10007)
```
<br>
<hr>
