# 3주차 summary

## 에러/예외 처리 (Error/Exception Handling)

### 문법 에러(Syntax Error)

-   syntax error 발생하면 파이썬 프로그램은 실행되지 않음
-   파일이름, 줄번호, ^ 문자를 통해 파이썬이 코드를 읽어 나갈때 문제가 발생한 위치 표현
-   줄에서 에러가 감지된 가장 앞의 위치를 가리키는 캐럿 기호 ^ 를 표시
-   EOL (End of Line)
-   EOF (End of File)
-   Invalid syntax
-   assign to literal

### 예외 (Exception)

-   실행 도중 예상치 못한 상황을 맞이하면, 프로그램 실행을 멈춤
    -   문장이나 표현식이 문법적으로 올바르더라도 발생하는 에러
-   실행 중에 감지되는 에러들을 예외(Exception)라고 부름
-   예외는 여러 타입으로 나타나고, 타입이 메세지의 일부로 출력됨
    -   NameError, TypeError 등 발생한 예외 타입의 종류(이름)
-   모든 내장 예외는 Exception Class를 상속받아 이뤄짐
-   사용자 정의 예외를 만들어 관리할 수 있음
-   ZeroDivisionError: 0으로 나누고자 할 때 발생
-   NameError: namespace 상에 이름이 없는 경우
-   TypeError: 타입 불일치
-   TypeError: argument 부족
-   TypeError: argument 개수 초과
-   ValueError: 타입은 올바르나 값이 적절하지 않거나 없는 경우
-   IndexError
-   KeyError
-   ModuleNotFoundError: 존재하지 않는 모듈을 import 하는 경우
-   ImportError: Module은 있으나 존재하지 않는 클래스/함수를 가져오는 경우
-   IndentationError: Indentation이 적절하지 않는 경우
-   KeyboardInterrupt: 임의로 프로그램을 종료했을 때

### 예외처리

-   try문(statement) / except절(clause)을 이용하여 예외 처리를 할 수 있음
-   try문
    -   오류가 발생할 가능성이 있는 코드를 실행
    -   예외가 발생되지 않으면, except 없이 실행 종료
-   except문
    -   예외가 발생하면, except절이 실행
    -   예외 상황을 처리하는 코드를 받아서 적절한 조치를 취함

```python
try:
try 명령문
except 예외그룹-1 as 변수-1:
예외처리 명령문 1
except 예외그룹-2 as 변수-2:
예외처리 명령문 2
finally: (선택사항)
finally 명령문

#주의: try문은 반드시 한 개 이상의 except문이 필요
```

-   try: 코드를 실행
-   except: try문에서 예외가 발생 시 실행
-   else: try문에서 예외가 발생하지 않으면 실행
-   finally: 예외 발생 여부와 관계없이 항상 실행

### 예외 발생 시키기

raise를 통해 예외를 강제로 발생
`raise <표현식> (메세지)`

```python
raise
#--------
#RuntimeError Traceback (most recent call last)
#--------> 1 raise
#RuntimeError : No active exception to reraise
```

## 객체 지향 프로그래밍(OOP)

### 객체

-   객체의 특징
    -   타입(type): 어떤 연산자와 조작이 가능한가?
    -   속성(attribute): 어떤 상태(데이터)를 가지는가?
    -   조작법(method): 어떤 행위(함수)를 할 수 있는가?
-   객체지향 프로그래밍이란?
    -   프로그램을 여러 개의 독립된 객체들과 그 객체들 간의 상호작용으로 파악하는 프로그래밍 방법
    -   데이터와 기능(메서드) 분리, 추상화된 구조(인터페이스)
-   객체지향의 장점
    -   프로그램을 유연하고 변경이 용이하게 함, 대규모 sw개발에 주로 사용됨
    -   sw개발, 보수가 용이함, 보다 직관적인 코드 분석이 가능

### 클래스

```python
#클래스 젇의
class MyClassL
	pass
#인스턴스 생성
my_instance = MyClass()
#메서드호출
my_instance.my_method()
#속성
my_instance.attribute
```

### 클래스 메소드

-   클래스가 사용할 메소드
-   `@classmethod` 데코레이터를 사용해 정의
    -   데코레이터: 함수를 어떤 함수로 꾸며서 새로운 기능을 부여
-   호출 시 첫 번째 인자로 클래스(cls)가 전달됨

### 스태틱 메소드

-   인스턴스 변수, 클래스 변수를 전혀 다루지 않는 메서드
-   언제 사용?
    -   속성을 다루지 않고 단지 기능(행동)만을 하는 메서드를 정의할 때 사용
    -   `@staticmethod` 데코레이터를 사용하여 정의
    -   호출 시, 어떠한 인자도 전달되지 않음 (클래스 정보에 접근/수정 불가)

### 인스턴스

인스턴스 변수

-   인스턴스가 개인적으로 가지고 있는 속성(attribute)
-   각 인스턴스들의 고유한 변수

생성자 메소드에서 self.<name>으로 정의

인스턴스가 생성된 이후 <instance>.<name>으로 접근 및 할당

인스턴스 메소드

-   인스턴스 변수를 사용하거나, 인스턴스 변수에 값을 설정하는 메소드
-   인스턴스 조작을 위한 메서드
-   클래스 내부에 정의되는 메소드의 기본
-   호출 시, 첫번째 인자로 인스턴스 자기자신(self)이 전달됨

```python
class MyClass:
	def instance_method(self, arg1, ...)
```

self

-   인스턴스 자기 자신
-   파이썬에서 인스턴스 메소드는 호출 시 첫번째 인자로 인스턴스 자신이 전달되게 설계
    -   매개변수 이름으로 self를 첫번째 인자로 정의
    -   다른 단어로 써또 작동하지만, 파이썬이 암묵적인 규칙

생성자(constructor) 메소드

-   인스턴스 객체가 생성될 때 자동으로 호출되는 메서드
-   인스턴스 변수들의 초기값을 설정
    -   인스턴스 생성
    -   `__init__(self, ... )` 메소드 자동 호출

## 객체지향의 핵심 4가지

-   추상화
-   상속
-   다형성
-   캡슐화

---

# 파이썬 응용/심화

## List Comprehension

표현식과 제어문을 통해 특정한 값을 가진 리스트를 간결하게 생성하는 방법

`[<expression> for <변수> in <iterable>]`

`[<expression> for <변수> in <iterable> if <조건식>]`

```python
#1~3의 세제곱의 결과가 담긴 리스트를 만들기
cubic_list = []
for number in range(1, 4):
	cubic_list.append(number**3)
print(cubic_list)

[number**3 for number in range(1, 4)]
#특정한 원소(요소)로 구성된 리스트를 만들 때 사용 가능
```

## Dictionary Comprehension

표현식과 제어문을 통해 특정한 값을 가진 딕셔너리를 간결하게 생성하는 방법

`[key: value for <변수> in <iterable>]`

`[key: value for <변수> in <iterable> if <조건식>]`

```python
#1~3의 세제곱의 결과가 담긴 딕셔너리를 만들기
cubic_list = []
for number in range(1, 4):
	cubic_list.append(number**3)
print(cubic_list)

{number: number**3 for number in range(1, 4)}
```

## lamda [parameter] 표현식

-   람다함수: 표현식을 계산한 결과값을 반환하는 함수, 이름이 없는 함수라 익명함수로도 불림
-   특징: return문 가질 수 없음, 간편 조건문 외의 조건문이나 반복문 가질 수 없음
-   장점: 함수 정의해서 사용하는 것 보다 간결한 사용이 가능, def 사용할 수 없는 곳에서 사용 가능

```python
numbers = [1,2,3,4,5]
def multiple_3(n):
	return n * 3

print(list(map(multiple_3, numbers)))

print(list(map(lamda n: n*3, numbers)))
#임시적인 함수를 만들고 싶을 때 사용
```

```python
numbers = [1,2,3,4,5]
result = []
for number in numbers:
	if number % 3 == 0:
		result.append(number)
print(result)

print(list(filter(lamda n: n%3 == 0, numbers)))
```

## filter

순회 가능한 데이터구조의 모든 요소에 함수를 적용하고 결과가 True인 것들을 filter object로 반환

`filter(function, iterable)`

```python
def odd(n):
	retunr n % 2
numbers = [1, 2, 3]
result = filter(odd, numbers)
print(result, type(result)) # list(result) = [1, 3]
```

map(함수, 반복가능한 것)

: 반복가능한 것들의 모든 요소에 함수를 적용시킨 결과를 map object로 반환함

## 모듈 심화

### 파이썬 표준 라이브러리

파이썬에 기본적으로 설치된 모듈과 내장함수

### 파이썬 패키지 관리자(pip)

-   PyPI (Python Package Index)에 저장된 외부 패키지들을 설치하도록 도와주는 패키지 관리 시스템

명령어

-   패키지 설치: `$pip install SomePackage` `$pip install SomePackage==1.0.5`
-   패키지 삭제: `$pip uninstall SomePackage`
-   패키지 목록 및 특정 패키지 정보: `$pip list` , `$pip show SomePackage`
-   패키지 freeze: `$pip freeze`
-

## 가상환경

-   파이썬 표준 라이브러리가 아닌 외부 패키지와 모듈을 사용하는 경우 모두 pip 통해 설치 해야 함
-   복수의 프로젝트를 하는 경우 버전이 상이 할 수 있음
-   이러한 경우 가상환경을 만들어 프로젝트별 독립적 패키지 관리 가능

### venv

-   가상환경을 만들고 관리하는데 사용되는 모듈 (버전 3.5 부터)
-   특정 디렉토리에 가상환경을 만들고 고유한 파이썬 패키지 집합을 가질 수 있음

가상환경을 생성하면, 해당 디렉토리에 별도의 파이썬 패키지 설치됨
