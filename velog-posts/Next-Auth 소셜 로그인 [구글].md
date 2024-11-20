<p><img alt="" src="https://velog.velcdn.com/images/bell-ho/post/10bc4d9a-2721-4eb1-97ff-99cb3237e908/image.png" /></p>
<p>NextJS 에서 next-auth를 이용하면 google , facebook , naver 같은 소셜 로그인 기능을 쉽게 만들 수 있습니다.</p>
<p>next 13버전, next-auth 4버전을 사용했습니다.</p>
<pre><code class="language-javascript">next-auth 사용시 pages/api/auth 폴더안에 [...nextauth].js 파일을 만들어야 합니다.

import NextAuth from 'next-auth';
import GoogleProvider from 'next-auth/providers/google';

const nextAuthOptions = (req, res) =&gt; {
  return {
    providers: [
      GoogleProvider({
        clientId: process.env.GOOGLE_CLIENT_ID,
        clientSecret: process.env.GOOGLE_CLIENT_SECRET,
      }),
    ],
  };
};

const authHandler = (req, res) =&gt; {
  return NextAuth(req, res, nextAuthOptions(req, res));
};

export default authHandler;</code></pre>
<p>.env 파일을 이용해서 google 클라이언트 키와 시크릿키를 저장합니다.</p>
<p>구글 클라우드 플랫폼 이용하기
<a href="https://console.cloud.google.com/getting-started?hl=ko">https://console.cloud.google.com/getting-started?hl=ko</a></p>
<p>google API키와 시크릿키 얻는 방법은 생략하겠습니다.</p>
<pre><code class="language-javascript">로그인 화면에서 next-auth signIn 함수를 이용합니다

import { signIn } from 'next-auth/react';

const Login = () =&gt; {

  ... 생략

    return (
        &lt;Button onClick={() =&gt; signIn('google')}&gt;
              구글 로그인
        &lt;/Button&gt;
    );
}</code></pre>
<p>로그인 버튼을 누르면 ?
<img alt="" src="https://velog.velcdn.com/images/bell-ho/post/66fe948f-8a63-4a1f-9a43-820f7287c14d/image.png" /></p>