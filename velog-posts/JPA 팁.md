<ol>
<li>엔티티 매핑 최적화</li>
</ol>
<p>엔티티 클래스와 데이터베이스 테이블 간의 매핑을 최적화하는 것은 JPA 성능 향상에 매우 중요합니다.</p>
<p>필드 매핑: 필요하지 않은 필드는 매핑하지 않도록 합니다. 
모든 데이터베이스 열을 엔티티 필드로 매핑하면 메모리 사용량과 성능에 영향을 미칩니다.</p>
<p>Fetch Type 설정: 연관 관계를 매핑할 때 지연 로딩(LAZY)을 기본으로 사용하고, 
즉시 로딩(EAGER)은 꼭 필요한 경우에만 사용합니다.
지연 로딩은 실제로 데이터가 필요할 때 로드되므로 성능이 향상됩니다.</p>
<pre><code class="language-java">@Entity
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = &quot;category_id&quot;)
    private Category category;
}</code></pre>
<ol start="2">
<li>Query Optimization</li>
</ol>
<p>JPQL 사용: 필요한 데이터만 선택하여 불필요한 데이터를 가져오지 않도록 합니다.</p>
<p>Pagination: 대량의 데이터를 처리할 때는 페이징 처리를 통해 한 번에 가져오는 데이터 양을 제한합니다.</p>
<pre><code class="language-java">public List&lt;Product&gt; findProducts(int page, int size) {
    return entityManager.createQuery(&quot;SELECT p FROM Product p&quot;, Product.class)
        .setFirstResult(page * size)
        .setMaxResults(size)
        .getResultList();
}</code></pre>
<ol start="3">
<li>2차 캐시 활용
JPA의 2차 캐시(Second Level Cache)를 활용하면 동일한 데이터를 여러 번 조회할 때 
데이터베이스 액세스를 줄일 수 있습니다. 
Hibernate에서는 ehcache, infinispan 등을 사용하여 2차 캐시를 설정할 수 있습니다.</li>
</ol>
<pre><code class="language-java">&lt;!-- persistence.xml --&gt;
&lt;property name=&quot;hibernate.cache.use_second_level_cache&quot; value=&quot;true&quot;/&gt;
&lt;property name=&quot;hibernate.cache.region.factory_class&quot; value=&quot;org.hibernate.cache.jcache.JCacheRegionFactory&quot;/&gt;
&lt;property name=&quot;hibernate.javax.cache.provider&quot; value=&quot;org.ehcache.jsr107.EhcacheCachingProvider&quot;/&gt;</code></pre>