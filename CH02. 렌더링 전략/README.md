# CH02. 렌더링 전략
**렌더링 전략** : 웹 페이지 or 웹 어플리케이션을 웹 브라우저에 제공하는 방법   
- 정적으로 생성한 페이지 제공에 유리 : ex) `Gatsby`
- 서버 사이드 렌더링 페이지 제공에 유리 : 다른 프레임워크들   
→ `Next.js`: 새로운 수준으로 방법 제공   
    - 어떤 페이지를 **빌드 시점**에 **정적**으로 생성 & 어떤 페이지를 **실행 시점**에 **동적**으로 제공할지 쉽게 정할 수 있음    
    - 애플리케이션의 특정 페이지에 대한 요청이 있을 경우 페이지를 다시 생성할 수 있음   
    - 반드시 클라이언트에서 렌더링해야 할 컴포넌트 지정 가능    

## ▶️ 서버 사이드 렌더링 (SSR)
**SSR** : 웹 페이지를 제공하는 가장 흔한 방법   
ex) PHP, 루비, 파이썬 등의 언어 : HTML 페이지를 웹 브라우저로 전송하기 전에 서버에서 전부 렌더링   
&nbsp;&nbsp;&nbsp;&nbsp; → 해당 페이지의 모든 자바스크립트 코드가 적재 → 동적으로 페이지 내용 렌더링   
<br />

`Next.js` : 각 요청에 따라 서버에서 HTML 페이지를 동적으로 렌더링 & 웹 브라우저로 전송 가능   
- 서버에서 렌더링한 페이지에 스크립트 코드를 집어넣어 추후 웹 페이지의 동적 처리 가능 → **하이드레이션**(hydration)    
    - 리액트에서의 하이드레이션 
        - 서버 측에서 생성한 HTML 페이지에 클라이언트 측에서 실행하는 JS 코드를 추가해 애플리케이션 상태를 관리하고 렌더링하는 기법
        - HTML 페이지를 구성하는 각각의 DOM 객체에 필요한 자바스크립트 코드를 추가해 클라이언트가 동적으로 렌더링할 수 있는 것 의미
        - 서버 측에서 렌더링한 DOM과 클라이언트가 렌더링한 DOM이 한데 섞여 SPA처럼 보인다는 점에서 **하이드레이션**
<br />

- ex) 블로그 사이트를 만들어 어떤 사람이 작성한 모든 글을 한 페이지에 렌더링 → SSR 적용에 최적화된 상황    
&nbsp;&nbsp;&nbsp;&nbsp; → 사용자 : 페이지 접근     
&nbsp;&nbsp;&nbsp;&nbsp; → 서버 : 페이지를 렌더링해 결과로 생성한 HTML 페이지를 클라이언트로 전송    
&nbsp;&nbsp;&nbsp;&nbsp; → 브라우저 : 페이지에서 요청한 모든 스크립트 다운로드 & DOM 위에 각 스크립트 코드 하이드레이션    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : 페이지의 새로 고침 없이 사용자와 웹 페이지 간 상호작용 가능   
리액트의 하이드레이션 : 웹 앱은 **싱글 페이지 어플리케이션**(SPA)처럼 작동 가능   
→ CSR과 SSR의 장점 모두 O    
<br />

- **더 안전한 웹 애플리케이션**
    - 페이지를 서버에서 렌더링하는 것 === 쿠키 관리, 주요 API, 데이터 검증 등의 작업을 서버에서 처리한다는 의미   
    - 중요한 데이터를 클라이언트에 노출할 필요가 없기에 안전   
<br />

- **더 뛰어난 웹 사이트 호환성**
    - 클라이언트 환경이 JS를 이용 X or 오래된 브라우저 사용 시에도 웹 페이지 제공 가능  
<br />

- **더 뛰어난 SEO**
    - 클라이언트에서 서버가 렌더링한 HTML 콘텐츠를 받으므로 봇, 웹 크롤러 같은 검색 엔진 웹 문서 수집기가 페이지를 렌더링 할 필요 X
    - 웹 애플리케이션의 SEO 점수 ↑
    - SSR이 최적의 렌더링 전략이 아닌 경우도 존재
        - SSR 사용 시 클라이언트가 요청할 때마다 페이지를 다시 렌더링할 수 있는 서버 필요
        - CSR or SSG 방식 생성 → 정적 HTML 파일을 vercel or netlify와 같은 클라우드 서비스에 배포 & 클라이언트에 제공 가능
        - 웹 앱을 서버에 배포할 경우, SSR App이 더 많은 자원 소모 & 부하 유발 & 유지보수 비용 증가
        <br /><br />
    - SSR 사용 시 **페이지에 대한 요청 처리 시간 ↑**
        - 페이지가 외부 API 또는 데이터 소스에 접근해야할 경우, 해당 페이지를 렌더링할 때마다 API나 데이터 소스 재요청   
        - ✔️ 서버에서 렌더링한 페이지 간의 이동 : 클라이언트에서 렌더링한 페이지 or 정적으로 생성한 페이지 간의 이동보다 느림    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; → `Next.js` : 네비게이션 성능 향상 기능 제공    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : `Next.js` - 기본적으로 빌드 시점에 **정적으로 페이지 생성**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; → 페이지에서 외부 API 호출 or 데이터베이스에 접근하는 등 동적 작업 필요 시 : 해당 함수를 페이지에서 `export`   
```js
function IndexPage() {
    return <div>This is the index page</div>;
}

export default IndexPage;
```
- 위 페이지 : 페이지의 외부 API 호출 X, 데이터 소스에 접근 X, 각 요청에 대한 내용 : 항상 같은 문자열   

```js
export async function getServerSideProps() {
    const userRequest = await fetch('fttps://example.com/api/user');
    const userData = await userRequest.json();

    return {
        props: {
            user: userData,
        },
    };
}

function IndexPage(props) {
    return <div>Welcome, {props.user.name}!</div>;
}

export default IndexPage;
```
- Next.js의 `getServerSideProps` 예약 함수 사용   
    - 페이지에 대한 요청이 들어오면 서버가 REST API를 호출해 필요한 사용자 정보를 가져옴

1. 비동기 함수 `getServerSideProps` export     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; → 빌드 과정에서 `Next.js` : 해당 함수를 export하는 모든 페이지를 찾아 서버가 페이지 요청을 처리할 때    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `getServerSideProps` 함수를 호출하도록 함     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : 해당 함수 내의 코드는 항상 서버에서만 실행   
<br />

2. `getServerSideProps` 함수 : props라는 속성값을 갖는 객체 반환   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `Next.js` : 이 props를 컴포넌트로 전달해 서버와 클라이언트 모두가 props에 접근 & 사용 가능   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; fetch API : Next.js를 통해 서버에서 실행됨 → fetch APi를 별도의 폴리필로 끼워넣을 필요 X
<br />

3. `IndexPage` 함수를 수정해 props를 인자로 받음   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 해당 props는 `getServerSideProps` 함수에서 반환한 props의 모든 내용을 가짐   
<br />

> ⚠️ **SSR의 주의점**   
> 브라우저 전용 API를 사용해야 하는 컴포넌트가 있을 경우   
> 해당 컴포넌트를 반드시 **브라우저에서 렌더링하도록 명시적인 지정**이 필요    
> Next.js : 서버에서 페이지 렌더링 → `window`, `document`와 같은 객체 or API 제공 X   
> → CSR 필요   