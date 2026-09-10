# 🧑‍🤝‍🧑 Customer Research — 도구 매니페스트

Customer Research 에이전트가 고객 인터뷰·설문·사용성 테스트·피드백을 계획하고 분석하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 기존 조사 자료 분석만 가능 |
| 2 | Draft — 조사 계획·질문·분석 초안 작성 가능, 외부 접촉은 승인 필요 |
| 3 | Auto — 승인된 범위의 내부 조사 작업 자동 실행 |

Customer Research는 기본적으로 레벨 2를 사용한다.

인터뷰 질문·설문 초안·내부 분석은 자동으로 작성할 수 있다. 실제 사람에게 연락하거나 데이터를 수집하거나 외부 설문을 게시하는 일은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Customer Research 폴더에는 실제로 실행 가능한 전용 조사 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 고객 조사 계획
- 인터뷰 질문지
- 설문 문항
- 사용성 테스트 계획
- 인터뷰 기록 템플릿
- 고객 문제 분류표
- 조사 결과 보고서

실제 인터뷰·설문·사용성 테스트를 수행하지 않았다면 수행했다고 보고하지 않는다.

## 예정 도구

### `interview_guide_builder`

제품 가설과 조사 목적을 바탕으로 인터뷰 질문지를 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

질문은 실제 과거 행동과 구체적인 상황을 확인하는 방향으로 만든다.

### `survey_builder`

고객 문제와 행동 패턴을 확인하기 위한 설문 초안을 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `interview_note_analyzer`

인터뷰 기록에서 고객의 문제·행동·대체 방법·요구·불신 요인을 추출한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

개인 식별 정보는 분석 결과에 불필요하게 포함하지 않는다.

### `customer_problem_coder`

고객 발화를 주제별로 분류하고 반복되는 문제를 찾는다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

분류 결과와 조사자의 해석을 구분한다.

### `usability_test_planner`

프로토타입·MVP 사용성 테스트의 과업·질문·성공 기준을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_if_external_participants_contacted

### `feedback_aggregator`

베타테스트·고객 문의·리뷰·설문 결과를 통합한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_source
- `approval_required`: false

### `customer_segment_analyzer`

고객의 문제·행동·사용 상황을 기준으로 고객군 가설을 비교한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `willingness_to_pay_analyzer`

실제 지출 경험과 행동 신호를 바탕으로 지불 의향 가설을 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

가상의 가격 답변만으로 지불 의향을 확정하지 않는다.

## 조사 참여자와 외부 접촉

다음 행동은 반드시 승인받는다.

- 잠재 고객에게 연락
- 인터뷰 일정 조율
- 설문 게시
- 베타테스터 모집
- 사례비·보상 지급
- 이메일·메신저 발송
- 사용자 사진·피부정보 수집
- 녹음·녹화·전사

## 개인정보·민감정보 원칙

- 조사 목적에 필요한 정보만 수집한다.
- 이름 대신 참여자 ID를 사용한다.
- 피부 사진과 건강정보는 기본적으로 수집하지 않는다.
- 필요한 경우 수집 목적·보관 기간·삭제 방법을 안내한다.
- 원본 녹음·사진·연락처를 조사 보고서에 복사하지 않는다.
- 보고서에는 익명화된 인용만 사용한다.
- 참여자 동의 없이 외부 AI 서비스에 자료를 전송하지 않는다.

## 안전 규칙

- 실제 고객의 피부 상태를 진단하지 않는다.
- 고객에게 치료·제품 사용을 직접 지시하지 않는다.
- 인터뷰 답변을 회사가 원하는 방향으로 편집하지 않는다.
- 표본 수가 적으면 일반화하지 않는다.
- 고객의 말과 조사자의 해석을 구분한다.
- 모든 외부 행동은 `_agents/customer_research/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
