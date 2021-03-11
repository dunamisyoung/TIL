# C 기초

---

## C언어

```c
#include <stdio.h>

int main(void)
{
	printf("hello, world\n")
}
```

위 코드에서 int main(void)는 시작한다는 의미를 가진다.

또한 우리가 작성할 모든 코드들은 `{}` 안에 작성하게 될 것이다.

C언어 에서는 printf라는 함수가 있는데 printf("hello, world\n")를 출력하고 싶다면, 언제나 text에는 쌍따옴표로 감싸야한다.

또한 문장의 끝에 마침표처럼 세미콜론(;)을 붙여주어야한다.

위에서 `\n`의 역할은 줄바꿈의 역할을한다.

**#include <stdio.h>는 "stdio.h"라는 파일을 찾아 "printf" 함수에 접근할 수 있도록 해준다.**

### 컴파일러

우리가 직접 작성한 코드는 "소스 코드"라고 불리며 이를 2진수로 작성된 "머신 코드"로 변환해야 컴퓨터가 이해할 수 있다. 이런 작업을 컴파일러 가는 프로그램이 수행한다.

터미널창의 명령프롬프트에서 "$" 기호옆에 우리가 원하는 명령어를 입력하면된다.

**clang hello.c 라는 명령어는 "clang"이라는 컴파일러로 "hello.c"라는 코드를 컴파일 하라는 의미입니다.**

그 결과물로 a.out 이라는 파일이 생성되는데, **./a out** 이라는 명령어를 실행하면 컴퓨터가 a.out이라는 프로그램을 실행하게끔 해준다.

### 문제

"hello, boostcourse"를 출력해보기

```c
#include <stdio.h>

int main(void)
{
	printf("hello, boostcourse /n");
}
```

### 형식지정자

사용자의 이름을 입력받아 입력받은 사용자의 이름을 출력하는 그런 함수를 C언어로 만들어보자.

CS50 Sandbox에서는 get_string 함수를 이용 하면된다.

사용자의 이름을 받아 저장할 변수를 answer라고 정할때 C언어는 데이터의 종류를 아주 정확하게 명시해줘야한다.

```c
string answer = get_string("What's your name?\n");
```

이떄 우리는 저장하는 값의 종류가 **문자열(string)** 이라는 것을 알려줘야한다. 이때 string을 형식 지정자 라고한다.

### 할당연산자

프로그래밍 언어에서 `=` 는 수학과는 조금다르게 **"같다"**가 아닌 오른쪽에서 왼쪽으로 가는 화살표라고 생각해주면 좋다. 즉, 오른쪽에 있는것을 왼쪽에 지정한다고 생각하자.

즉, get_string 함수가 사용자의 이름을 반환하면 그 이름을 anwser이라는 변수에 저장하는 것이라고 생각하면된다.

### 변수출력

```c
string answer = get_string("What's your name?\n");
printf("hello, %s\n", answer);
```

우리는 answer라는 변수에 들어있는 이름을 출력해야 하기에 %를 사용해줘야한다. 이때도 어떤종류의 인자를 받는지 말해줘야하는데, 문자열을 받기때문에 string의 s를 %뒤에 붙여 인자를 받아 줍니다.

### 컴파일과정

![compile](https://user-images.githubusercontent.com/66991380/110762347-083e3f80-8294-11eb-8d23-4c6bb875ad67.jpg)

가장 위에 포함된 cs50.h 파일안에 string 이라는 문자열 형식과 get_string이라는 함수에 대한 코드가 있는데 이 파일을 포함 해야만 전체 코드를 컴파일 할수있다.

아래코드로 컴파일이 가능하다.

`$ clang -o string string.c -lcs50` 여기서 -o string은 string.out 이라는 머신코드로 저장하도록 하는 명령어이다.

-lcs는 link라는 의미를 지닌 -l 이라는 인자에 추가로 포함한 "cs50" 파일을 합쳐주므로 컴파일시 cs50파일을 연결하도록 알려줄 수 있다.

다소 복잡한 과정대신에 make 명령어를 통해 간단하게 컴파일을 수행할 수도 있다.

`$ make string` 명령어를 통해 컴파일을 간단히 수행할수도 있다.

### 문제

"좋아하는 동물을 알려주세요"로 질문하여 동물 이름을 animal이라는 변수에 저장하고, 이를 "내가 좋아하는 동물은"으로 출력해주는 코드를 작성하자.

```c
#include <stdio.h>
#include <cs50.h>

int main(void)
{
	string animal = get_string("좋아하는 동물을 알려주세요");
	printf("내가 좋아하는 동물은", %s\n, animal");
}
```
