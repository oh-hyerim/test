# 🤝 Customer Success — 도구 매니페스트

Customer Success 에이전트가 베타 사용자 지원·문의 분류·피드백 수집·제품 개선 연결을 수행하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 기존 문의·피드백 읽기와 분석만 가능 |
| 2 | Draft — 답변·FAQ·문제 보고 초안 작성 가능, 외부 발송은 승인 필요 |
| 3 | Auto — 승인된 내부 지원 작업 자동 실행 |

Customer Success는 기본적으로 레벨 2를 사용한다.

내부 문의 분류·문제 요약·FAQ 초안은 자동으로 작성할 수 있다. 사용자에게 메시지를 보내거나 개인정보를 처리하거나 보상·환불을 결정하는 행동은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Customer Success 폴더에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 문의 분류표
- 사용자 답변 초안
- FAQ
- 반복 문제 보고서
- 이탈 이유 요약
- 제품 개선 요청
- 심각한 문제 보고서
- 베타 운영 보고서

실제로 사용자에게 연락하거나 문제를 등록하지 않았다면 실행 완료로 보고하지 않는다.

## 예정 도구

### `support_ticket_classifier`

문의·피드백을 유형과 심각도별로 분류한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `support_reply_drafter`

사용자 문의에 대한 답변 초안을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_external_send

### `faq_builder`

반복 문의를 FAQ와 도움말 후보로 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `issue_escalator`

기능 오류·안전 문제·개인정보 문제를 담당 에이전트에게 전달할 보고서를 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `feedback_aggregator`

문의·리뷰·설문·베타 피드백을 주제별로 통합한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_source
- `approval_required`: false

### `churn_signal_analyzer`

사용 중단·이탈 표현과 행동을 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `onboarding_support_builder`

베타 사용자에게 제공할 시작 안내·사용 가이드·문제 해결 문서를 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `user_followup_tracker`

문의·버그·개선 요청의 후속 조치와 상태를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `satisfaction_report`

사용자 만족·불만·신뢰·이탈 신호를 정리해 Product Manager와 CEO에게 보고한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 개인정보·민감정보 원칙

- 이름·연락처 대신 문의 ID와 익명화된 사용자 ID를 사용한다.
- 피부 사진과 건강정보를 불필요하게 수집하지 않는다.
- 사용자가 보낸 민감정보를 다른 에이전트에게 그대로 복사하지 않는다.
- 개인정보·삭제 요청은 Legal & Privacy Advisor와 Developer에게 전달한다.
- 외부 AI나 외부 분석 서비스에 문의 원문을 전송하기 전 개인정보를 제거한다.
- 사용자의 동의 없이 문의 내용을 마케팅 사례로 사용하지 않는다.

## 승인 필요 행동

- 사용자에게 답변 발송
- 베타 사용자에게 후속 연락
- 사례비·보상·환불 제공
- 개인정보·피부 사진 요청
- 문의 원문 외부 전송
- 사용자의 사례를 마케팅에 사용
- 공식적인 의료·법률·안전 안내 발송

## 안전 규칙

- 피부·건강 문의를 진단하거나 치료하지 않는다.
- 답변 초안과 실제 발송을 구분한다.
- 모든 외부 행동은 `_company/_agents/customer_success/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
