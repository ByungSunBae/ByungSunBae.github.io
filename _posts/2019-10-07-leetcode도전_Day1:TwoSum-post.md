---
layout: post
categories: posts
title: "LeetCode 도전 Day1 : TwoSum"
tags: [python, leetcode]
date-string: October 7, 2019
---

### Intro
 - 코딩실력을 늘려보고자 1일 1코딩을 해보자는 마음으로 구글링을 하던중 leetcode라는 사이트를 발견했다.

 - 해당 사이트에서는 여러가지 알고리즘 및 인터뷰에 나올법한 문제들을 제공해준다.

 - 이 중에서 Top 100 Liked Questions 를 하루에 1개씩 풀어보려고한다.
     + https://leetcode.com/problemset/top-100-liked-questions/


### TwoSum 문제
 - 1번문제로 TwoSum 문제가 있다.

 - 이 문제는 여러개의 정수(int)값을 가지는 리스트와 target이라 하는 값을 input으로 집어넣으면 target을 구하기 위해 필요한 정수값의 index를 출력하도록 해야한다.
 
  - 단, target을 구하기 위해 1개의 정수값을 여러번 사용할 수 없고 정확하게 1개의 솔루션만 가진다는 제약조건이 걸려있다.
 
  - 난이도는 easy라고 써있었는데 생각보다 easy하지 않았다.
 

### 환경
 - os 및 스펙관련 환경은 제외하고, 사용한 언어는 파이썬3 이다.
 
### 풀이과정
 - 처음에는 아래와 같이 풀었다.
 
```python
from typing import List
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        result = []
        for i in range(len(nums)):
            for j in range(len(nums)):
                if i >= j:
                    next
                else:
                    if nums[i]+nums[j] == target:
                        result += [i,j]
                        break
                    else:
                        next
            if len(result) > 0:
                break
        if len(result) > 0:
            return result
        else:
            print("Nothing Solution.")
            return None
```

 - 단순한 방법으로는 nums 리스트안의 모든 요소들을 훑어가면서 솔루션을 찾아가는 방식이다.
 - 코드가 많이 더러운건 둘째치고, 최악의 경우 $O(n^2)$ 만큼의 복잡도를 가지기 때문에 리스트의 길이가 길어질수록 시간이 오래 걸리게 된다.
 - 실제로 leetcode에서 해당 코드를 제출했을때, 길이가 10000이상의 리스트를 가지고도 테스팅한다.
 - 여기서 Time Limted 로 인해 통과하지 못했다.
 
 - 그래서 단순히 숫자의 조합을 일일히 훑는것보다 더 적은 복잡도를 가지는 방법을 찾아야한다.
 - 아래는 고민한 끝에 생각해낸 접근법을 코드로 표현한 것이다.
 
```python

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        result = []
        for number in nums:
            res = target - number
            try:
                result += [nums.index(res)]
                if res == number:
                    result += [[i for i, k in enumerate(nums) if k == number][1]]
                else:
                    result += [nums.index(number)]
            except:
                result = []
                next
            finally:
                if len(result) == 2:
                    break
        return result
```

 - target은 nums내 2개의 정수합으로 이루어진 값이다.
 - 이에 착안하여 nums의 숫자들중 한개를 target에서 빼면 남는 숫자가 있다.
 - 이 숫자가 nums안에 있으면 그 숫자의 index를 추출하면 되는 것이다.
 - 만일 없으면 다른 숫자로 다시 시도하면 된다.
 - 이 접근법은 숫자의 조합을 전부 훑는 방식은 아니기 때문에 복잡도가 최악이라해도 $O(n)$정도밖에 안된다.
 - 해당 코드를 제출하니 다행히 통과가 되었다.
 - 정답을 살펴보니 필자가 생각했던 방식과 동일한 컨셉이 있었고, 또 하나는 hashing을 이용하는 방법이 있다.
 - hashing을 사용하는 방법은 다음에 따로 다뤄보도록하겠다.
