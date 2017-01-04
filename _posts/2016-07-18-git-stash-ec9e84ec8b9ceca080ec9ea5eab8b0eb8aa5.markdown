---
author: redreamer
comments: true
date: 2016-07-18T08:03:10.000Z
layout: post
title: Git stash 임시저장기능
categories:
  - git
tags:
  - 깃
  - git
  - github
  - 임시저장
  - stash
---

해결해야할 task마다 새로운 source를 받는 것만큼 server에 무리를 주는 일은 없다. branch를 사용하는 것이 가장 좋지만 더 간편한 기능이 있다.

**git stash**를 사용하는 방법이다.

이 명령어는 이럴 때 유용한다.

1. Working directory에 작업중인 코드 변경 사항에 영향을 주지 않고 다른 작업을 하고 싶을 때

1. 아직 commit으로 올리지 않은 변경 내역을 다른 branch로 옮기고 싶을 때

1. 미완성 된 code라 commit으로 올려 보관하기 껄끄러울 때

사용방법은 stack 구조와 비유하면 간단하다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1469157007146.png)](http://redreamer.files.wordpress.com/2016/07/wp-1469157007146.png)

코드 변경 내역을 넣을 때는

> $ git stash

뺄 때는

> $ git stash pop

무엇을 넣어두었는지 리스트를 확인할때는 아래 명령어를 압력한다.

> $ git stash list

stash를 수행하면 붉은 색으로 표기됐던 수정 내역이 사라져 clean하 working directory가 된다. 그 상태에서 branch를 바꾸고 git stash pop으로 저장해뒀던 변경 내역을 다시 불러와 적용하면 된다.

git stash list 를 수행하면

[![](http://redreamer.files.wordpress.com/2016/07/wp-1469157214091.png)](http://redreamer.files.wordpress.com/2016/07/wp-1469157214091.png)

이런 스택의 구조를 볼 수 있다. 변경 점을 눈으로 확인하고 싶다면 Edit

> $ git show stash@{0} ---> git show command를 이용

여기까지 알아도 충분히 활용가능하다. 너무 복잡해지면 차라리 patch형태로 파일저장하는 것이 편할 것이다.

더 적극적으로 활용하고 싶다면 아래를 보자.

여기서, 한걸음 더 나아간다면

1. 보통 pop을 이용하면 staging 된 상태도 모두 unstaging으로 변경되어 복원된다. 하지만 stage 상태(녹색)까지도 복원하고 싶다면 --index option을 붙여서 복원하면 된다. git stash시에는 따로 붙는 옵션이 없다.

1. git stash pop명령어는 적용하고 list에 있는 항목을 지운다. 하지만 git stash apply stash@{0} 처럼 apply를 사용하면 지우지 않고 복원만 시킨다. 언제든지 다시 꺼내 사용가능하다.

1. unstaging 된 상태(붉은색 폰트)에서 stash 한 항목들은 Editgit show stash@{0}로 보이지만 staging 된 상태로 저장된 파일들은 보이지 않았다. git stash show -p stash@{0} command를 사용하자. -p 옵션을 빼변 파일 이름 + 변경줄 정도로만 간단하게 표기되니 staging 된 파일이 없다면 git show가 편할 것이다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1469157507084.png)](http://redreamer.files.wordpress.com/2016/07/wp-1469157507084.png)[![](http://redreamer.files.wordpress.com/2016/07/wp-1469157480633.png)](http://redreamer.files.wordpress.com/2016/07/wp-1469157480633.png)
