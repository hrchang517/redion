# REDION 레디온 렌탈몰 — 작업 가이드 (Claude Code용)

렌탈 영업용 단일 페이지 사이트. 빌드 도구 없이 `index.html` 하나로 동작한다 (CSS·JS·로고·배너 이미지가 모두 인라인).

## 구조 (index.html 안)
- `<style>` 맨 위 `:root` 토큰: 색상(`--on` 브랜드 레드, `--ink`, `--muted`, `--line`, `--info` 파랑, `--violet` 보라 등), 폰트(`--display` Gothic A1, `--body` IBM Plex Sans KR, `--mono`, `--brand` Nunito). 라이트/다크 모드 모두 토큰으로 정의 — 색은 토큰으로만 쓴다.
- `<script>` 안 주요 데이터
  - `CONFIG` : 전화번호(1660-2564), 오픈채팅 링크, 담당자명, 상담시간, 사업자번호(**아직 000-00-00000 자리표시**)
  - `PRODUCTS` : 상품 배열. 필드 = `cat`(health|air|big), `catName`, `brand`, `name`, `model`, `price`(월 정가), `years`(약정 연수, 없으면 5), `promo`(행사 문구), `deal`("만원"이면 만원행사, 없고 promo 있으면 반값), `feat`[], `badge`, `url`, `img`/`pid`/`det`(제품 이미지)
  - `ADS` : 상단 광고 슬라이드. `{type:"image"|"video"|"youtube", src|id, alt, link, tab}`. 4초 간격 무한 회전, 터치 시 6초 정지.
  - `ILLUS` : 카테고리별 자체 제작 SVG 일러스트 (제품 사진이 없을 때 대체)
- 팝업 2종: `#sheet` 상담창(입력 검증 후 오픈채팅 이동), `#photo` 제품 사진·상세 팝업(X 버튼 sticky)
- 카테고리 탭: 전체 / 정수기·공기청정기 / 에어컨 / 냉장고·세탁기 / KT 가전구독 / 코웨이 / 쿠쿠 / SK매직 / 반값 / 만원 행사

## 지켜야 할 것
- 가격·약정 표기는 사실대로. 렌탈마인드 표시가(2026-11-06 기준): 삼성·LG(KT 가전구독)=5년(60개월), 코웨이·쿠쿠·SK매직=6년. 확인 안 된 약정을 다른 기간으로 바꿔 쓰지 말 것.
- 반값 문구는 렌탈마인드 기준 "7년 약정 시" 조건. 조건 미확인은 "(조건 상담)".
- 제품 사진/상세 이미지(`assets/p/…`)는 이 폴더에 **포함되어 있지 않다**(브랜드·렌탈마인드 저작물). 사용 허락받은 이미지만 `assets/p/<pid>/t.webp`, `d01.webp…`로 넣을 것. 없으면 카드 썸네일은 자동 숨김, 팝업은 일러스트로 대체됨.
- 브랜드 로고·풍선(`assets/brand/`)은 레디온 자체 자산.
- 헤드라인 폰트: Gothic A1 700, PC 26px / 모바일(≤600px) 20px 고정, 3번째 줄 1.05em.

## 미리보기 / 배포
- 로컬: `npx serve .` → http://localhost:3000 (또는 index.html 더블클릭)
- 배포: Netlify Drop(app.netlify.com/drop)에 폴더 드래그, 또는 `npx netlify deploy --prod --dir .`
