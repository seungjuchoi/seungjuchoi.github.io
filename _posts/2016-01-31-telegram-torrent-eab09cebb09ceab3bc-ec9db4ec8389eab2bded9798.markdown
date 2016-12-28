---
author: redreamer
comments: true
date: 2016-01-31 01:48:09+00:00
layout: post
title: Telegram-Torrent 개발과 이색경험
categories:
- programming
tags:
- Clien
- deluge
- 링크
- 방문자수
- java
- python
- Telegram
- transmission
---

프로그래머로서 재미있는 경험을 해서 소개한다.

이번 달 초에 구현하여 과정을 글로 풀어 놓았던  [Telebot을 이용한 원격 토렌트 다운로드 시스템](http://seungjuchoi.com/2016/01/03/telebot%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9B%90%EA%B2%A9-%ED%86%A0%EB%A0%8C%ED%8A%B8-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C/) 에 대해서 재미가 떨어질 때즈음 우연히 [Clien](http://www.clien.net/)에서 나와 비슷한 시스템을 만들어 올린 글을 봤다. 그렇다면 나도 한번 올려볼까 해서 그날 저녁 바로 블로그를 참고하여 작성했다. 사실 그 비슷한 시스템을 보고 내 시스템도 올려도 되겠다는 용기를 얻은 것이었다. 묻어가기도 좋았다.

[![20160131_100520](https://redreamer.files.wordpress.com/2016/01/20160131_100520.png)](http://www.clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=303706&sca=&sfl=wr_subject&stx=%ED%85%94%EB%A0%88%EA%B7%B8%EB%9E%A8)

[링크](http://www.clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=303706&sca=&sfl=wr_subject&stx=%ED%85%94%EB%A0%88%EA%B7%B8%EB%9E%A8)

그런데 왠일인가, 그날 하루만에 2,000 명이, 며칠 지나니 8,000명 9,000명이 내 글을 보기위해 클릭했다. 나는 이 사실에 적잖히 놀랐다. 두가지가 떠올랐는데 [Clien](http://clien.net)이 내가 생각했었던 것보다 훨씬 큰 Community였다는 것과 텔레그램와 토렌트를 잇는 시스템에 관심이 있거나 혹은 궁금했던 사람들이 의외로 많았다는 점이다.

[caption id="attachment_746" align="alignnone" width="506"]![20160131_101241.png](https://redreamer.files.wordpress.com/2016/01/20160131_101241.png) 좋은 반응만 추려낸 댓글[/caption]

반응도 내 예상을 훌쩍 뛰어넘었다. 고백컨데 이런 긍정적인 반응이 어색할정도로 처음이다.

![20160131_102956.png](https://redreamer.files.wordpress.com/2016/01/20160131_102956.png)

몇몇분들은 너무 어려워서 잘 모르겠다는 반응을 보이셨는데 비 전공자도 손쉽게 따라할 수 있는 구조를 만들어야겠다는 다짐을 하게 만들었다. 그러던 중에 이 시스템을 따라하는 글도 하나 생겨났다.

[caption id="attachment_759" align="alignnone" width="819"][![20160131_103212.png](https://redreamer.files.wordpress.com/2016/01/20160131_103212.png)](http://clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=305720&page=2) 칼날주먹님이 Java Version도 만들어 올리셨다.[/caption]

[링크](http://clien.net/cs2/bbs/board.php?bo_table=lecture&wr_id=305720&page=2)

이 글보면서 굉장히 뿌듯했고 고마웠다. 그리고 이런 시스템에 관심있는 것은 사용자뿐만 아니라 개발자도 있겠구나 싶었다. 이 시스템을 좀 더 발전 시킬 수 있는 방법을 모색하면서 컨셉 장표를 만들고 있었는데 이런 내가 올린 [Source Code](https://github.com/seungjuchoi/telegram-control-deluge)에 Request Pull이 달렸다. 내가 사용한 Torrent Client는 Deluge였는데 Transmission도 기능을 추가하고 싶다는 내용이었다.

[caption id="attachment_773" align="alignnone" width="779"]![20160131_103756](https://redreamer.files.wordpress.com/2016/01/20160131_103756.png) Transmission 기능도 추가하고 싶었던 나그네 개발자의 Commit[/caption]



내가 고민하는 사이에도 이미 잘 갖춰진 인프라에서 긍정적인 움직임이 포착되고 있는 것이다.  이날 바로 내가 추가하고 싶은 기능들을 issue로 발행했다. 관심있는 개발자들도 모아 컨셉을 더 구체화하고 이 시스템을 torrent 뿐만 아니라 다른 영역으로도 확장하는 시도를 할 생각이다. 이런 반응이 하나의 커뮤니티에 글을 올린 것으로부터 연쇄반응됐다는 것이 새삼 놀랍다.






