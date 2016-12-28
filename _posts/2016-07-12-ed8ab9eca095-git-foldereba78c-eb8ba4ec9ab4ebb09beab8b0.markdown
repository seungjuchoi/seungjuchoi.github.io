---
author: redreamer
comments: true
date: 2016-07-12 07:31:50+00:00
layout: post
title: 특정 git folder만 다운받기
categories:
- git
tags:
- download
- git
- repo
---

repo sync <project명> 을 사용하면 편리한 경우가 한가지 더 있다. 특정 Git folder만 다운로드 받을 때이다.

보통 이경우 git clone 명령어를 사용하기 마련인데 특정 git project의 name이 확실하지 않아 repo init 후 mainfest.xml 을 참고해야하거나 git web을 뒤져야 한다.


<blockquote>$ git clone <Repositary Address> -b <Branch name></blockquote>


자주 받는 git folder는 짐작이 가능하겠지만 한번도 받아보지 않은 git project는 정확한 ssh 주소를 알아 내기위해 manifest.xml을 참고한다.

이 파일은 repo init 과정에서 .repo 안에 생성된다. 정상적으로 init되었다면.repo가 생성되는 것을 볼 수 있다.


<blockquote>$ vi .repo/mainfest.xml</blockquote>


위 명령어로 파일을 열면 git project의 path와 name이 각 git 마다 기재되어 있는 것을 확인할 수 있다.

아래와 같은 형태로 Project tag를 볼 수 있다.


<blockquote><project name="<Project-name>" path="<Path-name>"></blockquote>




여기에서 Name 속성과 Path 속성 둘다 아래 처럼 사용가능하다.


<blockquote>$ repo sync <Project-name> -cj4
$ repo sync <Path-name> -cj4</blockquote>




이 방법은 clone보다 간편하고 직관적이다.


