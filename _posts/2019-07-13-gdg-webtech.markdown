---
layout: post
title:  "I/O Extended 2019 WebTech 후기"
author: Hyunseok
categories: seminar
---

<a href="https://festa.io/events/339"><img src="/assets/tech_seminar/gdg_webtech/gdg_io_2019_webtech.jpg" title="gdg io 2019 webtech"></a>

<b>`19.07.13일에 구글 스타트업 캠퍼스에서 진행된 Google I/O Webtech 세미나 간단 메모.</b>

Puppeteer, PWA는 최근에 개인적으로 공부를 진행했었는데,
마지막 세션이었던 Lighthouse는 세미나에서 처음 알게된 툴이었다. 

출근하게되면 회사에서 작성한 코드를 Lighthouse로 검사해서 리펙토링을 진행 해봐야겠다.

- <a href="https://web.dev/">Google Web Dev</a>

<h1 style="margin: 0px"><a href="https://web.dev/prerender-with-react-snap">Puppeteer</a></h1>
<hr style="margin: 0px"/>
- 구글에서 내놓은 Headless Chrome Node API
- 프로그래밍적 입력이 아닌 사용자의 입력을 흉내내는 방식으로 마우스 등의 조작도 가능.
- Jest를 이용한 테스트 가능.
    - Jest Puppeteer 라이브러리.
- React-Snap

<h1 style="margin: 0px">
<a href="https://web.dev/hands-on-portals">Hands on Portals</a>
</h1>
<hr style="margin: 0px"/>
### Micro Frontend
- MSA를 프론트엔드에 접목.
- 하나의 기능이 문제가 생겨도 전체 기능에는 영향이 가지 않도록
- 하나의 조직이 하나의 기능을 담당하도록 (프론트, 백, 개발 및 배포까지)
    - 도메인을 분리

### Portals
- HTML 규격
- 아직은 Chrome Canary에서만 동작 (2019-07-13 기준)
- Chrome Canary > Chrome Flags > Enable Portals
- 페이지간의 이동을 부드럽게 만들어주는 HTML 요소.
- 하나의 페이지에서 다른 페이지를 Import해 올때.
- iFrame과 Portals이 동작방식이 유사하므로, Portals를 지원하지 않는 페이지는 iFrame을 이용.
- PostMessage를 이용하여 데이터를 주고 받을 수 있다 (iFrame 처럼).

<h1 style="margin: 0px">New Capabilities for the Web</h1>
<hr style="margin: 0px"/>
- 웹의 새로운 기능, 확장성

### App Gap
- 네이티브 앱과 앱 사이 차이

### Project Fugu
- 네이티브 웹과 앱 사이의 격차를 줄이는 프로젝트
- Fugu (복어), 기능 개발도 중요하지만 사용자의 안정성도 중요.
- Web can do everything

### New Capabilities
1. Share Content and Receiving Shares
- Https, 사용자 액션 필요.

1. Web Share Target API
- WebApp Manifest안에 Share Target 필드 추가

1. Media Session API
- 시스템(안드로이드, Mac 등)의 미디어를 컨트롤 가능.

1. Detecting Barcode, Face
- Shape Detection API
- 사진을 올리면 얼굴을 디텍트.

1. Perception ToolKit
- Sensing
- Meaning
- UX

1. System Wake Lock and ScreenWake Lock
- 장치가 잠자기 상태가 되지 않게 설정.
- 화면의 꺼짐등을 제어할 수도 있음.

1. Badge API
- 웹 사이트를 어플리케이션 형태로 다운로드.

<h1 style="margin: 0px">WebAssembly 101</h1>
<hr style="margin: 0px"/>

### Emscription 프로젝트
- C, C++을 javascript로 컴파일할수있도록 도와주는 SDK
- LLVM 바이트코드를 Javascript로 컴파일
- C, C++ -> Emscripten -> Javascript(asm.js)
- asm.js
    - Javascript 고수준 요소는 제외
        - Object, String, Closure 등
    - 동적으로 타입이 변환하지 않는다는 전제.
    - 메모리를 직접 재어한다고 보장.
    - 네이티브에 준한 성능을 얻을 수 있음.
    - 차라리 이럴꺼면 브라우저에서 어셈블리어를 정의하는게 나을거 같다.. -> WebAssmbly
- Web을 위한 어셈블리어
- 기계어와 대응되는 명령어 집합.
- 웹 브라우저에서 실행되는 바이너리

### 어디서 쓸수있나
- Native에 준한 속도 처리
- Image, Video Editing
- Gaming
- C, C++ 코드 베이스를 재사용 가능.
- 이미지 압축 알고리즘.
    - Mozjpeg

### 사용 사례
- Wasmboy (게임보이를 웹에서 사용)
- Codebase
    - Typescript, javascript

### AssemblyScript
- Typescript Subset
- Typescript를 WebAssembly로 컴파일
- Any, undefined 타입은 사용 불가
- WebAssembly 타입을 사용
- GitHub (Awesome-wasm-langs)
- WebAssembly는 만능이 아님.
    - 다만, 일관적인 성능을 보장
    - 가벼운 작업을 하는데 굳이 쓸 이유는 없음.
    - 무거운 알고리즘에 유용.
    - https://Webassembly.studio


<h1 style="margin: 0px">Going Big - PWA</h1>
<hr style="margin: 0px"/>
- 기존의 웹 기술을 사용해서 네이티브 웹 경험을 사용자에게 제공.
- Chrome 76부터는 데스크탑도 지원
- Desktop, Mobile Same code

### 구성 요소
1. WebSite
1. Web App Manifest
- 설치할때, 시스템에서 어떻게 설치해야할지 알려주는 내용
1. Service worker
- 인터넷이 안되는 상황, Offline First
- 메인 스레드 외의 여분의 일꾼
- 네트워크가 불안정해서 데이터를 못가져왔을 경우, 캐싱 용도(가장 최근에 가져온 데이터를 보여줌)
- Workbox (캐시 만료에 대한 관리를 지원)
- Write Once Work Anywhere
1. Expanded Capabilities
1. OS integration


<h1 style="margin: 0px">Deep in Lighthouse Audits</h1>
<hr style="margin: 0px"/>
### Lighthouse 란?
- Google Chrome팀에서 만든 데브 툴.
- Google Chrome에서 Audits 탭에서 사용 가능.
- 분석 도구
    - 웹 사이트 퍼포먼스, 접근성, 검색 엔진 최적화.
    - 성능 테스트.
- 구글에서 사용하는 핵심 지표.
- 시크릿 모드에서 돌리는게 좋음
    - 크롬 확장 같은걸 제외시켜줌.
- cli 버전도 존재(CI 툴을 사용할 때)
- 도움이 될 만한 항목
    - CSS minify, Javascript minify
    - Interaction Observer

