# SEO란?

검색 엔진 최적화(Search Engine Optimization)의 약어로 웹 사이트가 검색 엔진에서 상위에 노출될 수 있도록 최적화하는 과정을 의미한다.

# SEO가 중요한 이유

인터넷 사용자는 정보를 찾을 때 보통 검색 엔진을 사용한다. 검색 엔진에서 상위에 노출된다면 더 많은 트래픽을 유도할 수 있고, 브랜드 인지도를 향상시킬 수 있다. 특히 대부분의 사용자는 검색 결과의 첫 페이지에서 정보를 찾기 때문에 상위 랭킹은 비즈니스 성장과 직결된다.

# SEO 종류

1. 기술적 SEO(Technical SEO)

   웹 사이트의 기술적 측면을 최적화하는 것을 의미한다. 검색 엔진이 웹 사이트의 콘텐츠를 효과적으로 크롤링하고 인덱싱할 수 있게 하는 것에 중점을 둔다.

   - 사이트의 로딩 속도
   - 모바일 친화성
   - xml 사이트맵
   - SSL 보안

2. 온페이지 SEO(On-page SEO) : 웹 페이지 내부의 콘텐츠와 HTML 소스 코드를 최적화하는 것을 의미한다. 콘텐츠를 더 관련성 높고 사용자 친화적으로 만드는 것에 중점을 둔다.
   - 키워드 최적화
   - 콘텐츠 품질
   - 메타 태그
   - 이미지 최적화
3. 오프페이지 SEO(Off-page SEO) : 웹사이트 외부 요소를 최적화하는 것을 의미한다. 주로 백링크 구축에 중점을 둔다.
   - 외부 링크
   - SNS 게시물
   - 다른 웹사이트 프로모션

# CSR과 SEO

대부분 CSR의 단점으로 SEO를 꼽는다. 그 이유는 무엇일까?

CSR은 사용자가 페이지를 요청하면 빈 페이지를 반환하고, 자바스크립트를 다운로드한 뒤에 내용을 동적으로 생성하여 보여준다. 또, 필요한 데이터만 API 서버를 통해 주고받는다.

대부분의 웹 크롤러, 봇들은 자바스크립트를 실행시키지 못하고 HTML 컨텐츠만 수집하기 때문에 빈 페이지를 전달 받는 CSR이 SEO에 불리할 수 있다.

반면, SSR은 서버 측에서 HTML 페이지를 생성하고, 렌더링한 후 클라이언트에 한 번에 제공한다. 때문에 SEO 처리에 필요한 정보들을 미리 입력하면 메타 태그 등에 담아줄 수 있게 된다. React.js의 Next.js나 Vue.js의 Nuxt.js가 이러한 SSR을 쉽게 처리할 수 있도록 도와주는 프레임워크이다.

# 참고

- https://ko.wix.com/blog/post/what-is-seo
- https://brunch.co.kr/@dongdong1/22
- https://brunch.co.kr/@theopenproduct/40
- https://library.gabia.com/contents/domain/4359/
- https://www.hedleyonline.com/ko/blog/seo-image-optimization/
