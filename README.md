# practice_Python

<br>

---

<br>

# 자료형

## 시퀀스 자료형
- 순서가 있는 요소들의 집합
- 요소들은 인덱스로 접근할 수 있으며, 슬라이싱, 반복, 포함 검사 등의 연산이 가능
- 주요 시퀀스 자료형 종류
    | 자료형      | 설명                           | 변경 가능성  |
    |-------------|--------------------------------|-------------|
    | `str`       | 문자열                         | ❌ 불변     |
    | `list`      | 여러 값 저장, 자료형 자유로움 | ✅ 가변     |
    | `tuple`     | 리스트와 유사하나 불변         | ❌ 불변     |
    | `range`     | 정수 범위 표현, 메모리 효율적 | ❌ 불변     |
    | `bytes`     | 바이트 시퀀스 (바이너리 데이터) | ❌ 불변     |
    | `bytearray` | 가변 바이트 시퀀스             | ✅ 가변     |
- 시퀀스 자료형이 제공하는 기능들
    | 기능     | 설명                   | 예시                  |
    | ------ | -------------------- | ------------------- |
    | 인덱싱    | 특정 위치의 요소 접근         | `s[0]`, `s[-1]`     |
    | 슬라이싱   | 범위를 지정해 부분 추출        | `s[1:4]`, `s[::-1]` |
    | 반복     | 순차적으로 요소 처리          | `for x in s:`       |
    | 포함 검사  | 특정 값이 포함되어 있는지 확인    | `'a' in s`          |
    | 길이 측정  | 전체 요소 개수             | `len(s)`            |
    | 연결     | 두 시퀀스를 합침            | `s1 + s2`           |
    | 반복 연산  | 시퀀스를 여러 번 반복         | `s * 3`             |
    | 최소/최대  | 가장 작은/큰 값 반환 (정렬 기준) | `min(s)`, `max(s)`  |
    | 정렬     | 요소 정렬 (리스트만 해당)      | `sorted(s)`         |
    | 인덱스 찾기 | 특정 값의 위치 반환          | `s.index(x)`        |
    | 개수 세기  | 특정 값이 몇 번 등장했는지 확인   | `s.count(x)`        |

### 인덱싱
- 시퀀스의 특정 위치(인덱스)에 있는 요소 하나를 가져오는 것
- 인덱스는 0부터 시작
- 기본 구조: `시퀀스[인덱스]`
- 예시
    ```
    s = 'abcd'
    print(s[0])  # 'a'
    print(s[1])  # 'b'
    print(s[-1]) # 'd' (음수는 뒤에서부터, 가장 뒤가 -1)
    ```
- 인덱스가 범위를 벗어나면 IndexError 발생

### 슬라이싱
- 시퀀스의 일정한 구간(부분)을 잘라내는 것
- 여러 요소를 포함한 부분 시퀀스를 반환
- 기본 구조: `시퀀스[시작:끝:간격]`
    - 시작(start)	시작 인덱스 (포함)
    - 끝(end)	끝 인덱스 (미포함)
    - 간격(step)	건너뛰는 간격 (기본값: 1)
    - 시작부터 끝 전까지 step 만큼 이동하며 요소 선택
- 예시
    ```
    s = 'abcdef'
    print(s[1:4])    # 'bcd' → 인덱스 1부터 3까지
    print(s[:3])     # 'abc' → 처음부터 2까지
    print(s[3:])     # 'def' → 3부터 끝까지
    print(s[::2])    # 'ace' → 0, 2, 4 (2칸씩)
    print(s[::-1])   # 'fedcba' → 역순
    ```
- **유연성: 인덱스 범위를 벗어나도 슬라이싱은 오류 없이 작동**
    - 예시
        ```
        s = 'abcdef'
        print(s[3:10])  # 'def' → s[3:]와 동일
        print(s[10:15]) # '' (빈 문자열)
        ```

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
- 참고
    - 문자열 내부에 있는 \n (newline)은 출력될 때 실제 줄바꿈을 발생시킴
        ```
        lines = ['a\n', 'b\n', 'c\n']
        print(*lines, sep='')

        # 출력
        a
        b
        c
        ```

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

# 제너레이터 표현식
- 파이썬에서 이터레이터(iterator)를 만들기 위한 간결하고 메모리 효율적인 방법
- 기본 구조
    ```
    (expression for item in iterable if condition)
    ```
    - expression: 반복할 때 계산할 값
    - item: 반복 변수
    - iterable: 반복 가능한 객체 (리스트, 튜플, range 등)
    - condition (선택): 조건을 만족하는 경우만 처리
- 반환값
    - generator 객체 (이터레이터의 일종)를 반환
    - 값을 하나씩 "지연 평가(lazy evaluation)"로 생성
    - 메모리 사용량이 매우 적음
- 예시
    ```
    # 제너레이터 표현식 만들기
    gen = (x * 2 for x in range(5))
    print(next(gen))  # 0
    print(next(gen))  # 2
    print(next(gen))  # 4
    # 한 번에 하나씩 값이 생성됨 (0, 2, 4, ...)

    # sum()과 함께 사용 (합계 구하기)
    total = sum(x for x in range(100) if x % 2 == 0)
    print(total)  # 2450

    # any() / all()과 함께 조건 검사
    any(x > 10 for x in [3, 7, 12])  # True
    all(x < 5 for x in [1, 2, 3])    # True

    # tuple(), set(), list() 등과 함께 변환
    tuple(x**2 for x in range(3))  # (0, 1, 4)
    set(x % 2 for x in range(5))   # {0, 1}
    list(x for x in 'abc')         # ['a', 'b', 'c']
    ```
- 주의
    - 이터레이터로써 for, next(), in 등에서 사용 가능
    - 한 번 사용하면 다시 사용할 수 없음, 다시 만들어서 사용
    - 메모리 효율적: 큰 데이터 처리에 유리 (전체 리스트를 만들지 않음)
    - 지연 평가: 실제 값은 꺼낼 때 계산됨 (next() 호출 시)

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

# 흐름 제어문

## 반복문

### for else 문
- 기본 구조
    ```
    for 변수 in 반복가능한객체:
        # 반복 실행할 코드
        if 어떤_조건:
            break  # 조건 만족하면 반복 중단
    else:
        # 반복이 끝나고, break 없이 "정상적으로" 종료된 경우 실행됨
    ```
    - for 루프가 정상적으로 모두 실행되면 → else 블록이 실행
    - for 루프 도중에 break로 빠져나오면 → else 블록은 실행되지 않음
    - for 루프가 아예 실행 안 돼도 break가 없으니 → else는 실행됨
- for-else는 조건 만족 여부를 판단하는 루프에서 유용
- else는 조건이 아니라 루프 종료 방식에 따라 실행됨
- break의 실행 유무가 else 실행의 키

## 패턴 매칭

### match case 문
- 패턴 매칭(Pattern Matching) 문법
- 기본 구조
    ```
    match 값:
        case 패턴1:
            실행문1
        case 패턴2:
            실행문2
        case _:
            기본 실행문 (default와 유사)
    ```
    - `case _`
        - 기본값 또는 else 역할
        - 어떤 패턴도 일치하지 않을 때 실행
- 예시
    ```
    # 정수 비교
    x = 2
    match x:
        case 1:
            print("1입니다.")
        case 2:
            print("2입니다.")
        case _:
            print("다른 숫자입니다.")
    
    # 튜플 매칭
    point = (0, 5)
    match point:
        case (0, y):
            print(f"y축 위의 점, y={y}")
        case (x, 0):
            print(f"x축 위의 점, x={x}")
        case (x, y):
            print(f"일반 좌표: ({x}, {y})")
    
    # 리스트 구조 매칭
    items = [1, 2, 3]
    match items:
        case [1, 2, 3]:
            print("정확히 1, 2, 3")
        case [1, *rest]:
            print(f"1로 시작하며 나머지는 {rest}")
        case _:
            print("일치하는 패턴 없음")
    
    # 딕셔너리 매칭 (부분 지원)
        - 일부 키만 지정해도 매칭 가능
    data = {"type": "user", "id": 42}
    match data:
        case {"type": "user", "id": id}:
            print(f"유저 ID는 {id}")
        case _:
            print("알 수 없는 데이터")
    ```
- Python 3.10 이상에서 사용 가능

## 예외 처리

### try except 문
- 프로그램 실행 중 발생할 수 있는 오류(예외)를 처리하기 위한 구문
- 기본 구조
    ```
    try:
    # 예외 발생 가능 코드
    except 예외종류:
        # 예외 처리
    else:
        # 예외가 없을 때 실행
    finally:
        # 무조건 실행 (예외 발생 여부와 무관)
    ```
    - try: 예외가 발생할 수 있는 코드
    - except: 예외 발생 시 실행할 코드
    - else: 예외가 없을 때 실행할 코드 (선택)
    - finally: 무조건 실행되는 코드 (선택)
- 예시
    ```
    # 0으로 나누기 예외 처리

    try:
        num = int(input("숫자를 입력하세요: "))
        print("100을", num, "으로 나누면:", 100 / num)
    except ValueError:
        print("숫자가 아닙니다!")
    except ZeroDivisionError:
        print("0으로는 나눌 수 없습니다!")
    else:
        print("정상적으로 계산되었습니다.")
    finally:
        print("프로그램 종료.")
    ```

<br>

---

<br>

# 키워드 (예약어)

## lambda
- **익명 함수(이름이 없는 함수)**를 만들 때 사용
- 일반적으로 `def` 키워드를 사용해 함수를 정의하지만, 간단한 함수를 짧게 표현하고 싶을 때 `lambda` 키워드를 사용
- 기본 구조
    ```
    lambda 매개변수: 표현식
    ```
    - 매개변수: 함수에 전달할 값 (0개 이상)
    - 표현식: 반환값을 계산하는 식 (단일 표현식만 가능)
- 예시
    ```
    # 기본적인 사용 두 수 더하기
    add = lambda x, y: x + y
    print(add(3, 5))  # 출력: 8

    # sorted()에서 key로 사용
    students = [("철수", 90), ("영희", 80), ("민수", 95)]
    sorted_students = sorted(students, key=lambda x: x[1])
    print(sorted_students)  # 점수 기준으로 정렬

    # map()과 함께 사용
    nums = [1, 2, 3, 4]
    squared = list(map(lambda x: x ** 2, nums))
    print(squared)  # [1, 4, 9, 16]

    # filter()와 함께 사용
    nums = [1, 2, 3, 4, 5]
    even = list(filter(lambda x: x % 2 == 0, nums))
    print(even)  # [2, 4]
    ```

<br>

---

<br>

# 구분자
- Delimiters

## ,
- 항목, 인자, 변수, 표현식 등을 나열하거나 구분할 때 사용하는 구분자
- 튜플 생성
    - 쉼표를 사용하면 튜플이 만들어짐
    - 괄호 없이도 ,만으로 튜플이 됨
    - 튜플 생성은 괄호가 아니라 쉼표가 핵심
        ```
        x = (1)    # int
        x = (1,)   # tuple
        x = 1,     # tuple
        ```
- 다중 변수 할당 (Multiple Assignment)
    - 좌변과 우변 모두 쉼표로 나눈 여러 값을 나열
        ```
        a, b = 1, 2
        ```
- Unpacking (언패킹 할당)
    - 좌변의 쉼표는 unpacking 문법의 일부로, *a가 iterable을 받을 수 있게 함
        ```
        *a, = [1, 2, 3]
        ```
    - 쉼표 없으면 문법 오류(SyntaxError)
- 함수 정의와 호출
    - 함수 인자들을 구분
- 리스트/딕셔너리/집합 항목 구분
    - 각 자료형의 요소/항목들을 구분
- return, yield 문에서 여러 값 반환
    ```
    def foo():
    return 1, 2

    x = foo()  # x == (1, 2)
    ```
    - 쉼표로 인해 튜플로 반환
- import 문에서 여러 모듈 나열
- 예외 처리에서 여러 예외 지정
    ```
    try:
        ...
    except (ValueError, TypeError) as e:
        ...
    ```
    - 괄호+쉼표 → 튜플로 예외 묶음

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
- `Walrus 연산자 :=`는 `대입 표현식 연산자`에 속하며, 전통적인 대입 연산자(=, += 등)와는 구분됨
    - 대입 계열이지만, 표현식 안에서 사용 가능한 특별한 형태
    - 우선 순위는 대입연산자의 바로 위 우선순위(대입 연산자보다 높음, 삼항 연산자보다 낮음)

## ^
- 정수 연산의 경우: 비트 연산자 XOR
    - 다른 비트는 1, 같은 비트는 0
        - 따라서 `자신^자신==0`, `자신^0==자신`
    - 결과: 정수
- **집합(set)** 연산의 경우: 집합 연산자 XOR, 대칭 차집합
    - 한쪽에만 있는 원소들 (A ∪ B) - (A ∩ B)
    - 결과: 집합
    - 사용 예: 중복 제거, 차이 찾기
- XOR은 교환법칙이 성립
    - 예시
        ```
        3^5 = 110 = 6
        5^3 = 110 = 6

        교환법칙이 성립하므로,
        2^7^2 = 2^2^7 = 0^7 = 7 성립
        이런 식으로 다른 하나의 원소를 골라낼 수 있음
        ```

## &
- 정수 연산의 경우: 비트 연산자 AND
    - 같은 자릿수의 비트가 모두 1일 때만 1
- **집합(set)** 연산의 경우: 교집함(intersection)
    - 예시
        ```
        a = set([1, 2, 3])
        b = set([2, 3, 4])

        print(a & b)  # → {2, 3}
        ```

## |
- 정수 연산의 경우: 비트 연산자 OR
    - 정수의 이진수 표현에서 각 비트 단위로 OR 연산을 수행
    - 두 비트 중 하나라도 1이면 결과 비트는 1
- **집합(set)** 연산의 경우: 합집합 (Union)
    - 두 집합을 합쳐서, 양쪽에 하나라도 있는 모든 원소를 포함한 새 집합을 만듬
    - 원소 중복 없이 하나로 합침
    - 예시
        ```
        a = {1, 2, 3}
        b = {3, 4, 5}

        print(a | b)  # 출력: {1, 2, 3, 4, 5}
        ```

## +
- 숫자형 연산의 경우: 덧셈을 의미
- 문자열 연산의 경우: 이어붙이는(연결하는) 기능
- 리스트, 튜플 등 시퀀스 자료형 연산의 경우 : 두 시퀀스를 합쳐서 새로운 시퀀스를 만듬
    - '+'연산자가 동작하는 주요 시퀀스형: list, tuple, str, bytes, bytearray
        - 순서가 있는 자료형에서만 동작
    - 안되는 시퀀스들: set, dict, range, frozenset, deque

## 나눗셈 연산자

### /
- 항상 float(실수) 값을 반환
- 결과가 정수더라도 .0이 붙음
- 예시
    ```
    print(7 / 2)   # 출력: 3.5
    print(10 / 5)  # 출력: 2.0
    ```

### //
- 정수 나눗셈 (버림 나눗셈, floor division)
- 결과를 소수점 아래 버리고, 정수 또는 소수로 반환
    - 정수끼리 연산하면 int, 실수 포함하면 float 반환됨
- 음수일 경우, 버림(floor) 처리를 해서 작은 쪽 정수로 내림
- 예시
    ```
    print(7 // 2)   # 출력: 3
    print(10 // 5)  # 출력: 2
    print(-7 // 2)   # 출력: -4
    print(7 // -2)   # 출력: -4
    ```

## 논리 연산자
- 논리 연산자의 우선순위
    1. not
    2. and
    3. or

### and
- 두 값이 모두 참일 때만 전체를 참(True)으로 만드는 논리 연산자
- 기본 개념
    ```
    A and B
    ```
    - A가 거짓이면, 그 값을 바로 반환하고 **B는 평가하지 않음**
        - 이것을 단축 평가 (short-circuit evaluation)라고 함
            - 논리 연산을 수행할 때, 결과가 이미 결정된 경우 남은 연산을 생략하는 것
            - 필요한 만큼만 계산하고, 나머지는 건너뛴다는 뜻
            - 오류 방지 가능
                ```
                user = get_user() and get_user().name
                # user가 None이면 user.name을 평가하지 않아서 AttributeError를 막을 수 있음
                ```
            - 성능 향상: 불필요한 계산을 자동으로 생략해서 속도가 빨라짐
    - A가 참이면, **B를 평가해서 그 값을 반환**함
- 예시
    ```
    True and True     # True
    True and False    # False
    False and True    # False
    0 and 5          # 결과: 0      (0은 False → 바로 반환)
    3 and 5          # 결과: 5      (3은 True → 5 반환)
    '' and 'hi'      # 결과: ''     (빈 문자열은 False)
    'hi' and 'hello' # 결과: 'hello' (둘 다 True → 마지막 값 반환)

    # 두 조건이 모두 참이어야 할 때
    if is_admin and is_active:
        print("관리자 접근 허용")
    
    # 값이 존재할 때 다음 동작 수행
    user = get_user() and get_user().name
    # user가 None이면 user.name을 평가하지 않아서 AttributeError를 막을 수 있음
    ```

### or
- 둘 중 하나라도 참이면 전체 결과를 참(True) 으로 만드는 역할
- 기본 개념
    ```
    A or B
    ```
    - A가 True이면, **B를 평가하지 않고** A를 반환
    - A가 False이면, **B를 평가**하고 B를 반환
    - 첫 번째 참 값을 반환
    - 모두 거짓이면 마지막 값을 반환
- 파이썬에서는 값 자체를 반환
    ```
    print(0 or 10)        # 10 (0은 False 취급)
    print("" or "Hello")  # "Hello" (빈 문자열은 False)
    print("Hi" or "Bye")  # "Hi" ("Hi"는 True 취급)
    ```
    - 파이썬에서 or는 불린값(True/False)뿐만 아니라 그 값을 직접 반환

### not
- 논리 부정(logical NOT) 을 수행하는 단항(boolean) 연산자
- 어떤 값의 참/거짓을 반대로 바꿔주는 역할
- 기본 개념
    ```
    not <값>
    ```
    - True → False
    - False → True
- not은 참/거짓처럼 평가되는 모든 값에 사용 가능
    - 파이썬에서 False로 간주되는 값들
        - None
        - False
        - 0, 0.0, 0j
        - 빈 문자열 ""
        - 빈 리스트 []
        - 빈 튜플 ()
        - 빈 딕셔너리 {}
        - 빈 세트 set()
    - 그 밖의 값은 모두 True로 간주

<br>

---

<br>

# 함수

## map()
- 이터러블(리스트, 튜플 등)의 모든 요소에 지정한 함수를 한 번씩 적용하고, 그 결과를 반환하는 함수
- 기본 구조
    ```
    map(function, iterable, ...)
    ```
    - function: 각 요소에 적용할 함수
    - iterable: 함수가 적용될 반복 가능한 객체 (리스트, 튜플 등)
    - 여러 개 iterable도 가능 (함수는 여러 인자를 받음)
- 반환값
    - map()은 map 객체(이터레이터)를 반환
    - 필요하면 list(), tuple() 등으로 변환해서 사용
- 주의점
    - map 객체는 한 번만 순회 가능 (이터레이터)
    - 순회 후 다시 사용하려면 다시 만들어야 함

## sorted()
- 반복 가능한 객체(iterable)를 정렬된 **리스트**로 반환
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
- 반환값
    - 정렬된 결과를 담은 새로운 **리스트 (list 객체)** 를 반환
    - 원래의 데이터를 변경하지 않고, 정렬된 복사본을 반환
        ```
        data = [3, 1, 4, 1, 5]
        result = sorted(data)

        print(result)  # [1, 1, 3, 4, 5] → 정렬된 새 리스트
        print(data)    # [3, 1, 4, 1, 5] → 원본은 그대로
        ```
    - iterable의 자료형과 상관없이 리스트 자료형을 반환
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
- `빈 세트형`을 만드는 방법
    - **`s=set()` 이렇게 사용**해야 함
    - *`s={}` 이렇게 하면 빈 딕셔너리임*
- 원소가 있는 집합은 `s={...}` 이렇게 사용하면 됨
- set 자료형의 저장과 탐색
    - set 자료형은 내부적으로 **해시 테이블(hash table)**을 사용해서 값을 저장
        - 해시 테이블(Hash Table)이란?
            - 해시 테이블은 키(또는 값)를 "해시 함수"로 숫자로 바꿔서, 배열의 특정 위치에 직접 저장하는 자료구조
            - 찾고 싶은 값을 직접 주소로 바꿔서 빠르게 찾아가는 방식
            - 예시
                ```
                hash("apple") → 5
                ```
                - "apple"이라는 값을 배열의 5번 인덱스에 저장
                - 검색할 때도 "apple" → hash("apple") → 5번 인덱스 → 바로 찾음
        - 값을 추가할 때 hash() 값을 기준으로 특정 슬롯(bucket)에 저장
        - 값을 검색할 때도 같은 방식으로 바로 해당 슬롯에 접근해서 확인
        - 리스트처럼 앞에서부터 하나씩(선형) 비교하지 않아도 됨
        - 해시 기반 탐색을 함
        - set의 요소는 hashable이어야 함
            - Hashable이란?
                - Hashable은 말 그대로 해시값을 가질 수 있는 객체를 뜻함
                - 파이썬에서 hash() 함수를 쓸 수 있고, 그 결과가 변하지 않는(immutable) 객체
                - 보통 불변(immutable) 객체가 hashable하며, 가변(mutable) 객체는 불가능
                - 해시 가능 여부는 객체의 `__hash__()` 메서드 존재 유무와 관련
            - 어떤 객체가 hashable일까?
                | 객체 타입        | 해시 가능 여부   | 이유                             |
                |------------------|-----------------|----------------------------------|
                | 정수 (int)       | 가능            | 변하지 않는 값                   |
                | 문자열 (str)     | 가능            | 불변(immutable) 객체             |
                | 튜플 (tuple)     | 가능(조건부)    | 튜플 내부가 모두 hashable일 때 가능 |
                | 리스트 (list)    | 불가능          | 내용 변경 가능(가변 객체)        |
                | 딕셔너리 (dict)  | 불가능          | 내용 변경 가능(가변 객체)        |
                | 집합 (set)       | 불가능          | 내용 변경 가능                   | 
    - 파이썬 set이 해시 테이블을 사용하는 방식
        - 값을 set에 추가할 때:
            - hash() 함수를 이용해 값을 숫자로 바꿈 (예: hash("banana") → 123456)
            - 그 숫자를 이용해서 내부 배열의 인덱스를 결정
            - 해당 위치에 값을 저장
        - 값을 검색할 때 (x in s):
            - hash(x)를 계산해서 저장된 위치를 바로 찾아감
            - 저장된 값과 일치하는지만 비교하고 바로 반환
    - 해시 기반 탐색 → 시간 복잡도:평균 O(1) / 최악 O(N) (해시 충돌이 극심한 경우지만 거의 없음)
        - 배열에서 값을 인덱스로 직접 접근하면 시간 복잡도는 O(1)
        - 해시 충돌이란?
            - 다른 두 값이 hash() 값이 같아지는 경우
            - 파이썬의 처리 방식: 오픈 어드레싱 방식
                - 같은 해시값이 나와도, 빈 자리를 찾아 옆으로 조금씩 이동하면서 저장
                - 검색 시에도 같은 방식으로 찾아감
                - 이 덕분에 해시 충돌이 생겨도 동작이 보장됨
                    - 다만 충돌이 많아지면 **성능이 O(1) → O(N)**에 가까워질 수 있음
    - Python의 `set`와 `dict`는 내부적으로 C로 구현된 해시 테이블 구조를 사용
        - `set`와 `dict`의 공통점과 차이점
            | 항목          | `set`                               | `dict`                                 |
            |---------------|--------------------------------------|-----------------------------------------|
            | **내부 구조** | 해시 테이블 (Hash Table)             | 해시 테이블 (Hash Table)               |
            | **저장 형태** | 값(`value`)만 저장                   | 키(`key`)와 값(`value`) 쌍으로 저장    |
            | **탐색 기준** | 값 자체                              | 키 기준                                 |
            | **삽입 예시** | `s.add('apple')`                     | `d['apple'] = 1`                        |
            | **조회 예시** | `'apple' in s`                       | `'apple' in d`                          |
            | **해시 대상** | 값 (`value`)                         | 키 (`key`)                              |
            | **중복 허용** | ❌ 중복 불가                          | ❌ 키 중복 불가 (값은 중복 가능)        |
            | **순서 보장** | Python 3.7+부터 삽입 순서 유지       | Python 3.7+부터 삽입 순서 유지         |
            | **사용 목적** | 빠른 포함 검사 (`in`)                 | 키-값 저장 및 조회                     |
            | **시간 복잡도** | 평균 O(1) for 추가/삭제/탐색        | 평균 O(1) for 추가/삭제/탐색           |
            | **해시 충돌 처리** | 오픈 어드레싱 등 내부 알고리즘 사용 | 동일                                    |

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
        - 시작값 따로 지정하지 않을 경우 `,`쓰지 말고 그냥 생략, `stop,step`만 넣으면 됨
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

## open()
- 파일을 열기 위해 사용하는 내장 함수
- 기본 구조
    ```
    f = open("파일명", "모드")
    ```
- 또다른 구조
    - `open()`은 파일 경로 대신 **파일 디스크립터(정수)**도 받을 수 있음
        - 파일 디스크립터: 운영체제 수준에서 열려 있는 파일/입출력 스트림에 대해 고유하게 부여되는 번호
            - 0: 표준 입력(stdin)을 파일 객체처럼 열 때 사용
            - 1: 표준 출력(stdout)
            - 2: 표준 에러(stderr)
        ```
        f = open(0)
        # 0번 파일 디스크립터인 **표준 입력(stdin)**을 텍스트 모드로 열가
        # 결과적으로 f는 사용자의 입력을 읽을 수 있는 파일 객체
        # 보통 input() 대신 좀 더 유연한 입력 처리를 원할 때 사용
        ```
    - 파이썬이 내부적으로 os.fdopen()을 활용해서 처리할 수 있기 때문
- `sys.stdin`과의 차이
    ```
    import sys
    f = sys.stdin
    ```
    - `open(0)`과 `sys.stdin`은 거의 같은 역할
    - `open(0)`은 표준 입력을 다시 열기 때문에, 원시적인 수준에서 파일처럼 다룰 수 있음
    - `sys.stdin`은 파이썬 인터프리터가 기본으로 열어주는 표준 입력 스트림
- `open(0)`
    - 파일 이름 대신 숫자 0을 인자로 주어 표준 입력(stdin)을 파일처럼 여는 것
    - 반환값은 TextIOWrapper 타입의 파일 객체
        - 이 객체를 사용해 `.read(), .readline(), .readlines(), .close()` 같은 파일 메서드를 사용 가능
        - 반환값은 iterable
            - 파일 객체는 내부적으로 __iter__()와 __next__() 메서드를 구현하고 있어서 
                for 루프에서 한 줄씩 자동으로 읽기 가능
            - itreable이지만 반환값 그 자체로는 인덱싱/슬라이싱 불가능
                - list 등의 인덱싱/슬라이싱이 가능한 자료형으로 변환 후 인덱싱/슬라이싱 가능

## ord()
- 문자 → 정수(유니코드 코드포인트 또는 아스키코드)로 변환
- 기본 구조
    ```
    ord(문자)
    ```
- ordinal의 약자
    - 순서상의, 순번의
- 몇가지 ASCII 코드
    - `NULL \0` : 0
    - `Tab \t` : 9
    - `줄바꿈 \n` : 10
    - `Space` : 32
    - `숫자 0 ~ 9` : 48 ~ 57
    - `대문자 A ~ Z` : 65 ~ 90
    - `소문자 a ~ z` : 97 ~ 122


## chr()
- 정수(유니코드 코드포인트 또는 아스키코드) → 문자로 변환
- 기본 구조
    ```
    chr(정수)
    ```
- character의 약자
    - 문자

## enumerate()
- 반복(iteration)할 때 **인덱스와 값을 동시에** 가져올 수 있는 함수
- *enumerate: 하나하나 열거하다, 번호를 붙이며 나열하다*
- 기본 구조
    ```
    for index, value in enumerate(iterable, start=0):
        ...
    ```
    - iterable: 리스트, 문자열, 튜플 등 반복 가능한 것
    - index: 현재 요소의 인덱스
    - value: 해당 인덱스의 실제 값
    - start=0: 인덱스를 몇부터 시작할지 (기본값은 0)
- 예시
    ```
    # 리스트에서 인덱스와 값 같이 얻기
    fruits = ['apple', 'banana', 'cherry']

    for i, fruit in enumerate(fruits):
        print(i, fruit)
            0 apple
            1 banana
            2 cherry
    
    # 인덱스를 1부터 시작하고 싶을 때
    for i, fruit in enumerate(fruits, start=1):
        print(i, fruit)
            1 apple
            2 banana
            3 cherry
    ```

## multimode()
- 주어진 리스트(혹은 문자열 등)에서 **최빈값(가장 자주 나오는 값)**을 리스트로 반환해주는 함수
- statistics 모듈에 포함된 함수
    - `from statistics import multimode` 해야함
- 파이썬 3.8 이상부터 사용 가능
- 기본 구조
    ```
    from statistics import multimode

    data = [1, 2, 2, 3, 3, 4]
    print(multimode(data))  # [2, 3]
    ```
    - data: iterable (반복 가능한 자료형)
        - 최빈값을 구할 대상 데이터. 문자열, 리스트, 튜플 등 반복 가능한 객체
- 반환값
    - data에서 가장 자주 등장한 값들을 **리스트**로 묶어 반환
    - 여러 값이 최빈값이라면 모두 포함
    - 단 하나의 최빈값만 있다면, 그것 하나만 리스트로
- 예시
    ```
    multimode(['a', 'b', 'b', 'c'])  # ['b']
    multimode([1, 1, 2, 2, 3])  # [1, 2]
    multimode(['x', 'y', 'z'])  # ['x', 'y', 'z']
    ```

## re.sub()
- 문자열 내에서 정규 표현식 패턴과 매칭되는 부분을 다른 문자열로 교체(replace)하는 함수
- 파이썬의 정규 표현식(Regular Expression) 모듈인 `re`에서 제공하는 함수
- `replace()`와의 비교
    - `replace()`가 단순 문자열 치환이라면, `re.sub()`는 복잡한 패턴 매칭을 지원하는 치환
- 기본 구조
    ```
    import re
    re.sub(pattern, repl, string, count=0, flags=0)
    ```
    - pattern: 정규 표현식 패턴 (찾고자 하는 문자열 규칙)
    - repl: 대체할 문자열 또는 함수
    - string: 검색 및 치환할 원본 문자열
    - count: 치환할 최대 횟수 (기본 0은 모두 치환)
    - flags: 정규식 옵션 (대소문자 무시 등)
- 반환값
    - string에서 pattern에 매칭되는 부분을 repl로 교체한 새 문자열을 반환
- 예시
    ```
    import re

    text = "apple 123 banana 456"
    result = re.sub(r"\d+", "#", text)  # 숫자 부분을 '#'으로 대체
    print(result)  # "apple # banana #"
    ```

## sum()
- 반복 가능한(iterable) 객체의 항목들을 왼쪽부터 오른쪽으로 합산하여 총합을 반환하는 내장 함수
- 기본 구조
    ```
    sum(iterable, start=0)
    ```
    - iterable: 리스트, 튜플, 제너레이터 등 반복 가능한 객체
        - bool 타입도 가능: True는 1, False는 0으로 취급
        - Decimal, Fraction 도 가능
            ```
            from decimal import Decimal
            from fractions import Fraction

            decimals = [Decimal('1.1'), Decimal('2.2')]
            print(sum(decimals))  # 출력: 3.3 (Decimal 타입)

            fractions = [Fraction(1, 3), Fraction(2, 3)]
            print(sum(fractions))  # 출력: 1
            ```
    - start: (선택) 합계를 시작할 초기값. 기본은 0
- 예시
    ```
    # 기본 사용
    numbers = [1, 2, 3, 4, 5]
    print(sum(numbers))  # 출력: 15

    # 초기값을 지정
    numbers = [1, 2, 3]
    print(sum(numbers, 10))  # 출력: 16 (10 + 1 + 2 + 3)
    ```
- 주의사항
    - 문자열의 합은 지원하지 않음
        -문자열을 합치려면 join()을 사용

## int()
- 정수(integer)를 생성하거나 변환하는 데 사용되는 내장 함수
- 기본 구조
    ```
    int(x=0, base=10)
    ```
    - x: 변환할 값 (문자열, 실수, 다른 숫자 타입 등)
    - base: 진법 (기본값은 10진수)
- 예시
    ```
    # 숫자 → 정수
    int(3.8)     # 3 (소수점 이하 버림)
    int(-2.9)    # -2
    소수점을 버리고 가장 가까운 정수로 내림

    # 문자열 → 정수
    int("123")       # 123
    int("-52")       # -52
    int("10", 2)     # 2 (이진수 문자열 → 10진수)
    int("1A", 16)    # 26 (16진수 문자열 → 10진수)
    문자열을 정수로 변환할 때는 문자열이 유효한 숫자 형식이어야 하며, base를 지정하면 해당 진법으로 해석

    # 다른 타입
    int(True)   # 1
    int(False)  # 0
    bool 타입도 int()로 변환 가능하며, True는 1, False는 0
    ```
- 예외
    - 문자열이 정수로 변환될 수 있는 형태가 아니거나, 타입이 아예 안 맞는 경우 예외가 발생

## all()
- iterable(반복 가능한 객체)을 받아서 
    그 안에 있는 모든 값이 참(True)이면 True를 반환하고, 하나라도 거짓(False)이면 False를 반환하는 함수
- 빈 리스트나 튜플을 넣으면 True를 반환(**"거짓이 없음" = "모두 참"**으로 간주하기 때문)
- 단순히 True/False만 넣는 게 아니라, 조건을 넣어서 자동 판별도 가능
    - for 루프와 함께 자주 사용 → 조건이 전부 만족되는지 검사할 때 유용
- 기본 구조
    ```
    all(iterable)
    ```
- 예시
    ```
    all([True, True, True])
    # → True

    all([True, False, True])
    # → False

    all([])  # 빈 리스트
    # → True  (중요!)

    단순히 True/False만 넣는 게 아니라, 아래처럼 조건을 넣어서 자동 판별도 가능
    nums = [2, 4, 6, 8]
    all(n % 2 == 0 for n in nums)
    # → True (모든 수가 짝수니까)

    nums = [2, 3, 4]
    all(n % 2 == 0 for n in nums)
    # → False (3은 홀수라서)
    ```

## permutations()
- 순열을 구할 때 사용하는 함수
    - 순열: 주어진 항목들 중에서 일부 또는 전부를 선택해서 순서를 고려하여 나열한 것
        - 전체 순열: n개의 원소 → n!
        - 부분 순열: n개 중 r개를 고름 → nPr = n! / (n - r)!
- itertools 모듈에 포함
- 기본 구조
    ```
    from itertools import permutations

    itertools.permutations(iterable, r=None)
    ```
    - iterable: 반복 가능한 객체 (예: 리스트, 문자열, 튜플 등)
    - r (선택): 순열을 구성할 원소 개수, 생략하면 기본값은 len(iterable) — 즉, 전체 순열을 생성함
        - r을 지정하면, iterable에서 r개를 선택해 만들 수 있는 모든 순열이 생성됨
        - 순열이므로 순서가 다르면 다른 결과로 간주됨
- 반환값
    - 반환값은 **이터레이터(iterator)**
    - 각 순열은 튜플(tuple) 형태로 반환
    - 반복문 또는 list()로 변환하여 사용 가능
    ```
    from itertools import permutations

    perm = permutations([1, 2, 3])
    print(type(perm))  # <class 'itertools.permutations'>
    print(next(perm))  # (1, 2, 3)
    ```
- 예시
    ```
    # 예시 1: 전체 순열

    from itertools import permutations

    data = [1, 2, 3]
    result = list(permutations(data))

    print(result)
    # 출력: [(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)]
    # 3! = 6개의 순열이 생성

    # 예시 2: 부분 순열 (r 지정)

    from itertools import permutations

    data = ['A', 'B', 'C']
    result = list(permutations(data, 2))

    print(result)
    # 출력: [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
    # 3P2 = 6개의 순열 생성
    # 2개씩 뽑되 순서를 고려함

    # 문자열에서도 사용 가능

    from itertools import permutations

    word = "abc"
    result = list(permutations(word))

    print(result)
    # 출력: [('a', 'b', 'c'), ('a', 'c', 'b'), ('b', 'a', 'c'), ...]
    # 반환된 각 튜플을 문자열로 합치고 싶다면:
    [''.join(p) for p in permutations(word)]
    # 출력: ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
    ```
    - 중복 제거를 원하면 set()으로 감쌀 수 있음

## combinations()
- 조합을 구할 때 사용하는 함수
    - 조합: 주어진 항목들 중에서 일부를 선택하는 경우의 수, 선택한 순서는 고려하지 않음
        - "A와 B를 뽑는 것"과 "B와 A를 뽑는 것"은 같은 조합
    - nCr = n! / (r! × (n - r)!)
- 기본 구조
    ```
    from itertools import combinations

    itertools.combinations(iterable, r)
    ```
    - iterable: 리스트, 튜플, 문자열 등 반복 가능한 객체
    - r (필수): 조합을 구성할 원소의 개수 (반드시 지정해야 함)
- 반환값
    - 조합의 튜플을 담은 이터레이터(iterator)를 반환
    - 각 조합은 정렬된 원소의 튜플로 표현
    - 순서를 고려하지 않기 때문에 (A, B)와 (B, A)는 하나만 포함됨
- 예시
    ```
    # 예시 1: 숫자 리스트에서 조합

    from itertools import combinations

    data = [1, 2, 3]
    result = list(combinations(data, 2))

    print(result)
    # 출력: [(1, 2), (1, 3), (2, 3)]
    # 3개의 원소 중 2개를 뽑는 모든 조합을 반환
    # 3C2 = 3가지 조합

    # 예시 2: 문자열에서 조합

    from itertools import combinations

    word = "ABC"
    result = list(combinations(word, 2))

    print(result)
    # 출력: [('A', 'B'), ('A', 'C'), ('B', 'C')]
    # 문자열도 iterable이므로 조합 생성 가능
    # 문자열로 합치고 싶다면:
    [''.join(p) for p in combinations(word, 2)]
    # 출력: ['AB', 'AC', 'BC']

    # 예시 3: 중복된 원소가 있을 때

    from itertools import combinations

    data = [1, 1, 2]
    result = list(combinations(data, 2))
    print(result)
    # 출력: [(1, 1), (1, 2), (1, 2)]
    # 입력에 중복이 있으면 결과에도 중복된 조합이 나올 수 있음
    # 하지만 combinations() 자체는 중복된 조합을 의도적으로 생성하지는 않음
    ```

## 곱집합 (Cartesian Product)
- 두 개 이상의 집합의 모든 가능한 순서쌍(또는 순서튜플)을 만든 것
    - 마치 중첩된 for문처럼 작동
    - 중복 순열의 개념과 동일
- 원소를 중복해서 사용 가능
- 순서를 중요하게 여김 (즉, (A, B) ≠ (B, A))
- 기본 구조
    ```
    from itertools import product

    itertools.product(*iterables, repeat=1)
    ```
    - *iterables: 반복 가능한 객체들
    - repeat: 곱집합을 자기 자신과 몇 번 반복할지 지정 (기본값 1)
- 반환값
    - 튜플들의 반복자(iterator) 반환
- 예시
    ```
    rom itertools import product

    result = list(product('AB', repeat=2))
    print(result)
    # 출력: [('A', 'A'), ('A', 'B'), ('B', 'A'), ('B', 'B')]
    # 'A'와 'B' 중 2개를 중복해서 골라, 가능한 모든 순열을 생성
    ```

## 중복 조합
- 주어진 요소들 중에서 중복을 허용하면서 순서 없이 r개를 선택
- 순서는 상관없고, 중복은 가능
- 기본 구조
    ```
    from itertools import combinations_with_replacement

    itertools.combinations_with_replacement(iterable, r)
    ```
    - iterable: 조합의 대상 (리스트, 문자열 등)
    - r: 선택할 항목 개수
- 반환값
    - 중복을 허용하는 조합들을 생성하는 이터레이터(iterator)
    - 중복 허용, 순서 비중 없음, 사전순(정렬된) 결과를 반환
- 예시
    ```
    mport itertools

    data = ['A', 'B', 'C']
    r = 2

    result = itertools.combinations_with_replacement(data, r)

    for item in result:
        print(item)
    
    # 출력
    ('A', 'A')
    ('A', 'B')
    ('A', 'C')
    ('B', 'B')
    ('B', 'C')
    ('C', 'C')
    ```

## next()
- 이터레이터(iterator)에서 다음 값을 하나씩 꺼내는 함수
- 보통 for 루프 내부에서 자동으로 사용
- 수동으로 반복을 제어할 때 유용
- 기본 구조
    ```
    next(iterator[, default])
    ```
    - iterator: 다음 값을 꺼낼 이터레이터 객체
    - default(선택): 더 이상 꺼낼 값이 없을 때 반환할 기본값. 없으면 StopIteration 예외 발생
- 반환값
    - 이터레이터의 다음 값을 반환
    - 만약 더 이상 꺼낼 값이 없으면:
        - default 인자가 있으면 → 기본값 반환
        - default 인자가 없으면 → StopIteration 예외 발생
- 예시
    ```
    # 예제 1: 기본 사용
    numbers = [1, 2, 3]
    it = iter(numbers)  # 리스트를 이터레이터로 변환

    print(next(it))  # 1
    print(next(it))  # 2
    print(next(it))  # 3
    # print(next(it))  # 오류 발생: StopIteration

    # 예제 2: default 값 사용
    numbers = [1, 2]
    it = iter(numbers)

    print(next(it, '끝'))  # 1
    print(next(it, '끝'))  # 2
    print(next(it, '끝'))  # '끝' (이터레이터 끝나서 기본값 반환)

    # 예제 3: 반복문 없이 이터레이터 직접 처리
    text = "Hi"
    it = iter(text)

    while True:
        try:
            char = next(it)
            print(char)
        except StopIteration:
            break
    # 출력: 
    # H
    # i
    ```

## dict()
- 딕셔너리(dictionary)를 만드는 내장 함수
    - 딕셔너리는 key–value 쌍을 저장하는 자료구조
- 기본 구조
    ```
    dict([iterable_or_mapping], **kwargs)
    ```
    - iterable_or_mapping (선택):
        - (key, value) 쌍의 이터러블
        - 또는 딕셔너리 형태의 매핑 객체
    - **kwargs (선택):
        - 키워드 인자 형태의 key=value 쌍
- 반환값
    - 새로 만든 딕셔너리 객체(dict)를 반환
- 예시
    ```
    # 빈 딕셔너리 만들기
    d = dict()
    print(d)
    # 출력: {}   # 빈 딕셔너리

    # 튜플 리스트로 만들기 (iterable 인자)
    d = dict([('a', 1), ('b', 2)])
    print(d)
    # 출력: {'a': 1, 'b': 2}

    # 다른 딕셔너리로부터 생성 (mapping 인자)
    d = dict({'x': 10, 'y': 20})
    print(d)
    # 출력: {'x': 10, 'y': 20}

    # 키워드 인자 사용 (**kwargs)
    d = dict(name='Alice', age=30)
    print(d)
    # 출력: {'name': 'Alice', 'age': 30}
    # 문자열 키일 때만 사용 가능, 변수명 규칙 따라야 함

    # zip()과 함께 사용
    keys = ['a', 'b', 'c']
    values = [1, 2, 3]
    d = dict(zip(keys, values))
    print(d)
    # 출력: {'a': 1, 'b': 2, 'c': 3}
    ```
- 주의
    - 키는 해시 가능(hashable) 해야 함 → 숫자, 문자열, 튜플(불변) 등
    - (key, value) 형식이 잘못되면 오류 발생

## Counter()
- 파이썬 표준 라이브러리의 `collections 모듈`에 포함된 데이터 계수기
- 반복 가능한(iterable) 객체에서 요소의 개수를 셀 때 유용한 클래스
- 내부적으로는 딕셔너리처럼 작동하지만 값은 항상 정수로 요소의 개수를 나타냄
- dict를 확장해서 빈도수 계산에 특화된 기능들을 추가한 클래스
- 기본 구조
    ```
    from collections import Counter

    Counter(iterable_or_mapping)
    ```
    - iterable_or_mapping: 문자열, 리스트, 튜플 같은 반복 가능한 객체(iterable) 또는 딕셔너리 형식(mapping)
- 반환값
    - 각 요소의 등장 횟수(빈도수) 를 세어 딕셔너리 형태로 반환
    - Counter 객체는 딕셔너리처럼 생겼으며, 각 요소를 키(key)로 하고 그 빈도(횟수)를 값(value)으로 가짐
    - 내부적으로는 dict를 상속한 클래스이지만, 값을 자동으로 정수로 관리
    - 존재하지 않는 키에 접근하면 자동으로 0을 반환
- 예시
    ```
    # 예제 1: 문자열에서 문자 개수 세기
    from collections import Counter

    text = "hello world"
    counter = Counter(text)
    print(counter)
    #출력: Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

    # 예제 2: 리스트에서 항목 빈도수 세기
    fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
    fruit_count = Counter(fruits)
    print(fruit_count)
    #출력: Counter({'apple': 3, 'banana': 2, 'orange': 1})

    # 예제 3: 가장 많이 등장한 요소 추출
    print(fruit_count.most_common(2))
    #출력: [('apple', 3), ('banana', 2)]

    # 예제 4: 요소 합치기 / 빼기
    a = Counter(['a', 'b', 'a', 'c'])
    b = Counter(['a', 'b', 'b', 'd'])

    print(a + b)     # 합치기
    print(a - b)     # 빼기
    #출력:
    Counter({'a': 3, 'b': 2, 'c': 1, 'd': 1})
    Counter({'a': 1, 'c': 1})
    ```
- 사용 가능한 주요 메서드
    - 실제로 dict의 서브클래스이므로 대부분의 딕셔너리 메서드를 사용 가능
    - 요약 표
        | 메서드                       | 설명                  |              |
        | ------------------------- | ------------------- | ------------ |
        | `elements()`              | 개수만큼 요소 반복          |              |
        | `most_common([n])`        | 가장 흔한 요소 반환         |              |
        | `subtract()`              | 다른 Counter에서 개수 감산  |              |
        | `update()`                | 다른 Counter에서 개수 가산  |              |
        | `clear()`                 | 모든 항목 제거            |              |
        | `copy()`                  | 얕은 복사본 반환           |              |
        | `total()`                 | 전체 개수 합계 반환 (3.10+) |              |
        | 산술 연산자 (`+`, `-`, `&`, \` | \`)                 | 요소별 빈도 계산 수행 |
    - dict와 공통된 메서드
        - update(), clear(), copy() 등 기본적인 컬렉션 메서드
    - Counter만의 고유 메서드 및 기능
        - elements(), most_common(), subtract(), total()
        - 산술 연산자 (+, -, &, |)

## gcd()
- 최대공약수 (GCD: Greatest Common Divisor)
- 기본 구조
    ```
    import math

    math.gcd(a, b)
    ```
    - 매개변수: a, b는 정수 (음수도 가능)
        - 음수는 절댓값 기준
    - **a, b, ... : Python 3.9부터 세 개 이상의 인자를 사용 가능**
- 반환값
    - a와 b의 최대공약수(GCD)를 정수로 반환
- 예시
    ```
    import math

    print(math.gcd(12, 18))  # 출력: 6
    print(math.gcd(-12, 18)) # 출력: 6 (음수여도 절댓값 기준)
    print(math.gcd(17, 5))   # 출력: 1 (서로소)
    ```    
- Python 버전
    - math.gcd()는 Python 3.5 이상에서 사용 가능

## lcm()
- 최소공배수 (LCM: Least Common Multiple)
- 기본 구조
    ```
    import math

    math.lcm(a, b, ...)
    ```
    - 매개변수: a, b, ...은 최소공배수를 구할 두 개 이상의 정수
- 반환값
    - 입력된 모든 수의 최소공배수
    - lcm(a, b)에서 하나라도 0이면 결과는 0
    - math.lcm()은 내부적으로 math.gcd()를 사용
        ```
        예를 들어 직접 lcm()을 만들면,
        import math

        def lcm(a, b):
        return abs(a * b) // math.gcd(a, b)
        ```
- 예시
    ```
    import math

    print(math.lcm(6, 8))         # 출력: 24
    print(math.lcm(4, 6, 8))      # 출력: 24
    print(math.lcm(3, 5, 7))      # 출력: 105
    print(math.lcm(10, 0))        # 출력: 0
    ```
- Python 버전
    - math.lcm은 Python 3.9 이상에서만 사용 가능

## deque()
- "double-ended queue"의 줄임말
- 양쪽 끝에서 데이터를 추가(append, appendleft)하거나 제거(pop, popleft) 가능
- 기본 구조
    ```
    from collections import deque

    q=deque()
    ```
    - deque()는 비어 있는 덱(큐)을 생성
    - list와 비슷하지만, 양쪽 끝 삽입/삭제가 빠름
    - list처럼 초기값을 넣어 생성 가능
        ```
        q = deque([10, 20, 30])
        print(q)  # deque([10, 20, 30])

        q = deque("abc")
        print(q)  # deque(['a', 'b', 'c'])
        ```
- 반환값
    - 반환되는 객체는 collections.deque 클래스의 인스턴스
    - deque()는 빈 덱(큐)을 생성
        ```
        from collections import deque
        q = deque()
        print(q)    # 출력: deque([])
        print(type(q))  # 출력: <class 'collections.deque'>
        ```
- deque와 list는 비교 불가능
    ```
    from collections import deque

    q = deque([1])
    print('10'[q > []])  # TypeError 발생

    # [q>[]]를 사용하고 싶다면 deque를 리스트로 변경 후 비교
    q = deque([1])
    print('10'[list(q) > []])  # 출력: '0'

    # 혹은 not을 사용
    q = deque([1])
    print('01'[not q])  # 정상 작동, 출력: '0'
    ```

<br>

---

<br>

# 메서드

## 리스트 메서드

### sort()
- 리스트의 원본 자체를 정렬하며, 새 리스트를 반환하지 않음
- 기본 구조
    ```
    list.sort(key=None, reverse=False)
    ```
    - key: 정렬 기준이 되는 함수를 지정 (len, str.lower 등)
    - reverse: 기본값은 False (오름차순), True일 경우 내림차순
- 반환값
    - 리턴값은 None
    - 리스트를 제자리(in-place)에서 정렬하므로, 정렬된 결과가 원본 리스트에 적용
    - 리스트 자체를 정렬하며, 리턴값이 없는 메서드
- 예시
    ```
    # 기본 오름차순 정렬
    numbers = [5, 2, 9, 1]
    numbers.sort()
    print(numbers)  # [1, 2, 5, 9]

    # 내림차순 정렬
    numbers = [5, 2, 9, 1]
    numbers.sort(reverse=True)
    print(numbers)  # [9, 5, 2, 1]

    # key 인자 사용 — 문자열 길이 기준 정렬
    words = ["banana", "apple", "kiwi"]
    words.sort(key=len)
    print(words)  # ['kiwi', 'apple', 'banana']

    # key 인자 사용 — 대소문자 무시하고 정렬
    words = ["Banana", "apple", "Cherry"]
    words.sort(key=str.lower)
    print(words)  # ['apple', 'Banana', 'Cherry']

    # 주의: 반환값은 None
    my_list = [3, 1, 2]
    result = my_list.sort()

    print(result)  # None ← 반환값 없음
    print(my_list) # [1, 2, 3] ← 원본이 정렬됨
    ```

### pop()
- 리스트에서 요소를 꺼내고 리스트에서 제거
- 괄호 안에 인덱스를 지정할 수도 있고, 생략하면 기본적으로 마지막 요소를 제거
- 제거된 요소를 반환(return)하므로, 변수에 담거나 바로 사용 가능
- 기본 구조
    ```
    list.pop()           # 마지막 요소를 제거하고 반환
    list.pop(index)      # 지정한 위치(index)의 요소를 제거하고 반환
    ```
- 반환값
    - 제거된 요소를 반환
    - 리스트에서 제거는 되지만, 그 값을 다시 쓸 수 있도록 반환
    - 주의
        - *리스트가 비어 있으면 pop()은 IndexError를 발생*
- 예시
    ```
    # 예제 1: 기본 pop (마지막 요소)
    a = [1, 2, 3]
    v = a.pop()
    print(v)    # 출력: 3
    print(a)    # 출력: [1, 2]

    # 예제 2: 인덱스 지정해서 pop
    a = ['a', 'b', 'c', 'd']
    v = a.pop(1)
    print(v)    # 출력: 'b'
    print(a)    # 출력: ['a', 'c', 'd']

    # 예제 3: 조건문으로 안전하게 사용
    stack = []
    if stack:
        print(stack.pop())
    else:
        print("스택이 비어있음")
    ```

### remove()
- 리스트에서 값 x를 찾아 가장 첫 번째 항목을 제거
- 기본 구조
    ```
    list.remove(x)
    ```
- 반환값: None
- 값이 없으면 ValueError 발생

## 문자열 메서드

### split()
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
- 반환값
    - 구분자를 기준으로 나누어진 문자열 조각들을 **리스트** 자료형으로 반환
- 예시
    ```
    "a b  c\n d".split()          # ['a', 'b', 'c', 'd']
    "a,b,c".split(',')            # ['a', 'b', 'c']
    "1-2-3".split('-', 1)         # ['1', '2-3']
    ```

### rsplit()
- **구분자(sep)**를 기준으로 오른쪽에서부터 문자열을 나눔
- 기본 구조
    ```
    rsplit(sep=None, maxsplit=-1)
    ```
- 예시
    ```
    "1-2-3".rsplit('-', 1)       # ['1-2', '3']
    ```

### splitlines()
- 줄 단위로 나눔 (\n, \r, \r\n 등 모두 인식)
    - `\n` (LF: Line Feed, 유닉스/리눅스)
    - `\r` (CR: Carriage Return, 구형 Mac)
    - `\r\n` (CRLF: Windows)
- 기본 구조
    ```
    splitlines(keepends=False)
    ```
    - keepends: 줄바꿈 문자를 결과에 포함할지 여부 (False가 기본값)
        - True면 줄바꿈 문자도 포함
- 예시
    ```
    s = "line1\nline2\rline3\r\nline4"
    s.splitlines()
    # ['line1', 'line2', 'line3', 'line4']

    s.splitlines(keepends=True)
    # ['line1\n', 'line2\r', 'line3\r\n', 'line4']

    text = "a\n\nb"
    print(text.splitlines())  
    # 결과: ['a', '', 'b']
    → 줄 사이에 빈 줄(\n\n)이 있어도 빈 문자열로 포함
    ```

### partition()
- **특정 구분자(sep)**를 기준으로 문자열을 3부분으로 분리
    - 앞부분, sep, 뒷부분
- 기본 구조
    ```
    str.partition(sep)
    ```
    - `sep`: 분할 기준이 되는 문자열
        - 구분자가 처음 등장하는 위치에서 한번만 분리
    - 결과는 **튜플 (앞부분, sep, 뒷부분)**로 반환
- 예시
    ```
    s = "key=value"
    result = s.partition("=")
    print(result)
    # 출력: ('key', '=', 'value')

    s = "hello"
    print(s.partition("="))
    # 출력: ('hello', '', '')
    ```
    - 구분자가 없으면 전체가 첫 번째 요소로 들어감
    - 나머지 두 요소는 빈 문자열

### rpartition()
- 가장 마지막에 나오는 구분자(sep)를 기준으로 문자열을 3부분으로 분리
    - 오른쪽에서 부터 분리
- 기본 구조
    ```
    str.rpartition(sep)
    ```
    - `(앞부분, sep, 뒷부분)` 형태의 **튜플**을 반환
    - sep가 문자열에 없으면 `()'', '', 원본 문자열)` 이 반환
- 예시
    ```
    s = "user=name=alice"
    print(s.rpartition("="))
    # 출력: ('user=name', '=', 'alice')
    → 마지막 '=' 기준으로 나눔

    s = "hello"
    print(s.rpartition(":"))
    # 결과: ('', '', 'hello')
    sep이 없으면 ('', '', 원본문자열) 튜플 반환
    ```

### join()
- **문자열 리스트(또는 이터러블)**를 하나의 문자열로 구분자와 함께 이어 붙이는 메서드
- 기본 구조
    ```
    '구분자'.join(반복가능한_문자열들)
    ```
    - '구분자': 문자열 사이에 넣을 텍스트 (예: " ", ",", "\n" 등)
    - 반복가능한_문자열들: 문자열들로 구성된 리스트, 튜플 등
        - join()의 인자는 반드시 문자열들이 iterable이어야 함 (list, tuple, set, 등)
        - 숫자 같은 문자열이 아닌 요소가 포함되어 있으면 TypeError
            - TypeError 예시
                ```
                nums = ['1', 2, '3']
                print(','.join(nums))  # TypeError: sequence item 1: expected str instance, int found
                ```
                - 반드시 모든 요소가 문자열이어야 함
- 예시
    ```
    words = ['apple', 'banana', 'cherry']
    result = ', '.join(words)
    print(result)  # apple, banana, cherry
    ```

### find()
- 문자열 안에서 특정 문자열(문자 또는 문자열)을 찾아서, 처음 등장하는 위치(인덱스)를 반환하는 문자열 메서드
- 기본 구조
    ```
    string.find(substring, start=0, end=len(string))
    ```
    - `substring`: 찾고자 하는 부분 문자열 (필수)
    - `start`: 검색을 시작할 인덱스 (기본: 0)
    - `end`: 검색을 멈출 인덱스 (기본: 문자열 끝까지)
- 반환값
    - 찾으면: 처음 등장하는 인덱스 (int) (0부터 시작)
    - **없으면: -1 (int)**
- 예시
    ```
    text = "hello world"
    print(text.find("o"))     # 결과: 4
    print(text.find("world")) # 결과: 6
    print(text.find("z"))     # 결과: -1

    text = "banana"
    print(text.find("a", 2))        # 결과: 3 (인덱스 2부터 찾음)
    print(text.find("a", 2, 4))     # 결과: 3 (인덱스 2~3까지만 탐색)
    print(text.find("a", 4, 6))     # 결과: 5
    print(text.find("a", 6))        # 결과: -1
    ```

### replace()
- 문자열(string)에서 부분 문자열을 다른 문자열로 바꾸는 메서드
- 기본 구조
    ```
    str.replace(old, new[, count])
    ```
    - old: 바꾸고자 하는 기존 부분 문자열 (필수)
    - new: 대체할 새 문자열 (필수)
    - count: 바꿀 횟수 (선택, 기본값은 모든 항목을 바꿈)
        - *`[, count]`이 표기는 문서나 설명에서 해당 매개변수가 선택적이라는 뜻*
- 반환값
    - old를 new로 바꾼 **새로운 문자열(str)**을 반환
    - `원본 문자열을 변경하지 않고, 새로운 문자열을 반환`
    - 문자열은 불변(immutable)하기 때문에 replace()를 호출해도 원본 문자열에는 아무런 영향을 주지 않음
    - 따라서 `i=i.replace(a,b)` 형식으로 사용해야 원본을 바꿀 수 있음
- 예시
    ```
    # 기본 사용
    text = "apple banana apple"
    new_text = text.replace("apple", "orange")
    print(new_text)  # "orange banana orange"

    # 특정 횟수만 교체 (count 인자 사용)
    text = "apple apple apple"
    new_text = text.replace("apple", "orange", 2)
    print(new_text)  # "orange orange apple"

    # 원본 문자열 유지 확인
    text = "hello world"
    text.replace("world", "python")
    print(text)  # "hello world"  (원본 그대로)
    ```
- 주의 사항
    - 대소문자를 구분
    - old에 해당하는 부분 문자열이 없으면 변경 없이 원본 문자열 그대로 반환
    - count가 0이면 아무 것도 변경되지 않음

## 세트 메서드

### add()
- 집합에 **요소 하나**를 추가
- 기본 구조
    ```
    set.add(element)
    ```
    - 반환값 없음 (None)
    - 집합 객체를 그 자리에서 직접 변경

### update()
- 집합에 **iterable(반복 가능한 객체)한 요소**들을 추가
- 기본 구조
    ```
    set.update(iterable)
    ```
    - iterable: 리스트, 튜플, 세트, 문자열 등 반복 가능한 객체
    - 반환값 없음 (None)
    - 기존 세트를 변경
- 예시
    ```
    a = {1, 2}
    a.update([3, 4])
    print(a)  # 출력: {1, 2, 3, 4}

    a.update("56")
    print(a)  # 출력: {1, 2, 3, 4, '5', '6'}
    문자열 "56"은 문자 하나하나가 세트에 추가됨
    ```

### remove()
- 세트에서 특정 요소를 제거
- 기본 구조
    ```
    set.remove(element)
    ```
    - element : 집합에서 제거하고자 하는 특정 값(요소)
        - element가 집합에 없으면, KeyError 예외 발생
- 예시
    ```
    s = {10, 20, 30}
    s.remove(20)  # 20 제거
    print(s) -> s는 {10, 30}

    s.remove(40)  # 40이 없으므로 KeyError 발생
    ```

### discard()
- 세트에서 특정 요소를 제거
- 기본 구조
    ```
    set.discard(element)
    ```
    - element : 집합에서 제거하고자 하는 특정 값(요소)
        - element가 집합에 없으면 그냥 무시하고 아무런 예외도 발생하지 않음
- 예시
    ```
    s = {10, 20, 30}
    s.discard(20)  # 20 제거
    print(s) -> s는 {10, 30}

    s.discard(40)  # 40이 없지만 예외 발생 안 함
    print(s)       # 여전히 {10, 30}
    ```
- remove() vs discard()
    - remove는 "이 요소가 반드시 있어야 한다"는 전제 하에 사용
    - discard는 "있으면 지우고 없으면 무시하자"는 경우에 사용

### clear()
- 세트(set)의 모든 원소를 삭제
- 세트는 빈 세트가 됨
- 기본 구조
    ```
    set.clear()
    ```
- 예시
    ```
    s = {1, 2, 3, 4}
    s.clear()
    print(s)  # 출력: set()
    ```

## 딕셔너리 메서드

### get()
- 딕셔너리에서 특정 키에 해당하는 값을 가져오는 메서드
- 기본 구조
    ```
    dict.get(key, default=None)
    ```
    - key (필수): 찾으려는 키
    - default (선택, 기본값: None): 키가 없을 때 반환할 값
- 반환값
    - 키에 대응하는 값 또는 default
    - default가 없으면 None을 반환
- 반환값 타입
    - 키에 매핑된 값의 타입 또는 default 타입
- 예시
    ```
    d = {'a': 1, 'b': 2}
    print(d.get('a'))        # 출력: 1
    print(d.get('c'))        # 출력: None
    print(d.get('c', 0))     # 출력: 0
    ```

### keys()
- 딕셔너리의 모든 키를 담은 뷰 객체를 반환
- 기본 구조
    ```
    dict.keys()
    ```
- 반환값
    - 딕셔너리의 키를 모두 포함한 뷰 객체
- 반환값 타입
    - dict_keys 객체 (반복 가능)
- 예시
    ```
    d = {'a': 1, 'b': 2}
    print(d.keys())          # 출력: dict_keys(['a', 'b'])
    ```

### values()
- 딕셔너리의 모든 값을 담은 뷰 객체를 반환
- 기본 구조
    ```
    dict.values()
    ```
- 반환값
    - 딕셔너리의 값을 모두 포함한 뷰 객체
- 반환값 타입
    - dict_values 객체 (반복 가능)
- 예시
    ```
    d = {'a': 1, 'b': 2}
    print(d.values())        # 출력: dict_values([1, 2])
    ```

### items()
- 딕셔너리의 모든 (키, 값) 쌍을 담은 뷰 객체를 반환
- 기본 구조
    ```
    dict.items()
    ```
- 반환값
    - (키, 값) 튜플들의 뷰 객체
- 반환값 타입
    - dict_items 객체 (반복 가능, 요소는 (key, value) 튜플)
- 예시
    ```
    d = {'a': 1, 'b': 2}
    print(d.items())         # 출력: dict_items([('a', 1), ('b', 2)])
    ```

### update()
- 다른 딕셔너리나 키-값 쌍 iterable로 현재 딕셔너리를 업데이트
- 기본 구조
    ```
    dict.update(other)
    ```
    - other (선택): 딕셔너리 또는 키-값 쌍 iterable
        - 인자를 생략할 경우, 딕셔너리는 그대로 유지되고 아무 작업도 하지 않음
- 반환값
    - 없음 (None), 원본 딕셔너리를 직접 수정
- 예시
    ```
    d = {'a': 1, 'b': 2}
    d.update({'b': 3, 'c': 4})
    print(d)  # {'a': 1, 'b': 3, 'c': 4}
    ```

## 공통 메서드

### index()
- 리스트, 문자열, 튜플 같은 **시퀀스 자료형**에서 특정 값이 처음으로 등장하는 **인덱스(위치)**를 찾아주는 메서드
- 기본 구조
    ```
    시퀀스.index(value, start=0, stop=len(시퀀스))
    ```
    - value: 찾고자 하는 값(필수)
    - start: 검색을 시작할 인덱스, 기본값:0 (선택적)
    - stop: 검색을 멈출 인덱스, 기본값: 시퀀스 길이 (선택적)
        - stop 인덱스는 검색 범위에 포함 안함
        - stop 인덱스 앞까지만
- 반환값
    - 찾으면: 해당 값이 처음 등장하는 인덱스(int) 반환
    - **없으면: ValueError 예외 발생**
- 예시
    ```
    lst = [10, 20, 30, 20]
    print(lst.index(20))  # 출력: 1
    ```

## deque 메서드

### rotate()
- deque의 요소들을 회전(순환 이동) 시킴
    - 오른쪽 회전: 마지막 요소가 맨 앞으로 이동
    - 왼쪽 회전: 첫 번째 요소가 맨 뒤로 이동
- 기본 구조
    ```
    deque.rotate(n=1)
    ```
    - n: 정수 (기본값 = 1)
        - n > 0: 오른쪽으로 n칸 회전
        - n < 0: 왼쪽으로 n칸 회전
- 반환값
    - 반환값 없음 (None)
    - deque 자체를 제자리에서(in-place) 수정
- 예시
    ```
    from collections import deque

    dq = deque([1, 2, 3, 4, 5])

    # 오른쪽으로 2칸 회전
    dq.rotate(2)
    print(dq)  # deque([4, 5, 1, 2, 3])

    # 왼쪽으로 3칸 회전
    dq.rotate(-3)
    print(dq)  # deque([2, 3, 4, 5, 1])
    ```

### appendleft()
- deque의 왼쪽(앞쪽) 끝에 요소를 추가하는 메서드
- list.append()가 오른쪽 끝에 요소를 추가하는 것과 달리, deque.appendleft()는 왼쪽에 빠르게 삽입
- 기본 구조
    ```
    deque.appendleft(x)
    ```
    - x: 왼쪽에 추가할 요소
- 반환값
    - 반환값은 None
- 예시
    ```
    from collections import deque

    dq = deque([10, 20, 30])
    dq.appendleft(5)

    print(dq)  # 출력: deque([5, 10, 20, 30])
    ```

<br>

---

<br>

# 정규 표현식(Regular Expression)
- **문자열 패턴을 정의하는 언어 독립적인 문법**
- 문자열 안에서 특정한 패턴(규칙)을 찾거나, 검사하거나, 바꾸기 위해 만든 특별한 문자열 표기법
- 예를 들어, 전화번호, 이메일 주소, 특정 단어, 숫자 패턴 등을 쉽게 찾을 수 있게 해줌
- 왜 사용할까?
    - 긴 텍스트나 로그에서 원하는 정보만 빠르게 뽑아내거나
    - 데이터 유효성 검사(예: 이메일 형식 검사)
    - 텍스트 치환이나 분리 등 복잡한 문자열 작업을 간단한 패턴으로 처리
- 정규 표현식은 대부분의 프로그래밍 언어와 텍스트 처리 도구에서 사용
    - Python: re 모듈에서 지원

## 정규 표현식 기본 문법
- 정규 표현식 기본 문법
    | 패턴       | 의미                     | 예시                      |
    | -------- | ---------------------- | ----------------------- |
    | `.`      | 임의의 한 문자 (개행 제외)       | `a.b` → "acb", "a-b"    |
    | `^`      | 문자열의 시작                | `^a` → "apple"만 매칭      |
    | `$`      | 문자열의 끝                 | `e$` → "apple"만 매칭      |
    | `*`      | 0회 이상 반복               | `a*` → "", "a", "aa"    |
    | `+`      | 1회 이상 반복               | `a+` → "a", "aa"        |
    | `?`      | 0회 또는 1회               | `a?` → "", "a"          |
    | `{n}`    | 정확히 n번 반복              | `a{3}` → "aaa"          |
    | `{n,m}`  | n\~m번 반복               | `a{2,4}` → "aa", "aaa"  |
    | `[]`     | 문자 집합, 괄호 안의 문자 중 하나   | `[abc]` → "a", "b", "c" |
    | `[^abc]` | 괄호 안에 없는 문자            | `[^a]` → "b", "c", ...  |
    | `\|`     | OR (또는)                 | `cat \| dog` → "cat" 또는 "dog" |
    | `()`     | 그룹화                    | `(ab)+` → "ab", "abab"  |
    | `\`      | 이스케이프 문자 또는 특수문자 이스케이프 | `\.` → "." 자체           |

## 자주 쓰는 특수 문자 패턴 (메타 문자 (meta characters))
- 자주 쓰는 특수 문자 패턴 (메타 문자 (meta characters))
    | 패턴   | 의미                            | 예시                    |
    | ---- | ----------------------------- | --------------------- |
    | `\d` | 숫자 (0\~9)                     | `\d+` → "123", "456"  |
    | `\D` | 숫자가 아닌 문자                     | `\D+` → "abc"         |
    | `\w` | 알파벳, 숫자, 언더바 (`[A-Za-z0-9_]`) | `\w+` → "hello\_123"  |
    | `\W` | 단어 문자가 아닌 것 (`\w`의 반대)        | `\W+` → "!@#"         |
    | `\s` | 공백 문자 (스페이스, 탭, 줄바꿈 등)        | `\s+` → " " or "\n"   |
    | `\S` | 공백이 아닌 문자                     | `\S+`                 |
    | `\b` | 단어 경계 (word boundary)         | `\bcat\b` → "cat"만 매칭 |
    | `\B` | 단어 경계 아님                      | `\Bcat\B` → 중간에만 매칭   |

## 자주 쓰는 정규 표현식 패턴 (실용 예시)
- 자주 쓰는 정규 표현식 패턴 (실용 예시)
    | 목적         | 패턴                                               | 예시 매칭                                     |
    | ---------- | ------------------------------------------------ | ----------------------------------------- |
    | 숫자만 찾기     | `\d+`                                            | "123", "456"                              |
    | 영어 소문자만    | `[a-z]+`                                         | "abc"                                     |
    | 이메일 주소     | `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}` | "[test@email.com](mailto:test@email.com)" |
    | 전화번호 (단순형) | `\d{3}-\d{3,4}-\d{4}`                            | "010-1234-5678"                           |
    | 주민등록번호     | `\d{6}-\d{7}`                                    | "990101-1234567"                          |
    | HTML 태그 제거 | `<[^>]+>`                                        | `<div>`, `<a href=...>`                   |
    | 공백 제거      | `\s+`                                            | "   "                                     |
    | 한글만 추출     | `[가-힣]+`                                         | "안녕하세요"                                   |

## 주요 함수 요약 (re 모듈)
- 주요 함수 요약 (re 모듈)
    | 함수                              | 설명                             |
    | ------------------------------- | ------------------------------ |
    | `re.match(pattern, string)`     | 문자열 **시작**에서만 패턴 찾음            |
    | `re.search(pattern, string)`    | 문자열 전체에서 **처음 하나만** 매칭         |
    | `re.findall(pattern, string)`   | 문자열 전체에서 **모든 매칭 결과를 리스트로 반환** |
    | `re.sub(pattern, repl, string)` | 패턴을 찾아 다른 문자열로 **치환**          |
    | `re.compile(pattern)`           | 정규식을 객체로 만들어 **재사용 가능**        |

## 파이썬에서 예시
- 파이썬에서 예시
    ```
    import re

    text = "My email is hello123@gmail.com and phone is 010-1234-5678."

    email = re.search(r"[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}", text)
    phone = re.search(r"\d{3}-\d{3,4}-\d{4}", text)

    print(email.group())  # hello123@gmail.com
    print(phone.group())  # 010-1234-5678
    ```
    - **정규식 패턴은 r'패턴' 형식으로 raw string으로 쓰는 게 좋음 (\ 문자 처리 때문)**

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

6. 문제 6
    ```
    *B,=range(1,N+1)
    ```
    - 여기서 `,`(콤마)는 튜플의 핵심 문법
        ```
        a = 1, 2, 3    # 튜플 (1, 2, 3)
        print(a)       # (1, 2, 3)
        print(type(a)) # <class 'tuple'>

        b = (1, 2, 3)  # 튜플 (1, 2, 3)
        print(b)       # (1, 2, 3)
        print(type(b)) # <class 'tuple'>

        c = (1)        # 그냥 정수 1, 튜플 아님!
        print(c)       # 1
        print(type(c)) # <class 'int'>

        d = (1,)       # 길이 1짜리 튜플
        print(d)       # (1,)
        print(type(d)) # <class 'tuple'>

        e = 1,
        print(e)       # (1,)
        print(type(e)) # <class 'tuple'>
        ```
    - 예를들어
        ```
        n,*m=range(1,N+1)
        ```
        - 이 표현은 `(n,*m)=range(1,N+1)` 이것과 같음
            - `,`(콤마)가 튜플 타입으로 만들기 때문
        - 여기서 n에 정수 1
        - 나머지 2부터N까지 정수가 리스트형태로 m에 들어감
    - 위의 예를 적용하면, `(*B,)=range(1,N+1)` 이런 형태와 같음
        - 따라서 B에 1부터 N까지의 정수가 리스트 형태로 들어감

7. 문제 7
    ```
    import re
    print(len(re.sub('dz=|[ln]j|\w\W','Z',input())))
    ```
    - `re.sub`: pattern에 맞는 부분들을 repl로 치환
    - 패턴: `'dz=|[ln]j|\w\W'`
        - `dz=`: 이렇게 생긴 문자열
        - `[ln]j`: "lj" 또는 "nj" (l 또는 n 다음에 j) - 정규 표현식
            - 정규 표현식에서 [] 안은 문자 클래스(character class)
                - `[ln]`은 'l' 또는 'n' 중 하나를 의미
        - `\w\W`: 임의의 두 문자 조합 - 정규 표현식
            - 정규 표현식에서 메타문자(meta characters)
            - `\w`는 알파벳 대소문자/숫자/언더바 (word character)
            - `\W`는 알파벳/숫자/언더바가 아닌 문자 (non-word character)

8. 문제 8
    ```
    print(sum([*x]==sorted(x,key=x.find)for x in open(0))-1)
    ```
    - `[ *x ]`: 문자열 x를 리스트로 풀어줌
        - 예: "abca" → ['a','b','c','a']
    - `sorted(x, key=x.find)`: 문자열을 문자가 처음 등장한 순서대로 정렬
        - "abca"
            - x.find('a')=0, x.find('b')=1, x.find('c')=2, x.find('a')=0
            - 정렬 결과: ['a','a','b','c']
            - 중복 문자가 떨어져서 등장한 경우를 판별
    - sum(... for x in open(0))
        - 위 비교의 결과가 True/False가 되므로, True=1, False=0
        - sum(...)으로 그룹 단어인 개수만 셈
        - 파이썬에서는 True와 False도 숫자로 취급

9. 문제 9
    ```
    # 잘 동작
    r = []
    next(o := open(0))
    for i in o:
        r.append(tuple(map(int, i.split())))
    r.sort()
    for i, j in r:
        print(i, j)
    
    # 시간 초과
    r = []
    N, *l = map(int, open(0).read().split())
    while l:
        i, j, *l = l
        r.append((i, j))
    r.sort()
    for i, j in r[1:]:
        print(i, j)
    ```
    - `i, j, *l = l`이 부분이 핵심 병목
        - `*l = l[2:]`는 리스트 슬라이싱을 매번 수행
        - 리스트 슬라이싱은 O(n) 시간복잡도가 듬
        - 따라서 전체 반복에서 시간 복잡도는 O(n^2)가 됨
            - 리스트 슬라이싱 O(n)을 while로 n/2번 반복
    - 첫 번째 코드는 왜 빠른가?
        - 파일을 한 줄씩 순회하면서 처리
        - 입력 전체를 메모리에 올리지도 않고, 슬라이싱도 안 함
            - for의 in에 open(0)을 넣어서 파일을 한 줄씩 처리
        - O(n)으로 동작함 → 빠름
    - 슬라이싱 대신 인덱스 접근 혹은 컴프리헨션을 사용하면 시간초과 문제 해결

10. 문제 10
    ```
    while '()'in l or '[]'in l:l=l.replace('()','').replace('[]','')
    ```
    - 메서드 체이닝
        - 객체의 메서드 호출 결과로 다시 객체를 반환하고, 그 반환된 객체에 대해 또 메서드를 연달아 호출하는 방식
        - replace() 메서드의 반환값에 다시 replace() 메서드를 호출하는 것 같은 방식
        - 반환된 객체가 또 메서드를 가질 수 있어서 연결이 가능
    - 체이닝은 일반적인 메서드 나열 방식에 비해 더 간결하고 직관적
        ```
        # 일방적인 방식
        text = text.strip()
        text = text.lower()
        text = text.replace("!", "")

        # 메서드 체이닝
        clean = text.strip().lower().replace("!", "")
        ```

<br>

---

<br>