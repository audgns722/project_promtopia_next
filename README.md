# promptopia 프롬프트 공유사이트 next14

"Promtopia"는 AI사진 생성과 관련된 프롬프트를 공유하는 웹 애플리케이션입니다.  
이 프로젝트는 사용자가 쉽게 정보를 검색하고 공유하는 환경을 제공합니다.\
[참고영상](https://www.youtube.com/watch?v=wm5gMKuwSYk&list=PLpwSgcyFeRw3jKpo_WtvrIl9CFSwXNe9R&index=2&t=10457s)

## [완성작 미리보기](https://project-promtopia-next-6i6z8qs9q-hoonsdevs-projects.vercel.app/)

<div align=center>
<img width=100% src="https://github.com/audgns722/project_promtopia_next/blob/main/public/assets/images/promptopia.png?raw=true">
</div>

## 주요 기능

- 반응형 디자인: 모든 기기에서 일관된 사용자 경험을 제공합니다. Tailwind CSS를 사용하여 모바일, 태블릿, 데스크톱 환경에서 완벽하게 작동합니다.
- 사용자 관리: 사용자 등록, 로그인, 프로필 관리 기능을 제공합니다. Next-auth를 사용하여 간편하고 안전한 인증 과정을 구현합니다.
- 데이터 시각화: 사용자 데이터를 시각적으로 표현하여 이해를 돕습니다.

## 기술 스택

- Frontend  
   React: 사용자 인터페이스 구축  
   Next.js: 서버 사이드 렌더링 및 페이지 라우팅  
   Tailwind CSS: 유틸리티 우선의 CSS 프레임워크
- Backend  
   Node.js & Express: RESTful API 서버 구축  
   MongoDB & Mongoose: NoSQL 데이터베이스 관리
- Authentication  
   Next-auth: 간편하고 효율적인 사용자 인증 처리
- Security  
   Bcrypt: 비밀번호 암호화 및 보안 강화

## 설치 및 실행 방법

`npx create-next-app@latest`  
`npm install`  
`npm run dev`

```javascript
npm install mongodb
npm install mongoose
npm install next-auth
npm install bcrypt
```

## 프로젝트 구성

<details>
<summary>filetree</summary>

```
├── app
│   ├── api           # API 관련 로직 및 라우팅
│   ├── create-prompt # 프롬프트 생성 관련 컴포넌트
│   ├── layout.jsx    # 애플리케이션 레이아웃 컴포넌트
│   ├── profile       # 사용자 프로필 페이지
│   └── update-prompt # 프롬프트 수정 기능
├── components        # 재사용 가능한 UI 컴포넌트
├── models            # 데이터 모델 정의 (Mongoose 스키마)
├── public
```

</details>

## 주요 기능 요약

- API 통신 (api 폴더):

  서버와의 데이터 교환을 위한 API 호출 관리.  
   사용자 요청 및 서버 응답 처리.  
   데이터 검증 및 오류 처리를 위한 로직 포함 가능.

- 새 프롬프트 생성 (create-prompt 폴더):

  사용자 입력을 받아 새로운 프롬프트 생성.  
   폼 검증, 데이터 전송 및 사용자 피드백 처리.  
   사용자 경험(UX) 최적화를 위한 인터페이스 설계.

- 레이아웃 관리 (layout.jsx):

  애플리케이션의 전반적인 레이아웃 및 스타일 설정.  
   반응형 디자인을 고려한 레이아웃 구성.  
   네비게이션, 헤더, 푸터 등 공통 요소 포함.

- 페이지 구성 (page.jsx):

  개별 페이지의 구조 및 기능 정의.  
   사용자 인터페이스(UI) 요소 및 이벤트 핸들링.  
   페이지별 데이터 관리 및 상태 관리.

- 사용자 프로필 관리 (profile 폴더):

  사용자 정보 표시 및 수정 기능.  
   보안 및 개인정보 보호를 위한 접근 제어.  
   사용자 경험에 맞는 인터페이스 디자인.

- 프롬프트 업데이트 (update-prompt 폴더):

  기존 프롬프트의 수정 및 업데이트 기능.  
   데이터의 유효성 검사 및 오류 처리.  
   사용자 변경 사항의 효과적인 피드백 제공.

- Form.jsx:

  사용자 입력 처리, 유효성 검사
  다양한 유형의 폼 (로그인, 회원가입, 데이터 입력 등)

- Profile.jsx:

  사용자 정보 표시, 프로필 사진, 사용자 관련 설정 등을 제공.

- Provider.jsx:

  전역 상태 관리 또는 컨텍스트 제공을 담당  
   앱 전반에 걸친 데이터를 관리할 수 있음.

- prompt.js:

  제목, 내용, 생성 날짜, 사용자 정보 등을 포함
  데이터베이스에 저장되는 프롬프트 관련 정보의 스키마 및 관계를 정의하는 데 사용

- user.js:

  사용자와 관련된 데이터를 정의
  사용자 이름, 이메일, 비밀번호, 프로필 정보 등 사용자의 기본적인 정보를 포함

  - 특히 사용자 정보를 다루는 모델의 경우, 보안이 매우 중요합니다. 비밀번호와 같은 민감한 정보는 암호화하여 저장해야 합니다.

## 코드 미리보기

<details>

<summary>NextAuth 설정과 인증 공급자</summary>

```javascript
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";

const handler = NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
  // ...
});
```

</details>

    NextAuth 함수는 Next.js 애플리케이션에서 사용자 인증을 구성합니다.
    GoogleProvider는 Google OAuth 서비스를 인증 공급자로 사용합니다.
    clientId와 clientSecret은 환경 변수에서 가져와 Google OAuth를 설정하는 데 사용됩니다.

<details>

<summary>로그인 콜백</summary>

```javascript
async signIn({ account, profile, user, credentials }) {
  try {
    await connectToDB();

    const userExists = await User.findOne({ email: profile.email });

    if (!userExists) {
      await User.create({
        email: profile.email,
        username: profile.name.replace(" ", "").toLowerCase(),
        image: profile.picture,
      });
    }

    return true;
  } catch (error) {
    console.log("Error checking if user exists: ", error.message);
    return false;
  }
}
```

</details>

    signIn 콜백은 사용자가 로그인할 때 호출됩니다.
    데이터베이스에 연결한 후, 사용자의 이메일로 이미 존재하는 사용자인지 확인합니다.
    존재하지 않는 경우, 새로운 사용자를 생성합니다.
    로그인 과정 중 발생한 에러는 콘솔에 로그를 출력하고, 로그인을 중단합니다.

<summary>폼 상태 관리</summary>

<details>

```javascript
const [submitting, setIsSubmitting] = useState(false);
const [post, setPost] = useState({ prompt: "", tag: "" });
```

</details>

    post 상태는 사용자가 입력한 프롬프트의 내용과 태그를 저장합니다. 초기값은 빈 문자열입니다.
    setPost 함수를 사용하여 사용자의 입력에 따라 post 상태를 업데이트합니다.
    submitting 상태는 폼이 제출 중인지 여부를 나타냅니다. 네트워크 요청이 진행 중일 때는 true로 설정됩니다.

<details>

<summary>에러 처리 및 네트워크 요청 관리</summary>

```javascript
const createPrompt = async (e) => {
  e.preventDefault();
  setIsSubmitting(true);

  try {
    const response = await fetch("/api/prompt/new", {
      method: "POST",
      body: JSON.stringify({
        prompt: post.prompt,
        userId: session?.user.id,
        tag: post.tag,
      }),
    });

    if (response.ok) {
      router.push("/");
    }
  } catch (error) {
    console.log(error);
  } finally {
    setIsSubmitting(false);
  }
};
```

</details>

    try 블록 안에서 /api/prompt/new 엔드포인트로 POST 요청을 보내고 있습니다.
    요청이 성공적으로 처리되면(response.ok), 사용자를 홈페이지로 리디렉션합니다.
    요청 중 오류가 발생하면, catch 블록이 실행되어 오류를 콘솔에 로그로 출력합니다.
    finally 블록은 요청이 성공하든 실패하든 실행되며, submitting 상태를 false로 설정합니다.

## 참고 내용

- bcrypt: 비밀번호 해싱을 위한 라이브러리. 사용자의 비밀번호를 안전하게 저장하기 위해 사용됩니다.
- mongodb: MongoDB 데이터베이스와의 상호작용을 위한 드라이버.
- mongoose: MongoDB 데이터베이스를 위한 ODM(Object Data Modeling) 라이브러리. 데이터베이스 스키마를 정의하고 관리하는 데 사용됩니다.
- next: Next.js 프레임워크. 서버 사이드 렌더링(SSR) 및 정적 사이트 생성을 포함한 웹 애플리케이션 개발에 사용됩니다.
- next-auth: Next.js 애플리케이션을 위한 인증 라이브러리. 사용자 인증 및 세션 관리를 쉽게 구현할 수 있도록 도와줍니다.
- react: 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리.
- react-dom: React 엘리먼트를 DOM에 렌더링하기 위한 라이브러리.
- tailwindcss: 유틸리티 우선의 CSS 프레임워크. 빠르고 유연한 스타일링을 가능하게 합니다.

## Tailwind CSS란?

Tailwind CSS는 유틸리티 우선(utility-first)의 CSS 프레임워크로, 다양한 스타일을 빠르고 효율적으로 적용할 수 있게 해줍니다

    - Tailwind CSS의 장점
    유연성과 생산성: Tailwind CSS는 매우 유연하며, 개발자가 빠르게 프론트엔드 디자인을 구현할 수 있도록 돕습니다.

    응집력 있는 디자인 시스템: 일관된 디자인 시스템을 구축할 수 있으며, 이는 프로젝트 전반에 걸쳐 일관된 룩앤필을 유지하는 데 도움이 됩니다.

    사용자 정의 및 확장성: Tailwind CSS는 사용자 정의가 용이하며, 프로젝트의 요구사항에 맞게 확장할 수 있습니다.

    반응형 디자인: 반응형 디자인을 쉽게 구현할 수 있습니다. Tailwind는 다양한 화면 크기에 맞게 스타일을 조정하는 데 필요한 유틸리티 클래스를 제공합니다.

    유지보수성: 유틸리티 클래스를 사용함으로써 스타일 시트의 크기를 줄이고, 유지보수를 용이하게 할 수 있습니다.
