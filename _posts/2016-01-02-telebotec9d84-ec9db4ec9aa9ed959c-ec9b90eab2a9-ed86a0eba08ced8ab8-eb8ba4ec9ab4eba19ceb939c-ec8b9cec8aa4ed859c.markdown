---
author: redreamer
comments: true
date: 2016-01-02 23:44:28+00:00
layout: post
title: Telebot을 이용한 원격 토렌트 다운로드 시스템
categories:
- programming
tags:
- 라즈베리파이
- 텔레봇
- 텔레그램
- Raspberry Pi
- Telebot
- Telegram
- Torrent
- Torrent Download
---

## 




## 취지


가족을 위해 원격 Torrent 다운로드 시스템을 만들기로 했다. 일반적으로 토렌트를 다운 받으려면 다음과 같은 일련의 과정이 필요하다.



	
  1. Torrent App을 다운 받고 실행한다. 필요하면 사용법을 익힌다.

	
  2. Torrent Site에 들어가 원하는 컨텐츠를 다운 받아 App으로 연다. Magnet주소이거나 Torrent File이거나 둘중에 하나다.

	
  3. Torrent App을 사용하여 다운로드한다.

	
  4. 컨텐츠를 원하는 곳에 복사한다. Google TV나 Phone.

	
  5. Player로 열기 위해 컨텐츠의 위치를 찾아가 Play 한다.


복잡하다. 그래서 이런 과정없이 간편히 **Chat**으로 Download 가능하도록 만들고자 했다.

그러기 위해 필요한 것은 아래 정도다.



	
  1. Telegram: 메신저 앱

	
  2. Raspberry pi2: 핵심적인 수행을 담당할 중앙 서버

	
  3. (Optional) Google TV: 컨텐츠를 플레이할 Android 기반 TV




## 설계도 (Block Diagram)


![Telebot_Schemetics](https://redreamer.files.wordpress.com/2015/12/telebot_schemetics.png)


### Telegram


일단 원론적인 이야기부터 해보자. 2015년 6월 부터 [Telegram](https://telegram.org/)은 **[Bot API System](https://core.telegram.org/bots/api)**을 도입했다. 간단히 설명하자면, 개발자가 만든 임의의Server와 통신하면서 Text, Image, Location 등을 주고 받을 수 있도록 해준다. 제공해주는 예제로는 Bot이 Text를 받고 적절한 그림을 보내준다거나 채팅 내용을 저장하는 정도가 있었다. Bot은 일반 User처럼 ID가 있고 누구나 그 ID와 대화를 시작하면 서비스를 이용할 수 있다. (물론 특정사용자만 이용토록 할 수도 있다.)

![ad3f74094485fb97bd](https://redreamer.files.wordpress.com/2015/12/ad3f74094485fb97bd.jpg)

더 재미있는 것은 이 Bot들을 위한 Open Market도 하나의 Bot으로 존재한다는 것이다.

![Screenshot_20151220-163927](https://redreamer.files.wordpress.com/2015/12/screenshot_20151220-163927.png?w=576)

Telegram을 선택한 이유는 대부분의 Platform지원하고 개발이 쉽기 때문이다. 그리고 Bot API System이 이 프로젝트에 딱 적합해보였다. 실제로 Keyboard자리를 대체하는 GUI Button의 조합이 아주 유용했다.


### Raspberry Pi 2


[Raspberry Pi2](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/)는 Single Board Computer다. 손바다 보다 작은 크기지만 Linux가 돌아간다.

[caption id="attachment_548" align="alignnone" width="348"]![raspberry-pi.png](https://redreamer.files.wordpress.com/2015/12/raspberry-pi.png) Rasberry pi2의 이전 제품인 Pi, 크기는 2와 같다.[/caption]

그래서 이 프로젝트에서 서버 역할을 하기에 충분하다. 또 핸드폰 충전정도의 작은 전력만 소모하기 때문에 하루 종일 켜놓아도 부담없다.

이 작은 Board에서  명령어 처리뿐만 아니라 Torrent도 다운 받는다. 받아진 데이터는 꼳혀진 Micro SD Card에 저장된다. 그리고 FTP로 열어두면 어디서나 어느 장치에서도 접근 가능하다. 예를 들어 지하철에서 LTE폰으로 접근할 수 있다.


### Google TV & PC


Google TV는 가정 내 공유기와 연결되어 있다. Raspberry pi2는 이야기했듯이 FTP Server로 열어두고 Google TV와 유선 연결된다. 물론 같은 Network상에 PC도 FTP를 통해 Raspberry pi2 Server에 접근할 수 있다.

![20151220_170638.png](https://redreamer.files.wordpress.com/2015/12/20151220_170638.png)




## 코드 설명


참고하실 분들을 위해 Github에 공유한다.
[https://github.com/seungjuchoi/telegram-control-deluge](https://github.com/seungjuchoi/telegram-control-deluge)
(Version Update 진행중: 댓글 참고)

python으로 작성됐고 크게 3가지로 나눌 수 있다.

![Blank Flowchart - New Page](https://redreamer.files.wordpress.com/2016/01/blank-flowchart-new-page2.png)



	
  1. **Chat**
Telebot에서 제공해주는 API를 사용하면 된다. [공식 사이트](https://core.telegram.org/bots)에 [예제](https://core.telegram.org/bots/samples)까지 아주 간단히 나와 있다. 이중에 실제로 사용한 Library는 python으로 만든 Telepot이다.**
**
Telepot: Python framework for Telegram Bot API.
[https://github.com/nickoala/telepot](https://github.com/nickoala/telepot)bot의 b를 위아래로 뒤집으면 p라는 점이 새삼 재밌어 보여서 선택했는데 꽤 편리한 Python API를 제공했다.Example을 보면 아래 단 세줄이 Telegram과 내 서버를 이어 주는 코드다.
![제목 없음](https://redreamer.files.wordpress.com/2016/01/eca09cebaaa9-ec9786ec9d8c.png)
MessageCounter는 실행할 Class자리리고 TOKEN은 Telegram에서 부여받은 BOT Key다.

	
  2. **Torrent Search**
Torrent Search Site에 따라 알맞은 툴을 써야 한다. 처음에는 python web 분석 툴로 유명한 [Beautiful Soup](http://www.crummy.com/software/BeautifulSoup/)를 사용하려 했으나 막히는 부분이 있었다. 고민 끝에 Target이었던 Torrent site에서 검색 결과를 RSS로도 제공해준다는 것을 보고 그쪽으로 선회했다.Feedparser는 RSS를 Parsing하는 Tool로 자세한 방법은 [여기](http://pythonhosted.org/feedparser/)를 참고하면 된다.
Parsing은 아래 한줄이면 된다.
~~~~
self.navi = feedparser.parse(대상 웹사이트)
~~~~

	
  3. **Torrent Torrent Download**
리눅스 기반에 설치가능한 토렌트 시스템에는 여러 가지가 있다. 그중에 [Transmission](http://www.transmissionbt.com/)은 사용해봤기 때문에 [Deluge](http://www.deluge-torrent.org/)를 사용해봤다. 비슷하지만 좀 더  Web과 App에서 상대적으로 유려한 UI를 제공해준다.
Deluge-console을 apt에서 설치하면 Linux Shell에서 핵심적인 command를 수행할 수 있다.
~~~~
$ deluge-console add <magnet>      - torrent 추가
$ deluge-console info                          - 현재 상태정보
$ deluge-console del <id>                  - torrent 삭제
~~~~





## Screen Shot


[caption id="attachment_681" align="alignnone" width="1080"]![Screenshot_20160103-082238](https://redreamer.files.wordpress.com/2016/01/screenshot_20160103-082238.png) 검색 요청[/caption]

[caption id="attachment_692" align="alignnone" width="1080"]![Screenshot_20160103-084112](https://redreamer.files.wordpress.com/2016/01/screenshot_20160103-084112.png) 토렌트 검색[/caption]

[caption id="attachment_694" align="alignnone" width="1080"]![Screenshot_20160103-084121](https://redreamer.files.wordpress.com/2016/01/screenshot_20160103-084121.png) 검색 후 리스트업[/caption]

[caption id="attachment_693" align="alignnone" width="1080"]![Screenshot_20160103-084125](https://redreamer.files.wordpress.com/2016/01/screenshot_20160103-084125.png) 선택[/caption]




