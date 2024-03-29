# 정보처리기사 2024

## # 4-2. 프로그래밍 언어 활용 - 프로그래밍 언어 활용

### # 1. 기본문법 활용 4-46page

### 8. C언어에서 비트 논리 연산자에 해당하는 것

- & : 두 값을 비트로 연산하여 같은 비트의 값이 모두 1이면 해당 비트 값이 1이 되고, 그렇지 않으면 0이 되는 연산자
- | : 두 값을 비트로 연산하여 같은 비트의 값이 하나라도 1이면 해당 비트 값이 1이 되고, 그렇지 않으면 0이 되는 연산자
- ^ : 두 값을 비트로 연산하여 같은 비트의 값이 서로 다르면 해당 비트 값이 1이 되고, 그렇지 않으면 0이 되는 연산자
- ~ : 모든 비트의 값을 반대로 바꾸는 반전 기능을 하는 연산자

### 11. C언어 프로그램이 실행되었을 때의 결과

```C
#include <stdio.h>
int main(int argc, char *argv[]){
  char a;
  a = 'A' + 1;

  print("%d", a);
  return 0;
}
```

- `66`
- stdio.h 헤더 파일을 포함
- main 함수 선언
- 문자 타입 변수 a를 선언
- 'A'에 1을 더한 값 66을 a에 대입
- a를 화면에 출력함
- main 함수의 정상종료를 의미하는 0을 리턴

### 13. C언어에서 연산자 우선순위가 높은 것에서 낮은것 순서

- 연산자 우선순위 (증산시 관비 논삼대)
  - 증감 연산자
  - 산술 연산자
  - 시프트 연산자
  - 관계 연ㅅ나자
  - 비트 연산자
  - 논리 연산자
  - 삼항 연산자
  - 대입 연산자

```markdown
ㄱ. ()
ㄴ. ==
ㄷ. <
ㄹ. <<
ㅁ. ||
ㅂ. /
```

- 괄호의 우선순위가 가장 높고, 산술 연산자인 '/'가 다음으로 높다.
- 시프트 연산자인 '<<'가 다음으로 높다.
- 관계 연산자인 '<', '=='가 다음으로 높으나 둘 중에서는 대소 비교가 동일 비교보다 높으므로 '<' '=='보다 높다.
- 논리 연산자인 '||'가 우선순위가 가장 낮다.

### 17. C언어 프로그램이 실행되었을 때의 결과

```C
#include <stdio.h>

int main() {
  int n = 4;
  int* pt = NULL;
  pt=&n;

  print("%d", &n + *pt - *&pt + n);
  return 0;
}
```

- `8`
- n의 주솟값은 모르므로 x라고 가정하면 다음과 같다

|||
|--|--|
|n|4|
|||
|pt|n의 주솟값(x)|

1. &n : n의 주솟값이므로 x
2. *pt : pt가 가리키는 값인 4
3. *&pt : pt의 주솟값이 가리키는 값(*과 &는 반대 역할이므로 pt와 같음)인 x
4. n : n의 값인 4

---

### 24. 파이썬 프로그램이 실행되었을 때의 결과

```python
def cs(n):
  s = 0
  for num in range(n+1):
    s += num
  return s

print(cs(11))
```

- 66
1. cs(11)에 의해 호출(이때 n=11이 됨)
2. for 문은 range(11+1)이므로 num이 0부터 11까지 반복
3. num 값인 `0부터 11까지 더하므로` 반복문이 종료할 때 s는 66이 됨
4. cs에 11을 넣었을 때 결괏값을 출력

---

### C언어에서 정수 변수 a, b에 각각 1,2가 저장되어 있을 때 다음 식의 연산 결과는?

```C
a < b + 2 && a << 1 <= b
```

- `1`
- 연산자 우선순위 (증산시 관비 논삼대)
  - 증감 연산자
  - 산술 연산자
  - 시프트 연산자
  - 관계 연산자
  - 비트 연산자
  - 논리 연산자
  - 삼항 연산자
  - 대입 연산자
- '<' 관계 연산자
- '+' 산술 연산자
- '&&' 논리 연산자
- '<<' 시프트 연산자
- '<=' 관계 연산자
- '+' 산술 연산자

1. a < b + 2 && a << 1 <= b
2. 1 < `2 + 2` && 1 << 1 <= 2
   1. 산술 연산자인 '+'가 가장 우선순위
3. 1 < `4` && 1 << 1 <= 2
   1. 그 다음 시프트 연산자인 '<<'가 우선순위
   2. 시프트 연산자에서 1은 이진수로 바꾸면 1이고
   3. 왼쪽으로 1칸 시프트 시키면 이진수로 10이 되는데,
   4. 이진수 10은 십진수로 2가 된다.
4. 1 < 4 && `1 << 1` <= 2
5. 1 < 4 && `2` <= 2
   1. 그 다음 관계 연산자인 '<' 와 '<='가 우선순위
   2. 1 < 4는 참이므로 1이 되고, 2 <= 2도 참이므로 1이 된다
6. `1 < 4` && `2 <= 2`
7. `1` && `1`
   1. 마지막으로 논리 연산자인 '&&'를 수행하면 1이 된다
   2. 1은 참을 의미하므로 참과 참을 AND 연산하면 참이 되어 1이 된다.

### 27 C언어에서 두 개의 논릿값 중 하나라도 참이면 1을, 모두 거짓이면 0을 반환하는 연산자

- `||`

- || : 두 개의 논릿값 중 하나 이상 참이면 참(True)을 반환하고, 그렇지 않으면 거짓(False)을 반환(OR 연산)하는 연산자
- && : 두 개의 논릿값이 모두 참이면 참(True)을 반환하고, 그렇지 않으면 거짓(False)을 반환(AND 연산)하는 연산자
- != : 두 값이 다른지 확인하는 연산자

### 28. Python 데이터 타입 중 시퀀스(Sequence) 데이터 타입에 해당하며 다양한 데이터 타입들을 주어진 순서에 따라 저장할 수 있으나 저장된 내용을 변경할 수 없는 것은?

- `튜플`
- 세트(Set) : 중복된 원소를 허용하지 않는 집합의 성질을 가지고 있는 자료구조
- 리스트(List) : 크기가 가변적으로 변하는 선형리스트의 성질을 가지고 있는 자료구조
- 튜플(Tuple) : 초기에 선언된 값에서 값을 생성, 삭제, 수정이 불가능한 형태의 자료구조
- 딕셔너리(Dictionary) : 키와 값으로 구성된 객체를 저장하는 구조로 되어 있는 자료구조

### 31. C언어 프로그램이 실행되었을 때 실행 결과는?

```C
#include <stdio.h>
int main(int argc, char *argv[]){
  int arr[2][3] = {1, 2, 3, 4, 5, 6};
  int (*p)[3] = NULL;
  p = arr;
  printf("%d, ", *(p[0]+1)+*(p[1]+2));
  printf("%d", *(*(p+1+0)+*(*(p+1)+1)));
  return 0;
}
```

- `8, 9`

|주소|메모리|값|
|:--:|:--:|:--:|
|*(arr+0) == arr[0]|1|arr[0][0]|
|arr[0]+1|2|arr[0][1]|
|arr[0]+2|3|arr[0][2]|
|*(arr+1)==arr[1]|4|arr[1][0]|
|arr[1]+1|5|arr[1][1]|
|arr[1]+2|6|arr[1][2]|

- *(p[0]+1) + *(p[1]+2) -> 8
  - *(p[0]+1) = 2
  - *(p[1]+2) = 6
- *(*(p+1)+0) + *(*(p+1)+1) -> 9
  - *(*(p+1)+0) = 4
  - *(*(p+1)+1) = 5

### 34. JAVA 프로그램이 실행되었을 때, 실행 결과

```java
public class Soojebi{
  static void rs(char a[]){
    for(int i = 0; i<a.length; i++)
      if(a[i] == 'B')
      a[i] = 'C';
    else if(i == a.length - 1)
      a[i] = a[i-1];
        else a[i] = a[i+1];
  }
  static void pca(char a[]){
    for(int i - 0; i < a.length; i++)
    System.out.print(a[i]);
    System.out.println();
  }

  public static void main(String[] args){
    char c[] = {'A', 'B', 'D', 'D', 'A', 'B', 'C'}
    rs(c);
    pca(c);
  }
}
```

- `BCDABCA`

|i|a[i]|if 문|else if 문|else 문|
|:--:|:--:|:--:|:--:|:--:|
|0|'A'|거짓|거짓|1|
|1|'B'|참 (2)|||
|2|'D'|거짓|거짓|3|
|3|'D'|거짓|거짓|4|
|4|'A'|거짓|거짓|5|
|5|'B'|참 (6)|||
|6|'C'|거짓|참|7|

1. a[0] = a[1]이므로 a[1]의 값인 'B'를 a[0]에 대입
2. a[1] = 'C'
3. a[2] = a[3]이므로 a[3]의 값인 'D'를 a[2]에 대입
4. a[3] = a[4]이므로 a[4]의 값인 'A'를 a[3]에 대입
5. a[4] = a[5]이므로 a[5]의 값인 'B'를 a[4]에 대입
6. a[5] = 'C'
7. a[6] = a[5]이므로 a[5]의 값인 'C'를 a[6]에 대입

### 36. C언어 프로그램이 실행되었을 때, 실행 결과

```C
# include <stdio.h>

int main(int argc, char *argv[]){
  int a = 5, b = 3, c = 12;
  int t1, t2, t3;
  t1 = a&& b;
  t2 = a || b;
  t3 = !C;
  printf("%d", t1 + t2 + t3);
  return 0;
}
```

- `2`
- C언어에서 0이면 참, 0이면 거짓으로 인식하고, 계산한 결과는 참이면 1로, 거짓이면 0이 된다.

1. a는 5이므로 참, b는 3이므로 참이기 때문에 (참 && 참)은 참이므로 t1은 1
2. a는 5이므로 참, b는 3이므로 참이기 때문에 (참 || 참)은 참이므로 t2는 1
3. c는 12이므로 참이지만 !(NOT) 연산에 의해 참은 거짓이 되므로 t3는 0

### 46. 파이썬 프로그램이 실행되었을 때의 결과는?

```python
a = [1, 2 [3, 4, ['life', 'is']]]
print(a[2][2][0])
```

- `life`

|||
|--|--|
|a[0]|1|
|a[1]|2|
|a[2]|3, 4 ['life', 'is']|
|a[2][0]|3|
|a[2][1]|4|
|a[2][2]|['life', 'is']|
|a[2][2][0]|'life'|
|a[2][2][1]|'is'|

---

### # 2. 언어특성 활용 4-71page

- pass

---

### # 3. 라이브로리 활용 4-79page

### 7. C언어에서 문자열 처리 함수의 서식과 그 기능의 연결 관련

- strlen(s) : s의 길이를 구한다.
- strcpy(s1, s2) : s2를 s1으로 복사한다.
- strcmp(s1, s2) : s1과 연결한다.
- strrev(s) : s를 거꾸로 변환한다.

|||
|:--:|--|
|strlen|문자열을 길이를 알려주는 함수(String Length)|
|strcpy|문자열을 복사하는 함수(String Copy)|
|strcmp|문자열을 비교하는 함수(String Compare)|
|strrev|문자열 거꾸로 뒤집는 함수(String Reverse)|
