# 🛡️ QA & Safety — 도구 매니페스트

QA & Safety 에이전트가 기능·보안·개인정보·피부 안전·접근성·출시 위험을 검토하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 결과 읽기·분석·보고만 가능 |
| 2 | Draft — 내부 검수·테스트 계획·수정 요청 작성 가능 |
| 3 | Auto — 승인된 내부 테스트 자동 실행 |

QA & Safety는 기본적으로 레벨 2를 사용한다.

내부 테스트와 검수 보고는 자동화할 수 있다. 운영 데이터 접근·외부 스캔 서비스 사용·데이터 삭제·배포·취약점 공개는 승인 대상이다.

## 현재 사용 가능한 기능

현재 QA & Safety 폴더에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 테스트 계획
- 테스트 케이스
- 버그 보고서
- 보안·개인정보 체크리스트
- 피부·추천 안전성 체크리스트
- 출시 전 검수표
- 재검수 보고서
- 미해결 위험 보고서

실제로 테스트나 스캔을 실행하지 않았다면 실행 완료로 보고하지 않는다.

## 예정 도구

### `acceptance_test_runner`

Product Manager가 작성한 수용 기준에 따라 기능을 테스트한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `user_flow_test_runner`

핵심 사용자 흐름을 단계별로 테스트한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `security_scan`

시크릿 노출·입력 검증·권한·의존성·오류 메시지를 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `privacy_audit`

데이터 수집·저장·전송·로그·삭제 흐름을 검토한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

실제 사용자 데이터나 피부 사진을 외부 검사 서비스로 보내지 않는다.

### `recommendation_safety_check`

추천 결과의 근거·주의사항·불확실성·위험 표현을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `copy_safety_check`

피부·건강·의료적 오해·효과 보장·과장 표현을 검사한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

전문가나 법률 자문을 대체하지 않는다.

### `accessibility_check`

색상 대비·텍스트 크기·터치 영역·키보드·스크린리더·오류 안내를 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `data_access_test`

사용자별 데이터 분리와 권한 검사를 테스트한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_environment
- `approval_required`: false

운영 데이터가 아니라 테스트 환경과 가짜 데이터만 사용한다.

### `dependency_audit`

사용 중인 패키지와 라이브러리의 알려진 취약점·버전을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `release_readiness_check`

출시 전 기능·보안·개인정보·문구·접근성·정책 체크리스트를 실행한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `bug_reporter`

문제의 재현 방법·심각도·담당자·완료 기준을 기록한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 외부 자료와 전문가 검토

다음 항목은 Researcher, Skin & Cosmetic Advisor, Developer 또는 외부 전문가에게 검토를 요청한다.

- 피부·성분·건강 안전성
- 최신 보안 권고
- 개인정보 법률·규정
- 앱스토어 정책
- 외부 데이터 저장·전송
- 의료적 표현

자료를 확인하지 못한 경우 안전하다고 가정하지 않는다.

## 승인 필요 행동

- 운영 데이터 접근
- 실제 사용자 사진·피부정보 사용
- 외부 보안 스캔 서비스로 코드·데이터 전송
- 사용자 데이터 삭제
- 운영 배포
- 취약점의 외부 공개
- 법률·의료·개인정보 기준의 최종 확정

## 안전 규칙

- 테스트에는 가짜 데이터만 사용한다.
- 민감정보를 로그·스크린샷·보고서에 남기지 않는다.
- 보안 취약점을 외부에 공개하지 않는다.
- 검수 범위를 벗어난 안전성을 보장하지 않는다.
- 모든 외부 행동은 `_agents/qa_safety/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
