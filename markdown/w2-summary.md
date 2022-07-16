# 2주차 summary

## 파이썬

객체 지향 언어, 모든 것이 객체로 구현되어 있음

## 파이썬 기초

### 자료형

-   불린형(Boolean type)
-   수치형 (Numeric type): int, float, complex
-   문자열 (String type)
-   None

### 컨테이너

-   시퀀스형 컨테이너: 인덱스로 접근(순서가 있음)

    -   리스트: 변경 가능, 반복 가능 `[ ]`
    -   문자열: 변경 불가, 반복 가능
    -   튜플: 변경 불가, 반복 가능 `( )`
    -   레인지:변경 불가, 반복 가능 `range()`

-   컬렉션/비시퀀스형 컨테이너: 순서가 없음
    -   세트: 순서 없음, 중복된 값 없음, 변경 가능, 반복 가능 `set()` or `{ }`
    -   딕셔너리: 키와 값의 쌍으로 이뤄진 모음, 변경 가능, 반복 가능 `{key: value}`

```markdown
### 시퀀스형 주요 공통 연산자

|       연산       |                           결과                            |
| :--------------: | :-------------------------------------------------------: |
|       s[i]       |                     s 의 i 번째 항목                      |
|      s[i:j]      |               s 의 i 에서 j 까지의 슬라이스               |
|     s[i:j:k]     |           s 의 i 에서 j 까지 스텝 k 의 슬라이스           |
|      s + t       |                   s 와 t 의 이어 붙이기                   |
| s _ n 또는 n _ s |               s 를 그 자신에 n 번 더하는 것               |
|      x in s      | s 의 항목 중 하나가 x 와 같으면 True, 그렇지 않으면 False |
|    x not in s    | s 의 항목 중 하나가 x 와 같으면 False, 그렇지 않으면 True |
|      len(s)      |                         s 의 길이                         |
|      min(s)      |                    s 의 가장 작은 항목                    |
|      max(s)      |                     s 의 가장 큰 항목                     |
```

## 파이썬 제어문

### 제어문

-   특정 상황에 따라 코드를 선택적으로 실행(분기/조건)하거나 실행(반복)하는 제어가 필요함
-   제어문은 순서도로 표현 가능

### 조건문

조건문은 참/거짓을 판단할 수 있는 조건식과 함께 사용

```python
if <expression> :
    #code block
else:
    #code block
```

복수 조건문

```python
if :
    #code block
elif :
    #code block
elif :
    #code block
else :
    #code block
```

중첩 조건문

```python
if :
    #code block
    if :
        #code block
else:
    #code block
```

조건 표현식

`<true인 경우 값> if <expression> else <false인 경우 값>`

```python
value = num if num >= 0 else -num
#보통 변하는 값을 확인하고 저장할 때 사용

#위의 조건 표현식을 동일하게 풀어쓰면
if num >= 0:
    value = num
else:
    value = 0
```

### 반복문

특정 조건에 도달할때 까지 반복된는 일련의 문장

while문: 조건식이 참인 경우 반복적으로 코드를 실행, 무한 루프를 하지 않도록 종료조건이 반드시 필요함

```python
while <expression>:
    #code block
```

for문: 시퀀스를 포함한 순회가능한 객체 요소들 모두 순회함, 처음부터 끝까지 모두 순회하므로 별도의 종료조건이 필요하지 않음

```python
for <변수명> in <iterable>:
    #code block
```

딕셔너리 순회: 딕셔너리는 기본적으로 key를 순회하며 key를 통해 값을 활용

```python
grades = {'luke': 80, 'leia': 90}
for name in grades:
    print(name)
    #luke, leia 출력

for name in grades:
    print(name, grades[name])
    #luke 80, leia 90 출력
```

### 반복문 제어

-   break: 반복문을 종료
-   continue: continue 이후의 코드 블록은 수행하지 않고, 다음 반복을 수행
-   for-else: 끝까지 반복문을 실행한 이후에 else문 실행

## 파이썬 함수

### 함수 기본 구조

-   선언과 호출 (define & call)
-   입력 (input)
-   범위 (scope)
-   결과값 (output)

### 함수의 입력

-   parameter: 함수를 실행할 때, 함수 내부에서 사용되는 식별자
-   argument: 함수를 호출 할 때, 넣어주는 값

```python
def add(x, y):
    return x + y

add(x=2, y=2) #가능
add(2, y=2) #가능
add(x=2, 2) #불가능
```

```python
def add(x, y=0):
    return x+y
add(2)
```

### 함수의 범위

-   함수는 코드 내부에 local scope를 생성하며, 그 외의 공간인 global scope로 구분
-   scope
    -   global scope: 코드 어디에서든 참조할 수 있는 공강
    -   local scope: 함수가 만든 scope. 함수 내부에서만 참조 가능

### 이름 검색 규칙(name resolution)

-   파이썬에서 사용되는 이름(식별자)들은 이름공간에 저장되어 있음
-   LEGB Rule: 아래와 같은 순서로 이름을 찾아나감
    -   Local -> Enclosed -> Global -> Built-in
-   즉, 함수 내에서 바깥 scope의 변수에 접근은 가능하지만 수정은 불가

## 데이터 구조

### 시퀀스

-   문자열 탐색/검증 메서드

| 문법        | 설명                                                     |
| ----------- | -------------------------------------------------------- |
| s.find(x)   | x의 첫 번째 위치를 반환. 없으면 -1 반환                  |
| s.index(x)  | x의 첫 번째 위치를 반환. 없으면 오류 발생                |
| s.isalpha() | 알파벳 문자 여부 (단순 알파벳이 아닌 유니코드 상 Letter) |
| s.isupper() | 대문자 여부                                              |
| s.islower() | 소문자 여부                                              |
| s.istitle() | 타이틀 형식 여부 (eg. The Title)                         |

-   문자열 변경 메서드

| 문법                           | 설명                                       |
| ------------------------------ | ------------------------------------------ |
| s.replace(old, new[,count])    | 바꿀 대상 글자를 새로운 글자로 바꿔서 반환 |
| s.strip([chars])               | 공백이나 특정 문자를 제거                  |
| s.split(sep=None, maxsplit=-1) | 공백이나 특정 문자를 기준으로 분리         |
| 'separator'.join([iterable])   | 구분자로 iterable을 합침                   |
| s.capitalize()                 | 가장 첫 번째 글자를 대문자로 변경          |
| s.title()                      | ''나 공백 이후를 대문자로 변경             |
| s.upper()                      | 모두 대문자로 변경                         |
| s.lower()                      | 모두 소문자로 변경                         |
| s.swapcase()                   | 대문자 <-> 소문자 서로 변경                |

-   리스트 메서드

| 문법                   | 설명                                                                                           |
| ---------------------- | ---------------------------------------------------------------------------------------------- |
| L.append(x)            | 리스트 마지막에 항목 x 를 추가                                                                 |
| L.insert(i, x)         | 리스트 인덱스 i에 항목 x를 삽입                                                                |
| L.remove(x)            | 리스트 가장 왼쪽에 있는 항목(첫 번째) x를 제거<br />항목이 존재하지 않을 경우 Value Error 발생 |
| L.pop()                | 리스트 가낭 오른쪽에 있는 항목 (마지막)을 반환 후 제거                                         |
| L.pop(i)               | 리스트의 인덱스 i에 있는 항목을 반환 후 제거                                                   |
| L.extend(m)            | 순회형 m의 모든 항목들의 리스트 끝에 추가 (+=과 같은 기능)                                     |
| L.index(x, start, end) | 리스트에 있는 항목 중 가장 왼쪽에 있는 항목 x의 인덱스를 반환                                  |
| L.reverse()            | 리스트를 거꾸로 정렬                                                                           |
| L.sort()               | 리스트를 정렬(매개변수 이용가능)                                                               |
| L.count(x)             | 리스트에서 항목 x가 몇 개 존재하는지 갯수를 반환                                               |
| L.clear()              | 모든 항목을 삭제함                                                                             |

---

### 컬렉션, 비시퀀스

-   세트 메서드

| 문법            | 설명                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------- |
| s.copy()        | 세트의 얕은 복사본을 반환                                                                     |
| s.add()         | 항목 x가 세트 s에 없다면 추가                                                                 |
| s.pop()         | 세트 s에서 랜덤하게 항목을 반환하고, 해당 항목을 제거<br />세트가 비어있을 경우 KeyError 발생 |
| s.remove(s)     | 항목 x를 세트 s에서 삭제<br /> 항목이 존재하지 않을 경우 KeyError 발생                        |
| s.discard(x)    | 항목 x가 세트 s에 있는 경우, 항목 x를 세트 s에서 삭제                                         |
| s.update(t)     | 세트 t에 있는 모든 항목 중 세트 s에 없는 항목을 추가                                          |
| s.clear()       | 모든 항목을 제거                                                                              |
| s.isdisjoint(t) | 세트 s가 세트 t의 서로 같은 항목을 하나라도 갖고 있지 않은 경우 True 반환                     |
| s.sissubset(t)  | 세트 s가 세트 t의 하위 세트인 경우, True 반환                                                 |
| s.issuperset(t) | 세트 s가 세트 t의 상위 세트인 경우, True 반환                                                 |

-   딕셔너리 메서드

| 문법              | 설명                                                                                                             |
| ----------------- | ---------------------------------------------------------------------------------------------------------------- |
| d.clear()         | 모든 항목을 제거                                                                                                 |
| d.keys()          | 딕셔너리 d의 모든 키를 담은 뷰를 반환                                                                            |
| d.values()        | 딕셔너리 d의 모든 값을 담은 뷰를 반환                                                                            |
| d.items()         | 딕셔너리 d의 모든 키-값의 쌍을 담은 뷰를 반환                                                                    |
| d.get(k)          | 키 k의 값을 반환하는데, 키 k가 딕셔너리 d에 없을 경우 None을 반환                                                |
| d.get(k, v)       | 키 k의 값을 반환하는데, 키 k가 딕셔너리 d에 없을 경우 v를 반환                                                   |
| d.pop(k)          | 키 k의 값을 반환하고 키 k인 항목을 딕셔너리 d에서 삭제하는데,<br />키 k가 딕셔너리 d에 없을 경우 KeyError를 발생 |
| d.pop(k, v)       | 키 k의 값을 반환하고 키 k인 항목을 딕셔너리 d에서 삭제하는데,<br /> 키 k가 딕셔너리 d에 없을 경우 v를 반환       |
| d.update([other]) | 딕셔너리 d의 값을 매핑하여 업데이트                                                                              |
