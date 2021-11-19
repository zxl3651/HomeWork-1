# Homework-1
---
## ***awk 명령어***
+ ***awk***란 패턴 탐색과 처리를 위한 명령어로 간단하게 파일에서 결과를 추려내고 가공하여 원하는 결과물을 만들어내는 유틸리티임
+ 초기 개발자 Aho, Weinberger, Kernighan의 첫글자를 따서 이름이 지어짐
+ GNU 프로젝트에서 만들어진 텍스트 처리 프로그래밍 언어로 유닉스 계열의 OS에서 사용 가능함
+ 텍스트 형태로 되어있는 입력 데이터를 행과 단어 별로 처리해 출력함
---
### **사용법**
```
awk [OPTION][awk program][ARGUMENT]
```
***OPTION***의종류
  + -f : awk program 파일 경로 지정
  + -F : 필드 구분 문자 지정
  + -v : awk program에서 사용될 특정 값 지정

awk program : -f옵션이 사용되지 않았을때, awk가 실행할 awk program 코드 지정 \
ARGUMENT : 입력파일 지정 또는 variable(값) 지정 

---
### **awk의 주 사용용도** 
1. 텍스트 파일의 전체 내용 출력
2. 파일의 특정 필드만 출력
3. 특정 필드에 문자열을 추가해서 출력
4. 패턴이 포함된 레코드 출력
5. 필드 값 비교에 따라 레코드 출력

---
### **사용 예시**

*예시에 사용할 파일(file.txt)*

![image](https://user-images.githubusercontent.com/94293365/141801105-8a0b3b1d-a03b-4775-94ad-c3ee60ed97c1.png)

$0 = 파일내용 전체 \
$n = n번째 필드

1. 파일의 전체 내용 출력 \
` awk '{print}' ./file.txt ` 
![image](https://user-images.githubusercontent.com/94293365/141801504-0b65745f-265a-4fb2-b894-4aefd0742e82.png)
2. 특정 필드 값 출력 \
` awk '{print $n}' ./file.txt //n은 필드위치 `
![image](https://user-images.githubusercontent.com/94293365/141802371-368d389c-52ee-4ed1-82e1-a8165560565b.png)
3. 특정 필드에 문자열을 추가해서 출력 \
` awk '{print "text:"$n, "text:"$n}' ./file.txt //text는 문자열, n은 필드위치 `
![image](https://user-images.githubusercontent.com/94293365/141802700-3cc38ebe-46e6-4f1a-80cd-f644f83e7f92.png)
4. 지정된 문자열을 포함하는 레코드 출력 \
` awk '/text/' ./file.txt //text는 문자열 또는 숫자, text가 들어있는 문자열만 출력함 `
![image](https://user-images.githubusercontent.com/94293365/141802972-a8e28792-aad7-4594-8ada-cfe12754dccb.png)
5. 필드 값 비교에 따라 레코드 출력 \
` awk '$3 > 60 {print $0}' ./file.txt //세번째 필드(몸무게)가 60을 넘기는 레코드 전체출력 `
![image](https://user-images.githubusercontent.com/94293365/141803658-ad5bb916-ac0d-4de4-8b32-71398b395121.png)
---
## ***sed 명령어***
+ ***ed*** 명령어와 ***grep*** 명령어 기능의 일부를 합친 것이 ***sed(stream editor)***명령어임
+ 기억장치 안의 버퍼를 사용하지 않아 파일의 크기에 제한 없이 작업가능
+ 비 대화형 모드의 줄 단위 편집기
+ 원본을 건드리지 않고 편집하기 때문에 작업이 완료돼도 원본에 영향이 없음(**-i 옵션을 사용하면 원본을 바꿈**)

||sed|vi|
|---|:---:|:---:|
|공통점|편집기|편집기|
|차이점|커맨드 창 또는 스크립트에서 동작을 하여 원하는 부분만 수정가능|직접 파일을 열어 편집함|

---
### **사용법**
`sed [OPTION] 'command' [input file]`
  ***OPTION의 종류***
  + -n : 자동출력을 사용하지 않음
  + -e : command를 가지고 텍스트파일을 가공함
  + -i : 변경된 내용을 파일에 적용함
  + **대부분 -n과 -e 옵션을 사용함**
---
### **sed의 주 사용용도**
1. 특정 행 출력(Print - p)
2. 특정 행 삭제(Delete - d)
3. 단어 치환(Substitute - s)
4. 문자열 추가 (Append - a,Insert - i)
5. 특정 행의 내용을 전부 교체(Change - c)

---
### **사용 예시**

*예시에 사용할 파일(file.txt)*

![image](https://user-images.githubusercontent.com/94293365/141944853-462014c4-2b5e-4254-ae86-a5f5b3fe49a3.png) 
  1. 전체 행 출력 \
  `sed -n -e '1,$p' ./file.txt //1번째 줄부터 끝까지(전체) 출력 시 '1,$p' 사용`
  ![image](https://user-images.githubusercontent.com/94293365/141946070-aa541ee3-9fe4-4e27-97b5-18e0115d9bae.png)

  + 특정 행 출력 \
  `sed -n -e '1p' ./file.txt //1번째 줄만 출력`
  ![image](https://user-images.githubusercontent.com/94293365/141945559-4168d646-457e-4402-badd-78e5db57b97f.png)

    + 여기서 -n 옵션을 사용하지 않을시 자동으로 출력돼 명령을 수행하고 한번더 전체 출력을 하는 모습이다. 

  2. 특정 행 삭제 \
  `sed -n -e '1d' -e '1,$p' ./file.txt //1번째 줄을 삭제 후 전체출력 ` 
  ![image](https://user-images.githubusercontent.com/94293365/141946630-55cf1cde-a4f4-4ef8-96fe-a53ed9bca854.png)

  + 특정 행 삭제( -e옵션의 중요성) \
  ![image](https://user-images.githubusercontent.com/94293365/141946720-18e3e89d-4aa4-4d16-8e38-efd77c868dcb.png)

    + -e 옵션을 사용하지 않은 command는 가공하지 않아 반영이 안되는 모습임

  3. 단어 치환 \
  `sed -n -e 's/old/new/g' ./file.txt //old = 치환할 문자열, new = 치환한 문자열(비어있으면 삭제한 효과),g = global(전체에 적용됨) `
  ![image](https://user-images.githubusercontent.com/94293365/141947048-f87ca15b-10b4-45b6-a77a-cc13c4eb63dc.png)

  + seonghyeon 을 donggil 로 치환하는 모습임 
  
  4. 문자열 추가

  ```
  sed -n -e '/찾을 문자열/a\다음 줄에 추가할 문자열 //또는
  sed -n -e '/찾을 문자열/i\위에 삽입할 문자열
  ```
  ![image](https://user-images.githubusercontent.com/94293365/141947346-d02455f7-960f-4ee5-81e7-da533b465a26.png)

  + mongryong의 a(다음줄)와 i(위에) 를 사용해 gilsu를 추가하는 모습임 
  
  5. 문자열 교체 \
  `sed -n -e '/바꿀 행이 포함된 문자열/c\바꿀 행의 내용' -e '1,$p' ./file.txt`
  ![image](https://user-images.githubusercontent.com/94293365/141947630-8cf2c1e1-233c-46c1-a976-a48fe3a58858.png)

  + seonghyeon의 기록을 gilsu의 기록으로 교체하는 모습임
  
  ---

## ***getopts 명령어***
+ 쉘에서 명령을 실행할때 ***OPTION***을 사용할 수 있는데 스크립트 파일 안에서 실행할때도 ***OPTION***을 사용할 수 있음
+ 이 때 스크립트 내에서 직접 옵션을 해석해야하는데 이 작업을 하는 명령어임
+ ***getopts***를 사용하지않고 ***OPTION***을 사용할 수 있지만 그렇게되면 쉘스크립트가 많이 복잡해짐

---

### **사용법** 
```
getopts optstring varname [args]
ex) command -a xyz -b -c hello world //option argument:xyz / option string:-a,-b,-c
```
---

### **옵션의 종류** 
1. ***short***
2. ***long***

+ ***short*** : 옵션앞에 - 하나만 붙는 옵션, ***getopts*** 명령을 이용하지 않고 직접 해석해 처리하면 스크립트가 복잡해짐
  + ` $ command -a -b -c ` 
  + ` $ command -abc = $ command -b -ca // 옵션을 붙여서 사용할 수 있으며 순서가 바뀌어도 된다 `
  + ` $ command -a xxx -b yyy = $ command -axxx -byyy // 옵션인수를 가질 수 있다 / 옵션인수를 옵션에 붙여 쓸 수 있음 `
  + ` $ command -a -b -- -c // 옵션 구분자 '--'가 올 경우 우측에 있는 값은 옵션으로 해석하면 안됨 `
+ ***long*** : 옵션앞에 -- 가 붙는 옵션, ***short*** 옵션과는 달리 붙여 쓸 수가 없기에 사용방법이 간단하여 직접 해석하여 처리하는 것이 어렵지않음
  + 주의해야 할 점: 
  + ` ./test.sh -a aaa --posix --long 123 -b --warning=2 -- hello world ` 와 같은 문장에서 getopts 사용시
  1. getopts는 하나의 문자를 옵션으로 보기 때문에 p,o,s,i,x를 모두 붙여쓰기한 옵션명으로 인식
  2. 위의 ***long***옵션처럼 ***long***옵션이 옵션인수를 사용하게 되면 그 이후의 옵션(-b)는 getopts에 의해 인식이 되지않음
  => 따라서 ***getopts*** 명령으로 ***long,short***를 동시에 처리하긴 힘드므로 ***long***을 먼저 처리하고 ***short***를 처리하면 동일하게 사용가능
  + `$ -a aaa -b -- hello world // 처리한 long 옵션은 삭제하고 short 옵션만 getopts 명령에 전달 `
---
### **Error reporting** 
***getopts*** 명령은 ***error reporting***과 관련해서 다음과 같은 두 개의 모드를 제공함
|Verbose mode||
|:---:|:---:|
|invalid 옵션 사용|opt 값을 ? 문자로 설정/OPTARG 값은 unset/ 오류 메시지 출력|
|옵션인수 값을 제공 X | opt 값을 ? 문자로 설정/OPTARG 값은 unset/ 오류 메시지 출력|

|Silent mode||
|:---:|:---:|
|invalid 옵션 사용|opt 값을 ? 문자로 설정/OPTARG 값은 해당 옵션 문자로 설정|
|옵션인수 값을 제공 X | opt 값을 : 문자로 설정/OPTARG 값은 해당 옵션 문자로 설정| 

+ default는 verbose mode인데 기본적으로 옵션과 관련된 오류메시지가 표시되므로 스크립트를 배포할 때는 silent mode를 이용
+ silent mode를 설정하기 위해서는 옵션 스트링의 맨 앞부분에 : 문자를 추가해 주면 됨
+ 주의해야 할 점: ***OPTION***, ***OPTARG*** 변수는 ***local*** 변수가 아니므로 함수 내에서 ***local***로 설정해 사용해야 함
+ `$ command -a -b -c ` => 옵션 스트링이 'a:bc' 이면 -a는 옵션인수를 가지게 되는데 옵션인자에는 어떤 문자도 올 수 있기 때문에 다음과 같이 -a에 옵션인수가 설정되지 않으면 -b가 -a의 옵션 인수가 됨
+ `$ command -a foo.c -b -c ` => 파일명이나 기타 스트링은 마지막에 와야하는데 그렇지 않은 경우 이후 옵션은 인식되지 않음, 다음과 같은 경우에는 -b -c 옵션은 인식되지않음

---

## ***getopt 명령어***
+ ***getopt***명령어 는 이름이 ***getopts***명령어와 비슷한데 /usr/bin/getopt 에 위치한 외부 명령임
+ 기본적으로 ***short,long***옵션을 모두 지원함
+ 옵션 인수를 가질 경우 : 문자를 사용하는 것은 ***getopts*** 명령어와 동일함
```bash
$ getopt -o a:bc
=> short 옵션 지정은 -o 옵션으로 함

$ getopt -l help,path:,name:
=> long 옵션 지정은 -l 옵션으로 하고 옵션명은 ','로 구분함
=> 명령 라인에서 옵션 인수 사용은 "--name foo" 또는 "--name=foo" 두 가지 모두 가능

$ getopt -o a:bc -l help,path:,name: -- "$@"
=> 명령 마지막에는 -- 와 함께 "$@" 를 붙임
```
