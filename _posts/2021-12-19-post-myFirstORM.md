---
title: "클라우드 환경에서 스프링 부트를 이용해 서비스 개발하기"
excerpt_separator: "<!--more-->"
categories:
  - Patterns
tags:
  - IntelliJ
  - JPA
---

***개발환경 구축하기***<br>


# 개발환경  
IDE : IntelliJ  
F/W : Spring Boot  
Build : Gradle  


개발툴은 보통 사용하는 이클립스가 아닌 IntelliJ를 사용한다.  
그 이유는 아래와 같다. (이클립스에 비해 IntelliJ가 갖는 장점)  
  1. 스프링 부트 개발에 좀 더 친숙하다.
  2. 강력한 추천 기능
  3. 다양한 리팩토링 및 디버깅 기능
  4. git 연동
  5. 빠른 검색 속도(프로젝트 시작 시 인덱싱)
  6. 최근 강세를 보이는 IT 기업에서도 IntelliJ 유료 버전을 공식 IDE로 사용함
     - 네이버, 카카오, 라인, 쿠팡, 우아한형제들 등



## 개발환경 구축하기

### 1. <https://start.spring.io/>에서 초기 개발환경 만들기
스프링 이니셜라이저에 접속하여 원하는 설정대로 셋팅 및 Dependency를 추가한다.  
모든 설정 마친 후 하단의 GENERATE 버튼 클릭하면 ZIP 파일로 프로젝트를 내려받는다.  
내려받은 프로젝트 파일을 IntelliJ에 Import  
![image](\assets\image\startspring.png)

### 2. build.gradle 설정  
이제 프로젝트의 기본적인 설정을 할 차례다.  
먼저, build.gradle 파일을 열어 스프링 부트, JPA, H2, Lombok 등 필요한 설정이 올바르게 되어 있는지 확인하고, IntelliJ의 우측 [Gradle] 탭을 클릭하여 의존성들이 잘 받아졌는지 확인한다.  
*의존성설정은 github에서 확인가능하다.*
![image](\assets\image\gradleset.png)

### 3. IntelliJ와 Github 연동  
IntelliJ에서 Action 검색창을 열고(ctrl+shift+a) "share project on github"를 검색한다.  
github 로그인 창 또는 github repository 생성 창이 열릴 것이다. 필요정보를 기입하고 "Share" 버튼을 클릭하여 해당 프로젝트를 Git과 연동한다.  

github 연동 후 Git에 커밋할 필요가 없는 파일들을 제외해야 한다.  
gitignore를 통해 제외할 수 있는데, IntelliJ는 따로 plug-in을 내려받아 gitignore를 사용할 수 있다.  
IntelliJ에서 Action 검색창을 열고 "plugins" 검색하여 열고 ".gitignore"를 설치한다.  
첫 IntelliJ 프로젝트라면 바로 [Generate] 버튼을 클릭한다.  
gitignore 파일에 제외할 이름을 입력한다.  

**git Commit 단축키 : ctrl + k**  
**git Push 단축키 : ctrl + shift + k**




<!--
줄바꿈       스페이스바를 두번 + Enter 해준다.
문법표시     마크다운 문법 앞에 \를 붙여준다.
링크        <링크주소>
이미지삽입   ![image](이미지주소)
헤더        # h1
            ## h2
            ### h3
            #### h4
            ##### h5
            ###### h6

굵게         **강조된 텍스트입니다**
기울기       *기울여진 텍스트입니다*
취소선       ~~취소된 텍스트입니다~~
밑줄        <u>밑줄 있는 텍스트입니다</u>
글씨색      <span style="color:yellow">노란 글씨입니다.</span>

```언어 이름(소문자)
이 부분에 코드 적기
```

체크박스    - [ ] 체크 안됨
            - [X] 체크 됨

-->
