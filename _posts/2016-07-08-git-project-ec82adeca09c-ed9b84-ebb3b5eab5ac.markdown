---
author: redreamer
comments: true
date: 2016-07-08 05:39:51+00:00
layout: post
link: http://seungjuchoi.com/2016/07/08/git-project-%ec%82%ad%ec%a0%9c-%ed%9b%84-%eb%b3%b5%ea%b5%ac/
slug: git-project-%ec%82%ad%ec%a0%9c-%ed%9b%84-%eb%b3%b5%ea%b5%ac
title: Git Project 삭제 후 복구
wordpress_id: 1078
categories:
- Git 강의
tags:
- 깃
- git
- github
---

간혹, 특정 git folder 전체가 삭제되는 경우가 있다. 이런 경우에는 전체 repo sync를 할 필요없이 특정 folder만 sync하면 복구된다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467956777217.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467956777217.png)
삭제된 폴더를 다시 임의로 만들고 그 안으로 경로변경을 한 뒤 repo sync . 을 하면 된다. 현재 경로에 대한 sync작업을 진행하겠다는 의미다.

물론 아래처럼 mkdir작업없이 android 폴더에서 바로 삭제된 폴더명을 써줘도 된다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467956783062.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467956783062.png)
폴더명만 되겠는가? git project 명을 바로 적어줘도 좋다. (git project는 manifest.xml파일에서 확인가능하다.)

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467956788921.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467956788921.png)
이렇게 되면 git fetch 후 git merge 작업을 하게 된다.


## 소스폴더 삭제 후 sync받으면 어떻게 되나


HEAD가 remote server 상태의 HEAD와 일치되도록 맞춰진 상태로 생성된다. 그래서 local commit 작업분이 사라졌다고 생각하고 쉽다. 그러나 1강에서 배운 git reflog를 실행해보면 올렸던 commit들이 쭉 list up 되며 commitID로 access 또한 가능하다. 뿐만 아니라 branch도 그대로 남아 있다. 다만 HEAD를 맞추면서 branch는 no branch 상태가 된다.


## 원리


.git는 심볼릭 링크로 이뤄진 "바로가기"파일로 이뤄져 있다. 이 때문에 git안에서 이뤄지는 모든 수정사항은 git의 대모격인 .repo에 모아 저장된다. 따라서 repo 는 개발자가 어떤  프로젝트를 sync 하고 싶은 것인지 단서만 제공해준다면 기꺼이 sync 작업을 진행하는 것이다. 그래서 .git 폴더가 삭제되도 한번 올린 commit은 복구가 가능하다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467956796420.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467956796420.png)


## 완전 삭제


repo sync 작업은 .repo에 있는 소스파일을 정돈(fetch)하여 복사하는 과정이다. 실제로 완벽하게 특정 git project의 history를 지우고 싶다면 .repo안에 있는 .git 폴더를 지우고 sync하면 된다. kernel의 경우 .repo/projects/android/kernel.git 이 실제 본체가 된다. 아래 sync 작업은 서버에서 kenrel 파일 전체를 가져오는 것때문에 상대적으로 시간이 오래 걸린다. 하지만 이 작업은 평상시에는 필요하지 않다. 정말 특정 폴더만 심각한 오류가 있을 때만 사용하자. 보통 git reset --hard도 commit을 돌리면 작업하기 좋게 책상정리가 됐다고 보면 된다. 이런 삭제 작업은 책상을 버리고 새로운 책상을 사는 격이다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467956804653.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467956804653.png)


## 이럴 때 좋다.





	
  1. 특정 Git folder가 삭제 되었을 때 전체 sync 없이 부분 folder만 내려 받는다.

	
  2. merge작업이 잘못되어 commit 구조가 알아보기 힘들게 꼬였거나 버그로 repo upload가 되지 않을 때


특정 git때문에 전체 소스를 받아야 하는 우를 범하지 않길 바란다. 지우고 그것만 다시 받자.

다음 시간에는 repo의 manifest.xml파일과 git config파일에 대해서 알아보겠다.
