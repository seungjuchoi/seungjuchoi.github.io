---
author: redreamer
comments: true
date: 2016-07-04 23:50:33+00:00
layout: post
title: 타임머신 Git Reflog
categories:
- git
tags:
- 깃
- 깃허브
- git
- github
---

한번이라도 git commit명령어로 commit을 만들었다면 git은 그것을 복구할 수 있다. Branch, Tag 에 상관이 없다. 한번이라도 HEAD로 올라온 commit을 git을 모두 list에 저장해두기 때문이다.

이 Git Reflog 명령어는 이런 용도로 사용 가능하다.



	
  1. 복구하여 해당 commit 으로 분기하고 싶다면 두 단계를 거치면 된다.`$ git reflog`
Commit 확인 후 돌아가고 싶은 ID를 복사한다.
`$ git reset --hard 5ac925c
`해당 commit으로 분기한다.
Commit ID인 Hash값은 부모 Commit ID를 input으로 받아들여 만들어진 값이다. 따라서 HEAD의 부모가 누구인지는 정해져 있다. 재귀적으로 부모의 부모도 결정되어 있다.쉽게 말해, 저 commit으로 reset 되는 것은 저 **commit이 생성된 직후로** 타임머신을 탔다는 이야기다. 후회할 일을 했다면 reflog로 확인하고 다시 손쉽게 돌아간다.

	
  2. No Branch에서 올린 Commit을 Branch를 넘나들며 Cherry-Pick할 수 있다. Commit ID는 Branch에 의존성이 없다.![upload_4_7_2016_at_09_24_47.png](https://redreamer.files.wordpress.com/2016/07/upload_4_7_2016_at_09_24_47.png)repo start를 하면 마지막으로 server와 fetch된 commit으로 branch가 생성된다. no branch에서 작업한 것은 사라진다. no branch 상황에 올린 commit 도 reflog에 저장되어 있으니 놀랄 필요가 없다.`$ git reflog`
ID를 확인하고,
`$ git reset --hard 5ac925c
`commit을 하나 가져오면 된다. 두개라면 차례대로 두번 cherry-pick한다.

	
  3. 해당 git에서 지금까지 무슨 일이 벌어졌는지 개괄적인 History를 알 수 있다. amend를 사용한 경우도 괄호로 표기된다.![upload_4_7_2016_at_09_24_58.png](https://redreamer.files.wordpress.com/2016/07/upload_4_7_2016_at_09_24_58.png)


