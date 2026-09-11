# 🧴 Skin & Cosmetic Advisor — 도구 매니페스트

Skin & Cosmetic Advisor가 피부·화장품·성분·논문을 조사하고 지식 업데이트를 관리하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 자료 읽기·분석·보고만 가능 |
| 2 | Draft — 자문·지식 업데이트 초안 작성 가능, 기준 변경은 승인 필요 |
| 3 | Auto — 승인된 범위의 자료 감시와 내부 정리 자동 실행 |

이 에이전트는 기본적으로 **레벨 2**를 사용한다.

논문 검색·원문 확인·내부 자문 보고서 작성은 자동화할 수 있다. 추천 로직 변경·사용자 문구 확정·외부 전문가 연락은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Skin & Cosmetic Advisor에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 논문 조사 요청
- 성분 근거 보고서
- 피부 고민별 근거 정리
- 추천 기준 검토
- 안전 문구 검토
- 지식 업데이트 초안
- 외부 전문가 검토 요청

실제로 논문·원문을 확인하지 않았다면 확인 완료로 보고하지 않는다.

## 조사 협업 도구

### `paper_search`

피부·화장품·성분 관련 논문을 검색한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: false

우선 자료원:

- PubMed
- Europe PMC
- Crossref
- Semantic Scholar
- 학술지·학회 공식 자료

### `paper_reader`

논문의 초록 또는 접근 가능한 원문을 읽고 연구 구조와 결과를 추출한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: false

초록과 전체 원문을 반드시 구분한다.

### `paper_quality_assessor`

연구 유형·표본·대조군·한계·이해관계를 바탕으로 연구 품질을 평가한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `ingredient_evidence_lookup`

성분의 기능·근거·주의사항·연구 자료를 조회한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_source
- `approval_required`: false

### `evidence_compare`

새 연구와 기존 지식·다른 연구를 비교한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `safety_rule_checker`

성분·제품·루틴 관련 주의사항과 위험 가능성을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

이 도구는 의료 전문가의 최종 판단을 대체하지 않는다.

### `knowledge_update_draft`

새로운 연구를 기존 지식과 비교해 업데이트 초안을 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

출력:

- 새 주장
- 근거 자료
- 기존 지식과의 관계
- 신뢰도
- 안전 영향
- 추천 기준 변경 여부
- 검토 담당자
- 반영 보류 사유

### `advisory_report`

제품·문구·추천 기준에 대한 전문 자문 보고서를 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 정기 모니터링

### `literature_monitor`

새로운 피부·화장품 관련 논문과 공식 자료를 정기적으로 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: false

새 자료 발견은 자동화할 수 있지만, 제품 기준 변경은 자동화하지 않는다.

## 지식 반영 규칙

다음은 자동 반영하지 않는다.

- 추천 점수 변경
- 제품 제외 기준 변경
- 사용자에게 표시되는 안전 문구 변경
- 치료·효과 관련 표현 변경
- 새로운 성분의 안전성 확정
- 기존 지식의 폐기

모든 변경은 업데이트 초안·근거·검토 상태를 남긴 뒤 관련 에이전트와 CEO가 판단한다.

## 승인 필요 행동

- 외부 전문가에게 연락
- 유료 논문·자료 구매
- 로그인된 학술 데이터베이스 접근
- 사용자 피부 사진이나 건강정보 외부 전송
- 추천 로직 변경
- 사용자에게 표시되는 의학·안전 문구 확정
- 제품 추천 기준 확정

## 안전 규칙

- 논문 초록을 전체 논문 분석처럼 표현하지 않는다.
- 출처 없는 성분 효능을 만들지 않는다.
- 연구 결과와 개인별 효과를 동일시하지 않는다.
- 사용자 데이터를 자문 자료에 불필요하게 포함하지 않는다.
- 모든 외부 행동은 `_agents/skin_advisor/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
