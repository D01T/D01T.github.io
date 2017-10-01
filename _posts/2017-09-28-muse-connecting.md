---
title: "Muse Headband 연동"
author: Scripter36
date: 2017-09-28 20:55
category: Report
tags: ["Programming", "UWP", "C++", "Javascript", "Muse"]
---

뇌파와 기타 여러가지를 측정할 수 있는 [Muse Headband](http://www.choosemuse.com/)를 UWP(Universal Windows Platform)을 통해 연결하고, 브라우저로 넘겨 웹에서 사용할 수 있도록 하는 과정을 소개합니다.

## 소개하기 전에...

아래에서 소개하는 UWP 외에도 다른 방법들로 연결이 가능한데, 굳이 UWP를 선택한 이유는

* [Web Bluetooth](https://developer.mozilla.org/en-US/docs/Web/API/Web_Bluetooth_API)를 사용한다면 웹에만 접속하면 되니 편하겠지만, 비표준인데다 지원하지 않는 기기가 많습니다.

* [MuseIO](http://developer.choosemuse.com/research-tools/museio)는 Muse를 만든 회사에서 제공하는 리서치 툴로 Mac, Windows, Linux를 모두 지원하는 좋은 툴인데, 정작 2016년형 Muse 연결은 지원하지 않습니다.

등이 있습니다.

또한, 운영체제는 Windows 10 이어야 하며, [Visual Studio](https://www.visualstudio.com/ko/)가 필요합니다. 설치 시(또는 추가로 설치) UWP 관련 툴도 받아 주세요.

## LibMuse

[LibMuse](http://developer.choosemuse.com/)는 Muse를 만든 회사에서 지원하는 SDK로, 2016년형 Muse 연결을 지원하나 Windows 10, Android, IOS밖에 지원하지 않습니다. 우리는 이 SDK를 이용해서 데이터를 받아 볼 겁니다.

윈도우 문양 아래에 [Download](http://developer.choosemuse.com/developer-sdk-windows/) > [DOWNLOAD 6.0.1](https://storage.googleapis.com/ix_downloads/libmuse-6.0.1-api8/libmuse-windows-6.0.1-windows-installer.exe)을 클릭하여 인스톨러를 다운로드 받고, 실행하여 적당한 위치에 파일을 추출해 주세요.

`(추출한 폴더)\libmuse_6.0.0\windows\examples` 경로에 가 보면 `LibMuseExamples.sln` 이라는 비주얼 스튜디오 솔루션 파일이 있을 겁니다. 예제 파일이죠. 파일을 열어서 `GettingData`를 한 번 실행해 봅시다.

![GettingData](https://imgur.com/download/mAZaRBS)

위와 같이 창을 띄운 뒤 Muse를 켜고, Refresh 버튼을 눌러 Muse를 찾은 뒤 Connect를 눌러 연결해 줍시다.

위 창에서는 Accelerometer, 즉 가속도를 인식하도록 해 봤습니다.

## Artifacts

우리가 이 Muse로 무슨 생각을 했는지, 아니면 집중했는지라도 알 수 있다면 좋겠지만, 아쉽게도 무슨 생각을 했는지는 알 수 없고, 집중했는지 알려면 꽤 복잡한 시행착오를 거쳐야 할 것입니다.

그러면 우리가 바로 얻을 수 있는 데이터는 없을까요?

다행히도, Muse 기기에서 얼굴의 움직임을 파악해 눈 깜박임과 턱 움직임을 얻어올 수 있습니다. 패킷 타입 중 Artifacts에서 이것들을 받아 오죠.

그러면, 예제를 다음을 포함하여 수정해 봅시다.

* 웹 브라우저 넣기: Microsoft Edge가 들어가므로 큰 성능 차이는 안 날 겁니다.
* 받아온 데이터로 UI를 변경하는 대신 자바스크립트를 실행하여 웹에 정보 넘겨주기

![MuseClient](https://imgur.com/download/ad2VDoX)

[Vokkit](https://github.com/Vokkit/Vokkit)에 넣어 본 결과물입니다. 턱이 움직였을 때 채팅으로 알리고 앞으로 가도록 해 봤습니다.

소스 전체를 Github에 올리고 싶었으나 파일이 너무 커서 주요 소스만 압축해서 올려 놨습니다. (코드가 더러운데다, 복붙하면 오류날 가능성이 높으니 참고만 해 주세요) [Dropbox](https://www.dropbox.com/s/lk550u56jtj2qfc/GettingData.zip?dl=0)