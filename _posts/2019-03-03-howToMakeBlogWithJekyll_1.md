---
title: "Jekyll 테마 적용하여 블로그 만들기(feat.Minimal Mistakes)_1"
categories: 
  - blogging
last_modified_at: 2018-07-01T13:00:00+09:00
toc: true
---
# Jekyll 테마 적용하여 블로그 만들기
### #컴맹도 할 수 있다.
### part 1. 블로그 생성하기

Jekyll 테마를 적용하여 블로그 만드는 방법에는 여러가지가 있다.  
다른 블로그들에도 많이 설명되어있듯이 되게 간단하다.  
난 삽질 여러번했다ㅜㅜ  
핑계를 대자면 다른 블로그에는 중간 과정이 생략되어있었다.  
그래서 나는 Jekyll을 이용한 블로그만들기 A to Z까지 상세히 적어보았음 ㅎ

### 0. 블로그 만들기
블로그 만드는 것에는  
① 블로그만들고 -> 테마입히기  
② 테마입힌 블로그만들기
두가지 방법이 있는데, 어떤 방법을 해도 상관없지만 나는 ②로 했다.(귀찮거든..)  
그러기 위해서는 테마부터 선택해야한다.

### 1. 테마 선택하기
[지킬테마] <http://jekyllthemes.org>   
위 사이트에 가면 똑똑한 사람들이 만들어놓은 여러가지 지킬 테마가 있다.
처음에는 여기서 제일 간지나는 걸로 신중하게 선택했었는데, 커스터마이징하는 방법이 상세히 설명되어있지 않아서 컴맹인 나는 따라하기가 힘들었다 ㅠ.ㅠ  
 그래서 사람들이 `많이` 사용하고 `사용법 설명이 많은` Minimal Mistakes 테마 선택 
[minimal-mistakes] <https://github.com/mmistakes/minimal-mistakes>

덧붙임) ①의 방법대로 하면 fork해서 테마를 `쉽게` 입힐 수도 있지만, 그 방법대로 하면 minimal-mistakes의 모든 커밋로그가 내 블로그에도 따라오기 때문에 추천하지 않는다.

### 2. 테마 다운로드
![릴리즈 다운로드]({{site.url}}/assets/images/howToPosting/5.jpg)
[Minimal Mistakes] <https://github.com/mmistakes/minimal-mistakes/releases)>  
위 사이트에 가면 Minimal Mistakes release를 다운받을 수 있다.

### 3. 불필요한 파일 삭제
    - .editorconfig
    - .gitattributes
    - .github
    - /docs 
    - /test
    - CHANGELOG.md
    - minimal-mistakes-jekyll.gemspec
    - README.md
    - screenshot-layouts.png
    - screenshot.png
`/docs` <- <https://github.com/mmistakes/minimal-mistakes> 를 만드는 것에 사용된 파일이 있기 때문에 참조하려면 삭제하지 않아도 된다.
### 4. _posts 폴더 생성
_posts : 배포될 포스트들이 담기는 폴더

### 5. gem파일 수정
gem파일을 아래의 내용으로 수정한다.
    
    source "https://rubygems.org"

    gem "jekyll", "~> 3.5"
    gem "minimal-mistakes-jekyll" 
    
    

여기까지 잘 따라했다면 블로그를 만드는데 필요한 파일들은 모두 준비가 되었다.
여기까진 쉬움ㅋ  
루비설치부터 골때림

---
### 5. 루비 다운로드
루비를 받아야 지킬을 설치할 수 있다.

![루비 다운로드]({{site.url}}/assets/images/howToPosting/1.jpg)

[루비 다운로드] <https://rubyinstaller.org/downloads/> ==>Ruby+Devkit 2.5.4-1(x64)를 다운로드한다.  
Devkit까지 함께 있는 파일을 다운로드한다.

### 6. 루비 설치
![루비 설치1]({{site.url}}/assets/images/howToPosting/2.jpg)

`add ruby executables to your PATH` 체크하여 path 환경변수에 등록하도록 설정

아래 화면이 나오면 1, 2, 3 순서대로 설치한다.

![루비 설치2]({{site.url}}/assets/images/howToPosting/3.jpg)

아래 명령어를 통해 루비 설치가 제대로 되었는지 확인한다

	ruby -v

    
아래 이미지처럼 루비 버전이 나온다면 루비 설치 성공!

![로컬 블로그 인코딩 오류]({{site.url}}/assets/images/howToPosting/6.jpg)

### 7. gem 명령어를 통해 지킬과 실행에 필요한 패키지 설치
루비 콘솔이나 콘솔창(cmd)를 켜서 블로그 파일이 저장된 경로로 이동
     
    gem install jekyll
    gem install minima
    gem install bundler
    gem install jekyll-feed
    gem install tzinfo-data
    
    
패키지들이 제대로 설치됐다면 이제 로컬에서 블로그 미리보기가 가능하다.

### 8. 로컬에서 블로그 미리보기
① 블로그 저장 폴더로 이동한다.  
② 지킬을 실행한다.
    
    bundle exec jekyll serve 
    
    
③ windows에서 실행할 경우 아래 에러가 날 수 있다.

![로컬 블로그 인코딩 오류]({{site.url}}/assets/images/howToPosting/7.jpg)  
인코딩 에러 발생시 다음의 코드를 실행한다.  
    
    chcp 65001
    
    
④ 지킬 실행
    
    bundle exec jekyll serve 
    
    
 ⑤ localhost:4000에서 생성된 블로그 확인
 
 