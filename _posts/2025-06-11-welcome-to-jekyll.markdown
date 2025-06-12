---
layout: post
title:  "GitHub 블로그 너무 어려워요..."
date:   2025-06-11 15:35:16 +0900
categories: daily
---
### **까불지말걸**

구글에서 검색이 좀 되게 하려고 google 검색에 노출이 되게하려고 네이버 블로그를 잠시 유기하고 
tistory는 좀 왠지 안하고 싶은 느낌이 있고해서 아무래도 개발이 취미인 사람이면 github blog지 ^ㅇ^ 
이런 마인드로 괜히 시작해봤는데 초보 주제에 너무 나댔다는 생각을 한다

테마도 no CSS인 이 뭔가 옛날 컴퓨터화면이 마음에 들어서 이거로 선택했는네 역시 예쁜 주어진거 쓸 걸 싶기도 하고..
개인적으로 추구하는 가치가 다른 모든 불편함이 있더라도 그럼에도 나를 찾아주는 것, 이런 걸 원하기 때문에 그래도 이 스타일 그대로 간다.

아무튼 돌고 돌고 돌아서 이제 겨우 게시판 제목만 돌아가게 만들어놓고, 댓글 기능을 좀 추가했다. 
여러 무림의 고수들이 이미 잘 정리해주고 있지만 고수들이 초보의 마음을 어떻게 파악하겠는가... 
군주론에서도 산을 보려거든 낮은 곳에서 올려다봐야한다 했듯이 개발자가 아닌 입장에서 바라본 바를 정리하려한다.

참고로 한글 옆에 영어 섞어써둔 것은 글을 read 하기 어렵게 하려는게 아니라 제가 몰랐던 오피셜 용어들이라 기록하려고 그렇게 씀.

### **기본 준비**
 1. VScode
  - GitHub 블로그그를 해야지하는 사람이라면 python에서 helloworld는 출력해봤을테니 VScode 같은 코드 편집기는 당연히 있을 것임

 2. Ruby
  - Ruby는 python처럼 프로그래밍 언어의 하나임. 깃허브 블로그는 아래에 나올 Jekyll 이라는 사이트 생성기를 사용하는데, 이 빌어먹을 Jekyll이 Ruby 언어를 기반으로 작동하기 때문에 Ruby를 선제적으로 다운받아줘야함. [윈도우 Ruby Installer 다운 링크](https://rubyinstaller.org/downloads/)
  - ![Image](https://github.com/user-attachments/assets/35d04c28-f1c2-476b-973b-8540f4dae3f4)
  - Ruby를 다운받으면 위와 같은 화면이 나오는데 아무것도 모르는 사람(=나)을 위해 확신이 없으면 엔터누르라니까 엔터누르면 알아서 필수 파일인 1, 3이 다운로드 됨.
  ```bash
  $ ruby -v
  $ ridk version
  ```
  - 위 명령어를 했을 때 버전 정보가 충분히 잘 나온다면
  ```bash
  $ gem install jekyll bundler
  ```
  - 이제 jekyll을 까는 것... 하다보면 ㄹㅇ 제길이란 욕이 절로나옴. 제길과 하이드자식...
 
 3. Jekyll
  - 위에 설명했듯이 제ㅡ길은 사이트 생성기다. 블로그 프로젝트를 담고 싶은 디렉토리로 이동한 다음
  ```bash
    $ jekyll new 폴더명
  ```
    을 입력하면 jekyll이 다운받아진다. 
  - 다음은 터미널에서 디렉토리를 폴더명으로 변경 한 다음 
  ```bash
    $ bundle exec jekyll serve
  ```
    을 입력하면 터미널에 Server address: http://127.0.0.1:4000/ 이 나타날텐데 그러면 1차 과정은 완성이다.

### **GitHub**
  1. Repository - settings - pages - deploy from a branch 로 안내하고 있는 옛날 글들이 많은데, 초보인 내가 이거 선택하고 무작정 따라하다가 도대체 왜 안되는지를 몰라서 한참을 고생했다. 결론부터 말하자면 블로그 한정, ★deploy from a branch 말고 GitHub Actions로★ 추세가 바뀌었고 branch에서 배포하는 것은 옛날 방식이라 일반적으로는 지금 쓸 필요는 없다는 것.

  이게 무슨 차이냐면 deploy from a branch도 jekyll을 사용해서 사이트를 만들고(빌드) 배포(deploy)를 하지만, 코드엔 변화가 없어도 이건 github 자체적인 build와 deploy기능(옛날 방식)이라 최ㅡ신 테마나 플러그인은 오류가 나서 사이트가 제대로 빌드되지 않게된다. 사이트까지 잘 봐놓고 테마가 적용안되서 한참 삽질했는데 이게 문제임을 나중에 깨달았다.

  아무튼 그래서 GitHub Actions의 jekyll을 선택하면, \\.github\\workflows에 jekyll.yml이 만들어지고 얘를 통해서 build와 deploy이 이루어지기 때문에 제가 겪었던 뭐 jekyll 버전 오류, 플러그인 오류 기타 등등을 안겪으실 수 있습니다...

  2. 이게 되고나면 뭐 폴더와 repository를 연결하고 평범하게 push를 하시면 됩니다.

### **테마의 적용**
  1. 결론부터 말하자면 코드를 본인 repository로 고대로 가져가서(github의 fork를 클릭) 이름을 바꾼 뒤에 그걸 배포해버리는게 가장 편하고, 그게 아니라면 파일로 다운받아서 기존 폴더 내용을 덮어씌우는게 편함. 내 경우는 deploy from a branch로 해서 gemfile을 수정하고 테마바꿨으나 build가 안됐다. 이유는 처음에는 jekyll 버전 충돌, ruby 버전 충돌, 플랫폼 충돌... 결론은 local에서는 파일이 변한 것 같았지만 deploy가 전혀 안됐다. 이래서 위에 말한 고생을 한건데, 아무튼 기존 폴더 내용을 모두 가져와서 덮고, readme를 읽으면서 커스터마이징을 하는게 정론입니다.

  2. 덮어씌우더라도 위에 말한 플랫폼 충돌은 그래도 일어날 가능성이 있는데 아래와 같은 error가 나온다.
  ```bash
  Your bundle only supports platforms ["x64-mingw-ucrt"] but your local platform
  is x86_64-linux. Add the current platform to the lockfile with
  `bundle lock --add-platform x86_64-linux` and try again.
  Error: The process '/opt/hostedtoolcache/Ruby/3.1.6/x64/bin/bundle' failed with exit code 16
  ```
  역시 초보를 위해 설명해두었지만 bundle은 리눅스를 사용하는데, 네 로컬은 윈도우라 저 명령어를 사용해서 gemfile.lock 을 수정하라는 뜻이다. 
  ```bash
  bundle lock --add-platform x86_64-linux
  ```
  하면 잘 해결된다.

  3. 겉멋충인 내가 선택한 [no-style-please](https://github.com/riggraz/no-style-please)는 초보용이 아닌 테마인 것인지 간략하게 어떻게 커스터마이징하는가를 뭔가 좀 당연히 안다는 듯이 써놓은 느낌이라 이 과정도 꽤 헤맸다. 테마마다 그 내부 구성을 어떻게 하였는지는 전부 다를 수 있겠지만, 대락적인 구성은 크게 다르지 않을 텐데, 결국 블로그 하는 사람이 궁금한건 어떻게 게시판을 만들고, 그 게시판 하위에 분류를 또 나눌 것인가 밖에 없다. 그것 말고는 설정할 것이라곤 딱히 없는 레이아웃이라...이걸 주소를 어떻게 바꿔야하나해서 config.yml에서 permalink를 손대고 기타등등 헛짓을 또 했지만 
  
  아무튼 결론으로 가면
   - _config.yml 여기서는 기본적인 정보들을 넣는 곳. 딱히 건드릴 건 없음★
   - \\_data\\menu.yml 이게 기본적인 메뉴를 수정하는 곳. 문법은 나와있듯이 entry\\title\\entry\\title.. 이런식으로 게시판을 나눠 나가면 되는데 중요한건 그렇게 나눈다 치고 post를 어떻게 특정 category로 집어넣는가 하는 것이다. 이걸 하려면 title 하위에 ★category 를 지정해줘야한다... 이렇게 다 가능하도록 쉽게 구현해놨는데 이걸 몰라서 그렇게 해맸다. 현 블로그의 경우 저렇게 돼있으니 나중에 post를 쓸 때 categories: "projects"로 지정해주면 된다는 것. 

   ```yml
  - title: Projects
    post_list:
      category: projects 
      limit: 10         
      show_more: true   # '더보기' 링크를 표시할지 여부
      show_more_text: See all projects... # '더보기' 링크에 표시될 텍스트
      show_more_url: archive-projects.html
   ```
    - 이렇게 해주고나면 10개까지 보여주고, 이후는 더보기 링크를 표시하고, 더보기를 누르면 archive-projects.html을 띄운다는 뜻이다. 이때 현 템플릿은 기본적으로 all posts 라는 기능을 제공하고 얘는 archive.html로 연동되는데 그 사이트를 보면 
    ```html
    ---
    layout: default
    ---

    {%-include back_link.html-%}

    <h1>{{ page.title }}</h1>

    {%-include post_list.html category=page.which_category-%}
    ```

    이렇게 생겼다. 이것을 조금 활용해서 categories로 게시글을 연동하고 싶으면 아래와 같이 which_category: projects라고 지정을 해주면 되겠다.
    ```html
    ---
    layout: default
    title: "Daily - Archive"
    which_category: daily
    ---

    {%- include back_link.html -%}

    <h1>All Posts in: Daily</h1>
    ```

  4. 그럼 이제 \\_posts\\YYYY-MM-DD-my-title.md 파일을 만들고 

    ```
    ---
    layout: post
    title:  "GitHub 블로그 너무 어려워요..."
    date:   2025-06-12 12:52:16 +0900
    categories: daily
    ---
    ```
  
    이렇게 헤드를 달아주면 posts 폴더에 있는 글도 daily로 귀신같이 분류가 된다.

### **댓글**
1. 아직도 댓글이 사이트에서 유난히 툭 튀는게 아주 거슬리지만 능력이 없으면 참고 쓰는 수 밖에(?). Github blog는 데이터베이스를 사용하는게 아니라 계속해서 commit하여 페이지를 만드는 개념이라 외부인이 댓글 기능을 사용하기가 불가능한데, 이를 해결하는게 github repository의 issue 혹은 discussion을 사용하는 것이다. 이미지 올릴 때도 사용하는 기능인데 뭐냐면, github repository에 issue 나 discussion은 github ID가 있는 누구나 올릴 수 있는데(repository가 public이라면) 거기에 글을 올리게되면 그 issue 와 discussion은 주소가 할당되기 때문에 가져올 수 있게 되는 것. 그래서 post를 올리면 그 글 내용의 discussion이 발생하고, 거기 댓글 다는 것을 블로그로도 가져오게 된다. 

2. 설명이 길었는데 그래서 하는 법은 issue를 기반으로 하는 utterances, discussion을 기반으로 하는 giscus가 있고 나는 대댓글 기능까지 가능한 giscus를 사용했다. 순서는
 - [giscus 설치 링크](https://github.com/apps/giscus) 여기서 selected repository로 본인 블로그가 있는 repository를 선택해서 설치
 - github에서 Repository settings -> general -> features -> discussions 탭을 활성화, 이후 pull request 옆에 discussions tab으로 직접이동해서 general 등의 카테고리를 클릭해서 discussion을 하나 만듦
 - [giscus App 연동 페이지](https://giscus.app/ko) 여기서 저장소: GitHub 아이디/repository 이름 만 적어넣고 나머지 모르겠는 기타 경로 이런건 기본값 그대로 두고 아래에 discussion category를 아까 만든 general 등의 카테고리로 선택. 
 ![Image](https://github.com/user-attachments/assets/00ee2b0c-0e14-4cbd-a9c8-9ebb13669163)
 - 다음에는 아래에 있는 어울릴 것 같은 테마만 선택해주면 준비 완료. 
 - 그걸 바탕으로 아래 생성된 코드를
 ```html
 <script src="https://giscus.app/client.js"
        data-repo="[ENTER REPO HERE]"
        data-repo-id="[ENTER REPO ID HERE]"
        data-category="[ENTER CATEGORY NAME HERE]"
        data-category-id="[ENTER CATEGORY ID HERE]"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="ko"
        crossorigin="anonymous"
        async>
</script>
```
 - 댓글이 달려야하는 layout, 현 템플릿의 경우 \\_layouts\\post.html 가장 아래에다가 갖다 붙여넣으면 된다. 


### **확인**
![Image](https://github.com/user-attachments/assets/051958b9-aa0c-4e1b-9633-7e54febf41db)
고난의 흔적들...
아무튼 그렇게 posts를 다 작성하셨다면 github action tab에서 가장 위처럼 commit 명으로 push 가 잘 되었는지 확인하면 진짜 끝.

험난했지만 요정도했으면 github 블로그 시작하기의 기본 정리는 된 것 같다.
시작부터 험ㅡ난..

