# CH01. Next.js 알아보기

## ▶️ Next.js
- 리액트를 위해 만든 오픈소스 자바스크립트 웹 프레임워크 (확장성 ↑, 성능 ↑)
- `하이브리드 렌더링`, `라우트 프리페칭(pre-fetching)`, `자동 이미지 최적화`, `국제화` 등의 기능 제공
- SSR (Server Side Rendering) : 서버 사이드 렌더링
- SSG (Static Site Generation) : 정적 사이트 생성
- ISR (Incremental Static Regeneration) : 증분 정적 재생성
<br />

- React : 메타 엔지니어 개발
- 메타의 PHP, Hack Developer → XHP를 통해 프론트엔드 부분에서 `재사용할 수 있는 컴포넌트` 제작    
<br />

- **React 단점**
    - _클라이언트 사이드_ 에서만 작동
    - 웹 브라우저에서만 실행되기에 _검색 엔진 최적화(SEO)의 효과를 거의 볼 수 없음_    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; → 첫 화면에 웹 애플리케이션을 제대로 표시하기 위해 실행 초기의 성능 부담 ↑   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : 1. 브라우저가 전체 웹 앱 번들 다운로드   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : 2. 해당 내용을 분석 & 코드 실행해 결과를 얻어야 함    
→ 웹 애플리케이션을 서버에서 미리 렌더링해두는 방법 연구   
: 서버 사이드 렌더링 사용이 가능하다면, 리액트 앱을 순수한 HTML 페이지로 미리 렌더링한 후,    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 브라우저가 이를 다운로드해 **즉각 화면에 표시**    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;& 클라이언트에서 JS 번들을 다 받으면 `USER` ↔️ `WEB APP` 상호작용 가능      
<br />

- vercel : Next.js 제작   

|**`Next.js` 제공 기능**|
|---------------------|
|코드 분할|
|서버 사이드 렌더링|
|파일 기반 라우팅|
|경로 기반 프리페칭|
|정적 사이트 생성|
|증분 정적 콘텐츠 생성|
|타입스크립트에 대한 기본 지원|
|자동 폴리필 적용|
|이미지 최적화|
|웹 애플리케이션의 국제화 지원|
|성능 분석|   

## ▶️ Next.js와 비슷한 프레임워크
- `Gatsby`
    - Next.js 대신 사용할 수 있는 프레임워크
    - 정적 웹 사이트 제작에 최적화 (Next.js와 달리 Gatsby는 정적 사이트 생성만 지원)
    - 모든 페이지를 _빌드 시점에 미리 렌더링해 정적 콘텐츠 형태로 만듦_ : 어떤 콘텐츠 전송 네트워크(CDN)로도 제공 가능
    - 단점 : 동적 서버 사이드 렌더링 지원 X → 데이터에 따라 동적으로 변하는 복잡한 웹 사이트 제작 불가능
<br />

- `Razzle`
    - SSR 가능한 JS 애플리케이션 제작 가능
    - CRA 도구를 쉽게 사용 && 서버와 클라이언트의 복잡한 애플리케이션 설정 추상화 가능
    - 사용할 프레임워크 관련 지식이 없어도 됨 (Next.js와의 차이점)
    - React, Vue, Angular, Elm, Reason-React 등 어떤 프레임워크든 사용 가능
<br />

- `Nuxt.js`
    - Vue를 사용한 웹 애플리케이션 개발에서 리액트의 Next.js에 해당하는 것
    - SSR, SSG, PWA(Progressive Web App) 등의 기능 제공 (성능, SEO, 개발 속도 등 별다른 차이 X)
    - Next.js에 비해 많은 설정 필요 (레이아웃, 전역 플러그인, 컴포넌트, 라우트 등 지정 가능)
    - 기저 라이브러리가 무엇이냐는 점
        - `Next.js` : React 기반
        - `Nuxt.js` : Vue 기반
<br />

- `Angular Universal`
    - 서버에서 JS 코드 실행 & 렌더링 기능 제공
    - SSG, SSR 지원 (`Next.js`, `Nuxt.js`와의 차이점 : 구글에서 개발)

## ▶️ 리액트에서 Next.js로
- 단일 Next.js 애플리케이션에서 별도의 설정 파일을 만들지 않아도 특정 페이지에 SSR, SSG 적용 지정 가능   
- 각 페이지에서 특정 함수를 `export`하면 Next.js에서 나머지 작업 처리
- `React` : 자바스크립트 라이브러리
- `Next.js` : 프레임워크 - 클라이언트 & 서버에서 실행할 수 있는 코드
    - 서버 사이드 렌더링 페이지 & 정적으로 생성된 페이지 모두 `Node.js`에서 실행
        - ⭐️ `fetch`, `window`, `document` 등 웹 브라우저에서 제공하는 전역 객체 접근 X
        - ⭐️ `canvas` 등의 HTML 요소 접근 X
    - `fs`, `child_process` 등 Node.js에서만 사용할 수 있는 라이브러리 & API 사용 시,   
        - 각 요청 별 데이터를 클라이언트로 보내기 전에 서버 사이드 코드 실행 or 페이지 생성 시점에 해당 코드 처리하는 방식 지원
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; → 각 페이지가 어떤 렌더링 방식을 사용하느냐에 따라 결정
- 클라이언트 사이드 앱 생성 시에도 CRA 대신 Next.js 사용 가능



