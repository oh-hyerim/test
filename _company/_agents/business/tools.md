# 💼 Business — 도구 매니페스트

Business 에이전트가 사업성, 수익모델, 가격, 경쟁 서비스와 실제 매출을 분석하는 데 사용하는 도구를 정의한다.

---

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 읽기·분석·보고만 가능 |
| 2 | Draft — 분석 초안 작성, 외부 행동은 승인 필요 |
| 3 | Auto — 허용된 내부 작업 자동 실행 |

Business는 기본적으로 **레벨 2**를 사용한다.

공개 자료 검색, 내부 분석, 보고서 작성은 자동으로 진행할 수 있다. 결제, 계약, 외부 연락, 광고 집행, 실제 가격 변경은 반드시 승인받는다.

---

## 사용 가능한 도구

### `paypal_revenue`

PayPal 거래 데이터를 가져와 실제 매출을 분석한다.

- `enabled`: true
- `requires_credentials`: true
- `autonomy`: read_and_analyze
- `approval_required`: false

분석 항목:

- 총매출
- 환불액
- 수수료
- 순매출
- 거래 수
- 통화별 매출
- 기간별 추세
- 최근 거래
- 환불률
- 다음 액션

실제 데이터가 없거나 인증이 실패하면 숫자를 추정하지 않는다.

---

### `mobile_payment_compare` _(예정)_

Google Play, Apple App Store 및 국내 결제 시스템의 수수료·정산·구독·환불 구조를 비교한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

비교 대상:

- Google Play Billing
- Apple In-App Purchase
- 토스페이먼츠
- 카카오페이
- 네이버페이
- PortOne

---

## 조사 위임 요청

현재 실제 검색 도구가 연결되지 않은 경우에도, 외부 조사가 필요한 업무는 다음 형식으로 조사 요청을 생성한다.

### `market_research_request`

시장·경쟁사·고객·가격 관련 조사를 요청한다.

- `enabled`: planned
- `status`: implementation_required
- `requires_credentials`: depends_on_search_provider
- `approval_required`: false

요청 항목:

- 조사 주제
- 조사 목적
- 핵심 질문
- 조사 대상
- 필요한 최신성
- 필요한 출처 수준
- 원하는 결과물
- 제품 의사결정과의 연결

---

### `competitor_pricing_compare`

경쟁 서비스의 가격·기능·무료/유료 구성을 비교한다.

- `enabled`: planned
- `status`: implementation_required
- `requires_credentials`: depends_on_search_provider
- `approval_required`: false

비교 항목:

- 서비스명
- 주요 고객
- 핵심 기능
- 무료 기능
- 유료 기능
- 가격
- 구독 주기
- 체험 기간
- 추천·제휴 구조
- 확인 날짜
- 출처 링크

---

### `customer_signal_analysis`

앱스토어 리뷰, 공개 커뮤니티, 인터뷰 결과 등에서 고객의 불편과 지불 신호를 분석한다.

- `enabled`: planned
- `status`: implementation_required
- `requires_credentials`: depends_on_source
- `approval_required`: false

분석 항목:

- 반복되는 고객 문제
- 문제의 심각도
- 현재 대체 방법
- 지불 의향 신호
- 이탈 이유
- 원하는 기능
- 근거 출처

---

## 예정 도구

### `analytics_pull`

웹 또는 앱 분석 데이터에서 가입, 전환, 재방문, 이탈 데이터를 가져온다.

- `enabled`: false
- `status`: planned

### `revenue_pull`

Stripe, Toss 등 다른 결제 채널의 매출을 가져온다.

- `enabled`: false
- `status`: planned

### `pnl_generator`

매출·비용 데이터를 이용해 월별 손익 초안을 작성한다.

- `enabled`: false
- `status`: planned

### `unit_economics`

고객획득비용, 고객생애가치, 전환율, 유지율을 바탕으로 단위경제성을 계산한다.

- `enabled`: false
- `status`: planned

---

## 조사 결과 처리 원칙

조사 결과는 다음을 구분한다.

- 확인된 사실
- 업체 또는 출처의 주장
- Business의 해석
- 추정값
- 아직 확인되지 않은 내용

경쟁사 가격이나 기능을 조사할 때는 확인 날짜와 출처를 반드시 기록한다.

---

## 승인 필요 행동

다음 행동은 자동으로 실행하지 않는다.

- 실제 가격 변경
- 유료 플랜 개설 또는 폐지
- 결제 서비스 연결
- 광고비 집행
- 제휴 계약
- 외부 업체에 연락
- 사용자의 개인정보를 활용한 사업 분석
- 투자자·파트너·고객에게 공식 자료 발송

---

## 안전 규칙

- 외부 API 호출 전 자격증명과 비용 발생 여부를 확인한다.
- 비공개 매출·고객·경쟁사 정보를 추정해서 사실처럼 표현하지 않는다.
- 출처 없는 숫자를 만들지 않는다.
- 건강·피부 관련 서비스의 수익성을 검토할 때 안전성과 신뢰도를 우선한다.
- 제휴 수익과 추천 순위의 이해상충을 CEO와 QA & Safety에 보고한다.
- 모든 외부 행동은 `_agents/business/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
