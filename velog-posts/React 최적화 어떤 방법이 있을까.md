<h2 id="11-느려지는-원인-분석">1.1 느려지는 원인 분석</h2>
<p>state가 변경되면서 컴포넌트가 리렌더링됨
부모 컴포넌트 리렌더링 -&gt; 자식컴포넌트 리렌더링 -&gt; 그 안에 무수한 컴포넌트 리렌더링
리렌더링을 안 해도 되는 상황인데 모두 리렌더링되서 느린것</p>
<p>함수형 컴포넌트에서는 컴포넌트를 만들고 나서 React.memo 함수로 감싸주면 최적화 가능</p>
<pre><code class="language-javascript">const MyComponent=({a, funcA, funcB})=&gt;{
    (...)
}

export default React.memo(MyComponent);
// MyComponent를 React.memo 함수로 감싸주면 a, funcA, funcB가 바뀌지 않는 이상 리렌더링 되지 않음</code></pre>
<p><strong>하지만... 여기서 끝이 아니다</strong>
funcA, funcB가 a를 참조한다면 a가 바뀔 때마다 funcA, funcB도 새롭게 만들어짐</p>
<p>해결 방법</p>
<h2 id="12-usestate의-함수형-업데이트">1.2 useState의 함수형 업데이트</h2>
<pre><code class="language-javascript">const [todos, setTodos] = useState([]);

const onInsert = useCallback(text =&gt; {
  const todo = {
      text
  }
  // setTodos(todos.concat(todo)) ; // X
  setTodos(todos =&gt; todos.concat(todo));
},[])</code></pre>
<p>setTodos 함수를 사용할 때 새로운 상태를 파라미터로 넣는 대신
<strong>어떻게 업데이트 하는지 정의하는 함수</strong>를 넣으면 됨
그럼 useCallback 함수의 두 번째 파라미터에 특정 값을 넣지 않아도 됨</p>
<h2 id="13-usereducer-사용">1.3 useReducer 사용</h2>
<pre><code class="language-javascript">function reducer(todos, action){
    switch(action.type){
        case 'insert'
        return  todos.concat(todo);
    }
}

const [todos,dispatch] = useReducer(reducer, []);

const onInsert = useCallback(text =&gt; {
  const todo = {
      text
  };
  dispatch({type:'insert' , todo});
},[])</code></pre>
<p>useReducer를 사용하면 기존 코드를 많이 고쳐야 한다는 단점이 있지만 
로직을 모아서 컴포넌트 바깥에 둘 수 있다는 장점이 있음.</p>
<p><strong>결론</strong>
둘 다 성능이 비슷해서 골라서 사용하면 됨</p>