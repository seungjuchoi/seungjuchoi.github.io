---
author: redreamer
comments: true
date: 2016-07-04 00:12:01+00:00
layout: post
title: 시간을 아껴주는 Git 강의 - 시작
wordpress_id: 1019
categories:
- git
tags:
- 깃
- git
- github
---

이 Git 연재를 통해 풀어내고 싶은 숙제는 이것이다.


<blockquote>“어떻게 하면 source 전체를 다시 다운로드 받는 경우를 줄일 수 있을까?”</blockquote>


소스를 새로 받지 않아도 될 상황에 새로 소스를 받게 되다면 우리는 서버 자원을 낭비하고 할일을 못하게 된다. 심지어는 코딩의 맥이 끊키고 네이버뉴스를 어슬렁거릴지도 모른다.

그런데 슬프게도 git을 잘 이해할 기회가 없었던 프로그래머가 Code 꼬임으로 다다르는 종착역은 거의 '다시 받자ㅠ'인 경우가 많다.




MKDIR ---->   Repo Init & Sync ----> Issue! -----> RE-MKDIR ---->  [REPEAT]




또 그것이 짧은 keyward 하나만 알고 있어도 해결될 일이라는 걸 알게 되면 참 안타깝다. 그래서 Source를 다시 받지 않아도 꼬인 문제를 풀 수 있는 간단한 방법에 대해 풀어나가고자 한다.

만약 Git를 처음 접하거나 심도있는 이해를 원한다면 [Pro Git (번역본)](http://dogfeet.github.io/progit/progit.ko.pdf)을 먼저 읽어보아야 한다. 다른 문서들이 비해 알기 쉽게 설명되어 있고 상대적으로 실전에서 많이 사용하는 내용들을 담고 있기 때문이다.

가장 중요한 Keyword 순으로 시작한다.
