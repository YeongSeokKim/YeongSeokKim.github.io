---
title: "설치 없이 Jekyll 블로그 만들기"
layout: single
excerpt: "설치가 귀찮은 사람들을 위한 Jekyll 설치 기록"
sitemap: false
permalink: /Easy_Jekyll_Blog.html
---

고민 끝에 Jekyll 블로그를 만들기로 결정했으나 이를 제대로 사용하기 위해서는 Ruby, Python, Jekyll 등을 설치하고 빌드해야 한다.

사실 원칙적으로는 그렇게 사용하는게 맞겠지만 귀찮아서 설치 없이 블로깅을 바로 시작하는 방법을 찾아보았다.

#### 가장 처음에 해야 하는 일
1. [원하는 저장소](https://github.com/mmistakes/minimal-mistakes)에 접속하여 해당 저장소를 내 github으로 fork한다.
![Fork](https://mmistakes.github.io/minimal-mistakes/images/mm-theme-fork-repo.png)
2. Fork한 뒤 저장소의 이름을 [내_계정명].github.io로 바꿔서 Github Pages를 통해 접속할 수 있도록 변경한다.
3. \_config.yml 파일의 제목, 설명, 프로필 등등을 수정한다.
4. "https://[내_계정명].github.io" 로 접속하여 제대로 나오는지 확인

#### 첫 포스팅 올리기
1. \_posts 폴더 내부에 [2016-07-20-writing-jekyll-posts.md]와 같은 형식으로 마크다운 파일을 생성한다.
2. http://[내_계정명].github.io 로 접속하여 제대로 나오는지 확인

#### 그래도 설치하면 좋은 것들
1. [Github Desktop](https://desktop.github.com/): Github 저장소에 이미지, 비디오, 포스팅 파일 등을 업로드할 때 편하다.
2. [Atom](https://atom.io): Sublime text와 더불어 쓸만한 프리웨어 Text Editor. Markdown preview 기능이 있어 포스팅을 쓸 때 실시간으로 확인이 가능하다!


#### 참고 URL
1. https://github.com/mmistakes/minimal-mistakes 내가 fork한 Jekyll blog 저장소
2. https://mmistakes.github.io/minimal-mistakes/ 해당 저장소의 guide page
