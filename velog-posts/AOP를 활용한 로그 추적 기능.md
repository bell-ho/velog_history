<p>aop를 활용하여 메소드 실행중 슬로우 쿼리와 오류 발생시 해당 상황을 로그테이블에 저장하는 기능을 만들어 보았다.</p>
<pre><code class="language-java">@Aspect
@Component
public class LogTraceAspect {

    private static final long SLOW_QUERY_THRESHOLD = 1000; // 슬로우 쿼리 기준
    private final ThreadLocal&lt;Long&gt; startTime = new ThreadLocal&lt;&gt;();

    // 클래스 이름이 서비스인것을 추적
    @Pointcut(&quot;execution(* *..*Service.*(..))&quot;)
    private void allService() {}

    @Before(&quot;allService()&quot;)
    public void beforeMethod() {
        startTime.set(System.currentTimeMillis());
    }

    @After(&quot;allService()&quot;)
    public void afterMethod(JoinPoint joinPoint) {
        long endTime = System.currentTimeMillis();
        long elapsedTime = endTime - startTime.get();

        if (elapsedTime &gt; SLOW_QUERY_THRESHOLD) {
            logSave();
        }
    }

    @AfterThrowing(value = &quot;allService()&quot;, throwing = &quot;exception&quot;)
    public void afterThrowing(JoinPoint joinPoint, Exception exception) {
        logSave();
    }
}</code></pre>
<p>Service 클래스에 있는 특정 기능에 sleep을 걸고 메소드를 실행하였다. log가 잘 저장되었을까</p>
<pre><code class="language-java">    public void delayed() {
        try {
            Thread.sleep(2000);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }</code></pre>
<p>엣 저장 실패</p>
<blockquote>
<p>Connection is read-only. Queries leading to data modification are not allowed</p>
</blockquote>
<p>성능 향상의 이유로 Service 클래스 상단에 @Transactional(readOnly = true) 어노테이션을 해놨는데 로그 저장 메소드를 이용하기 위해선 별도의 트랜잭션이 필요함</p>
<hr />
<p>해결 방법 : 로그 저장시 새로운 트랜잭션을 생성하고 현재 트랜잭션이 있으면 일시 중단하고 로그 저장이 완료되면 원래 트랜잭션 다시 시작</p>
<pre><code class="language-java">    @Override
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void logSave() {
        // 로그 저장..
    }</code></pre>
<blockquote>
<p>@Transactional(propagation = Propagation.REQUIRES_NEW) 사용할 때 주의할 점</p>
</blockquote>
<ol>
<li>리소스 사용 증가 : 새로운 트랜잭션을 시작하려면 추가적인 리소스가 필요하여 성능에 영향을 줄 수 있음</li>
<li>트랜잭션 관리 복잡성 증가 : 두 개 이상의 트랜잭션이 동시에 발생하면 트랜잭션 관리가 복잡해질 수 있음</li>
</ol>
<p>내가 만든 로그 저장 같은 기능은 성능에 큰 영향을 주지 않을거 같음</p>