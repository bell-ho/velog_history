<h2 id="리액트-라이프-사이클-메서드">리액트 라이프 사이클 메서드</h2>
<p>Will 접두사 : 어떤 작업 전에 실행되는 메소드
Did 접두사 : 어떤 작업 후 실행되는 메소드</p>
<h2 id="11-라이프사이클-종류">1.1 라이프사이클 종류</h2>
<ul>
<li>마운트 <code>페이지에 컴포넌트 등장</code></li>
<li>업데이트 <code>컴포넌트 업데이트</code></li>
<li>언마운트 <code>컴포넌트 소멸</code></li>
</ul>
<h3 id="111-마운트">1.1.1 마운트</h3>
<p><code>DOM이 생성되고 웹 브라우저상에 나타나는 것</code></p>
<blockquote>
<p><strong>메서드 호출 단계</strong></p>
</blockquote>
<ol>
<li>constructor : 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자</li>
<li>getDerivedStateFromProps : props에 있는 값을 state에 넣을 때 사용</li>
<li>render : 화면에 뿌림</li>
<li>componentDidMount : 컴포넌트가 다 뿌려진 후 호출</li>
</ol>
<h3 id="112-업데이트">1.1.2 업데이트</h3>
<p><code>컴포넌트 정보를 업데이트</code></p>
<ul>
<li><strong>업데이트 발생 요건</strong><ul>
<li>부모 컴포넌트에서 전달하는 props가 바뀔 때</li>
<li>자신이 들고 있는 state가 setState로 업데이트 될 때</li>
<li>부모 컴포넌트 리렌더링</li>
<li>this.forceUpdate로 강제로 렌더링을 트리거할 때</li>
</ul>
</li>
</ul>
<blockquote>
<p><strong>메서드 호출 단계</strong></p>
</blockquote>
<ol>
<li>getDerivedStateFromProps</li>
<li>shouldComponentUpdate : 컴포넌트가 리렌더링 할지 안 할지 결정</li>
<li>render</li>
<li>getSnapshotBeforeUpdate : 컴포넌트 변화를 DOM에 반영하기 직전에 호출</li>
<li>componentDidUpdate : 업데이트 작업이 끝난 후 호출</li>
</ol>
<h3 id="113-언마운트">1.1.3 언마운트</h3>
<p><code>컴포넌트를 DOM에서 제거</code></p>
<ol>
<li>componentWillUnmount : 컴포넌트가 사라지기 전에 호출</li>
</ol>