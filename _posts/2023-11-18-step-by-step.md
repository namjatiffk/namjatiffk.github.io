---
layout: post
title: Github Pages 하나씩 이해하기
subtitle: Jekyll, Liquid부터 알아가는 시간
tags: [Skit, GithubPages]
categories : [Github-Pages]
---

### Github Pages를 쓸러면 Jekyll을, Jekyll을 쓸려면 Liquid를

Github Pages 튜토리얼 따라하면서 아무것도 모르지만 그냥 클릭 몇번만으로 나만의 Github Pages가 완성이 됨 <br>
commit 해서 push만 해주면 Github Action이 알아서 workflow대로 build랑 deploy를 해줌

난 개발자도 아니고 Github Action이 대충 CI/CD 개념인가하고 대충 이해하고 넘어감 <br>
여튼 Github Pages의 기본 workflow의 build/deploy가 [1시간에 10번까지로 제한이 있음](https://docs.github.com/ko/pages/getting-started-with-github-pages/about-github-pages#usage-limits)

`GitHub Pages sites have a soft limit of 10 builds per hour. This limit does not apply if you build and publish your site with a custom GitHub Actions workflow`

일단 내가 1시간에 10번이나 build 해가면서 열정적으로 할 것 같지는 않지만, 나름 다크테마 노가다할려고 css 파일이나 _config.yml이든 이것저것 값을 바꾸면서 적용시키다보니 이 build 제한이 좀 빠듯하게 느껴짐

근데 공식문서 보면 커스텀 workflow에 대해선 제한이 없다고 함 <br>
마침 내가 가져다 쓴 이름부터 Beautiful한 [Beautiful Jekyll](https://github.com/daattali/beautiful-jekyll#readme) 디렉토리상 .github 폴더가 있었고, 이 안에 workflows 폴더랑 workflow 파일로 보이는 ci.yml이 있었음

파일명부터가 딱 ci인거보면 이게 커스텀 workflow 파일임에 확실해서 내 디렉토리 복붙한 상태임

이제 1시간에 10번 build 제한 걸리는 지는 아주 나중에 확인해 보면 되구 <br>
JeKyll에 대해서 공부좀 해볼겸 _config.yml이나 _layout, _includes 폴더 등에 있는 html 파일 딱 열어서 봄 

근데 일단 오늘은 여유로운 일요일이니깐 JeKyll 디렉토리 구조부터 좀 알아야겠다싶어서 유튜브에 검색해서 JeKyll에 대해 설명 잘해주신 영상 보면서 기본 개념을 파악함

['Jekyll 기반의 GitHub Page 생성(1) - 환경설정' 얼큰우동TV,쉽게배우는 IT](https://www.youtube.com/watch?v=2ClW2LdqP30)

러닝머신에서 40분동안 러닝하면서 1.5배속으로 얼큰우동님 영상보면서 기본 개념 익힘 <br>
되게 목소리 좋으시고 설명 깔끔하시고, 오프라인 강의를 주로 하신다고 하는데 유튜브 강의영상도 정말 잘 만들어주심

그렇게 JeKyll 디렉토리 구조랑 _config.yml 내 변수 의미들을 파악하고, 고작 40분 영상으로 공부하고나서 JeKyll 마스터한 기분으로 다시 html 파일들 열어봄

딱 봐도 Python Django 개발 때 사용했던 문법들이 html에 속속 박혀있는데, 찾아보니 이런걸 Liquid 라고 함 <br>
Django 때 많이 봐오던 친구들이니깐 크게 거부감 없이 가볍게 [Liquid 공홈 문서](https://shopify.github.io/liquid/basics/introduction/) 정독 함

이제 진짜 마스터했다 싶어서 다시 html 내부에 Liquid 코드들 보는데, site, page 등등 내가 알 수 없는 Object 변수명들이 나옴..

[도대체 이게뭐지 싶어서 JeKyll 공홈 문서](https://jekyllrb.com/docs/variables/) 찾아보니 JeKyll에서 사용하는 변수명들이었음 <br>
아 분명 Github Pages 처음 시작할 때, JeKyll 공홈 문서 보면서 한번씩 읽었던 내용들인데 너무나도 당연히 까먹은 상태였음

다시 JeKyll 문서 정독하고나니 나의 일요일이 끝나감 <br>
천천히 하나씩 알아가야징

끝
