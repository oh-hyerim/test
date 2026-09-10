# 🗃️ Knowledge Curator — 도구 매니페스트

Knowledge Curator가 회사 지식·근거·출처·업데이트·충돌을 관리하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 지식과 출처 읽기·분석만 가능 |
| 2 | Draft — 업데이트 초안과 검토 요청 작성 가능, 공식 반영은 승인 필요 |
| 3 | Auto — 승인된 범위에서 지식 정리와 모니터링 자동 실행 |

Knowledge Curator는 기본적으로 레벨 2를 사용한다.

자료 메타데이터 정리·중복 제거·업데이트 후보 작성은 자동화할 수 있다. 공식 지식 변경·추천 기준 변경·제품 문구 변경은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Knowledge Curator에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 지식 항목
- 출처 기록
- 기존 지식 비교표
- 업데이트 후보
- 충돌 보고서
- 검토 요청서
- 변경 이력
- 재검토 목록

실제 지식베이스가 수정되지 않았다면 공식 반영 완료로 보고하지 않는다.

## 예정 도구

### `knowledge_indexer`

조사 보고서·논문·공식 자료에서 지식 항목과 출처를 추출한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `source_registry`

지식 항목의 원문 URL·저자·기관·발표일·확인일·자료 유형을 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `duplicate_detector`

새 자료와 기존 자료·지식 항목의 중복 여부를 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `knowledge_comparator`

새 자료와 기존 지식의 관계를 같은 내용·보완·부분 충돌·중대한 충돌·무관으로 분류한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `confidence_assessor`

출처·근거 수준·최신성·독립성·연구 품질을 바탕으로 신뢰도를 평가한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `update_proposal_builder`

새 자료를 공식 지식에 반영할지에 대한 업데이트 초안을 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `conflict_tracker`

기존 지식과 새로운 연구·정책·자료의 충돌을 기록하고 담당 검토자를 지정한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `knowledge_version_manager`

공식 지식의 버전·변경 이유·승인·영향 범위를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_for_official_update

### `review_workflow`

Skin & Cosmetic Advisor·QA & Safety·Legal & Privacy Advisor·CEO의 검토 상태를 추적한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `staleness_monitor`

오래된 지식·재검토 기한·정책 변경 가능성이 있는 항목을 표시한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `impact_mapper`

지식 변경이 추천 로직·제품 문구·기능·안전 기준에 미치는 영향을 연결한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 공식 반영 기준

다음 조건을 만족하지 않으면 공식 지식으로 반영하지 않는다.

- 출처와 원문이 확인됨
- 기존 지식과 비교됨
- 신뢰도와 한계가 기록됨
- 필요한 전문 검토가 완료됨
- 제품 영향이 평가됨
- 승인 주체와 날짜가 기록됨
- 변경 이력이 남음

## 승인 필요 행동

- 공식 지식 변경
- 기존 지식 삭제·폐기
- 추천 로직 변경 요청 확정
- 사용자 문구 변경 요청 확정
- 안전·의료·법률 기준 변경
- 외부 전문가에게 검토 자료 발송

## 안전 규칙

- 원문과 요약을 구분한다.
- 공식 지식과 참고 메모를 구분한다.
- 충돌하는 자료를 임의로 하나로 합치지 않는다.
- 승인되지 않은 변경을 다른 에이전트가 확정 기준처럼 사용하지 않게 한다.
- 모든 외부 행동은 `_agents/knowledge_curator/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
