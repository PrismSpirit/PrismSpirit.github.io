---
title: "앱 구동 중 권한이 변경되는 경우에 대한 대응 방법"
toc: true
toc_sticky: true
categories:
  - iOS
  - Swift
---
# 앱 구동 중 Privacy Settings가 변경되는 경우에 대한 처리?

## 문제 상황

BluetoothLE 디바이스와 통신이 필요한 프로젝트를 진행하는 중, 사용자가 앱 사용 중에 설정으로 들어가서 Privacy Setting을 변경할 경우 어떻게 처리해야할까? 라는 의문점이 생겼다.

이 상황을 재현하기 위해 앱 실행 중 설정으로 진입해 블루투스 권한을 허용 안함으로 변경했으나 아래와 같은 로그와 함께 계속해서 앱이 종료되었다.

![img](/assets/images/TerminatedWithSignal9.png)

구현 상의 문제가 있는 것으로 생각하고 구글링을 하던 중, 나와 같은 곤란한 상황을 겪고있는 글을 발견했다.

[App killed when privacy settings changed](https://stackoverflow.com/questions/43179334/app-killed-when-privacy-settings-changed)

앱 사용 중 설정으로 진입하면 앱의 State가 suspended로 전환되고 Privacy Settings를 변경하면 앱이 종료되는 것이 정상적인 동작임을 확인했다. 다만, 종료 전에 현재 state나 저장해야 할 data가 있을 경우 AppDelegate 또는 SceneDelegate의 didEnterBackground 메소드에서 처리해 줘야한다.



## 참고 자료

https://stackoverflow.com/questions/43179334/app-killed-when-privacy-settings-changed

https://stackoverflow.com/questions/15930708/having-app-restart-itself-when-it-detects-change-to-privacy-settings/15930922#15930922
