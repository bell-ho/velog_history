<ul>
<li>함수가 호출될 때 this는 호출부에 따라 결정됨</li>
<li>클래스의 임의 메소드가 특정 HTML 요소의 이벤트로 등록되는 과정에서
메소드와 this의 관계가 끊김</li>
<li>이 때문에 임의 메소드가 이벤트로 등록되어도 this를 컴포넌트 자신으로 <strong>제대로 가리키기</strong>   위해 메소드를 this와 바인딩하는 작업이 필요</li>
<li>바인딩하지 않은 경우라면 this가 undefined를 가리키게 됨
<code>자바스크립트는 호출하는 함수에 객체를 바인딩 해주지 않으면 전역 객체로부터 값을 받아옴</code></li>
<li>아래 코드는 constructor에서 함수를 바인딩하는 작업이 이루어지고 있음</li>
</ul>
<pre><code class="language-javascript">constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
}

handleClick(e) {
    alert(this.state.message);
    this.setState({
      message: '',
    });
  }

render() {
    return (
      &lt;div&gt;
        &lt;h1&gt;이벤트 연습&lt;/h1&gt;
        &lt;input
          type=&quot;text&quot;
          name=&quot;message&quot;
        /&gt;
        &lt;button onClick={this.handleClick}&gt;확인&lt;/button&gt;
      &lt;/div&gt;
    );
}</code></pre>
<p>새 메서드를 만들 때마다 constructor도 수정해야 하므로 귀찮음
그래서 <strong>화살표 함수</strong>로 메서드를 만들면 귀찮음 해결
화살표 함수의 this는 인스턴스를 가리키기 때문</p>
<pre><code class="language-javascript">handleClick=(e)=&gt; {
  alert(this.state.message);
  this.setState({
    message: '',
  });
}</code></pre>