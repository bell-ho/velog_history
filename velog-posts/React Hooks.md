<blockquote>
</blockquote>
<ul>
<li>useState</li>
<li>useEffect</li>
<li>useReducer</li>
<li>useMemo</li>
<li>useCallback</li>
<li>useRef</li>
</ul>
<h2 id="11-usestate">1.1 useState</h2>
<ul>
<li>useState는 가장 기본적인 Hook</li>
<li>함수형 컴포넌트에서도 <strong>가변적인 상태를 지닐 수 있게</strong> 해 줌</li>
<li>useState()의 파라미터는 상태의 기본값을 넣어줌</li>
<li>useState()를 호출하면 배열을 반환<ul>
<li>배열의 첫 번째는 상태의 기본값</li>
<li>두 번째는 상태를 설정하는 함수</li>
</ul>
</li>
<li>하나의 useState함수는 하나의 상태 값만 관리가능<pre><code class="language-javascript">const [상태값, 상태를 설정하는 함수] = useState(상태의 기본 값);
// ex) const [number, setNumber] = useState(0);</code></pre>
</li>
</ul>
<h2 id="12-useeffect">1.2 useEffect</h2>
<ul>
<li>useEffect는 <strong>컴포넌트가 렌더링될 때마다 특정 작업을 수행</strong>하도록 설정</li>
<li>기본적으로 렌더링 직후에 실행되고 
두 번째 파라미터(배열) 에 뭘 넣느냐에 따라 실행 조건이 달라짐<pre><code class="language-javascript">// 기본
useEffect(()=&gt;{
  doSomthing();
})
</code></pre>
</li>
</ul>
<p>// 마운트될 때만 실행하고 싶을 때는 함수 두 번째 파라미터로 비어 있는 배열을 넣음
useEffect(()=&gt;{
    doSomthing();
},[])</p>
<p>// 특정 값이 변경될 때만 실행하고 싶을 때는 두 번째 파라미터(배열) 안에 특정 값을 넣음
// 배열 안에는 useState로 관리하는 상태를 넣어도 되고, props로 전달받은 값을 넣어도 됨
useEffect(()=&gt;{
    doSomthing();
},[name])</p>
<p>// 컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떤 작업을 수행하고 싶으면
// return을 사용하여 클린업 함수를 반환해야함
useEffect(()=&gt;{
    doSomthing();
    return () =&gt;{
        console.log('clean-up');
    }
},[])</p>
<pre><code>
## 1.3 useReducer
- useReducer는 useState보다 더 다양한 상황에 따라 상태를 다른 값으로 업데이트할 때 사용
- reducer함수는 (~~useReducer 아님~~) **현재 상태**, 그리고 **업데이트를 위해 필요한 정보를 담은 액션값**을 전달받아 **새로운 상태를 반환**하는 함수,
**새로운 상태를 만들 때는 반드시 불변성을 지켜줘야함**
- useReducer의 첫 번째 파라미터는 reducer함수를 넣고, 
두 번째 파라미터는 해당 reducer 기본 상태값을 넣음
- useReducer는 **현재 상태를 가리키는 state**, 
**액션을 발생시키는 dispatch 함수**를 반환하는데
dispatch는 action과 같은 형태로 dispatch 함수 안에 파라미터 값을 넣으면 
reducer 함수가 호출되는 구조

```javascript
const [state, dispatch] = useReducer(reducer, {value:0});

function reducer(state, action){
    switch(action.type){
        case 'plus'
            return {value: state.value + 1};
        case 'minus'
            return {value: state.value - 1};
    }
}

...
    return (
        &lt;div&gt;
            현재 값 : {state.value}
        &lt;/div&gt;
    )
</code></pre><pre><code class="language-html">&lt;button onClick={() =&gt; dispatch({ type:'plus'  })}&gt;증가&lt;/button&gt;
&lt;button onClick={() =&gt; dispatch({ type:'minus' })}&gt;감소&lt;/button&gt;</code></pre>
<h2 id="14-usememo">1.4 useMemo</h2>
<ul>
<li>useMemo를 사용하면 함수형 컴포넌트 내부에서 발생하는 연산을 최적화할 수 있음</li>
<li>렌더링 과정에서 특정 값이 바뀌었을 때만 연산을 실행<pre><code class="language-javascript">const value = useMemo(() =&gt; doSomething(),[특정값])</code></pre>
</li>
</ul>
<h2 id="15-usecallback">1.5 useCallback</h2>
<ul>
<li>useCallback은 useMemo와 비슷한 함수, 주로 렌더링 성능을 최적화해야 하는 상황에 사용</li>
<li>리렌더링 과정에서 함수들이 새로 계속 생성되기 때문에
useCallback를 사용하면 이벤트 핸들러 함수를 필요할 때만 생성할수 있음</li>
<li>useCallback의 첫 번째 파라미터는 <strong>생성하고 싶은 함수</strong>, 두 번째 파라미터는 <strong>배열</strong>
배열에는 특정값을 넣을 수 있고 특정값이 바뀌면 함수가 생성됨 
배열에 아무것도 안넣으면 렌더링될 때 단 한번만 실행됨<pre><code class="language-javascript">const onClick = useCallback(() =&gt; {
  console.log('click');
},[]) // 컴포넌트가 처음 렌더링될 때만 생성
</code></pre>
</li>
</ul>
<p>const onClick = useCallback(() =&gt; {
    console.log('click');
},[특정값]) // 특정값이 바뀌었을 때 생성</p>
<pre><code>
## 1.6 useRef
- useRef는 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있게함
- useRef를 사용하여 만든 객체안에 **current** 값이 실제 엘리먼트를 가리킴
- ref안의 값이 바뀌어도 렌더링되지 않는다
```javascript
const input = useRef(null);
console.log(input.current.value)</code></pre><pre><code class="language-html">&lt;input value=&quot;abc&quot; ref={input}/&gt;</code></pre>