<p>띄어쓰기는 자손
<code>&gt;</code> 는 첫번째 자식</p>
<pre><code class="language-css">nav ul {

}

nav &gt; ul &gt; li &gt; a {

}</code></pre>
<p>인접 형제 선택자 A + B A 근접 B만
A 뒤에 따라오는 B는 전부 A ~ B</p>
<pre><code class="language-css">h1 + ul {

}

h2 ~ ul {

}</code></pre>
<p>자식 요소중 포커스에 걸리면</p>
<pre><code class="language-css">form:focus-within{

}</code></pre>