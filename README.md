## Homework-1
---
***awk 명령어***
+ awk란 패턴 탐색과 처리를 위한 명령어로 간단하게 파일에서 결과를 추려내고 가공하여 원하는 결과물을 만들어내는 유틸리티입니다.
+ 초기 개발자 Aho, Weinberger, Kernighan의 첫글자를 따서 이름이 지어졌습니다.
+ GNU 프로젝트에서 만들어진 텍스트 처리 프로그래밍 언어로 유닉스 계열의 OS에서 사용 가능합니다.
+ 텍스트 형태로 되어있는 입력 데이터를 행과 단어 별로 처리해 출력해줍니다.
---
**사용법**
```
awk [OPTION][awk program][ARGUMENT]
```
 *option의종류*
  + -f : awk program 파일 경로 지정
  + -F : 필드 구분 문자 지정
  + -v : awk program에서 사용될 특정 값 지정

awk program : -f옵션이 사용되지 않았을때, awk가 실행할 awk program 코드 지정 \
ARGUMENT : 입력파일 지정 또는 variable(값) 지정 

---
**awk의 주 사용용도** 
1. 텍스트 파일의 전체 내용 출력
2. 파일의 특정 필드만 출력
3. 특정 필드에 문자열을 추가해서 출력
4. 패턴이 포함된 레코드 출력
5. 필드 값 비교에 따라 레코드 출력

---
**사용 예시**

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
