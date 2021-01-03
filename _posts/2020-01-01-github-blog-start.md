---
layout: post
title: Github 블로그 시작하기
subtitle: Jekyll을 활용한 Github 블로그 만들기
thumbnail-img: https://media.vlpt.us/images/cyongchoi/post/9f4a8b71-bdf4-4266-b25c-40fc5e29d761/asasf.png
tags: [개발]
---

제 Github 블로그의 첫 번째 글로 `Github 블로그 시작하기`를 써보려고 합니다.    

저는 이제 개발을 시작한지 대략 2년 정도밖에 안된 개린이입니다. 짧은 기간 동안 개발 공부를 하면서 안드로이드 프로그래밍, 리액트 등 
여러 기술 스택을 쌓으려고 노력해왔고, 꽤 많은 공부를 한 것 같습니다. 하지만 공부하면서 따라가기에 급급했고, 제대로 정리해보거나 
체계적으로 공식문서 등을 보며 익히지는 못해습니다. 그래서 새해를 맞이하면서 이런 부분을 고치고, 더 좋은 개발 실력을 쌓기 위해 개발
블로그를 시작하게 되었습니다.  

여러 개발 블로그에 대해 알아보면서 어떤 플랫폼을 활용하면 좋을까 고민을 했는데 Github Contribution 초록점도 찍을 수 있고, 마크다운 문서
작성법에도 익숙해지면 좋을 것 같다고 생각해서 Github 블로그를 선택하게 되었습니다. 무엇보다 Github Pages는 **무료 호스팅**이기 때문에 선택하지
않을 이유가 없다고 생각하였습니다.

그렇게 Github 블로그를 만드는 방법에 대해 구글링을 시작했고, Github Pages와 Jekyll을 활용하여 만든다는 것을 알게되어 그 내용을 제 블로그의
첫 글로 작성하게 되었습니다.

## 1. Github Repository 만들기

![repo 생성](https://user-images.githubusercontent.com/49465188/103454172-96da9180-4d24-11eb-8e8e-d8b15559784d.png){: width="700"}{: .mx-auto.d-block :}

우선 **Github Repository**를 하나 만들어야 합니다. 레포 이름은 무엇으로 하든 상관없이 Github Pages로 호스팅 할 수 있지만 저는 편의를 위해 바로 
호스팅 되는 yourname.  
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
이 파일은 보통 블로그의 홈페이지를 나타내는 파일입니다. 이외에도 `posts.md` 등 테마에 따라 필요한 파일이 더 있을
수도 있습니다. 만약 블로그가 제대로 나오지 않는다면 필요한 파일들을 확인해주세요.

### 수동으로 설정하기

두번째 방법은 수동으로 설정하는 방법입니다. Jekyll은 Ruby 기반의 정적 웹 사이트 생성기이기 때문에 만약 로컬에서 테스트하고
싶으시면 Ruby를 다운 받고, 원하시는 테마를 Github에서 zip 형태로 다운받으셔서 개발하시면 됩니다. 저는 Github 내에서만 모든
작업을 할 생각이기 때문에 Ruby를 다운받지 않고, 레포에 바로 올려서 사용하겠습니다.
