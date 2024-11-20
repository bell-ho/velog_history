<p>style을 적용할 때 인라인 스타일을 이용할 때가 많았다 (<del>편하니까</del>)</p>
<pre><code class="language-html">&lt;div style={{ width:100px }}&gt;
    &lt;h1&gt;자바스크립트&lt;/h1&gt;      
&lt;/div&gt;</code></pre>
<p>이런식으로..</p>
<p>하지만 인라인식으로 작성하게 되면 불필요한 리랜더링을 하게 된다. <strong>이유는?</strong>
결론부터 말하면 {} === {} 가 false 이기 때문!
리액트의 버추얼돔이 검사를 하면서 어디가 달라졌는지 찾다가
이전 값과 비교했을때 다른 객체로 인식하기 때문에 리랜더링을 하게된다.
=&gt; 규모가 큰 웹이나 앱이면 성능이 느려짐.</p>
<h3 id="개선방법">개선방법</h3>
<ul>
<li>useMemo 사용하기<ul>
<li><pre><code class="language-javascript">const style = useMemo(() =&gt; ({ width: 100px }), []);</code></pre>
</li>
</ul>
</li>
<li>styled-components 사용하기<ul>
<li><pre><code class="language-javascript">const CustomDiv = styled.div`width:100px`; </code></pre>
</li>
</ul>
</li>
</ul>
<p>위의 방법을 통해 리랜더링 문제를 최적화 할 수 있다~</p>