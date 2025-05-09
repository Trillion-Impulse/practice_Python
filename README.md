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