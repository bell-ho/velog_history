<p>유투브 보다가 팁 발견</p>
<pre><code class="language-javascript">
for in 문 활용법

const person = { name:'p1', age:1 , good:false};

for(const p in person){
    console.log(p);
  // name
  // age
  // good
}

객체 key를 뽑아내기 쉽다

이런것도 가능
if('name' in person){
    true;
}
// true;</code></pre>
<p>출처 : <a href="https://www.youtube.com/watch?v=VgMJFzZQBjQ&amp;ab_channel=ZeroChoTV">제로초 : 잘 모르는 &quot;간단한&quot; 자바스크립트 문법 5가지</a></p>