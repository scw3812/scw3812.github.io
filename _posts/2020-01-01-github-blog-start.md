---
layout: post
title: Github 블로그 시작하기
subtitle: Jekyll을 활용한 Github 블로그 만들기
cover-img: /assets/img/path.jpg
thumbnail-img: https://media.vlpt.us/images/cyongchoi/post/9f4a8b71-bdf4-4266-b25c-40fc5e29d761/asasf.png
tags: [개발]
---

제 Github 블로그의 첫 번째 글로 `Github 블로그 시작하기`를 써보려고 합니다.    

저는 이제 개발을 시작한지 대략 2년 정도밖에 안된 개린이입니다. 짧은 기간 동안 개발 공부를 하면서 안드로이드 프로그래밍, 리액트 등 
여러 기술 스택을 쌓으려고 노력해왔고, 꽤 많은 공부를 한 것 같습니다. 하지만 여러 기술들을 공부하면서 따라가기에 급급했고, 제대로 
정리해보거나 체계적으로 공식문서 등을 보며 익히지는 못해습니다. 그래서 새해를 맞이하면서 이런 부분을 고치고, 더 좋은 개발 실력을
쌓기 위해 개발 블로그를 시작하게 되었습니다.  

여러 개발 블로그에 대해 알아보면서 어떤 플랫폼을 활용하면 좋을까 고민을 했는데 Github Contribution 초록점도 찍을 수 있고, 마크다운 문서
작성법에도 익숙해지면 좋을 것 같다고 생각해서 Github 블로그를 선택하게 되었습니다. 무엇보다 Github Pages는 **무료** 호스팅이기 때문에 선택하지
않을 이유가 없다고 생각하였습니다.

그렇게 Github 블로그를 만드는 방법에 대해 구글링을 시작했고, Github Pages와 Jekyll을 활용하여 만든다는 것을 알게되어 그 내용을 제 블로그의
첫 글로 작성하게 되었습니다.

## 1. Github Repository 만들기

![repo 생성](https://user-images.githubusercontent.com/49465188/103454172-96da9180-4d24-11eb-8e8e-d8b15559784d.png){: width="700"}{: .mx-auto.d-block :}

우선 **Github Repository**를 하나 만들어야 합니다. 레포 이름은 무엇으로 하든 상관없이 Github Pages로 호스팅 할 수 있지만 저는 편의를 위해 바로 
호스팅 되는 **yourname.github.io**(yourname에 자신의 Github 아이디를 넣으면 됩니다)로 만들었습니다.

## 2. Jekyll 테마 찾기

![Jekyll 테마](https://user-images.githubusercontent.com/49465188/103454331-38161780-4d26-11eb-914c-cf7131ad122a.png){: width="700"}{: .mx-auto.d-block :}

먼저 원하는 **Jekyll 테마**를 찾아야 합니다.  
Github에 공개되어 있는 [Jekyll 테마](https://github.com/topics/jekyll-theme)들을 보면서 원하시는 것을 고르시면 됩니다. 저는 사용하기 간단해
보이고 제가 보기에 예쁘다고 생각되었던 `beautiful-jekyll`을 선택하였습니다.

## 3. Jekyll 테마 적용하기

Jekyll 테마를 적용하는 방법은 여러가지가 있는데 제가 사용해본 두 가지 방법을 소개해보려고 합니다.

### jekyll remote theme 사용하기

