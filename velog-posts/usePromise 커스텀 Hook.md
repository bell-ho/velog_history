<pre><code class="language-javascript">//usePromise.js
export default function usePromise(promiseCreator, deps) {
  // 대기/완료/실패에 대한 상태 관리
  const [loading, setLoading] = useState(false);
  const [resolved, setResolved] = useState(null);
  const [error, setError] = useState(null);

  // useEffect에 등록하는 함수는 async로 작성하면 안됨
  // 함수 내부에 async 함수를 따로 만들어야 함
  // useEffect에서 반환하는 함수는 뒷정리 함수이기 때문
  useEffect(() =&gt; {
    const process = async () =&gt; {
      setLoading(true);
      try {
        const resolved = await promiseCreator();
        setResolved(resolved);
      } catch (e) {
        setError(e);
      }
      setLoading(false);
    };
    process();
  }, deps);
  return [loading, resolved, error];
}


//MyComponent.js
const list = ({params}) =&gt;{

    const [loading, response, error] = usePromise(()=&gt;{
        return axios.get('~~~');
    },[params])

    (...)
}</code></pre>