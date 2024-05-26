---
layout: post
title: VSCode에서 GCC 이용하기
subtitle: 진짜 간단함 ㄹㅇ
date: 2024-05-26 00:00:00 +0900
sitemap :
  changefreq : daily
  priority : 1.0
---

## 전제

* **이 글을 먼저 읽고 시도 바란다.**
* 일단 [VS Code](https://code.visualstudio.com/download)가 필요하지 않겠는가?  
* 그리고 Extension(확장/플러그인) 중 [C/C++ extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)이 필요하다. 설치 해주자.  
* 곧 설치 할 64비트 Windows 8.1 이상을 요구한다. 글쓴이 피셜 8.1 이하는 없으리라고 본다. 
* F**k it, We ball.

## MinGW-w64 Toolchain 설치

[MSYS2](https://www.msys2.org/)를 통한 MinGW-w64를 설치하도록 하자.

1. [이 곳](https://github.com/msys2/msys2-installer/releases/download/2024-01-13/msys2-x86_64-20240113.exe)에서 다운로드 한다.
2. 보통 `C:\msys2` 아래에 설치 되는데, **다른 경로가 필요하다면 기억하자.**
3. 까먹고 스크린 샷을 안 했다. **바로 실행하도록 Run MSYS2 체크해주자.**
4. 터미널 창이 열릴 것이다. 다음과 같은 명령어를 입력하자. 붙여넣기는 `Shift` + `Insert`이다.
   * `pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain`
5. ![alt text](/assets/images/240526/image.png) 그리고 `Enter` 누른다.
6. ![alt text](/assets/images/240526/image2.png) 다음 Y 후 Enter 누르면 된다. 알아서 설치 할 것이다.
7. 환경 변수를 설정하자.
   1. `Win` + `R` 하여 나타난 실행 창에 `sysdm.cpl` 그리고 `Enter`
   2. **고급** 탭 - 아래의 **환경 변수**
   3. 사용자 환경 변수? 아무튼 **위쪽 상자**에서 **`Path`를 누르고 수정 - 새로 만들기 후 리스트에 텍스트를 쓸 수 있는 공간이 나오면 `C:\msys64\ucrt64\bin` 입력 후 확인 버튼 광클해서 나오면 된다.**
8. `cmd` 내지 `터미널`<sup>Terminal</sup>을 열어서 다음 명령어들을 입력한다

    ```text
    gcc --version
    g++ --version
    gdb --version
    ```

## 잘 보인다면 당신은 성공 (1따봉)

![alt text](/assets/images/240526/image3.png)

상단에 코드를 실행할 수 있는 버튼이 있다는 것은 모두가 안다.  
이 버튼에 마우스를 올려서 *Run C/C++ File*이라고 Tooltip이 뜬다면 바로 눌러도 좋다!  
  
하지만 안 뜬다면 옆의 화살표를 눌러 사진처럼 실행해주면 되고,  
실행하면 상단에 뭔가 뜰 텐데 그냥 첫 번째 항목을 누르고 바로 실행되지 않는다면 실행 버튼을 한 번 더 눌러보길 바란다.

---

## sources, footnotes

<!-- [^1]: -->

Source: [https://code.visualstudio.com/docs/cpp/config-mingw#_installing-the-mingww64-toolchain](https://code.visualstudio.com/docs/cpp/config-mingw#_installing-the-mingww64-toolchain)