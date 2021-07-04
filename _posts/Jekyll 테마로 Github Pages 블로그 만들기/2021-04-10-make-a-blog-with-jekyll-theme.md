---
title: 🐣 Jekyll 테마로 Github Pages 블로그 만들기
date: 2021-04-10 17:27:00 +09:00
tags: [github pages, jekyll]
category: [posts]
description: 마음에 드는 Jekyll 테마로 Github pages 블로그 만들기
---



내가 보려고 쓰는 jekyll theme으로 github pages 블로그 만들기~<br>

## github repo 생성

github repository에 `username.github.io`라는 리포지토리를 생성한다.

- `username`은 자기 github 아이디
- 특정 repo 안에 블로그를 만들고 싶었는데 경로 문제 때문에 삽질하다가 일단 기본 경로에 만들기로...

그리고 로컬에 clone 해준다.<br><br>



## 만든 repo에 jekyll 기본 설치하기

1. 만들어 둔 repo 로컬 경로에 가서 `jekyll new ./` 하면 해당 폴더에 새 jekyll 블로그가 생성됨
2. `bundle install` 해서 번들 설치하기
3. `bundle exec jekyll serve` 한 후 `localhost:4000`으로 들어가서 기본 블로그 실행되는지 확인



그럼 이제 테마를 정합시다.<br><br>

## Jekyll 테마 정하기

'jekyll theme'이라고 구글에 검색하면 많이 나오니 하나 고르기<br><br>



## 마음에 드는 테마 github 가서 clone하기

Jekyll 테마 github에 가서 clone하던지 zip 파일을 받던지 암튼 내려받기<br><br>



## 다운 받은 테마 적용하기

clone한 테마 폴더에 있는 것들을 모두 `username.github.io` 폴더에 붙여넣기

zip 다운 받았으면 압축 풀어서 복사-붙여넣기.<br><br>



## 다운 받은 테마에 있는 bundle 다운 받기

1. 다시 터미널에서 `bundle install` 해줌.
2. 다시 서버 실행 `bundle exec jekyll serve`<br><br>
3. 잘 되면 `username.github.io` 리포지토리에 commit, push 하기



## _congif.yml 수정해서 나만의 블로그 만들기

이건 테마 제작자마다 달라서 해당 테마의 문서를 참고하는 것이 좋을 것.

대충 authorname 이라던지 repo url 이라던지 블로그의 기본 정보를 변경할 수 있다.<br><br>



## 글 작성은 _posts 디렉토리에

`YEAR-MONTH-DAY-title.md` 형식으로 `_posts` 디렉토리 밑에 마크다운 형식으로 글을 쓰면 됨~!<br><br>



## 에러 발생

❗ `tzinfo` 에러 발생

- Gemfile에 가서 다음 추가

```ruby
gem "jekyll", "~> 4.1.0"
# 여기 밑에 추가  
gem "tzinfo"
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw]
```

<br>

❗ github pages 빌드 실패하면서 `...welcome-to-jekyll.markdown.erb` 어쩌구 invalid post date 에러 발생

- _config.yml 파일에 가서 `- vendor` 추가

```ruby
exclude:
  - ... #어쩌구저쩌구
  - vendor #추가하기
```

<br><br>