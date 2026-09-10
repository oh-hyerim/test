# 🛡️ Editor — 도구 매니페스트

Editor 에이전트가 제품 품질·안전·개인정보·출시 전 검수를 수행하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 결과 읽기·분석·보고만 가능 |
| 2 | Draft — 내부 검수와 수정 요청 작성 가능, 외부 변경은 승인 필요 |
| 3 | Auto — 허용된 내부 검수 자동 실행 |

Editor는 기본적으로 **레벨 2**를 사용한다.

검수 보고서·수정 요청·체크리스트는 자동 작성할 수 있다. 원본 코드·디자인·문구를 직접 수정하거나 운영 배포하는 행동은 담당 에이전트와 승인 절차를 확인한다.

## 현재 사용 가능한 기능

현재 Editor 폴더에는 품질·안전 검수용 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 수동 또는 마크다운으로 작성한다.

- 요구사항 체크리스트
- 사용자 흐름 검수표
- 문제 목록
- 안전·개인정보 검수표
- 출시 전 체크리스트
- 수정 요청서
- 재검수 결과

실제로 테스트나 스캔을 실행하지 않았는데 실행 완료라고 보고하지 않는다.

## 예정 도구

### `requirements_trace`

요구사항과 디자인·코드·테스트 결과의 연결 관계를 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `user_flow_check`

핵심 사용자 흐름의 누락·단절·잘못된 연결을 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

검수 범위:

- 온보딩
- 동의·권한
- 피부 정보 입력
- 분석
- 추천
- 루틴 저장·기록
- 오류·재시도
- 데이터 수정·삭제

### `copy_safety_check`

피부·건강·의료적 오해·과장 표현·개인정보 안내 문구를 검사한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

전문가나 법률 자문을 대체하지 않는다.

### `privacy_check`

피부 사진·피부 상태·사용자 계정 정보의 수집·저장·전송·로그 노출을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `security_scan`

시크릿 노출, 의존성 위험, 입력 검증, 권한 확인, 로그와 오류 메시지를 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `accessibility_check`

색상 대비, 키보드·스크린리더 사용, 터치 영역, 오류 안내, 텍스트 가독성을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `acceptance_test`

Product Manager가 정의한 완료 기준에 따라 기능을 검증한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `release_checklist`

출시 전 기능·보안·개인정보·문구·스토어 자료를 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `issue_reporter`

발견된 문제를 담당 에이전트·심각도·완료 기준과 함께 기록한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 기존 음악·영상 도구

현재 Editor 폴더의 다음 도구는 제품 MVP와 직접 관련이 없으므로 보류한다.

- `music_studio_setup`
- `music_generate`
- `music_to_video`

처리 원칙:

- 기존 파일은 삭제하지 않는다.
- `enabled`: false로 취급한다.
- 현재 CEO 업무 배정 대상에서 제외한다.
- 나중에 Growth 또는 콘텐츠 제작 에이전트가 필요할 때 재검토한다.

## 외부 자료가 필요한 경우

다음 항목은 Researcher, Developer, Skin & Cosmetic Advisor 또는 외부 전문가의 자료가 필요할 수 있다.

- 피부·성분·건강 관련 안전 기준
- 법률·개인정보·의료 표현
- 최신 보안 권고
- 앱스토어 정책
- 접근성 기준
- 외부 서비스의 데이터 처리 방식

자료가 없으면 안전하다고 가정하지 않고 `blocked` 또는 `needs_revision`으로 표시한다.

## 승인 필요 행동

다음 행동은 자동으로 실행하지 않는다.

- 원본 코드의 대규모 수정
- 사용자 데이터 삭제
- 운영 배포
- 앱스토어 제출
- 외부 전문가·고객에게 메시지 발송
- 법률·의료·개인정보 관련 공식 확정
- 외부 스캔 서비스에 민감정보 업로드

## 안전 규칙

- 실제 사용자 피부 사진과 건강정보를 테스트에 사용하지 않는다.
- 민감정보를 로그·보고서·스크린샷에 포함하지 않는다.
- 검수 과정에서 발견한 보안 취약점을 공개 채널에 게시하지 않는다.
- 검수 범위를 벗어난 영역의 안전성을 보장하지 않는다.
- 모든 외부 행동은 `_agents/editor/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
