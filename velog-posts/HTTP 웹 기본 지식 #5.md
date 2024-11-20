<blockquote>
<p>#5</p>
</blockquote>
<ul>
<li>HTTP 메서드 활용</li>
<li>HTTP API</li>
</ul>
<h2 id="51-http-메서드-활용">5.1 HTTP 메서드 활용</h2>
<h3 id="511-클라이언트에서-서버로-데이터-전송">5.1.1 클라이언트에서 서버로 데이터 전송</h3>
<ul>
<li>쿼리 파라미터를 통한 데이터 전송<ul>
<li><strong>GET</strong></li>
<li>주로 정렬 필터 (검색어)</li>
</ul>
</li>
<li>메시지 바디를 통한 데이터 전송<ul>
<li><strong>POST, PUT, PATCH</strong>
ex) 회원 가입, 상품 주문, 리소스 등록, 리소스 변경</li>
</ul>
</li>
</ul>
<h3 id="512-전송-상황-4가지">5.1.2 전송 상황 4가지</h3>
<blockquote>
<ul>
<li>정적 데이터 조회</li>
</ul>
</blockquote>
<ul>
<li><p>동적 데이터 조회</p>
</li>
<li><p>HTML Form 데이터 전송</p>
</li>
<li><p>HTTP API 데이터 전송</p>
</li>
<li><p><strong>정적 데이터 조회</strong> <code>ex) 이미지. 정적 텍스트 문서</code></p>
<ul>
<li>GET</li>
<li>정적 데이터는 일반적으로 <strong>쿼리 파라미터 없이</strong> 리소스 경로로 단순하게 조회 가능<img src="https://images.velog.io/images/bell-ho/post/34f96b50-efd3-47f3-b5d1-2b9dc90df8d6/image.png" width="70%" />
</li>
</ul>
</li>
<li><p><strong>동적 데이터 조회</strong></p>
<ul>
<li>GET</li>
<li><strong>쿼리 파라미터를 사용</strong></li>
<li>주로 검색, 게시판 목록에서 정렬 필터(검색어)<img src="https://images.velog.io/images/bell-ho/post/701a2aa4-97f1-4c7e-94ee-c30d11992def/image.png" width="70%" />
</li>
</ul>
</li>
<li><p><strong>HTML Form 데이터 전송</strong></p>
<ul>
<li><p><strong>GET 전송 - 조회</strong></p>
<img src="https://images.velog.io/images/bell-ho/post/ac848ac1-c635-4769-82f0-6583a136d172/image.png" width="70%" />
</li>
<li><p><strong>POST 전송 - 저장</strong></p>
<ul>
<li>HTML Form submit시 POST로 전송하는 경우 
<code>ex) 회원 가입, 상품 주문, 데이터 변경등</code></li>
<li>기본적으로 Content-Type: application/x-www-form-urlencoded 사용<ul>
<li>form의 내용을 메시지 바디를 통해서 key=value 형식으로 전송(쿼리 파라미터 형식)</li>
<li>전송 데이터를 url encoding 처리</li>
</ul>
</li>
</ul>
</li>
</ul>
<img src="https://images.velog.io/images/bell-ho/post/265f3808-7dc1-4273-a360-b1b7f3b41a7d/image.png" width="70%" />

<ul>
<li><strong>multipart/form-data</strong><ul>
<li>Content-Type: multipart/form-data<ul>
<li>파일 업로드 같은 바이너리 데이터 전송시 사용</li>
<li>다른 종류의 여러 파일과 폼의 내용 함께 전송 가능</li>
</ul>
</li>
</ul>
</li>
</ul>
<img src="https://images.velog.io/images/bell-ho/post/0373ace9-09dd-4f57-a791-502700f2cb7c/image.png" width="90%" />
- **참고 : HTML Form 전송은 GET, POST만 지원**
<br /></li>
<li><p><strong>HTTP API 데이터 전송</strong></p>
<ul>
<li>백엔드 시스템 통신</li>
<li>앱 클라이언트 - 아이폰, 안드로이드</li>
<li>웹 클라이언트<ul>
<li>자바스크립트를 통한 통신에 사용(AJAX, AXIOS 등..)</li>
</ul>
</li>
<li>POST, PUT, PATCH : <strong>메시지 바디</strong>를 통해 데이터 전송</li>
<li>GET: 조회, <strong>쿼리 파라미터</strong>로 데이터 전송</li>
<li>Content-Type: application/json 주로 사용</li>
</ul>
<img src="https://images.velog.io/images/bell-ho/post/61982686-93d5-4717-9222-123e95cfd106/image.png" width="60%" />


</li>
</ul>
<h2 id="52-http-api">5.2 HTTP API</h2>
<ul>
<li>HTTP API - 컬렉션 <del><code>서버가 Resource들을 모아두는 곳</code></del><ul>
<li><strong>POST 기반</strong> 등록</li>
<li>ex) 회원 관리 API 제공</li>
</ul>
</li>
<li>HTTP API - 스토어 <del><code>클라이언트가 Resource들을 모아두는 곳</code></del><ul>
<li><strong>PUT 기반</strong> 등록</li>
<li>ex) 정적 컨텐츠 관리, 원격 파일 관리</li>
</ul>
</li>
<li>HTML FORM 사용<ul>
<li>웹 페이지 회원 관리</li>
<li>GET, POST만 지원</li>
</ul>
</li>
</ul>
<p><strong>참고</strong></p>
<ul>
<li>문서(document)<ul>
<li>단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)</li>
<li>ex) /members/100, /files/star.jpg</li>
</ul>
</li>
<li>컬렉션(collection)<ul>
<li>서버가 관리하는 리소스 디렉터리</li>
<li>서버가 리소스의 URI를 생성하고 관리</li>
</ul>
</li>
<li>스토어(store)<ul>
<li>클라이언트가 관리하는 자원 저장소</li>
<li>클라이언트가 리소스의 URI를 알고 관리</li>
</ul>
</li>
<li>컨트롤러(controller), 컨트롤 URI<ul>
<li>문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행</li>
<li>동사를 직접 사용
ex) /members/{id}/delete</li>
</ul>
</li>
</ul>
<h4 id="출처">&lt;출처&gt;</h4>
<p><a href="https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC">모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한</a></p>