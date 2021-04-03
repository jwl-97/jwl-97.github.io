---
layout: post
title:  "그리디모음"
type: "그리디"
algorithm: true
text: true
date:   2021-04-03
author: "Jiwoo Lee"
comments: true
---

<br><br>
<hr>
<font size="2em" color="green">2021.04.03</font>
## 1. 모험가길드
한 마을에 `모험가가 N명` 있다. 모험가 길드에서는 N명의 모험가를 대상으로 '공포도'를 측정했다. <br>
공포도가  `X인 모험가는 반드시 X명 이상`으로 구성한 모험가 그룹에 참여해야 여행을 떠날 수 있도록 규정했다.<br>
N명의 모험가에 대한 정보가 주어졌을 때, 여행을 떠날 수 있는 그룹 수의 최댓값을 구하는 프로그램을 작성해라.<br>

- 입력 조건<br>
-- 첫째 줄에 모험가의 수 N 이 주어진다. (1 <= N <= 100,000)<br>
--  둘째 줄에 각 모험가의 공포도의 값을 N이하의 자연수로 주어지며, 각 자연수는 공백으로 구분한다.<br>

- 출력 조건<br>
-- 여행을 떠날 수 있는 그룹 수의 최댓값을 출력한다. 

```python
/**
* 최대의 그룹 수는 최소 인원으로 여러 그룹을 만드는 것이 유리하다.
*/

n = int(input())
mList = list(map(int, input().split()))

mList.sort()

groupCount = 0
adventurerCount = 0

for i in mList : 
  adventurerCount += 1
  if adventurerCount >= i :
    groupCount += 1
    adventurerCount = 0

print(groupCount)
```
<br>
<hr>

<font size="2em" color="green">2021.04.03</font>
## 2. 곱하기 혹은 더하기
각 자리의 숫자(0부터 9)로만 이루어진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 <br>
숫자 사이에 'x' 혹은 '+' 연산자를 넣어 결과적으로 만들어질 수 있는 가장 큰 수를 구하는 프로그램을 작성해라. <br>
단, +보다 x를 먼저 계산하는 일반적인 방식과는 달리, 모든 연산은 왼쪽에서부터 순서대로 이루어진다고 가정한다.

- 입력 조건<br>
-- 첫째 줄에 여러 개의 숫자로 구성된 하나의 문자열 S가 주어진다. (1 <= S의 길이 <= 20)<br>

- 출력 조건<br>
-- 첫째 줄에 만들어질 수 있는 가장 큰 수를 출력한다. 

```python
n = input()
result = int(n[0])

for i in range(1, len(n)):
  num = int(n[i])
  if result <= 1 or num <= 1 :
    result += num
  else : 
    result *= num

print(result)
```
<br>
<hr>

<font size="2em" color="green">2021.04.03</font>
## 3. 문자열 뒤집기
다솜이는 0과 1로만 이루어진 문자열 S를 가지고 있다. 주인공은 이 문자열 S에 있는 모든 숫자를 전부 같게 만들려고 한다. <br>
다솜이가 할 수 있는 행동은 S에서 연속된 하나 이상의 숫자를 잡고 모두 뒤집는 것이다. <br>

예를 들어 0001100일 때는 다음과 같다. <br>
전체를 뒤집으면 1110011, <br>
이후 4번째 문자부터 5번째 문자까지 뒤집으면 1111111이 되어서 두 번 만에 모두 같은 숫자로 만들 수 있다. <br>

하지만 처음부터 4번째 문자부터 5번째 문자까지 뒤집으면 모두 0으로 한 번 만에 모두 같은 숫자로 만들 수 있다.  <br>
다솜이가 해야하는 행동의 최소 횟수를 구하여라.

- 입력 조건<br>
-- 첫째 줄에 0과 1로만 이루어진 문자열 S가 주어진다. S의 길이는 100만보다 작다.

- 출력 조건<br>
-- 첫째 줄에 다솜이가 해야 하는 행동의 최소 횟수를 출력한다. 

```python
n = input()

count0 = 0
count1 = 0

if(n[0] == '1'):
  count0 += 1
else :
  count1 += 1

for i in range(len(n)-1):
  if(n[i]!= n[i+1]):
    if n[i+1] == '1' :
      count0 += 1
    else :
      count1 += 1
    
print(min(count0, count1))
```

<br>
<hr>

<font size="2em" color="green">2021.04.03</font>
## 4. 만들 수 없는 금액
동네 편의점의 주인인 동빈이는  N개의 동전을 가지고 있다. <br>
이때 N개의 동전을 이용하여 만들 수 없는 양의 정수 금액 중 최솟값을 구하는 프로그램을 작성해라.<br>
예를 들어, N = 5이고, 동전이 각각 3, 2, 1, 1, 9원이라면 최솟값은 8원이다.<br>
               N = 3이고, 동전이 각각 3, 5, 6원이라면 최솟값은 1원이다.<br>

- 입력 조건<br>
-- 첫째 줄에는 동전의 개수를 나타내는 양의 정수 N이 주어진다.<br>
-- 둘째 줄에는 각 동전의 화폐 단위를 나타내는 N개의 자연수가 주어지며, 각 자연수는 공백으로 구분한다.

- 출력 조건<br>
-- 첫째 줄에 주어진 동전들로 만들 수 없는 양의 정수 금액 중 최솟값을 출력한다. 

```python
n = input()
numList = list(map(int, input().split()))
count = 1
numList.sort()

for i in numList :
  if i > count : 
    break
  count += i

print(count)
```
