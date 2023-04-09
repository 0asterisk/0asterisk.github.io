---
layout: post
title: 윈도우11 0xc190011f, 0x80888002, 0xC1900108 등 업데이트 도중 다양한 오류 고치기
subtitle: 
date: 2023-04-09 22:00:00 +0900
sitemap :
  changefreq : daily
  priority : 1.0
---

## 오류 상황

* Windows 업데이트에서 다운로드 오류: `0xc190011f`
* `C:\$WINDOWS.~BT\Sources\Panther`에서 `setupact.log` 로그파일 확인

```text
2022-11-23 23:07:32, Info MOUPG Finalize: Remapping install error [0x80888002] -> [0xC1900108] for telemetry.
```

* `0x80888002`, `0xC1900108`, 게 섯거라

* 다시 한 번 위 경로에서 `setuperr.log` 로그파일 확인

```text
2022-11-23 23:07:31, Error CONX Windows::Compat::Appraiser::Utilities::ExtractResourceToFile (676):   Could not LoadLibrary to resource: [2].[gle=0x80070002]
~~ <모두 0x80888002 에러인 것 같으므로 중략>
2022-11-23 23:07:31, Error MOUPG CSetupManager::ExecuteDownlevelMode(574): Result = 0x80888002
```

* `0x80888002` 네 이놈!!!!!!!!!!!!

## 해결 방법 모음  

* **공통**
  * VPN이 있다면 지우고 해볼 것. 잔재하는 VPN 드라이버도 모두 지워야 한다; 아래의 '오작동중인 드라이버 제거'로.
* **`0xc190011f`의 경우** (`0xc1900101`과 유사)
  * `devmgmt.msc`에서 오작동중인 드라이버 제거, 블루투스 등 주변 기기 제거
    * **드라이버 제거와 관련하여: Unsigned(서명되지 않은) 드라이버들을 제거해야 한다.** 제거 방법은 하단 내용 참고.[^2]
  * MacType 해제, `C:\$WINDOWS.~BT` 제거.[^1]
* **`0x80888002`의 경우**
  * [**이 명령어**](https://github.com/AveYo/MediaCreationTool.bat/blob/main/bypass11/Skip_TPM_Check_on_Dynamic_Update.cmd) 사용.

## **서명되지 않은 드라이버** 제거 방법[^2]  

가끔 `bcdedit /set nointegritychecks` 명령어를 통해 서명되지 않은 드라이버들을 강제로 설치해 본 경험이 있을 것이다. 그런데 Windows 업데이트에서 이를 감지하여 오류를 뿜을 수 있다. 그렇기 때문에 제거해주는 것이 좋다.  
  
**가끔 amdkmpfd.\* 파일들이 블루스크린 등으로 골치 아프게 한다. 물론 본인도 이것이 오류임을 찾았다. 본인은 이를 기준으로 설명하겠다.**  

`Win + R`키를 통해 Run(실행) 실행, 그리고 `sigverif.exe`를 실행하면 다음과 같은 창이 뜬다.  

![Run.exe](/assets/images/230409_1/Screenshot%202023-04-09%20230039.png)
![sigverif.exe](/assets/images/230409_1/Screenshot%202023-04-09%20230308.png)  

여기선 그냥 Start를 눌러주면 알아서 검색한다.  

![No violations on scanned drivers](/assets/images/230409_1/Screenshot%202023-04-09%20230424.png)  

그런 드라이버를 설치한 적이 없거나 문제가 없다면 이렇게 뜬다. (영어긴 한데 대충 전부 디지털 서명이 됐다는 의미)  

![AMD Drivers not digitally signed.](/assets/images/230409_1/0x0000007E-4.jpg)  

사진을 좀 빌리자면 위처럼 `amdkmpfd`라는 이름을 가진 여러 파일이 검색된다. 본인은 글을 쓰는 시점에 해결되었기 때문에 나오지 않았다.
이는 **AMD 그래픽카드 드라이버**의 문제기 떄문에 보통 **노트북 제조사가 제공하는 드라이버를 사용하지 않았을 때** 나타난다고 한다. 본인도 그랬다.  
  
이를 제거하려면 그냥 제어판에 가서 `AMD Software`를 제거하면 되며, 제조사에서 공식적으로 제공하는 그래픽카드 드라이버로 다시 설치하자! 다음 사진은 레노버 공식 지원 사이트이다.  

![Lenovo support pages where you can download drivers for your Lenovo products](/assets/images/230409_1/lenovo-site.png)  

---

## sources, footnotes

[^1] <https://answers.microsoft.com/zh-hans/insider/forum/all/windows-10-insider-preview/e7ae0ffd-6714-4d0b-9ab5-32dbc17ad55a>, 본인은 MacType를 이용중이었음.
