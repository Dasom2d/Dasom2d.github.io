---
title: "Jekyll 테마 적용하여 블로그 만들기(feat.Minimal Mistakes)_2"
categories: 
  - blogging
last_modified_at: 2018-07-01T13:00:00+09:00
toc: true
---
# Jekyll 테마 적용하여 블로그 만들기
### #컴맹도 할 수 있다.
### part 2. Github 저장소 연결 및 블로그 포스팅하기

part1까지 잘 되었으면 이제 Github에 로컬 저장소와 연동하고, 포스팅할 수 있다.
포스팅할 때는 md파일을 이용한다.
md파일을 편집할 때는 난 하루패드나 visual studio code를 이용하는데 둘 다 딱히 단점도 장점도 없다.

### 1. Github에 저장소 생성하기
- github에 저장소(Repositary)가 없는 경우 저장소부터 만든다.  
![create Github repositary]({{site.url}}/assets/images/howToPosting/8.jpg)

① 자신의 Github로 가서 새로운 저장소를 만든다.   
② Owner와 Repositary name을 일치시킨다. (Github 계정.github.io 라는 규칙으로 만들어야 한다.)
③ 저장소는 public으로 설정하고 Create repositary!  

gitbash를 이용해서 생성하는 방법도 있는데, 이게 더 간편하다. ㅎㅎ

### 2. 로컬 저장소와 생성한 Github 저장소 연결
로컬저장소가 저장된 경로로 이동

    git init    //git 명령어를 사용할 수 있는 디렉토리로 만든다.
    git remote add origin [원격저장소 url]  // 로컬과 원격 저장소를 연결한다.


![connect Github repositary]({{site.url}}/assets/images/howToPosting/4.jpg)  
이 화면이 나오면 로그인해준다. 그럼 연결 끝!

git이 파일을 관리하게 하려면 github 저장소에 파일을 추가하고 커밋해야한다.  
    
        git add .
        git commit -m "커밋메시지"
        git push orgin master



