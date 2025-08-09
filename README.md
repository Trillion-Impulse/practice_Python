# practice_Python

<br>

---

<br>

# print
- 기본구조
    ```
    print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
    ```
    - *objects: 출력할 여러 개의 값
    - sep: 출력할 때 여러 값 사이에 넣을 구분 문자 (separator)
        - 기본값: ' ' (공백)
    - end: 출력 마지막에 자동으로 붙는 문자열 (end of line)
        - 기본값: '\n' (줄바꿈)
    - file: 출력 대상 (기본은 화면/콘솔, 파일 객체로 바꿀 수도 있음)
        - 기본값: `sys.stdout`
    - flush: 출력 버퍼를 강제로 비울지 여부 (True면 바로 출력됨 — 로그 등에서 유용)
        - 기본값: False

<br>

---

<br>

# 문자열 리터럴 (string literal)
- 소스코드에 직접 작성된 문자열 값
- 이스케이프 문자를 해석하는 문자열

# raw string literal
- 이스케이프 문자를 무시하는 문자열 리터럴
- 기본 구조
    ```
    print(r"\n\t\\")
    ```
    - `r"..."`은 문자열을 있는 그대로(raw) 처리
    - `\` 같은 이스케이프 문자를 그대로 출력하고 싶을 때
    - 멀티라인 문자열
        ```
        print(r"""여러줄1
        여러줄2
        여러줄3""")
        ```
        - 여러줄 raw string 출력에 사용

# f-string (formatted string literal)
- 기본구조
    - 문자열 앞에 `f` 또는 `F`를 붙이고, `"` 혹은 `'`로 문자열을 묶음
    - 문자열 내부에 중괄호 `{}`를 사용해 변수나 표현식을 삽입
    - 여러 줄의 경우 `f"""내용"""` 또는 `f'''내용'''`
        ```
        name = "Alice"
        greeting = f"Hello, {name}!"
        print(greeting)  # Hello, Alice!
        ```
    - 문자열 안에 중괄호 문자를 사용하고 싶으면 이중 중괄호로 작성
        ```
        print(f"Use {{ and }} to show braces.")
        # 출력: Use { and } to show braces.
        ```
- 활용
    - 변수 삽입
        ```
        age = 30
        print(f"I am {age} years old.")
        # 출력: I am 30 years old.
        ```
    - 표현식 삽입
        ```
        a = 5
        b = 3
        print(f"The sum of {a} and {b} is {a + b}.")
        # 출력: The sum of 5 and 3 is 8.
        ```
    - 함수 호출
        ```
        def upper_name(name):
            return name.upper()

        print(f"My name is {upper_name('Alice')}.")
        # 출력: My name is ALICE.
        ```
- 포맷팅 옵션
    - 숫자 포맷
        ```
        pi = 3.14159
        print(f"Pi is approximately {pi:.2f}")
        # 출력: Pi is approximately 3.14
        ```
    - 정렬과 공백
        - 문자열 총 너비 10칸 안에서의 정렬
        ```
        name = "Bob"
        print(f"{name:>10}")  # 오른쪽 정렬
        print(f"{name:<10}")  # 왼쪽 정렬
        print(f"{name:^10}")  # 가운데 정렬
        ```
        - 공백 대신 다른 문자로 채워서 정렬
        ```
        print(f"{name:*<10}")  # 왼쪽 정렬, 공백을 *로 채움
        print(f"{name:->10}")  # 오른쪽 정렬, 공백을 -로 채움
        print(f"{name:.^10}")  # 가운데 정렬, 공백을 .로 채움
        ```
- Python 3.6 이상에서만 사용가능

# Byte string
- 바이트 단위 문자열, 주로 바이너리 데이터 처리할 때 사용
- 텍스트가 아니라 바이트 배열로 취급
- 네트워크, 파일 입출력, 인코딩 처리할 때 사용
- 기본 구조
    ```
    b"hello"
    ```

# 멀티라인 문자열
- 여러 줄을 표현할 때 사용하는 문자열 (작은따옴표/큰따옴표 3개)
- 기본 구조
    ```
    '''Hello\nWorld'''
    """Hi"""
    ```

<br>

---

<br>

# 리스트 컴프리헨션
- 파이썬에서 리스트를 간결하고 빠르게 만드는 문법
- 언제 사용하는가
    - 리스트를 빠르게 만들고 싶을 때
    - map() 대신 직관적으로 쓰고 싶을 때
    - 이중 반복 (중첩 루프)도 짧게 쓰고 싶을 때
- `[표현식 for 변수 in 반복가능한객체]`
    - 일반적인 for문
        ```
        squares = []
        for i in range(5):
            squares.append(i * i)
        ```
    - 리스트 컴프리핸션
        ```
        squares = [i * i for i in range(5)]
        ```
    - 중첩 for문도 가능
        ```
        [i + j for i in [1, 2] for j in [10, 20]]

        결과: [11, 21, 12, 22]
        ```
        - 바깥→안쪽 순서대로 실행
- `[표현식 for 변수 in 반복가능한객체 if 조건]`
    - 예: 짝수만 제곱
        ```
        [i * i for i in range(10) if i % 2 == 0]
        ```
- map, split, input과 함께 쓰기
    - 예: 공백으로 구분된 숫자 입력 받아 리스트로 만들기
    ```
    일반적인 표현
    nums = list(map(int, input().split()))

    리스트 컴프리핸션
    nums = [int(x) for x in input().split()]
    ```

<br>

---

<br>

# 연산자

## %
- 나누기 후 나머지를 구하는 연산자
- 하지만 사실 파이썬에서 `%` 연산자는 수학적 나머지가 아님
    - 파이썬에서 `%`는 내부적으로 아래와 같이 동작
        ```
        a % b == a - (a // b) * b
        ```

## 삼항 연산자
- 피연산자를 세 개 가지는 조건 연산자
- `C, Java, JS` 같은 언어에서는 `condition ? a : b` 의 형식
    - 조건 condition이 참이면 a
    - 조건 condition이 거짓이면 b
- `파이썬에서는 아래와 같은 형식`
    ```
    <값1> if <조건> else <값2>
    ```

## 월러스 연산자(Walrus operator)
- `변수 := 값`
- 할당 표현식이라고 부르며, 파이썬 3.8부터 도입된 문법
- 값을 변수에 할당하면서 동시에 그 값을 표현식 안에서 사용할 수 있는 문법
- 기존의 `=`은 할당만 가능했지만, `:=`는 표현식 안에서 할당과 사용을 동시에 가능
- 기존 방식과의 비교
    - 기존 방식
        ```
        line = input()
        while line != "":
            print(line)
            line = input()
        ```
    - 월러스 연산자 사용
        ```
        while (line := input()) != "":
            print(line)
        ```
        - `line := input()`이 input() 결과를 line에 저장하면서, 조건 비교에도 사용
- 왜 `월러스` 연산자인가?
    - := 모양이 물개 얼굴 비슷하다고 해서 이름 붙음 (월러스 = 바다코끼리)
- :=는 표현식 안에서만 사용 가능, 문장 단위에서는 안 됨
- 파이썬 3.8 이상에서만 작동

<br>

---

<br>

# 함수

## sorted()
- 반복 가능한 객체(iterable)를 정렬된 리스트로 반환
- sorted()는 리스트, 문자열, 튜플, 집합 등 거의 모든 iterable에서 작동
- 기본 구조
    ```
    sorted(iterable, key=None, reverse=False)
    ```
    - key: 정렬의 기준이 될 함수
        - 기본값: None (요소 직접 비교)
        - 예
            - len: 길이
            - str.lower 또는 str.upper: 대소문자 무시
            - lambda 함수
            - itemgetter(n)
            - 사용자 정의 함수
    - reverse: 내림차순 정렬
        - 기본값: False
- 예시
    ```
    nums = [3, 1, 4]
    print(sorted(nums))  # [1, 3, 4]
    ```
    - sorted()는 원본을 바꾸지 않고, 정렬된 새 리스트를 리턴

## set()
- **중복을 제거**하고, 유일한 값들로 이루어진 집합(set)을 생성
- 여기서 set는 파이썬의 컬렉션 자료형 중 비시퀀스 자료형인 세트를 말함
- 비시퀀스 자료형이므로 순서를 보장하지 않음
- 예시
    ```
    nums = [1, 2, 2, 3, 3, 3]
    unique = set(nums)
    print(unique)  # {1, 2, 3}
    ```

## list()
- **반복 가능한 객체(iterable)**를 받아서 **그 안의 요소들을 꺼내** 리스트로 만듬
- 예를 들어 문자열, 튜플, set, 다른 리스트 등등
- 기본 구조
    ```
    list(iterable)
    ```
- 예시
    ```
    list("abc")       # ['a', 'b', 'c']
    list((1, 2, 3))    # [1, 2, 3]
    list(range(5))     # [0, 1, 2, 3, 4]
    ```
- `[...]` 리스트 리터럴
    - 지정한 값들을 직접 넣어서 리스트를 만듬
    - 반복 가능한 객체를 넣어도 **그 객체 자체가** 리스트에 들어감
    - 기본 구조
        ```
        [값1, 값2, 값3, ...]
        ```
    - 예시
        ```
        ["abc"]         # ['abc'] ← 문자열 하나를 요소로 갖는 리스트
        [(1, 2, 3)]     # [(1, 2, 3)]
        [range(5)]      # [range(0, 5)]
        ```
- 다양한 표현 방법
    | 문법              | 결과                       | 설명                          |
    |-------------------|----------------------------|-------------------------------|
    | `list("abc")`     | `['a', 'b', 'c']`           | 문자열을 문자 단위로 나눔     |
    | `["abc"]`         | `['abc']`                   | 문자열 하나가 리스트의 요소   |
    | `[*"abc"]`        | `['a', 'b', 'c']`           | unpacking 해서 문자 단위 분해 |
    | `list(range(3))`  | `[0, 1, 2]`                 | range의 요소를 리스트로       |
    | `[range(3)]`      | `[range(0, 3)]`             | range 객체 자체가 리스트 요소 |

## range()
- range 객체 (range type) 를 반환
- for 반복문, 슬라이싱, 리스트 변환 등에서 사용 가능
- 메모리를 효율적으로 사용 (→ 값을 미리 저장하지 않고, 필요할 때 생성하는 lazy evaluation 방식)
- range 객체
    - iterable: 반복 가능한 객체 (for문, list, tuple 등에서 사용 가능)
    - indexable: 인덱싱 가능 (r[0], r[-1] 등)
    - sliceable: 슬라이싱 가능 (r[1:4])
    - len(r): range 내 숫자의 개수를 반환
    - in 연산자: 특정 값이 포함되어 있는지 확인 가능
    - == 연산자: 값이 같으면 다른 range라도 같다고 판단함 (range(1, 4) == range(1, 4, 1))
- 기본 구조
    ```
    range(stop)
    range(start, stop)
    range(start, stop, step)
    ```
    - start: (선택, 기본값 0) 반복 시작 숫자
    - stop: (필수) 반복이 멈출 숫자 (이 숫자는 포함되지 않음)
    - step: (선택, 기본값 1) 증가/감소 간격. 음수도 가능
        - step이 0이면 ValueError 발생
        - 음수 step도 가능하지만, start > stop 형태로 써야 함

## exec()
- 문자열로 작성된 파이썬 코드를 실제로 실행하는 함수
- execute의 줄임말
- 기본 구조
    ```
    exec(expression_string)
    ```
    - expression_string: 파이썬 코드가 들어있는 문자열
    - 실행 결과는 별도의 반환값이 없고, 그냥 코드가 실행되는 것
- 숏코딩처럼 짧게 쓰고 싶을 때 사용
- 보안과 가독성에 주의

## eval()
- 문자열로 된 파이썬 표현식(expression)을 실제 코드로 실행하고 결과를 반환하는 함수
- 기본 구조
    ```
    eval(expression, globals=None, locals=None)
    ```
    - expression: 실행할 파이썬 표현식을 담은 문자열
    - globals, locals: 선택적이며 실행 환경(변수 영역)을 
- 주의점
    - 보안 위험: eval은 입력된 문자열을 그대로 실행하기 때문에 악성 코드가 실행될 수 있음
    - 성능 저하: **일반 연산에 비해 느릴 수 있음**
        - 루프(반복문)안에서 사용하면 성능 저하 주의

## eval() vs exec()

| 항목           | eval                                      | exec                                    |
|----------------|-------------------------------------------|----------------------------------------|
| 역할           | 단일 표현식(expression) 평가 및 결과 반환    | 복수 문장(statements) 실행 (코드 실행 전용)   |
| 반환값         | 표현식 계산 결과 반환 (예: 숫자, 리스트 등)  | 반환값 없음 (None)                      |
| 실행 가능한 코드 | 하나의 표현식 (ex: "1+2", "x*3")           | 여러 줄 문장, 함수 정의, 반복문 등도 가능       |
| 사용 예        | 수식 계산, 값 반환 필요할 때                 | 여러 줄 코드 실행, 함수나 클래스 정의 시        |
| 예시 코드      | `eval("1 + 2")  # 3`                       | `exec("for i in range(3): print(i)")` |
| 위험성         | 둘 다 위험 (임의 코드 실행 가능)              | 둘 다 위험                             |

## zip()
- 여러 개의 **iterable(반복 가능한 객체)**들을 동시에 순회하면서, 각 위치에 있는 요소들을 **튜플**로 묶음
- 기본 구조
    ```
    zip(iterable1, iterable2, ...)
    ```
- 예시
    ```
    a = [10, 20, 30]
    b = ['a', 'b', 'c']

    z = zip(a, b)
    print(list(z))

    출력: [(10, 'a'), (20, 'b'), (30, 'c')]
    ```
    - zip(a, b)는 각 리스트의 같은 인덱스에 있는 원소들을 묶어서 `(a[0], b[0]), (a[1], b[1]) ...` 형태로 만들어 줌

## max()
- 가장 큰 값을 반환
- 기본 구조
    ```
    max(iterable, *[, key, default]) → 최대값
    max(arg1, arg2, *args[, key]) → 최대값
    ```
    - iterable 모드: max([1, 2, 3])
        - iterable: 반복 가능한 객체 (리스트, 튜플, 문자열 등)
        - 문자열의 경우 아스키 코드 값 기준
        - 튜플의 경우 첫 번째 요소 기준, 같으면 두 번째 비교 == 사전식 비교
        - 딕셔너리의 경우
            ```
            d = {'a': 3, 'b': 7, 'c': 5}
            max(d)         # → 'c' (key 기준) 키끼리 비교
            max(d.values())  # → 7 (value 기준) 값끼리 비교
            max(d.items(), key=lambda x: x[1])  # → ('b', 7)
                        이것도 value 기준비교하지만 items()이므로 키값 쌍을 반환
            ```
    - arg1, arg2, *args 모드: max(1, 2, 3)
        - *args: 여러 개의 인자 전달 방식
    - key: 비교 기준을 정의하는 함수
        - 튜플, 문자열, 객체 등 비교 기준이 애매한 경우 사용
        - key에는 함수 또는 lambda 표현식이 들어감
        - 예시
            ```
            max(['apple', 'banana', 'kiwi'], key=len)
            결과 → 'banana' (길이가 가장 긴 단어)

            max([(1, 2), (3, 1)], key=lambda x: x[1])
            결과 → (1, 2) (두 번째 요소 기준)
            ```
    - default: 빈 iterable인 경우 반환할 기본값 (없으면 ValueError), (Python 3.4+)
        - 빈 iterable에서 max()를 호출하면 ValueError가 발생
        - default를 주면, 예외 대신 기본값을 반환
        - 예시
            ```
            max([], default=0)
            결과 → 0
            ```
        - default는 오직 iterable을 사용하는 형태에서만 사용 가능
            - 즉, max(1, 2, 3, default=0) ← 안 됨
- 반환값
    - 비교 기준에 맞는 최댓값 1개 반환
    - 같은 최댓값이 여러 개일 경우 첫 번째 등장하는 값 반환
- 기본적으로 비교 가능한 자료형끼리만 비교 가능
    - 다른 타입끼리 비교할 경우 TypeError 발생

<br>

---

<br>

# 메서드

## split()
- **구분자(sep)**를 기준으로 왼쪽에서부터 문자열을 나눔
- 기본 구조
    ```
    split(sep=None, maxsplit=-1)
    ```
    - sep: 나눌 기준 문자열
        - None일 경우
            - 모든 종류의 공백 문자를 기준으로 나눔
            - 스페이스 ' ', 탭 '\t', 줄바꿈 '\n', 캐리지 리턴 '\r' 등
            - 연속된 공백은 하나로 처리
            - 앞뒤 공백은 자동으로 무시
    - maxsplit: 최대 분할 횟수, 나눌 횟수를 제한할 수 있음, 기본값은 -1 (제한 없음)
            - 최대 maxsplit번까지만 나누고, 나머지는 마지막 요소에 다 들어감
            - maxsplit은 최종 리스트 개수가 아니라 나눈 횟수 기준
            - 따라서 결과 리스트의 길이는 최대 maxsplit + 1 개
            - 구분
                - 생략: 제한 없이 전부 나눔
                - 0: 아예 나누지 않음 (원본 그대로)
                - N: 최대 N번까지만 나눔
                - -1: (기본값) → 제한 없음
- 예시
    ```
    "a b  c\n d".split()          # ['a', 'b', 'c', 'd']
    "a,b,c".split(',')            # ['a', 'b', 'c']
    "1-2-3".split('-', 1)         # ['1', '2-3']
    ```

## rsplit()
- **구분자(sep)**를 기준으로 오른쪽에서부터 문자열을 나눔
- 기본 구조
    ```
    rsplit(sep=None, maxsplit=-1)
    ```
- 예시
    ```
    "1-2-3".rsplit('-', 1)       # ['1-2', '3']
    ```

<br>

---

<br>

# 변수

## 특별 변수명

### _ (underscore)
- underscore, throwaway variable, dummy variable 여러 가지 이름이 존재
- 파이썬에서 `사용하지 않을 값을 임시로 받는 변수`로 관례적으로 사용

<br>

---

<br>

# starred expression
- `*` 기호를 사용하여 여러 값을 한 번에 unpack하거나 pack할 수 있게 해주는 문법
- `*`의 의미
    - `*`는 iterable (리스트, 튜플 등)을 unpack하는 데 사용
        - iterable이 아니면 `*`는 사용 불가
        - `iterable`: Python에서 반복(iteration)이 가능한 객체
            - 즉 for 루프 같은 반복문에서 하나씩 꺼내 쓸 수 있는 객체
            - 반복 가능한 `데이터`
            - 리스트, 튜플, 문자열, 딕셔너리, 집합 등등
    - `**`는 dict를 unpack할 때 사용
- 함수 정의에서 역할
    - `*args`: 여러 위치 인자를 튜플로 묶어 받기
    - `**kwargs`: 여러 키워드 인자를 딕셔너리로 받기
- 함수 호출에서 역할
    - `*args`: 리스트, 튜플 등을 위치 인자로 풀기
    - `**kwargs`: 딕셔너리를 키워드 인자로 풀기
- 리스트/튜플 등에서의 unpacking
    - 예시
        ```
        numbers = [1, 2, 3, 4, 5]
        a, *b, c = numbers
        print(a)  # 1
        print(b)  # [2, 3, 4]
        print(c)  # 5
        ```
        - 중간에 *b를 사용하면, 나머지 값들을 리스트로 받음
        - 단, starred expression은 unpacking에서 딱 하나만 사용 가능
            - Python 3.11부터는 **다중 `*` unpacking도 가능**
- 시퀀스 결합 시 사용 (Packing)
    - 예시
        ```
        a = [1, 2]
        b = [3, 4]
        c = [*a, *b, 5]
        print(c)  # [1, 2, 3, 4, 5]
        ```
        - 리스트나 튜플을 풀어서 새로운 리스트를 만들 때 사용
- Dictionary unpacking (Python 3.5+)
    - 예시
        ```
        dict1 = {'x': 1, 'y': 2}
        dict2 = {'y': 3, 'z': 4}
        merged = {**dict1, **dict2}
        print(merged)  # {'x': 1, 'y': 3, 'z': 4}
        ```
        - 주의: 키가 겹치면 뒤의 값이 우선

<br>

---

<br>

# **kwargs
- kwargs = keyword arguments
- 파이썬 함수에 이름 있는 인자들을 넘길 때 사용되는 형식
- 내부적으로는 딕셔너리 형태로 처리
- 키워드 인자(이름 있는 인자)를 딕셔너리 형태로 수집
- 다른 언어에도 존재함 (다만 문법은 다름)

## Flask에서
- 예
    ```
    def login_required(view):
    @functools.wraps(view)
    def wrapped_view(**kwargs):
        if g.user is None:
            return redirect(url_for('auth.login'))

        return view(**kwargs)

    return wrapped_view
    ```

    - login_required 데코레이터가 위와 같이 정의된 경우
        - 예1 - 파라미터 없는 뷰
            ```
            @app.route('/dashboard')
            @login_required
            def dashboard():
                return '대시보드'
            ```
            - 이 경우엔 wrapped_view()가 호출될 때 **kwargs는 빈 딕셔너리
            - `wrapped_view() → kwargs == {}`
        - 예2 - 파라미터 있는 뷰
            ```
            @app.route('/post/<int:id>')
            @login_required
            def post_detail(id):
                return f'{id}번 게시물입니다.'
            ```
            - 사용자가 /post/5로 접속하면 `wrapped_view(id=5) → kwargs == {'id': 5}`
            - Flask는 URL에서 `<int:id>`를 추출해서 kwargs로 넘겨줌

<br>

---

<br>

# jinja2 문법
- Jinja2는 Python에서 널리 사용되는 템플릿 엔진
- Flask, Django 등 웹 프레임워크에서도 자주 사용

## 변수 출력
```
{{ 변수명 }}

{{ user.name }}        {# 객체 속성 접근 #}
{{ items[0] }}         {# 리스트/딕셔너리 인덱스 접근 #}
```

## 제어문 (조건문, 반복문 등)
- if / elif / else
    ```
    {% if user.is_admin %}
    관리자입니다.
    {% elif user.is_guest %}
    게스트입니다.
    {% else %}
    일반 사용자입니다.
    {% endif %}
    ```
- for 문
    ```
    {% for item in items %}
        {{ item }}
    {% endfor %}
    ```
    - for문 안에서 쓰이는 인덱스 관련 변수들
        - loop.index: 1부터 시작하는 인덱스
        - loop.index0: 0부터 시작하는 인덱스
        - loop.revindex: 끝에서부터 1부터 세는 인덱스
        - loop.revindex0: 끝에서부터 0부터 세는 인덱스
        - loop.first: 현재 반복이 첫 번째인가
        - loop.last: 현재 반복이 마지막인가
        - loop.length: 전체 반복 횟수
        ```
        {# 인덱스 번호 넣고 싶을 때 예시 #}
        <ul>
        {% for user in users %}
            <li>{{ loop.index }}. {{ user.name }}</li>
        {% endfor %}
        </ul>

        {# 첫 번째 요소만 강조하거나, separator 다르게 넣고 싶을 때 예시 #}
        {% for item in items %}
            {% if loop.first %}
                <strong>첫 번째:</strong> {{ item }}
            {% else %}
                {{ item }}
            {% endif %}
        {% endfor %}

        {# 마지막 요소 뒤에는 쉼표를 안 넣는 예시 #}
        {% for item in items %}
            {{ item }}{% if not loop.last %}, {% endif %}
        {% endfor %}
        ```

## 주석
```
{# 이것은 주석입니다. #}
```

## 필터 사용 (| 기호 사용)
- 예시
    ```
    {{ name | lower }}     {# 소문자로 변환 #}
    {{ title | length }}   {# 길이 출력 #}
    ```
- 자주 쓰는 필터
    - lower: 소문자로 변환
    - upper: 대문자로 변환
    - capitalize: 첫 글자만 대문자, 나머지는 소문자
    - length: 문자열, 리스트 등의 길이 반환
    - replace: 문자열 바꾸기
    - default: 값이 비어있을 때 기본값 설정
    - safe: HTML 이스케이프 방지 (즉, HTML 태그 그대로 출력)
        - 예시
        ```
        {{ "<b>중요</b>" | safe }}
        ```
            - 일반적으로는 <b>중요</b> → &lt;b&gt;중요&lt;/b&gt; 로 출력
            - safe를 쓰면 태그 그대로 렌더링됩니다 → 굵게 보임
        - 외부에서 입력받은 문자열을 safe로 그대로 출력하면 XSS(크로스사이트 스크립팅) 위험
        - 사용자가 `<script>` 같은 코드를 입력하면 실행될 수 있기 때문에, safe는 신뢰할 수 있는 데이터에만 써야 함

## 매크로 (재사용 가능한 템플릿 함수)
```
{% macro input(name, value='', type='text') %}
  <input type="{{ type }}" name="{{ name }}" value="{{ value }}">
{% endmacro %}

{{ input('username') }}
```

## 템플릿 상속
- base.html
    ```
    <!DOCTYPE html>
    <html>
        <head>{% block head %}{% endblock %}</head>
        <body>{% block content %}{% endblock %}</body>
    </html>
    ```
- child.html
    ```
    {% extends "base.html" %}

    {% block head %}
        <title>페이지 제목</title>
    {% endblock %}

    {% block content %}
        <h1>콘텐츠</h1>
    {% endblock %}
    ```

## include (템플릿 포함)
- 예시
    ```
    {# 예를 들어, header.html이라는 파일을 현재 페이지 상단에 포함하고 싶다면 #}
    <!DOCTYPE html>
    <html>
        <body>
            {% include "header.html" %}
            <p>메인 콘텐츠</p>
        </body>
    </html>
    ```
- 공통 레이아웃을 재사용하고 싶을 때 사용
- include는 단순 삽입이라서 불러오려는 템플릿(예시의 header.html) 안에 `{% block %}` 같은 건 사용할 수 없음
    - include는 단순히 그 파일의 HTML이나 템플릿 코드를 그대로 불러오는 것
    - 그래서 `{% block %}`을 선언해도 해석되지 않고 무시되거나 이상한 동작할 가능성 존재

<br>

---

<br>

# 코딩 테스트

1. 문제 1
    ```
    a, b = open(0)
    for x in *b[2::-1], b:
        print(int(a) * int(x))
    ```
    - `open()`은 파이썬의 내장 함수로, 보통은 파일을 열 때 사용하는 함수
        - `open(0)`은 파일 대신 '파일 번호 0'을 여는 것
            - 표준 입력 (stdin)을 의미
            - 입력을 여러 줄 받을 때 사용
            ```
            a, b = open(0)
            
            위의 코드는 아래의 코드와 같은 역할

            import sys
            a = sys.stdin.readline()
            b = sys.stdin.readline()
            ```
        - 파이썬에서 `open(0)` 같은 표현은 파일 디스크립터(file descriptor) 를 사용하는 것
            - 운영체제 수준의 개념
            - 운영체제는 파일이나 입출력 장치를 숫자로 구분
                - 0: 표준 입력(stdin)
                - 1: 표준 출력(stdout)
                - 2: 표준 에러(stderr)
            - 따라서
                - open(0): 키보드에서 입력 받기 (stdin)
                - open(1): 화면에 출력하기 위한 파일 핸들 (stdout) – 쓰기 전용
                - open(2): 에러 메시지 출력용 (stderr) – 쓰기 전용
            - 쓰기 전용은 read()하면 에러 발생
                ```
                아래와 같이 사용해야 함
                f = open(1)  # stdout 열기
                f.write("Hello\n")  # 화면에 출력됨
                ```
            - print가 있기때문에 일반적으로 open(1)은 거의 안 씀
        - 여러 입력 방법의 차이
            | 구분 | input() | sys.stdin.readline() | sys.stdin.read() | open(0) |
            |-----|-----|-----|-----|-----|
            | 입력 단위 | 한 줄 | 한 줄 | 전체 입력 | 여러 줄 (iterable) |
            | 줄바꿈 포함 | 제거됨 | 포함됨 (\n 있음) | 포함됨 (\n 있음) | 포함됨 (\n 있음) |
            | 속도 | 느림 | 빠름 | 매우 빠름 | 빠름 |
            | 가공 여부 | 줄바꿈 제거 포함됨 | 순수 입력 그대로 | 순수 입력 그대로 | 순수 입력 그대로 |
            | 사용 방식 | 고수준 함수 | 저수준 함수 | 저수준 함수 | 파일 객체처럼 취급 |
            | 반복문 사용 | 불편 (반복 안됨) | 불편 (반복 안됨) | 한 번만 호출 가능 | for line in open(0) 가능 |
            | 실전 사용 용도 | 일반적인 간단 입력 | 반복문 많은 줄 입력 | 전체 입력 후 처리 | 짧고 간단한 코드 작성 |
            - input()
                - 기본 내장 함수
                - 사용자 입력을 한 줄 받고, `\n`은 자동 제거
                - 내부적으로는 `sys.stdin.readline().rstrip('\n')` 같은 동작
            - sys.stdin.readline()
                - `\n` 포함됨, 그래서 s.strip()이나 s.rstrip() 필요
                    - strip()
                        - 앞뒤 공백이나 줄바꿈 \n 등을 제거
                        - 좌우 모두 제거
                    - rstrip()
                        - 오른쪽 (right)만 제거
                        - 주로 줄바꿈만 제거하고 싶을 때 사용
            - sys.stdin.read()
                - 입력 전체를 한꺼번에 읽음
                - 한 번에 다 읽기 때문에 반복문 쓰기 전 직접 가공 필요
                    ```
                    nums = list(map(int, sys.stdin.read().split()))
                    ```
                    - split()
                        - 공백 기준으로 문자열을 나눠서 리스트로 만듦
                        - 본 구분자: " " (공백)
                        - 인자로 구분자를 줄 수도 있음
                    - splitlines()
                        - 문자열을 줄 단위로 나눔 (`\n, \r\n, \r` 모두 대응)
                            - `\r`: 현재 줄에서 커서를 맨 앞으로 이동시키는 명령
                        - 줄바꿈 문자들은 제거됨
            - open(0)
                - 표준 입력을 파일처럼 여는 트릭
                - 줄바꿈 포함됨, `.strip()` 혹은 `.rstrip()` 필요
                - `open(0)`은 파일 객체를 반환
                    - **sys.stdin 또한 내부적으로 open(0)을 통해 생성된 객체이므로 동일**
                    - 파일 객체는 그 자체로 반복 가능한 iterable
                        - 따라서 for문의 in 인자로 줄 단위로 순회 가능
                    - 하지만 파일 객체를 가공하기 위해서는 `.read()`, `readline()` 등으로 내용을 문자열로 읽은 후 
                        `.split()`이나 `.strip()` 등으로 가공 가능
                        - `.read()`: 파일 또는 입력 스트림에서 전체 내용을 문자열로 읽는 메서드
                        - `readline()`: 한 줄을 문자열로 읽기
                        - `readlines()`: 모든 줄을 리스트로 읽기
            - 속도 차이 (코딩테스트에서 중요)
                - input()은 내부적으로 sys.stdin.readline()을 호출하고, 추가 처리를 함
                - 그래서 많은 입력을 받을 때는 sys.stdin.readline()이 훨씬 빠름
            - 예제
                ```
                입력으로 다음이 들어온다고 가정
                3 4
                7 8
                이걸 읽어서 두 줄을 각각 a, b로 받고,
                각 줄을 공백 기준으로 정수 리스트로 바꿔보기
                결과 → a = [3, 4], b = [7, 8]
                ```
                - input() (두 번 사용)
                    ```
                    a = list(map(int, input().split()))
                    b = list(map(int, input().split()))
                    print(a, b)
                    ```
                - sys.stdin.readline()
                    ```
                    import sys
                    a = list(map(int, sys.stdin.readline().strip().split()))
                    b = list(map(int, sys.stdin.readline().strip().split()))
                    print(a, b)
                    ```
                    - strip()으로 줄바꿈 \n 제거
                - sys.stdin.read() (전체 입력 후 분할)
                    ```
                    import sys
                    lines = sys.stdin.read().splitlines()
                    a = list(map(int, lines[0].split()))
                    b = list(map(int, lines[1].split()))
                    print(a, b)
                    ```
                    - splitlines()로 줄 기준 분리
                    - 각 줄을 다시 split()해서 숫자로 변환
                - open(0) (파일처럼 읽기)
                    ```
                    lines = list(open(0))  # 표준 입력 전체를 줄 단위로 읽음
                    a = list(map(int, lines[0].split()))
                    b = list(map(int, lines[1].split()))
                    print(a, b)
                    ```
                    - vs sys.stdin.read()
                        - sys.stdin.read()는 전체를 읽기 때문에 줄 기준 분리 해야됨
                        - open(0)은 줄 단위로 읽기 때문에 줄 단위 분리 필요 없음

2. 문제 2
    ```
    a,b=open(0)
    for x in*b[2::-1],b:print(int(a)*int(x))
    ```
    - `*b[2::-1],b`
        - `b[2::-1]`가 실행되어 리스트가 나옴
        - `*`는 리스트의 각 요소를 풀어서 나열
        - 결과적으로 *리스트,b는 리스트를 풀어서 나열한 뒤 b까지 나열한 튜플이 됨
            - 파이썬에서 쉼표로 나열된 값들은 기본적으로 튜플로 취급
        - `*`: 언팩 연산자 (리스트)
            - 파이썬에서 `*`는 리스트나 튜플처럼 여러 값을 담고 있는 객체의 "내용물"을 풀어서 꺼낼 때 쓰는 연산자
            - 사용
                *리스트: 리스트의 각 원소를 하나씩 풀어냄
                *args: 여러 인자를 묶어서 받을 때(인자를 튜플로 받음)
                * in 함수 호출: 인자를 여러 개로 나눠서 전달
                * in iterable unpack: 값을 여러 변수에 나눠서 받을 때
            - `**`: 언팩 산잔자 (딕셔너리)
            - `*args`와 `**kwargs`
                - 함수 정의에서 역할
                    - `*args`: 여러 위치 인자를 튜플로 묶어 받기
                    - `**kwargs`: 여러 키워드 인자를 딕셔너리로 받기
                - 함수 호출에서 역할
                    - `*args`: 리스트, 튜플 등을 위치 인자로 풀기
                    - `**kwargs`: 딕셔너리를 키워드 인자로 풀기

3. 문제 3
    ```
    X, N, *A = open(0)
    print("YNeos"[int(X)!=sum(eval(i.replace(*' *'))for i in A)::2])
    ```
    - `*A`: 시퀀스 언패킹 문법
        - 여러 값을 리스트로 받는 역할
        - `open(0)`이 입력을 한 줄씩 리스트로 읽어옴
        - 입력 예시
            ```
            260000
            4
            20000 5
            30000 2
            10000 6
            5000 8
            ```
            - 입력이 위와 같다면, 첫줄 X, 두번째줄 N, 나머지 줄 리스트 형식으로 A에 저장
            - X에 "260000\n"
            - N에는 "4\n"
            - A = ["20000 5\n", "30000 2\n", "10000 6\n", "5000 8\n"]
    - `.replace(a, b)`: 문자열에서 "a"를 "b"로 바꾸는 함수
        - `' *'`: 공백과 *로 이루어진 문자열
        - `*' *'`: 공백과 *로 이루어진 문자열을 언패킹
            - 언패킹하면 하나씩 분해됨
            - ' ', '*' 두개로 분해됨
        - `i.replace(*' *')` → `i.replace(' ', '*')`

4. 문제 4
    ```
    open(0)으로 입력을 받는 상황
    입력 예시
    apple
    banana
    cherry
    ```
    - 출력 비교 표
        | 특징 / 함수               | `.read()`                                 | `.readline()`                 | `.readlines()`                               | `.read().splitlines()`              |
        |--------------------------|--------------------------------------------|-------------------------------|-----------------------------------------------|-------------------------------------|
        | 반환값 타입           | `str`                                     | `str`                         | `list[str]`                                   | `list[str]`                         |
        | 반환 내용             | `'apple\nbanana\ncherry\n'`               | `'apple\n'` (첫 줄만 읽음)    | `['apple\n', 'banana\n', 'cherry\n']`         | `['apple', 'banana', 'cherry']`    |
        | 줄바꿈(`\n`) 포함 여부 | 포함                                      | 포함                          | 포함                                           | 제거됨                             |
        | 반복 처리 용이성      | split 필요                           | `while`이나 `for`로 반복 | `for line in lines:` 가능                | 바로 리스트 반복 가능         |
        | 메모리 사용 및 성능   | 높음 (전체 문자열 읽음)                   | 낮음 (한 줄씩 읽음)           | 높음 (전체 읽음)                              | 높음 (전체 읽음)                   |
        | 출력 예시             | `'apple\nbanana\ncherry\n'`               | `'apple\n'`                   | `['apple\n', 'banana\n', 'cherry\n']`         | `['apple', 'banana', 'cherry']`    |
        | 추천 사용 상황        | 전체 입력 후 직접 파싱할 때               | 입력 줄마다 처리할 때         | 전체 줄을 순회하며 줄바꿈 유지할 때           | 줄바꿈 제거된 줄 리스트가 필요할 때 |

5. 문제 5
    ```
    for i in range(int(input())):print('*'*-~i)
    ```
    - `~i`: 비트 연산자 NOT
        - 숫자를 2진수로 바꾼 뒤, 그 비트들을 반전시키는 연산
            ```
            5 → 00000101 → 비트반전 → 11111010 (1과 0이 뒤바뀜) → 이진수 11111010은 2의 보수 표현에서 -6
            ```
            - 2의 보수 읽는 방법
                1. 맨 앞 비트(부호비트)를 본다
                    - 0이면 양수 → 그냥 읽으면 됨
                    - 1이면 음수 → 2의 보수 해석 필요
                2. 맨 앞 비트가 1이면 `11111011`
                    - 다시 비트 반전 `00000100`
                    - +1 `00000101`==`5`
                    - `-`마이너스 붙임
            - 컴퓨터 사이언스에서 부호 있는 정수(Signed Integer)는 맨 앞 비트가 부호 비트
                - 그래서 8비트 부호 있는 정수라면
                    - 양수: 0 ~ 127 → `00000000` ~ `01111111`
                    - 음수: -1 ~ -128 → `11111111` ~ `10000000`
    - `-~i`
        ```
        ~i 결과 -6에 -해줘서 +6
        ```
    - 파이썬에서 `~i`==`-(i+1)`

<br>

---

<br>