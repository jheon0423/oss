### 오픈소스 SW개론 첫번째 과제

#### 쉘스크립트 관련 getopt / getopts 

#### 리눅스 명령어 관련 sed / awk

```c
#include <unistd.h >

int getopt(int argc, char *const argv[], const char *option);
```

getopt 함수는 옵션을 분석할수있게 제공하는 시스템 호출이다.

getopt 함수에 첫인자와 두번째인자는 main 함수의 argc와 arg를 그대로 전달하고, 세번째 옵셔에 제공하고자한느 옵션을 전달한다.

가령 a, l 옵션을 전달하고자 한다면, al 이라고 전달하게 된다. 그리고 옵션뒤에 인자를 사용해야 한다면 : 을 추가하게 된다.

만약 a에는 옵션뒤에 인자를 사용하고, l 에는 옵션뒤에 인자를 사용하지 않는다면, a:l 을 전달하게 된다



getopt 함수는 이번에 발견한 옵션의 아스키코드값을 반환하게 되며, 옵션 뒤에 인자를 사용하고자 한다면 이미 선언한 optarg를 이용한다.

그리고 더 이상 옵션을 발견하지 못하게될 경우 EOF를 반환하게 된다.






```
getopts OptionString Name[
  Arguments ....
]
```

getopts 명령은 매개변수 리스트에서 옵션 및 옵션인수를 검색하는 Korn/POSIX 쉘 내장 명령이다. 옵션은 + 혹은 - 부호로 시작하고 그 뒤에 문자가 오게된다.

'+' 혹은 '-' 로 시작하지 않는 옵션은 OptionString 을 종료한다. getopts명령은 호출될 떄마다 다음옵션값과 쉔 변수 OPTIND에서 처리될 다음인수의 색인을 배치한다.

쉘이 호출될떄마다 OPTIND는 1로 초기화됩니다. 옵션인 +로 시작된 경우 +는 Name의 값 앞에 추가된다.


OptionString의 문자 뒤에는 콜란이 오면 옵션에 인수가 있는것으로 간주된다. 옵션에 옵션-인수가 필요한 경우 getopts명령은 이를 변수 OPTARG에 배치하게 된다.

OptionString에 포함되지 않은 옵션문자가 발견되거나 찾은 옵션에 필요한 옵션 - 인수가 없는경우  :  
  * Name은 ? 문자로 설정된다
  * OPTARG가 설정되지 않으며
  * 진단 메시지가 표준오류에 기록된다.

이 조건은 getopts명령을 처리하는 중에 생긴 오류가 아니라 호출 어플리케이션에 인수가 표시되는 중에 발견된 오류라고 간주된다.

진단 메시지는 명시된내용과 같이 기록되지만 종료 상태는 0이 된다.

OptionString이 콜론으로 시작되는 경우
  * Name은 ? 문자로 설정되거나 누락된 필수옵션에 대해서는 콜론 문자로 설정된다.
  * OPTARG는 발견된 옵션문자로 설정되고
  * 출력이 표준오류에 기록되지 않는다.


  
다음 중 하나가 옵션의 끝을 식별하게 된다. 특수옵션 --, 이 - 또는 + 로 시작되지 않는 인수를 찾는경우 또는 오류가 발생하는경우.
옵션의 끝에 도달하는 경우 :
  * getopts 명령은 0보다 큰 리턴값으로 종료된다
  * OPTARG는 첫번째 비옵션-인수의 색인으로 설정된다. 여기서, 첫 번쨰 --인수는 그 전에 다른 비옵션-인수가 나타나지 않는 경우 옵션-인수로 간주되고 비옵션-인수가 없는 경우에는 값 $#+1로 간주된다.
  * Name은 ? 문자로 설정됩니다.
