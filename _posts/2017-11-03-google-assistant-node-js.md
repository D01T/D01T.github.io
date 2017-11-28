---
title: "Node.js에서 Google Assistant SDK 사용해 보기"
author: Scripter36
date: 2017-11-03 09:27
category: Report
tags: ["Programming", "Node.js", "Javascript", "Google Assistant"]
---

인공지능 비서 중 하나인 [Google Assistant](https://assistant.google.com/)를 [SDK](https://developers.google.com/assistant/sdk/overview)를 이용하여 다뤄 봅시다.

## 설치

SDK는 2가지로 나뉩니다.

* Google Assistant library for Python

Python - Linux에서 작동하며, Ok Google을 이용한 작동이 가능하고 여러 기능들이 Built-in 되어 있는 라이브러리입니다.

다만 파이썬 - 리눅스에서만 작동되므로 기각.

* Google Assistant gRPC API

gRPC를 지원하는 모든 언어에서 작동하나, Ok Google을 이용한 작동은 불가능하고 여러 기능들은 Reference code가 제공될 뿐입니다. 알람과 타이머도 작동하지 않으며,

Python Library는 어떨지 모르겠지만 영어만 지원하는 듯 하며, 오디오로만 통신이 가능하며 텍스트 입력 출력은 지원하지 않습니다.

어쨌든 Node.js는 gRPC를 지원하므로 사용이 가능하며, 이미 npm 모듈로 나와 있습니다!

[Google-Assistant](https://github.com/endoplasmic/google-assistant)

`$ npm install google-assistant` 하시면 됩니다...만

gRPC 버전이 낮아 최신 node에서 미리 컴파일된 버전이 없어서 컴파일하다 오류를 내뿜으므로

github에서 clone해 주시고 package.json에서 gRPC 버전을 적당히 올려주시면 (제 경우에는
node v8.8.1에서 gRPC 버전을 1.3.8로 올리니 되더군요) 사용이 가능할 겁니다.

## 구글 개발자 프로젝트 계정 설정
[여기](http://blog.naver.com/PostView.nhn?blogId=chandong83&logNo=221081942490&parentCategoryNo=&categoryNo=65&viewDate=&isShowPopularPosts=false&from=postView)를 참고하셔서 `client-secret.json`을 만들어 다운로드 해 주세요.

3번 문단부터 보면 될 겁니다.

## 실행

모두 끝났습니다! examples 폴더에서 config.auth.keyFilePath를 client-secret.json의 경로로 설정해 주시고 실행하면 Google Assistant와 대화할 수 있습니다.

## 여담

사실 카카오봇에 집어 넣어 보려고 했는데, 텍스트 인풋 아웃풋을 지원하지 않아서 실패하고 말았습니다.

게다가 언어는 영어 고정이라 더 슬펐던..

[IFTTT](https://developers.google.com/assistant/sdk/develop/device-control/ifttt)도 사용이 가능하다고 합니다. 참고해 보세요