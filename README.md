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
                - 줄바꿈 포함됨, .strip() 필요
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

<br>

---

<br>