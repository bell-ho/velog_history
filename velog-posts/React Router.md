<blockquote>
<p>Route란 컴포넌트로 특정 주소에 컴포넌트를 연결하는것</p>
</blockquote>
<h2 id="11-기본">1.1 기본</h2>
<pre><code>설치
npm i react-router-dom</code></pre><pre><code class="language-html">사용법
&lt;Router path=&quot;주소&quot; component={컴포넌트이름}/&gt;

예시1
&lt;div&gt;
    &lt;Router path=&quot;/&quot; component={home}/&gt;
    &lt;Router path=&quot;/abc&quot; component={Abc}/&gt;
&lt;/div&gt;</code></pre>
<p>예시1에서 /abc를 들어가면 두 컴포넌트가 다 나오는데, /abc 경로가 /에도 일치하기 때문
이를 수정 하려면 home을 위한 컴포넌트를 사용할 때 <strong>exact라는 props를 true로 설정</strong> 해야함</p>
<h2 id="12-link">1.2 Link</h2>
<p>Link는 클릭하면 다른 주소로 이동시켜 주는 컴포넌트</p>
<pre><code class="language-html">&lt;Link to=&quot;/&quot;&gt;홈&lt;/Link&gt;
&lt;Link to=&quot;/abc&quot;&gt;ABC&lt;/Link&gt;

&lt;div&gt;
    &lt;Router path=&quot;/&quot; component={home}/&gt;
    &lt;Router path=&quot;/abc&quot; component={Abc}/&gt;
&lt;/div&gt;</code></pre>
<h2 id="13-url-파라미터와-쿼리">1.3 URL 파라미터와 쿼리</h2>
<p>페이지 주소를 정의할 때 값을 전달해야 할 때가 있음
일반적으로 <strong>파라미터는 특정 아아디와 이름을 사용하여 조회할 때</strong> 사용하고 
<strong>쿼리는 키워드를 검색하거나 페이지에 옵션을 전달할 때</strong> 사용</p>
<ul>
<li>파라미터 : /profiles/hong</li>
<li>쿼리 : /about?dog=true</li>
</ul>
<h3 id="131-url-파라미터">1.3.1 URL 파라미터</h3>
<pre><code class="language-html">&lt;Link to=&quot;/&quot;&gt;홈&lt;/Link&gt;
&lt;Link to=&quot;/profile/gildong&quot;&gt;gildong의 프로필&lt;/Link&gt;

&lt;div&gt;
    &lt;Router path=&quot;/&quot; component={home}/&gt;
    &lt;Router path=&quot;/profile/:username&quot; component={Profile}/&gt;
&lt;/div&gt;</code></pre>
<pre><code class="language-javascript">// Profile 컴포넌트
const data = {
    gildong:{
        name:'길동'
    }
}

const profile = data[username];

const Profile = ({match}) =&gt;{
    const { username } = match.params
}</code></pre>
<p><strong>URL 파라미터</strong>를 사용할 때 <strong>match</strong>라는 객체안의 *<em>params *</em>값을 참조함
match 안에는 현재 컴포넌트가 어떤 경로 규칙에 의해 보이는지를 알 수 있음</p>
<h3 id="132-url-쿼리">1.3.2 URL 쿼리</h3>
<p>쿼리는 <strong>location 객체</strong>에 들어 있는 <strong>search 값</strong>에서 조회 가능
location 객체는 라우트로 사용된 컴포넌트에게 props로 전달되며 웹 현재 주소에 대한 정보가 있음</p>
<pre><code class="language-json">http://localhost:3000/about?dog=true 일때 location 객체 예시

{
  &quot;pathname&quot; : &quot;/about&quot;,
  &quot;search&quot; : &quot;?dog=true&quot;,
  &quot;hash&quot; : &quot;&quot;
}</code></pre>
<p>search 값을 읽어오기 위해 문자열을 객체 형태로 변환 해야함
쿼리 문자열을 객체로 변환할 때는 qs 라이브러리 사용</p>
<pre><code>npm i qs</code></pre><pre><code class="language-javascript">const query = qs.parse(location.search,{
    ignoreQueryPrefix: true // 맨 앞의 ?를 생략
});</code></pre>
<p><strong>쿼리 문자열을 객체로 파싱하는 과정에서 결과는 언제나 문자열</strong>이라
숫자는 parseInt로 변환하고 논리 자료형은 &quot;true&quot;나 &quot;false&quot; 문자열과 일치하는지 비교 해야함</p>
<h2 id="14-라우터-부가-기능">1.4 라우터 부가 기능</h2>
<h3 id="141-서브-라우트">1.4.1 서브 라우트</h3>
<p>서브 라우트는 라우트 내부에 또 라우트를 정의하는 것을 의미
라우트로 사용되고 있는 컴포넌트 내부에 Route 컴포넌트를 또 사용하면 됨</p>
<h3 id="142-withrouter">1.4.2 withRouter</h3>
<p>withRouter 함수는 라우트로 사용된 컴포넌트가 아니어도 match, location, history 객체를 접근할 수 있게함</p>
<h3 id="143-switch">1.4.3 Switch</h3>
<p>Switch 컴포넌트는 <strong>여러 Route를 감싸서</strong> 그중 일치하는 하나의 라우트만 렌더링함
Not Found 페이지 구현할 때 용이</p>
<pre><code class="language-html">&lt;Swich&gt;
  &lt;Router path=&quot;/&quot; component={Home}/&gt;
  &lt;Router path=&quot;/about&quot; component={About}/&gt;

  &lt;Route
      // path를 따로 정하지 않으면 모든 상황에 렌더링 됨
      render={({location})=&gt;(
      &lt;div&gt;
        &lt;h2&gt;존재하지 않는 페이지 입니다.&lt;/h2&gt;
      &lt;/div&gt;
    )}
   /&gt;
&lt;/Swich&gt;</code></pre>
<h3 id="144-navlink">1.4.4 NavLink</h3>
<p>Link와 비슷함. 현재 경로와 Link에서 사용하는 경로가 일치하는 경우 특정 스타일 or CSS 클래스를 적용 할 수 있음
NavLink 활성화시 스타일을 적용은 activeStyle , CSS 클래스 적용은 activeClassName 값을 props로 넘김</p>