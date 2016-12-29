---
author: redreamer
comments: true
date: 2016-07-07 07:47:56+00:00
layout: post
title: Git diff + vi를 한번에
categories:
- git
tags:
- 깃
- git
- gitdiff
- github
---

변경된 Code 내역을 보기 위해 우리는 보통

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878060437.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878060437.png)위 명령어를 사용한다. 그리고는 수정이 필요한 부분이 있다면 다시 vi로 파일경로를 입력하여 내역을 확인한다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878070408.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878070408.png)

수정 point가 바로 직전에 작업했던 파일이라면, 좀 더 편한 방법이 있다. vi 만 치고 빈파일을 연 후 Previous point로 돌아가는 Ctrl+O를 누루면 된다. (첫 화면에서는 2번 연타)

그리고 source insight를 사용하는 개발자는 간편히 File browsing을 하면 될 일이다.

하지만 source insight에서는 할 수 없는 기능이 있다. 간단히 수정사항을 diff view 형태로 보여주면서 편집도 가능한 기능이다. 이 기능은 아래 명령어로 가능하다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878077904.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878077904.png)

여러 파일이 수정되어 있다면 하나씩 수정전 원본 파일과 현 code를 diff 시키면서 보여준다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878083898.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878083898.png)
[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878090473.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878090473.png)

실제 열린창은 vimdiff이다. vimdiff는 수정이 없는 부분을 fold처리해주기 때문에 변경사항이 더 눈에 잘 띄도록 해준다.
다음은 관련 단축키다.


<blockquote>do - Get changes from other window into the current window.
dp - Put the changes from current window into the other window.
]c - Jump to the next change.
[c - Jump to the previous change.
diffupdate - change update

zo -> open fold.
zc -> close fold.
zr -> reducing folding level.
zm -> one more folding level, please.
zR -> Reduce completely the folding, I said!.
zM -> fold Most!.</blockquote>




임시파일 Edit[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878102117.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878102117.png)와 현재 파일 Edit[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878110754.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878110754.png)간의 비교이 때문에 왼쪽 파일을 수정해봤자 소용없다.
오른쪽 수정사항을 확인하면서 편집을 하면 되는데 작업 후 저장할 때 w!로 느낌표를 붙여서 read only 상태를 무시하고 저장해야 한다. (수정 전에 e!를 눌러도 RO가 풀림.)
또 두개의 창이 열리므로 :qa로 한꺼번에 닫아주는 것이 편하다.

파일을 많이 수정했다면 확인이 필요없는 file을 N으로 skip해주는 것도 일이 되는 데 아래 명령어처럼 path와 file 명을 명시해주면 바로 접근가능하다. -y옵션은 묻지 않고 바로 edit창을 열게 해준다.

[![](http://redreamer.files.wordpress.com/2016/07/wp-1467878123219.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878123219.png)
마지막으로, 좀 더 확장 응용하지면, Edit [![](http://redreamer.files.wordpress.com/2016/07/wp-1467878132206.png)](http://redreamer.files.wordpress.com/2016/07/wp-1467878132206.png)
처럼 commit 끼리 파일단위로 달라진 부분을 볼 수 있다. 물론 수정도 가능하다.
