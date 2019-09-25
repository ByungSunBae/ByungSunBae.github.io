---
layout: post
categories: posts
title: "Cython 사용하기"
tags: [python, cython, basic]
date-string: SETEMBER 25, 2019
---

### Intro

 - 파이썬으로도 속도가 괜찮은 함수를 작성할 수 있으나 한계가 있는 경우가 발생한다.
 - 특히, 병렬 및 분산처리 로직에 맞지 않은 순차적인 로직을 가진 함수가 대표적이다.
 - 그래서 C나 C++로 짜여진 함수를 사용하고 싶을 때가 있는데 이 때 사용할 수 있는 것이 Cython이라는게 있다.
 - Cython의 설명은 위키백과에서 가져왔다.
     + Cython은 CPython 확장 모듈을 손쉽게 생성하도록 고안된 컴파일 언어이다. 
     + 파이썬 문법을 기반으로 C/C++ 루틴을 호출을 위한 외부 함수 인터페이스와 실행 속도 향상을 위한 정적 형 지정 등이 추가된 형태를 하고 있다.
     

### 예제코드

 - 아래 예제코드는 강화학습에서 discounted return를 계산할 때 사용하는 함수이다.
     + http://karpathy.github.io/2016/05/31/rl/ 
     + https://gist.github.com/karpathy/a4166c7fe253700972fcbc77e4ea32c5
 
 - 참조한 URL의 함수를 해당 프로젝트에 맞게 아주 살짝만 고쳐서 사용하다가 조금이라도 성능 향상을 하고 싶어서 Cython을 사용해봤다.
 
 - 코드 작성 및 실행은 Ubuntu 18.04의 Anaconda 환경에서 수행했다.
     
 - 먼저 아래와 같은 코드를 지닌 `.pyx`파일을 생성한다.
     + `.py`가 아닌 `.pyx` 이다.
     + 여기서는 파일이름을 `rl_utils.pyx` 로 지정했다.
     
```python
import numpy as np
cimport numpy as np

DTYPE = np.float32

def compute_distd_r_imp(float[:] x, float gamma=0.99):
    cdef float[:] discounted_r = np.zeros_like(x, dtype=DTYPE)
    cdef float rollings=0.0
    for idx in reversed(range(0, len(x)):
        if x[idx] < 0:
            rollings=0.0
        rollings = rollings * gamma + x[idx]
        discounted_r[idx] = rollings
    return discounted_r
```

 - 그런 다음 `setup.py` 파일을 생성한다.
 
```python
from distutils.core import setup
from Cython.Build import cythonize
import numpy as np

setup(
    ext_modules=cythonize('rl_utils.pyx'),
    include_dirs=[np.get_include()],
)
```

 - 같은 경로에 pyx파일과 setup.py을 같이 두고 터미널에서 아래와 같은 명령어를 실행하면 된다.
     
```bash
python setup.py build_ext --inplace
```

 - 그러면 C코드에 해당하는 rl_utils.c 파일과 build 폴더가 생성이 되는데 이게 바로 pyx파일의 코드를 C코드로 컴파일링한 결과물이다.
 - 파이썬에서는 아래와 같이 불러와서 사용중이다.

```python
...(생략)
from rl_utils import compute_distd_r_imp
...(생략)
distd_r = compute_distd_r_imp(rewards, gamma=gamma).base
```

 - p.s. 추후에 실행결과 및 시간비교한 이미지를 올릴 예정입니다.
