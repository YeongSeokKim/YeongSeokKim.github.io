---
title: "설치 없이 Jekyll 블로그 만들기"
layout: single
excerpt: "설치가 귀찮은 사람들을 위한 Jekyll 설치 기록"
sitemap: false
permalink: /
---

고민 끝에 Jekyll 블로그를 만들기로 결정했으나 이를 제대로 사용하기 위해서는 Ruby, Python, Jekyll 등을 설치하고 빌드해야 한다.

사실 원칙적으로는 그렇게 사용하는게 맞겠지만 귀찮아서 설치 없이 블로깅을 바로 시작하는 방법을 찾아보았다.

### 가장 처음에 해야 하는 일
1. https://github.com/mmistakes/minimal-mistakes 저장소에 접속하여 해당 저장소를 내 github으로 fork한다.
2. Fork한 뒤 저장소의 이름을 [내_계정명].github.io로 바꿔서 Github Pages를 통해 접속할 수 있도록 변경한다.
3. _config.yml 파일의 제목, 설명, 프로필 등등을 수정한다.
4. http://[내_계정명].github.io 로 접속하여 제대로 나오는지 확인

### 첫 포스팅 올리기
1. 폴더 내부에 [2016-07-20-writing-jekyll-posts.md]와 같은 형식으로 마크다운 파일을 생성한다.
