# 💻 Developer — 도구 매니페스트

Developer 에이전트가 제품을 설계·구현·검증·미리보기·배포 준비하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 프로젝트 읽기·분석만 가능 |
| 2 | Draft — 코드 수정과 검증 가능, 외부 배포는 승인 필요 |
| 3 | Auto — 허용된 개발 작업 자동 실행 |

Developer는 기본적으로 **레벨 2**를 사용한다.

로컬 프로젝트 탐색, 코드 작성, 내부 테스트, 로컬 미리보기는 자동으로 수행할 수 있다. 운영 배포, 외부 서비스 연결, 비용이 발생하는 서비스 사용, 데이터 삭제는 승인 대상이다.

## 사용 가능한 도구

### `web_init`

웹 또는 모바일 프로젝트를 초기화한다.

- `enabled`: true
- `requires_credentials`: false
- `approval_required`: false

지원 템플릿:

- `vite-react`
- `nextjs`
- `astro`
- `expo`
- `vanilla`

선택 기준:

- 빠른 웹 MVP·대시보드·SPA → `vite-react`
- 서버 기능과 데이터 처리가 필요한 웹 앱 → `nextjs`
- 실제 iOS·Android 앱 → `expo`
- 단순 정적 페이지 → `astro` 또는 `vanilla`

프로젝트 초기화 전 프로젝트 이름과 출력 경로를 확인한다.

### `pack_apply`

프로젝트에 미리 구성된 UI·기능 키트를 적용한다.

- `enabled`: true
- `requires_credentials`: false
- `approval_required`: false

사용 전 다음을 확인한다.

- 기존 프로젝트 백업 또는 Git 상태
- 덮어쓰기 파일
- 설치될 의존성
- 현재 프레임워크와 키트의 호환성

기존 사용자 코드를 확인하지 않고 무조건 적용하지 않는다.

### `web_preview`

개발 서버를 실행하고 로컬 미리보기 URL을 확인한다.

- `enabled`: true
- `requires_credentials`: false
- `approval_required`: false

핵심 사용자 흐름을 직접 확인하는 용도로 사용한다. 실행되지 않은 서버나 URL을 실행되었다고 보고하지 않는다.

### `pwa_setup`

웹 프로젝트를 PWA로 변환한다.

- `enabled`: true
- `requires_credentials`: false
- `approval_required`: false

사용 전 다음을 확인한다.

- 웹 MVP가 PWA에 적합한지
- 오프라인 캐싱으로 민감정보가 남을 위험이 없는지
- 사진·피부정보를 캐시하지 않는지
- 아이콘과 앱 이름
- 서비스 워커가 최신 데이터를 방해하지 않는지

실제 앱스토어 배포를 대체하는 기능으로 설명하지 않는다.

### `lint_test`

TypeScript, JavaScript, Python, JSON, 테스트, 빌드 등을 검증한다.

- `enabled`: true
- `requires_credentials`: false
- `approval_required`: false

주요 코드 변경 후 반드시 사용한다.

검증 결과에는 다음을 포함한다.

- 실행한 검사
- 성공·실패 여부
- 실패한 파일과 오류
- 수정 후 재검증 여부
- 아직 실행하지 않은 검사

## 개발 조사 요청

다음 작업은 최신 외부 정보가 필요할 수 있다.

- 인증·결제·스토리지·분석 서비스 연결
- 최신 SDK나 API 사용
- 모바일 플랫폼 정책
- 개인정보·보안 구현
- 데이터베이스·배포 설정
- 외부 서비스 요금과 사용 제한

검색 기능이 연결되지 않은 경우 Researcher 또는 CEO에게 다음 형식으로 조사 요청한다.

- 조사 주제
- 구현 목적
- 확인할 공식 문서
- 필요한 버전
- 기술 결정에 미치는 영향
- 조사 결과가 없을 때의 임시 대안

## 예정 도구

### `database_setup`

MVP에 필요한 데이터베이스와 마이그레이션 구조를 초기화한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: true_if_external_resource_created

대상 데이터 예시:

- 사용자 계정
- 피부 정보
- 설문 응답
- 피부 사진 메타데이터
- 제품 정보
- 성분 정보
- 추천 결과
- 루틴
- 사용 기록
- 사용자 피드백
- 추천 로직 버전

### `auth_setup`

사용자 인증과 세션 구조를 초기화한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: true_if_external_account_created

### `recommendation_engine`

사용자 입력과 제품·성분 데이터에 기반한 설명 가능한 추천 로직을 구현·검증한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

반드시 지원해야 할 내용:

- 입력값 검증
- 추천 기준 버전
- 추천 이유
- 제외 또는 주의 이유
- 데이터 부족 상태
- 결과 재현성
- 안전 규칙 분리

### `analytics_events`

가입, 입력 완료, 분석 완료, 추천 확인, 루틴 저장, 루틴 실행, 이탈 등의 이벤트를 설계·검증한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_provider
- `approval_required`: true_if_external_data_sent

개인정보와 불필요한 피부 정보를 분석 이벤트에 포함하지 않는다.

### `security_scan`

의존성, 환경변수, 로그, 입력 검증, 권한, 개인정보 노출 가능성을 점검한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `api_contract_check`

프론트엔드와 백엔드 사이의 요청·응답 형식과 버전 호환성을 검증한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `deploy_cli`

운영 환경에 배포한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: true
- `approval_required`: true

운영 배포는 항상 사용자 승인 후 실행한다.

### `git_committer`

검증된 변경을 의미 있는 단위로 커밋한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

`git add -A`를 사용하지 않고 변경 파일을 명시한다.

## 안전 규칙

- 시크릿과 API 키를 코드·로그·커밋에 포함하지 않는다.
- 사용자 피부 사진과 민감정보를 불필요하게 외부로 전송하지 않는다.
- 실제 사용자 데이터로 테스트하지 않는다.
- 외부 서비스 연결 전 데이터 흐름과 비용을 확인한다.
- 운영 배포와 데이터 삭제는 항상 승인 게이트를 거친다.
- 인증·권한 검사를 우회하지 않는다.
- 추천 로직 변경은 버전과 변경 이유를 기록한다.
- 데이터베이스 스키마 변경 전 마이그레이션과 롤백 방법을 확인한다.
- 모든 외부 행동은 `_agents/developer/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
