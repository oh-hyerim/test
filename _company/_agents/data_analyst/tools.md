# 📊 Data & Experimentation Analyst — 도구 매니페스트

Data & Experimentation Analyst가 제품 행동 데이터와 실험 결과를 분석하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 기존 데이터 읽기·분석·보고만 가능 |
| 2 | Draft — 지표·실험·분석 초안 작성 가능, 데이터 수집 변경은 검토 필요 |
| 3 | Auto — 승인된 내부 분석 자동 실행 |

Data & Experimentation Analyst는 기본적으로 레벨 2를 사용한다.

내부 데이터 분석과 보고서 작성은 자동화할 수 있다. 새로운 외부 분석 서비스 연결, 개인정보가 포함된 이벤트 추가, 데이터 삭제, 사용자 대상 실험 실행은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Data & Experimentation Analyst에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 지표 정의서
- 이벤트 추적 계획
- 퍼널 분석 설계
- 실험 계획서
- 데이터 분석 보고서
- 데이터 품질 점검표
- 제품 개선 제안

실제 데이터를 확인하지 않았다면 분석 결과를 만들지 않는다.

## 예정 도구

### `event_plan_builder`

제품 가설과 사용자 흐름을 바탕으로 이벤트 추적 계획을 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

이벤트 항목:

- 이벤트명
- 발생 조건
- 필요한 속성
- 제외할 개인정보
- 관련 화면
- 관련 제품 가설
- 분석 목적

### `funnel_analyzer`

사용자 단계별 진입·완료·이탈을 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `retention_analyzer`

사용자의 재방문·유지·이탈을 기간별로 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `routine_usage_analyzer`

루틴 생성·저장·실행·반복 기록을 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

피부 사진이나 상세 건강정보를 분석 이벤트에 포함하지 않는다.

### `experiment_planner`

제품 가설을 검증하기 위한 실험 계획을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `experiment_analyzer`

실험 결과를 비교하고 성공 기준에 따라 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `data_quality_checker`

이벤트 누락·중복·잘못된 속성·기간 오류를 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `privacy_event_auditor`

분석 이벤트에 개인정보·피부정보·건강정보가 불필요하게 포함되었는지 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `report_generator`

분석 결과를 CEO·Product Manager·Business·Designer·Developer가 사용할 수 있는 보고서로 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 외부 분석 서비스 연결

향후 연결할 수 있는 서비스 예시:

- Firebase Analytics
- Google Analytics
- PostHog
- Mixpanel
- 자체 데이터베이스 분석
- Supabase 또는 PostgreSQL 기반 내부 분석

서비스를 연결하기 전 다음을 검토한다.

- 전송되는 데이터
- 사용자 동의와 고지
- 개인정보 포함 여부
- 데이터 보관 기간
- 삭제 요청 반영 여부
- 국외 이전 여부
- 비용과 사용 제한
- Legal & Privacy Advisor 검토 여부

## 승인 필요 행동

- 외부 분석 서비스 연결
- 새로운 개인정보 이벤트 추가
- 실제 사용자 대상 실험 실행
- 사용자에게 불이익을 줄 수 있는 분류 적용
- 운영 데이터 삭제
- 원본 사용자 데이터 외부 전송
- 유료 분석 서비스 사용

## 안전 규칙

- 실제 데이터가 없으면 숫자를 만들지 않는다.
- 개인을 식별할 수 있는 데이터를 분석 보고서에 포함하지 않는다.
- 피부 사진 원본과 건강정보를 이벤트 속성으로 저장하지 않는다.
- 데이터가 부족하면 한계를 명시한다.
- 모든 외부 행동은 `_agents/data_analyst/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
