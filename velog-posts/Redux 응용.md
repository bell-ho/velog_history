<p><a href="https://velog.io/@velopert/using-redux-in-2021">Redux 어떻게 써야 잘 썼다고 소문이 날까?</a> 라는 글을 읽던중
<a href="https://velog.io/@velopert/using-redux-in-2021#presentational--container-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%8A%94-%EC%9D%B4%EC%A0%9C-%EA%B7%B8%EB%A7%8C">Presentational &amp; Container 컴포넌트는 이제 그만</a> 을 참고하여 Todos를 만들어 보았다.</p>
<pre><code class="language-javascript">//리덕스의 상태와 액션을 사용하는 Custom Hook을 만들어줌
export function useTodos() {
  const dispatch = useDispatch();
  const { todos, input } = useSelector((state) =&gt; state.todos);

  const onChangeInput = (input) =&gt; {
    dispatch(changeInput(input));
  };
  const onToggle = (id) =&gt; {
    dispatch(toggle(id));
  };
  const onRemove = (id) =&gt; {
    dispatch(remove(id));
  };
  const onInsert = (text) =&gt; {
    dispatch(insert(text));
  };
  return { input, todos, onChangeInput, onToggle, onRemove, onInsert };
}</code></pre>
<pre><code class="language-javascript">const Todos = () =&gt; {
  const { input, todos, onChangeInput, onToggle, onRemove, onInsert } = useTodos(); // 커스텀 훅 적용

  const onSubmit = (e) =&gt; {
    e.preventDefault();
    onInsert(input);
    onChangeInput('');
  };

  const onChange = (e) =&gt; onChangeInput(e.target.value);

  return (
    &lt;div&gt;
      &lt;form onSubmit={onSubmit}&gt;
        &lt;input value={input} onChange={onChange} type=&quot;text&quot; /&gt;
        &lt;button type=&quot;submit&quot;&gt;등록&lt;/button&gt;
      &lt;/form&gt;
      &lt;div&gt;
        {todos.map((todo) =&gt; (
          &lt;TodoItem todo={todo} key={todo.id} onToggle={onToggle} onRemove={onRemove} /&gt;
        ))}
      &lt;/div&gt;
    &lt;/div&gt;
  );
};</code></pre>
<p>직접 만들어보니 프리젠테이션과 컨테이너를 분리하지 않고 하나의 컴포넌트로 하는게 더 편하다.</p>