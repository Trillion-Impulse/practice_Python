# practice_Python

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