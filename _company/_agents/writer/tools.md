# ✍️ Writer — 도구 매니페스트

Writer 에이전트가 앱 문구, 제품 콘텐츠, UX 라이팅, 서비스 문서를 작성하고 검수하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 자료 읽기·분석·검토만 가능 |
| 2 | Draft — 내부 문구·문서 초안 작성 가능, 외부 발행은 승인 필요 |
| 3 | Auto — 허용된 내부 콘텐츠 작업 자동 실행 |

Writer는 기본적으로 **레벨 2**를 사용한다.

앱 내부 문구와 문서 초안은 자동으로 작성할 수 있다. 앱에 실제 반영하거나 외부에 게시·발송하는 것은 승인 또는 담당 에이전트 검토가 필요하다.

## 현재 사용 가능한 기능

현재 Writer 폴더에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 화면별 문구 목록
- UX 라이팅 표
- 문구 대안
- 용어집
- FAQ
- 서비스 문서
- 검수 체크리스트

실제 파일이나 외부 게시물이 생성되지 않았는데 생성 완료라고 보고하지 않는다.

## 예정 도구

### `tone_learner`

사용자가 승인한 과거 문서와 문구를 바탕으로 대표와 서비스의 문체를 학습한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

주의사항:

- 승인된 자료만 학습 대상으로 사용한다.
- 개인정보와 비공개 문서를 자동으로 학습하지 않는다.
- 학습된 문체가 사실 검증이나 안전 검토를 대신하지 않는다.

### `ux_copy_validator`

화면 문구의 길이·명확성·행동 유도·용어 일관성을 검토한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

검토 항목:

- 문장 길이
- 버튼의 행동 명확성
- 오류 해결 방법 포함 여부
- 중복 표현
- 용어 일관성
- 모바일 화면 적합성
- 사용자 오해 가능성

### `safety_copy_checker`

피부·건강·의료적 오해·개인정보 관련 표현을 검토한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

이 도구는 전문가나 법률 검토를 대체하지 않는다.

### `content_consistency_checker`

화면·FAQ·앱스토어 설명·알림의 용어와 핵심 메시지 일관성을 확인한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `localization_prep`

향후 한국어 원문을 기준으로 다국어 번역이 가능하도록 문구의 변수·길이·문화적 표현을 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

번역 자체보다 원문 의미와 서비스 안전성을 우선한다.

### `document_formatter`

기획서·요구사항·FAQ·검수 보고서를 정해진 형식으로 정리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 보류 또는 비활성화 도구

### `multi_platform_adapt`

YouTube·Instagram·블로그용 콘텐츠 자동 변환 기능이다.

- `enabled`: false
- `status`: deferred

현재 회사의 핵심 목표와 직접 연결되지 않으므로 보류한다. 나중에 Growth 또는 콘텐츠 마케팅 에이전트가 필요해질 때 재검토한다.

### `hook_library`

후크와 CTA를 관리하는 기능이다.

- `enabled`: false
- `status`: deferred

현재는 앱 제품 문구가 우선이므로 보류한다. 출시 후 사용자 획득과 콘텐츠 마케팅을 시작할 때 재검토한다.

## 외부 자료가 필요한 경우

Writer는 다음 내용이 필요하면 직접 추측하지 않고 Researcher 또는 Skin & Cosmetic Advisor에게 근거를 요청한다.

- 피부·화장품·성분·건강 관련 사실
- 최신 연구 결과
- 의료적·법률적 표현
- 경쟁 서비스의 문구
- 앱스토어 정책
- 사용자 조사 결과

조사 결과가 실제로 제공되지 않았다면 출처를 임의로 만들지 않는다.

## 승인 필요 행동

다음 행동은 자동 실행하지 않는다.

- 앱 문구의 운영 반영
- 앱스토어 설명문 게시
- 외부 광고·게시물 발행
- 고객·파트너에게 메시지 발송
- 의료적·법률적 표현의 최종 확정
- 사용자 데이터가 포함된 콘텐츠 생성
- 유료 번역·외부 콘텐츠 서비스 사용

## 안전 규칙

- 사실이 아닌 효과·치료·진단 표현을 만들지 않는다.
- 출처 없는 수치와 연구 결과를 만들지 않는다.
- 제품 제휴 문구를 일반적인 객관적 추천처럼 작성하지 않는다.
- 개인정보와 피부 사진을 문구 작성에 불필요하게 포함하지 않는다.
- 외부 행동은 `_agents/writer/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
