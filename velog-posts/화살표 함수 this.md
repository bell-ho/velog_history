<p>화살표 함수는 ES6 문법에서 함수를 표현하는 새로운 방식
하지만 기존의 function을 다 대체할 수 없다.
사용 용도가 다르기 때문.</p>
<pre><code class="language-javascript">function blackColor(){
    this.color = '흰색';
    return {
      color : '검은색',
      showColor : function () { //일반 함수
          return this.color; 
      }
    }
}
console.log(new blackColor().showColor()); =&gt; '검은색'

function whiteColor(){
    this.color = '흰색';
    return {
      color : '검은색',
      showColor : ()=&gt; { //화살표 함수
          return this.color;
      }
    }
}
console.log(new whiteColor().showColor()); =&gt; '흰색'</code></pre>
<p><strong>일반 함수의 this</strong>는 <strong>자신이 종속된 객체</strong>를 가리키고, 
<strong>화살표 함수의 this</strong>는 <strong>자신이 종속된 인스턴스</strong>를 가리킨다.</p>
<p>화살표 함수는 값을 연산하여 바로 반환할 때 사용하면 가독성을 높일 수 있다.</p>