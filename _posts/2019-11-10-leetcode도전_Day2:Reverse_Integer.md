---
layout: post
categories: posts
title: "LeetCode 도전 Day2 : Reverse Integer"
tags: [python, leetcode]
date-string: Nobember 11, 2019
---

## Reverse Integer 문제
 - 32-bit의 부호가 있는 정수가 주어져있을때, 순서가 역순인 정수를 출력하는 함수를 만들어야한다.
     + 123이 들어오면, 321이라는 정수를 return하면 된다.
 
 - 32-bit라는 제한은 범위가 $[-2^{31}, 2^{31}-1]$ 인 숫자를 다룬다는 의미로, 결과값이 해당 범위를 벗어나는 경우 0으로 return하게 한다.
 
 - 음수가 들어오는 경우 음수는 그대로 붙인채 숫자의 순서가 역순이기만 하면된다.
     + -123이 들어오면, -321이라는 정수를 return하면 된다.
 
 - 0이 맨뒤에 있는 경우 역순으로 바꿀시 0은 제외한 나머지 숫자만 역순으로 있으면 된다.
     + 120이 들어오면, 21이라는 정수를 return하면 된다.


### 생각의 과정
 - 사용한 언어는 파이썬을 이용했으며, 어떻게하면 간단한 코드로 풀 수 있을지 생각해봤다.

 - 숫자의 제한에 걸리지만 않으면 상관없으니, 아래와 같이 심플하게 생각했다.
     + string으로 처리하면 되지않을까?

 - 파이썬에서는 string은 iterable하기 때문에 이를 이용하여 숫자를 역순으로 join시키면 될거라고 생각했다.
 
 - 출력은 integer로 해야하니 결과값은 int를 씌워서 정수로 만들면 될 것이고, 음수인 경우에는 '-'부호를 붙이면 된다.
 
 - 제한사항을 고려하여 아래와 같이 코드를 작성했다.

### Code
 
```python

class Solution:
    def reverse(self, x:int) -> int:
        if x <= 2**31 - 1 and x >= -2**31:
            if x > 0:
                res = int(''.join([i for i in reversed(str(x))]))
            else:
                res = -int(''.join([i for i in reversed(str(x)) if i.isdigit()]))
            if res <= 2**31 - 1 and res >= -2**31:
                return res
            else:
                return 0

```

 - 코드를 한줄한줄 줄이려다보니 보기가 어려운 코드가 작성되었다.
 - 위 코드는 제출용으로 냈던 것이니 아래와 같이 읽기 쉽도록 풀어서 작성했다.

```python

class Solution:
    def reverse(self, x:int) -> int:
        if x <= 2**31 - 1 and x >= -2**31:
            res = ''
            for i in reversed(str(x)):
                if i.isdigit():
                    res += i
            res = int(res)
            if x < 0:
                res = -1 * res
            if res <= 2**31 - 1 and res >= -2**31:
                return res
            else:
                return 0
```

 - 우선 32-bit에 해당하는지 if문을 이용하여 확인했다.
 - 32-bit 정수에 해당하면 아무것도 없는 string을 할당 후 for문을 이용하여 숫자를 차례대로 붙인다.
     + 이 때, reversed를 이용하여 숫자가 역순으로 들어오도록한다.
     + 그리고 음수인 경우 '-'부호가 string으로 되어 마지막에 붙여질수 있기때문에 string method인 isdigit을 통해 string값이 숫자인지아닌지 확인하여 숫자인 경우에만 붙인다.
 - 정수로 바꿔준다음 기존값이 음수면 -1을 곱한다.
 - 마지막으로 32-bit에 해당하는지 확인 후 해당하면 결과값을 return하고 그렇지않으면 0을 return한다.

 - 해당 코드가 꼭 정답이라는 법은 없으며, 다른 방식도 존재한다.
 - 다른 방식으로는 어떻게 풀수 있을지 고민하는 것도 좋을 것 같다.

### 참고
 - https://leetcode.com/articles/reverse-integer/
