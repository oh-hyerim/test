# ⚖️ Legal & Privacy Advisor — 도구 매니페스트

Legal & Privacy Advisor가 개인정보·법률·규제·플랫폼 정책·외부 서비스 데이터 처리를 검토하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 공식 자료 읽기·분석·보고만 가능 |
| 2 | Draft — 내부 검토·리스크 보고서 작성 가능, 법률 확정은 전문가 검토 필요 |
| 3 | Auto — 승인된 내부 점검 자동 실행 |

Legal & Privacy Advisor는 기본적으로 레벨 2를 사용한다.

공개 법령·정책 자료의 조사와 내부 검토 보고서는 자동화할 수 있다. 변호사 선임·계약·공식 신고·외부 연락·법률 문서 최종 확정은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Legal & Privacy Advisor에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 데이터 수집 목록
- 개인정보 흐름도
- 동의·권한 검토표
- 법률·규제 조사 요청
- 개인정보 처리방침 요구사항
- 이용약관 요구사항
- 외부 서비스 검토표
- 리스크 보고서
- 전문가 검토 요청서
- 출시 전 법률·개인정보 체크리스트

실제로 최신 법령이나 정책을 확인하지 않았다면 확인 완료로 보고하지 않는다.

## 예정 도구

### `regulation_search`

법령·정부기관·공공기관·규제기관의 공식 자료를 검색한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: false

검색 시 적용 지역·날짜·자료 유형을 기록한다.

### `policy_fetcher`

공식 플랫폼·외부 서비스·앱스토어 정책의 원문과 수정일을 수집한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `privacy_data_mapper`

앱에서 수집·저장·전송하는 데이터의 흐름을 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

항목:

- 데이터 종류
- 수집 시점
- 수집 목적
- 저장 위치
- 접근 주체
- 외부 전송
- 보관 기간
- 삭제 방법
- 사용자 안내와 동의

### `consent_flow_checker`

회원가입·권한·사진 업로드·분석·제3자 전송 동의 흐름을 검토한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `privacy_policy_outline`

개인정보 처리방침에 필요한 항목의 초안을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

법률 문서의 최종본을 자동 확정하지 않는다.

### `terms_outline`

이용약관에 포함되어야 할 서비스 범위·책임·이용자 의무·계정·탈퇴 관련 항목을 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `medical_claim_checker`

진단·치료·효과 보장·의료행위로 오해될 가능성이 있는 표현을 찾는다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

이 도구는 의료·법률 전문가의 최종 검토를 대체하지 않는다.

### `third_party_data_audit`

Supabase·Firebase·Google·AI API·분석·결제 서비스의 데이터 처리 위험을 비교한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `risk_register`

법률·개인정보·규제 위험을 심각도·담당자·완료 기준과 함께 기록한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `expert_review_request`

변호사·개인정보 전문가·피부과 전문의 등 외부 전문가에게 검토할 질문과 자료를 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_if_external_contacted

## 승인 필요 행동

- 변호사·전문가에게 연락
- 법률 자문 계약
- 개인정보 처리방침·이용약관 최종 확정
- 정부·플랫폼·기관에 공식 제출
- 외부 서비스 계약·위탁·결제
- 사용자에게 법률·의료 관련 공식 안내 게시
- 실제 사용자 개인정보를 외부 검토 서비스에 전송

## 안전 규칙

- 법률적 확정 표현을 사용하지 않는다.
- 적용 지역과 날짜가 불명확한 정책을 현재 기준으로 단정하지 않는다.
- 피부 사진·건강정보·개인정보를 검토 보고서에 불필요하게 포함하지 않는다.
- 공식 자료와 전문가 의견과 추정을 구분한다.
- 모든 외부 행동은 `_agents/legal_privacy/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
