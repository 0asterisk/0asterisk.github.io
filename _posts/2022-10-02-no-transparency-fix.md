---
layout: post
title: 윈도우 11에서 투명 효과가 안될 때 해결 방법
subtitle: 설정에서 켜도 안되면 레지스트리를 건드리면 쉽다
sitemap :
  changefreq : daily
  priority : 1.0
---

![이제 좀 잘 된다...](/assets/images/221002_1/제목%20없음.png)
<br/>

## 분명 나는 설정에서 켰는데...
하는 순간 당신의 윈도우는 특별하다. 사실 OS라는게 특별해야 맞는거지만! 아무튼 나는 몇 날 며칠을 수소문 했지만 나는 바로 알려줄 것이다 (ㅠ)  

<br/>

## 해결 방법[^1]  
![](/assets/images/221002_1/2.png)
<br>
레지스트리 편집기[^2]를 켜고 다음 경로로 이동한다:  
`컴퓨터\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Dwm`
<br><br>
들어가면 바로 `ForceEffectMode`가 있는데 이 값 데이터를 `2`로 바꾸면 된다. 설정에선 당연하게 투명 효과를 켜놔야 한다.

<br/>

## Sources / Footnotes

[^1]: https://www.elevenforum.com/t/transparency-effects-not-working.1568/  
[^2]: 윈도우 검색창에서 `regedit` 검색