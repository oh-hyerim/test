# 🗂️ Secretary — 도구 매니페스트

Secretary 에이전트가 회사의 업무·일정·결정·보고를 관리하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 읽기·분석·보고만 가능 |
| 2 | Draft — 내부 기록·초안·알림 작성 가능, 외부 행동은 승인 필요 |
| 3 | Auto — 허용된 내부 관리 작업 자동 실행 |

Secretary는 기본적으로 **레벨 2**를 사용한다.

내부 업무 기록, 상태 변경, 보고서 초안 작성은 자동으로 진행할 수 있다. 외부 발송, 일정 생성·변경, 계정 연결, 민감정보가 포함된 알림은 승인 대상이 될 수 있다.

## 현재 사용 가능한 도구

### `telegram_setup`

Telegram 봇 연결을 설정하고 연결 상태를 확인한다.

- `enabled`: true
- `requires_credentials`: true
- `approval_required`: true_if_test_message_sent

### `google_calendar_write`

Google Calendar의 일정을 읽고 업무 마감일에 맞는 일정을 생성·수정·삭제한다.

- `enabled`: true
- `requires_credentials`: true
- `approval_required`: true_for_external_calendar_change

현재 실제 도구가 실행되지 않거나 인증이 없으면 일정이 등록되었다고 보고하지 않는다.

## 업무 관리 로드맵

아래 도구는 현재 설계 목록이며, 실제 구현 전까지 실행할 수 없다.

### `task_registry`

회사 전체 업무를 생성·조회·수정·상태 변경한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

관리 항목:

- 업무 ID
- 담당자
- 상태
- 우선순위
- 마감일
- 선행 업무
- 완료 기준
- 결과물 위치
- 다음 액션

### `dependency_tracker`

업무 간 선행 조건과 대기 관계를 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `decision_log`

중요한 회사 의사결정과 근거를 기록한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

기록 위치 예시:

- `_company/_shared/decisions.md`

### `agent_output_index`

각 에이전트의 산출물과 핵심 결과를 색인화한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `progress_report`

완료·진행·대기·차단 업무를 바탕으로 일일·주간 보고서를 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `blocker_detector`

지연·누락·선행 업무 미완료·결정 대기 상태를 감지한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 일정·알림 로드맵

### `calendar_local`

외부 서비스 없이 로컬 업무 마감일을 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `calendar_caldav`

CalDAV 기반 캘린더와 연결한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: true
- `approval_required`: true_for_external_calendar_change

### `kakao_alert`

카카오톡 나에게 보내기 알림을 사용한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: true
- `approval_required`: true_for_message_send

### `email_triage`

메일을 분류하고 답장 초안을 만든다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: true
- `approval_required`: true_for_external_send

## 보고 원칙

- 상태 변경에는 근거와 날짜를 기록한다.
- 실제로 확인하지 않은 업무를 완료 처리하지 않는다.
- 보고서에는 반드시 다음 액션을 포함한다.
- 일정 생성과 내부 업무 등록을 구분한다.
- 외부 발송과 내부 기록을 구분한다.
- 사용자에게 중요한 결정이 필요한 항목은 별도로 표시한다.

## 안전 규칙

- 삭제·배포·발송·결제는 항상 승인 게이트를 거친다.
- 외부 API 호출 전 자격증명과 권한 범위를 확인한다.
- Telegram으로 민감한 사용자 정보를 보내지 않는다.
- 캘린더 제목과 설명에 피부 정보·건강 정보·인증정보를 넣지 않는다.
- API 키·토큰·비밀번호를 기록하거나 보고하지 않는다.
- 모든 외부 행동은 `_agents/secretary/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
