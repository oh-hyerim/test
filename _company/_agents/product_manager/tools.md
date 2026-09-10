# 📋 Product Manager — 도구 매니페스트

Product Manager 에이전트가 제품 요구사항·MVP 범위·우선순위·검증 계획을 관리하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 자료 읽기·분석·보고만 가능 |
| 2 | Draft — 제품 문서·요구사항 초안 작성 가능, 핵심 결정은 승인 필요 |
| 3 | Auto — 허용된 내부 제품 관리 작업 자동 실행 |

Product Manager는 기본적으로 레벨 2를 사용한다.

제품 문서와 업무 초안은 자동으로 만들 수 있다. MVP 범위 확정, 제품 방향 변경, 외부 사용자 테스트 실행, 운영 반영은 CEO 승인 또는 관련 담당자 검토가 필요하다.

## 현재 사용 가능한 기능

현재 Product Manager에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 제품 요구사항
- 사용자 스토리
- MVP 기능 목록
- 기능 우선순위표
- 수용 기준
- 제품 가설
- 사용자 테스트 계획
- 제품 결정 보고서

실제로 업무 추적 시스템이나 프로젝트 파일이 수정되지 않았다면 수정 완료라고 보고하지 않는다.

## 예정 도구

### `requirements_builder`

조사 결과와 사용자 요구를 제품 요구사항으로 변환한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `mvp_scope_manager`

기능을 MVP 포함·후순위·보류로 분류하고 범위 변경을 추적한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_scope_change

### `user_story_builder`

사용자 유형과 목표를 바탕으로 사용자 스토리와 완료 기준을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `acceptance_criteria_builder`

기능별 정상·오류·빈 상태·로딩 상태와 검수 기준을 정의한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `hypothesis_tracker`

제품 가설과 검증 결과를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

관리 항목:

- 가설
- 근거
- 검증 방법
- 성공 기준
- 결과
- 결정
- 다음 액션

### `roadmap_manager`

제품 단계·기능·선행 업무·우선순위를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_scope_change

### `user_test_planner`

프로토타입 또는 MVP 사용자 테스트의 목표·참여자·질문·성공 기준을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_if_external_participants_contacted

### `impact_assessor`

기능 변경이 UX·개발·사업·안전·개인정보에 미치는 영향을 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 조사 협업

다음 정보가 필요하면 Researcher, Customer Research, Business, Skin & Cosmetic Advisor 또는 Developer에게 조사를 요청한다.

- 고객 문제
- 경쟁 서비스
- 가격과 수익모델
- 피부·성분·논문
- 개인정보·안전
- 기술·API·플랫폼 정책

Product Manager가 직접 원문을 확인하지 않았다면 확인한 것처럼 표현하지 않는다.

## 승인 필요 행동

다음 행동은 자동으로 확정하지 않는다.

- MVP 범위의 최종 변경
- 핵심 제품 방향 변경
- 외부 사용자 모집·인터뷰 실행
- 개인정보를 사용하는 사용자 테스트
- 개발·운영 비용이 발생하는 기능 결정
- 외부 서비스 연결
- 출시·배포 결정
- 피부·건강 관련 추천 기준 확정

## 안전 규칙

- 제품 요구사항에 출처 없는 사실을 포함하지 않는다.
- 피부·건강 관련 기능은 전문가·안전 검토 대상을 표시한다.
- 고객 인터뷰 자료에 개인정보를 불필요하게 저장하지 않는다.
- 검증 전 가설을 확정된 요구사항처럼 표현하지 않는다.
- 보류한 기능을 현재 MVP 기능처럼 보고하지 않는다.
- 모든 외부 행동은 `_agents/product_manager/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
