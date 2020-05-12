회사에서 요즘 코드 정리하는 태스크에 집중하고 있는데 작성되어 있는 Python코드가 카오스 그 자체라 다시한 번 깔끔한 코드를 작성하는 것이 얼마나 중요한 것인가를 깨닫고 무엇을 하면 안되는지 메모했다.

# 참고하면 좋은 사이트

-   [PEP 8 -- Style Guide for Python Code](python.org/dev/peps/pep-0008/)
    
-   [typing — Support for type hints](https://docs.python.org/3/library/typing.html)
    
-   [Difference between _, \__ and **xx** in Python](http://igorsobreira.com/2010/09/16/difference-between-one-underline-and-two-underlines-in-python.html)
    
-   [Why you should be using pathlib](https://treyhunner.com/2018/12/why-you-should-be-using-pathlib/)
    

# Python에는 문법만큼 지켜야 하는 작성규칙이 있다

### 개행

-   import는 가능한 한 최상단에서만 이루어져야 한다
-   import아래에 바로 함수 혹은 클래스가 나온다면 2줄 개행하고 변수가 나온다면 1줄 개행한다

```python
import os
import sys


def do_sth():
    raise NotImplementError

```

-   클래스 내부는 1줄 개행한다

```python
class Example: 
    def __init__(self):
        raise NotImplementError

    def do_sth(self):
        raise NotImplementError

```

-   클래스 외부에서는 2줄 개행한다

```python
def do_sth1():
    raise NotImplementError


def do_sth2():
    raise NotImplementError

```

-   동일 스크립트 내에서 작성한 클래스 혹은 함수를 실행하기 위해 하단부에 적는 실행 코드는 main 내부에 있어야 한다
    -   main위로 2줄 개행한다

```python
if __name__ == '__main__':
    ...

```

-   스크립트 마지막에 1줄 개행한다
    
    -   한 줄은 너무 길면 안되고 중간에 개행해야 한다(정식으로는 79자로 제한하고 있다)
        

-   연산자로 이어진 긴 코드라면 연산자 직전에 개행해야 한다

```python
income = (gross_wages
        + taxable_interest
        + (dividends - qualified_dividends)
        - ira_deduction
        - student_loan_interest)
```

-   if문이나 for문의 처리는 무조건 개행해서 적어야 한다
    
    -   원라이너로 적고 싶다고 한 줄에 다 적어버리면 안된다

```python
if arg == "arg":
    return True
```

### 들여쓰기

-   코드 옆에 코멘트를 작성할 때에는 2번 띄고 #를 적고 1번 띈 다음에 내용을 적는다
    -   새 라인에 코멘트를 적는다면 #뒤에 1번만 띄어쓰면 되지만 indent를 맞춰야 한다

```python
# do_sonthing function
def do_sth():
    # pass
    pass  # do_something

```

-   Python은 indent가 중요한 언어이기 때문에 스페이스든 탭이든 통일해서 제대로 맞춰준다
    -   하나의 indent는 스페이스 4번이다

### import

-   같은 라이브러리 혹은 모듈에서 import하는 것이 아닌 이상 개행한다

```python
import os
import sys
from pathlib import Path
from datetime import timedelta, timezone, datetime

import tqdm
from tqdm.notebook import tqdm
```

-   작업하고 있는 디렉토리를 모듈로서 import해 사용하고 싶다면 `__init__.py`를 만들어 import가능한 클래스 혹은 함수를 import해 놓는다
    -   같은 디렉토리의 다른 스크립트를 import하고 싶은 거라면 앞에 `.`을 찍어야 한다
    -   다른 디렉토리의 스크립트를 import하고 싶은 거라면 그 경로를 지정해줘야 한다

```python
# directory_name: my_module
# file_name: my_file
# function_name: my_function
# __init__.py

from .my_file import my_function
```

```python
# directory_name: another_module
# function_name: another_function
# in another_module/another_file

from my_module.my_file import my_function
```

### 이름

-   이름을 정하지 않는 argument는 보통 arg라 적는다
    -   마찬가지로 keyargument는 kwarg라 적는다

```python
def my_func(arg, kwarg=None):
    print(arg)
    pring(kwarg)
```

```python
def my_func(some_arg, *args):
    print(some_arg)

    for arg in args:
        print(arg)
```

-   클래스 이름이 아닌 이상 전부 소문자 snake case로 명명한다
    -   클래스 이름은 대문자로 시작하는 camel case로 명명한다

```python
class MyClass:
    def __init__(self, arg):
        self.arg = arg

    def print_arg():
        print(self.arg)
```

-   메서드 이름은 절대 변수 이름으로 사용해선 안된다

```python
obj = object(some_arg)
dictionary = dict(some_arg)
some_list = list(some_arg)
```

-   클래스 내부 메서드가 private이라면 이름 앞에 `_`을 붙인다
-   Python의 빌트인기능을 사용해 그 값을 반환하는 메서드라면 `__`로 감싸서 호출한다

```python
class CrazyNumber(object):

    def __init__(self, n):
        self.n = n

    def __add__(self, other):
        return self.n - other

    def __sub__(self, other):
        return self.n + other

    def __str__(self):
        return str(self.n)
```

### 띄어쓰기

-   kwarg에 값을 적을 때에는 `=` 좌우로 띄어쓰면 안된다
    -   일반 파라미터는 `=` 좌우로 띄어써야 한다

```python
def some_kwarg(kwarg=True):
    if kwarg:
        print("True")
    else:
        print("False")


if __name__ == '__main__':
    kwarg = False
    some_kwarg(kwarg=kwarg)
```

-   하지만 힌트를 줄 때에는 반대이다

```python
def some_kwarg(kwarg: bool = True):
    if kwarg:
        print("True")
    else:
        print("False")


if __name__ == '__main__':
    kwarg = False
    some_kwarg(kwarg=kwarg)
```

-   예쁘게 쓴답시고 `=`의 열을 맞추면 안되고 좌우로 무조건 1번씩만 띄어쓰기 해야 한다

```python
arg = "arg"
some_arg = "something"
some_key_arg = "something secret"
```

### 데이터 형태

-   str, int, float 등은 소문자로 힌트를 줘도 되지만 list, dict, tuple 등 `typing`에서 import할 수 있는 것들은 import해서 힌트를 줘야 한다

```python
from typing import List, Dict, Tuple


def return_list(some_list: List[str]) -> List:
    return some_list


def return_dict(some_dict: Dict[str: str]) -> Dict:
    return some_dict


def return_tuple(some_tuple: Tuple[str, str]) -> Tuple:
    return some_tuple
```

-   `bool`값을 판정할 때에는 `==`이나 `!=`을 사용하면 안된다
    -   `is` 혹은 `is not`을 사용해야 한다

```python
def check_arg(arg):
    if arg is not False:
        return arg
    elif arg is False:
        return "wrong"
    elif arg == "string":
        return "wrong"
    else:
        raise ValueError("what is it?")
```

-   `except` 뒤에는 반드시 에러를 지정해야 한다

```python
try:
    import platform_specific_module
except ImportError:
    platform_specific_module = None
```

# 개인적인 취향: 전체 내용이 한단락이면 읽기 싫어진다

-   최대한 기능별로 나누어 직교성과 독립성을 갖춘다
    
    -   꼭 필요한 상황이 아니라면 모듈로 만들어놓고 import해서 사용하는 것이 좋다
-   메소드 내부의 코드가 하나의 기능을 구현하기 위한 하나의 이야기라지만 상황이 바뀔 때마다 개행한다
    

```python
from typing import List


def do_sth(arg: List[str]):
    arg = arg.split('/')  # split

    for a in arg:  # print
        print(a)


if __name__ == '__main__':
    arg = "/project/service/key/path"

```

-   개인적으로는 2줄 이하로는 개행하지 않는 것이 읽기 편하지만 그 이상이면 수행하는 작업이 진전되는 순간에 개행하는 것이 이해하기 쉽다

-   import할 때 builtin모듈을 위에 적고 1줄 개행하여 라이브러리 혹은 직접 구현한 모듈을 import하면 알기 쉽다
    -   짧은 것부터 적는 것이 코드가 깔끔하다

```python
import re
import sys
from pathlib import Path
```

-   if문을 사용할 때 elif를 사용하지 않는다면 else가 없어도 상관 없지만 elif를 사용할 때에는 무조건 else를 지정해주는 것이 에러를 막는데 도움이 된다
-   python3.x이라면 format-string보단 f-string을 사용하는 것이 좋다

```python
def return_sentence(name, age):
    return f"Hello, My name is {name}. I am {age} olds."
```

-   python3.x라면 `os.path.join()`보단 `pathlib.Path`로 묶어주는 것이 좋다

```python
from pathlib import Path


directory = Path(__file__).resolve().parent
file_path = directory / "file_name"
```

- 지금 귀찮더라도 나중을 위해 코드를 완벽하게 구현할 수 있도록 노력해야 한다
  - 반복작업은 없어야 한다
  - e.g. 같은 모듈에서 `import`되는 경우가 반복된다면`from import`를 사용한다

```python
from datetime import timedelta, timezone, datetime


this_day_in_last_week = (datetime.now(timezone.utc) - timedelta(days=-7)).strftime('%Y-%m-%d')
```
 - 클래스의 메서드가 `self`를 호출하지 않는다면 `@classmethod`로 래핑한다
 
```python
class PathSplitter:
    def __init__(self, arg: str):
        self.arg

    @classmethod
    def split_text(cls, text: str, point_str: str):
        return text.split(point_str)

    def return_split_text(self):
        return split_text(self.arg, "/")


if __name__ == '__main__':
    arg = "/project/service/key/path"
    my_class = MyClass(arg)
    print(my_class().return_split_text())
```
  
- 리스트 내포문을 적극적으로 사용한다
  - `if else`문을 없앨 수 있다
  - 하지만 반환값이 없는데 원라이너로 쓰고 싶다고 무의미하게 리스트를 생성해선 안된다
    
```python
def normal_list_comprehension(*args):
    return [arg for arg in args]


def list_comprehension_with_if(*args):
    return [idx for idx, arg in enumerous(*args) if arg is True]


def list_comprehension_with_if_else(*args):
    return [idx if arg is True else arg for idx, arg in args]

```
  

  
