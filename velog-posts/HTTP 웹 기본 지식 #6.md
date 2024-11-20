<blockquote>
<p>#6</p>
</blockquote>
<ul>
<li>HTTP 상태코드</li>
</ul>
<h2 id="11-상태-코드">1.1 상태 코드</h2>
<p><strong>클라이언트의 요청</strong>에 대한 상태를 <strong>서버가</strong> 알려주는 기능</p>
<ul>
<li>1xx (Informational): 요청이 수신되어 처리중 (<del>사용 잘 안함</del>)</li>
<li>2xx (Successful): 요청 <strong>정상</strong> 처리</li>
<li>3xx (Redirection): 요청을 완료하려면 추가 행동이 필요</li>
<li>4xx (Client Error): <strong>클라이언트 오류</strong>, 서버가 클라이언트의 요청을 수행할 수 없음 </li>
<li>5xx (Server Error): <strong>서버 오류</strong>, 서버가 정상 요청을 처리하지 못함</li>
</ul>
<h3 id="111-2xxsuccessful">1.1.1 2xx(Successful)</h3>
<p>클라이언트의 요청을 성공적으로 처리함</p>
<ul>
<li>200 OK : 요청 성공</li>
<li>201 Created : 요청을 성공해서 새로운 리소스가 생성됨 <code>Location 헤더필드로 식별</code></li>
<li>202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음</li>
<li>204 No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음</li>
</ul>
<h3 id="112-3xxredirection">1.1.2 3xx(Redirection)</h3>
<p>요청을 완료하기 위해 유저 에이전트(<del>클라이언트 프로그램 , 거의 웹 브라우저</del>)의 추가 조치 필요
웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동</p>
<p><strong>Redirection 종류</strong></p>
<ul>
<li>영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동<ul>
<li>301 Moved Permanently<ul>
<li>리다이렉트시 요청 메서드가 <strong>GET으로 변하고</strong>, <strong>본문이 제거될 수 있음</strong>
<code>ex) 게시판 등록을 했는데 URL이 변경된 경우 목록이나 글쓰기 화면으로 보냄</code></li>
</ul>
</li>
<li>308 Permanent Redirect<ul>
<li>301과 기능은 같지만 <strong>요청 메서드와 본문을 유지함</strong><br /></li>
</ul>
</li>
</ul>
</li>
<li>일시 리다이렉션 : 
리소스의 URI가 일시적인 변경
PRG: Post/Redirect/Get<ul>
<li>302 Found<ul>
<li>리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음</li>
</ul>
</li>
<li>307 Temporary Redirect<ul>
<li>리다이렉트시 요청 메서드와 본문 유지</li>
</ul>
</li>
<li>303 See Other<ul>
<li>리다이렉트시 요청 메서드가 GET으로 변경 (302와 기능 같음)
<code>ex) POST 주문후에 결과화면을 GET으로 리다이렉트 하기때문에 중복 불가</code> <h3 id="113-4xx-client-error">1.1.3 4xx (Client Error)</h3>
</li>
</ul>
</li>
</ul>
</li>
<li>오류의 원인이 클라이언트에 있음 <code>ex) 잘못된 문법 등..</code></li>
<li><strong>클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같이 재시도해도 실패함</strong> 
(<del>서버는 재시도하면 성공할 수도 있음</del>)</li>
</ul>
<p><strong>4xx 종류</strong></p>
<ul>
<li>400 Bad Request : 클라이언트의 잘못된 요청에 의해 서버가 처리할 수 없음<ul>
<li>`ex) 요청 구문, 메시지 오류 =&gt; 클라이언트가 다시 검토하고 재시도 해야함</li>
</ul>
</li>
<li>401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증이 필요함</li>
<li>403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함<ul>
<li><code>ex) 로그인은 했지만 관리자 기능은 쓰지 못함</code></li>
</ul>
</li>
<li>404 Not Found : 요청 리소스를 찾을 수 없음</li>
</ul>
<h3 id="114-5xx-server-error">1.1.4 5xx (Server Error)</h3>
<ul>
<li>서버 문제로 오류 발생</li>
<li>서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음</li>
</ul>
<p><strong>5xx 종류</strong></p>
<ul>
<li>500 Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류</li>
<li>503 Service Unavailable : 서비스 이용 불가
<code>ex) 서버가 일시적인 과부하, 예정된 작업으로 잠시 요청을 처리할 수 없을 때</code></li>
</ul>