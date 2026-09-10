# 🤖 AI & Recommendation Specialist — 도구 매니페스트

AI & Recommendation Specialist가 AI 분석·추천 기능을 설계·평가·변경 관리하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 모델·결과·자료 읽기와 분석만 가능 |
| 2 | Draft — AI 명세·평가·변경안 작성 가능, 운영 적용은 승인 필요 |
| 3 | Auto — 승인된 평가·모니터링 작업 자동 실행 |

AI & Recommendation Specialist는 기본적으로 레벨 2를 사용한다.

AI 명세·테스트 계획·평가 보고서·변경 제안은 자동 작성할 수 있다. 모델 변경·프롬프트 변경·추천 로직 변경·사용자 데이터 사용·운영 반영은 승인 대상이다.

## 현재 사용 가능한 기능

현재 전용 AI·추천 도구가 연결되어 있지 않을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- AI 기능 명세
- 입력·출력 스키마
- 추천 기준서
- 프롬프트 초안
- 평가 데이터셋 계획
- 테스트 케이스
- 평가 보고서
- 오류 사례
- 변경 제안서
- 안전 검토 요청서

실제로 모델을 실행하거나 평가하지 않았다면 실행 완료로 보고하지 않는다.

## 예정 도구

### `ai_feature_spec_builder`

AI 기능의 목적·입력·출력·한계·실패 조건을 정의한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `recommendation_rule_builder`

제품·성분·루틴 추천 기준과 우선순위 초안을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_logic_change

### `prompt_version_manager`

프롬프트 버전·변경 이유·평가 결과·롤백 정보를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_production_change

### `evaluation_dataset_builder`

AI 평가를 위한 익명화된 테스트 케이스와 기대 결과를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

실제 사용자 피부 사진은 기본적으로 사용하지 않는다.

### `ai_evaluator`

정확성·일관성·안전성·거부 적절성·설명 가능성을 평가한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_model_provider
- `approval_required`: false

### `recommendation_consistency_checker`

같은 조건에서 추천 결과가 과도하게 달라지는지 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_model_provider
- `approval_required`: false

### `hallucination_checker`

근거 없는 성분 효능·제품 정보·연구 결과를 생성하는지 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_model_provider
- `approval_required`: false

### `safety_refusal_checker`

진단·치료·고위험 질문에 적절히 제한하거나 전문가 안내를 제공하는지 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_model_provider
- `approval_required`: false

### `bias_auditor`

피부톤·연령·성별·환경·촬영 조건에 따른 성능 차이를 검토한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `model_change_comparator`

기존 모델·프롬프트·추천 기준과 변경안의 결과를 비교한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_model_provider
- `approval_required`: true_for_production_change

### `ai_cost_latency_monitor`

AI 호출 비용·응답 시간·실패율·재시도율을 모니터링한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: false

### `recommendation_explanation_builder`

추천 이유·근거·한계·주의사항을 사용자에게 설명하는 구조를 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 데이터 원칙

- 평가 데이터는 가능한 한 익명화·가명화한다.
- 피부 사진 원본을 기본 평가 데이터로 사용하지 않는다.
- 실제 사용자 데이터를 사용할 경우 Legal & Privacy Advisor와 QA & Safety 검토를 받는다.
- 평가 데이터와 운영 데이터를 구분한다.
- 테스트 결과에 실제 이름·연락처·피부 사진을 포함하지 않는다.
- 외부 AI 서비스로 데이터를 보내기 전 전송 범위를 확인한다.

## 승인 필요 행동

- 모델 변경
- 프롬프트의 운영 버전 변경
- 추천 점수·순위·제외 기준 변경
- 실제 사용자 데이터 사용
- 피부 사진 외부 전송
- 유료 AI API 사용
- 사용자에게 표시되는 AI 결과 구조 변경
- 운영 환경 반영
- AI 결과에 따른 자동화된 사용자 조치

## 안전 규칙

- AI의 성능과 안전성을 테스트 없이 보장하지 않는다.
- AI 생성 결과와 검증된 사실을 구분한다.
- 추천 기준 변경은 근거·평가·승인 기록을 남긴다.
- 고위험 질문에 확정적인 답변을 하지 않는다.
- 모든 외부 행동은 `_company/_agents/ai_recommendation/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
