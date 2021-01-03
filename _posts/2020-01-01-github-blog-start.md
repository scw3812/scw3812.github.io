---
layout: post
title: Github 블로그 시작하기
subtitle: Jekyll을 활용한 Github 블로그 만들기
thumbnail-img: https://media.vlpt.us/images/cyongchoi/post/9f4a8b71-bdf4-4266-b25c-40fc5e29d761/asasf.png
tags: [개발]
---

제 Github 블로그의 첫 번째 글로 `Github 블로그 시작하기`를 써보려고 합니다.    

저는 이제 개발을 시작한지 대략 2년 정도 밖에 안된 개린이입니다. 짧은 기간 동안 개발 공부를 하면서 안드로이드 프로그래밍, 리액트 등 
여러 기술 스택을 쌓으려고 노력해왔고, 꽤 많은 공부를 한 것 같습니다. 하지만 따라가기에 급급해 제가 공부한 내용을 제대로 정리해 본 적은
없었습니다. 그래서 새해를 맞이하면서 이런 부분을 고치고, 더 좋은 개발 실력을 쌓기 위해 개발 블로그를 시작하게 되었습니다.  

개발 블로그에 대해 알아보면서 어떤 플랫폼을 활용하면 좋을까 고민을 했는데 Github Contribution 초록점도 찍을 수 있고, 마크다운 문서
작성법에도 익숙해지면 좋을 것 같다고 생각하여 Github 블로그를 선택하게 되었습니다. 무엇보다 Github Pages는 **무료 호스팅**이기 
때문에 선택하지 않을 이유가 없다고 생각했습니다.

그렇게 Github Pages와 Jekyll로 Github 블로그를 만든는 방법을 공부하였고, 그 내용을 제 블로그의 첫 글로 작성하게 되었습니다.

## 1. Github Repository 만들기

![repo 생성](https://user-images.githubusercontent.com/49465188/103454172-96da9180-4d24-11eb-8e8e-d8b15559784d.png){: width="700"}{: .mx-auto.d-block :}

우선 **Github Repository**를 하나 만들어야 합니다. 레포 이름은 무엇으로 하든 상관없이 Github Pages로 호스팅 할 수 있지만 저는 
편의를 위해 바로 호스팅 되는 yourname.    
github.io(yourname에 자신의 Github 아이디를 넣으면 됩니다)로 만들었습니다.

## 2. Jekyll 테마 찾기

![Jekyll 테마](https://user-images.githubusercontent.com/49465188/103454331-38161780-4d26-11eb-914c-cf7131ad122a.png){: width="700"}{: .mx-auto.d-block :}

먼저 원하는 **Jekyll 테마**를 찾아야 합니다.  
Github에 공개되어 있는 [Jekyll 테마](https://github.com/topics/jekyll-theme)들을 보면서 원하시는 것을 고르시면 됩니다. 저는 사용하기 간단해
보이고 제가 보기에 예쁘다고 생각되었던 `beautiful-jekyll`을 선택하였습니다.

## 3. Jekyll 테마 적용하기

Jekyll 테마를 적용하는 방법은 여러가지가 있는데 제가 사용해본 두 가지 방법을 소개해보려고 합니다.

### Jekyll remote theme 사용하기

우선 선택한 테마의 `_config.yml` 파일을 복사해서 생성한 레포지토리에 같은 파일을 만듭니다. 이 파일은 Jekyll의 환경설정 파일이라고 생각하면 됩니다.  

그리고 생성된 파일의 밑에 아래와 같은 코드를 추가해주시면 됩니다.

{% highlight javascript linenos %}
remote_theme : daattali / beautiful-jekyll
{% endhighlight %}

이는 Github 페이지의 remote_theme를 설정하는 코드이며, `owner/repository`의 형식으로 이루어집니다.
이 다음에는 만약 url과 baseurl 값이 있다면 이를 설정해 주어야 합니다. url의 경우에는 Github 페이지의 url,
baseurl은 빈 문자열로 설정합니다.

{% highlight javascript linenos %}
url : "https://yourname.github.io"  
baseurl: ""
{% endhighlight %}

그리고 이외의 설정은 원하시는 값으로 적절히 설정하시면 됩니다.  

다음은 아까 `_config.yml`을 복사해 온 것처럼 이번에는 `index.html` 또는 `index.md` 파일을 복사해 옵니다.
이 파일은 보통 블로그의 홈페이지를 나타내는 파일입니다.  
이외에도 `posts.md` 등 테마에 따라 필요한 파일이 더 있을 수도 있습니다. 만약 블로그가 제대로 나오지 않는다면 
필요한 파일들을 확인해주세요.

Jekyll remote theme를 사용하면 앞서 봤던 것처럼 아주 간단하게 블로그를 만들 수 있습니다. 하지만 블로그의 css 
등을 커스터마이징하는 것은 불가능합니다. 커스터마이징을 하기 위해서는 자신만의 _layouts, _includes, _sass, assets 
등의 폴더들을 만들어야 합니다.

### 수동으로 설정하기

두번째 방법은 수동으로 설정하는 방법입니다. Jekyll은 Ruby 기반의 정적 웹 사이트 생성기이기 때문에 만약 로컬에서 테스트하고
싶으시면 Ruby를 다운 받고, 원하시는 테마를 Github에서 로컬로 가져와 개발하시면 됩니다. 저는 Github 내에서만 모든 작업을 
할 생각이기 때문에 Ruby를 다운받지 않고, 레포에 바로 올려서 사용하겠습니다.  

![코드 복사](https://user-images.githubusercontent.com/49465188/103469774-59214b80-4dac-11eb-907f-94764140de6b.png){: width="700"}{: .mx-auto.d-block :}

우선, 원하시는 테마의 레포로 이동합니다. 위 사진에 보이는 것처럼 Code라고 써진 초록 버튼을 누르면 여러 옵션이 있는데 url을
복사해서 `git clone`으로 가져오셔도 되고, 그냥 zip로 다운받아서 레포에 올리셔도 됩니다. 저는 후자를 선택하겠습니다.  
(이 두 가지 방법말고도 fork를 해오는 방법도 있는데 이 경우 초록점이 찍히지 않기 때문에 저는 직접 가져와서 레포에 올리는 방법을 선택하였습니다.)  

이제 다운받으신 파일을 Github 웹페이지에서 Add File을 이용하거나, `git push`로 업로드합니다. 업로드 성공하시면 아래처럼 여러
파일들이 레포에 올라가게 됩니다.

![푸쉬 성공](https://user-images.githubusercontent.com/49465188/103469868-df8a5d00-4dad-11eb-9139-151b14346010.png){: width="700"}{: .mx-auto.d-block :}

이제 앞서 했던 것처럼 `_config.yml` 파일을 적절히 수정하시면 됩니다.

## 4. 블로그 첫 글 작성하기

이제 드디어 블로그 설정이 끝났습니다. 이제 블로그 글을 작성하시면 됩니다. 일반적으로 Jekyll은 `_posts` 폴더 안에
일정 형식으로 마크다운 문서를 만들면 그 파일이 블로그 포스트로 적용됩니다. 제가 적용한 테마의 경우 '연-월-일-제목.md'
이런 형식으로 파일을 작성하면 됩니다.

![포스트 예시](https://user-images.githubusercontent.com/49465188/103469951-f2516180-4dae-11eb-8f7c-1d40c750ebd5.png){: width="700"}{: .mx-auto.d-block :}

그리고 생성한 파일 안에는 위 사진처럼 테마에서 요구하는 값들을 넣어주고, 그 아래로는 마크다운 문법에 맞춰 원하는
내용을 적어나가시면 됩니다.  

이렇게 나만의 Github 블로그가 만들어졌고, 이제 설정하신 url(yourname.github.io)로 들어가시면 완성된 블로그를 보실 수 있습니다.
아래는 제 블로그 예시입니다.

![블로그 예시](https://user-images.githubusercontent.com/49465188/103469983-6be94f80-4daf-11eb-8a55-292b01f48486.png){: width="700"}{: .mx-auto.d-block :}

## 마치며

이렇게 저의 첫 블로그 글이 완성 되었네요. 처음 블로그 설정을 하고, 글을 쓰면서 어려운 부분도 있었고, 귀찮은 점도 있었는데
막상 이렇게 다 만들고 나니 뿌듯하고 뭔가 개발 공부 의욕이 생깁니다. 블로그 만들기를 잘했다는 생각이 드네요.

{: .box-note}
**참고**    
- https://dreamgonfly.github.io/blog/jekyll-remote-theme/
- https://github.com/daattali/beautiful-jekyll
