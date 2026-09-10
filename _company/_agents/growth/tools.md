# 📈 Growth — 도구 매니페스트

Growth 에이전트가 앱 출시·사용자 획득·성장 실험·채널 분석을 수행하는 데 사용하는 도구를 정의한다.

## 자율도 레벨

AUTONOMY_LEVEL: 2

| 값 | 의미 |
|---|---|
| 0 | Off — 도구 전체 비활성 |
| 1 | Read-only — 자료·성과 읽기와 분석만 가능 |
| 2 | Draft — 성장 계획·콘텐츠·실험 초안 작성 가능, 외부 실행은 승인 필요 |
| 3 | Auto — 승인된 내부 분석과 계획 작업 자동 실행 |

Growth는 기본적으로 레벨 2를 사용한다.

내부 성장 계획과 실험 설계는 자동으로 작성할 수 있다. 외부 게시·광고 집행·사용자 연락·앱스토어 제출·비용 발생 행동은 승인 대상이다.

## 현재 사용 가능한 기능

현재 Growth 폴더에는 실제로 실행 가능한 전용 도구가 없을 수 있다.

도구가 연결되어 있지 않은 경우 다음을 마크다운으로 작성한다.

- 성장 계획
- 베타 사용자 모집 계획
- 채널 비교표
- 앱스토어 출시 체크리스트
- 성장 실험 계획
- 캠페인 초안
- 성과 분석 보고서
- 다음 성장 액션

실제로 게시·광고·사용자 모집·앱스토어 제출을 실행하지 않았다면 실행 완료로 보고하지 않는다.

## 예정 도구

### `channel_research`

핵심 고객이 활동하는 채널과 관련 대화를 조사한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_source
- `approval_required`: false

### `app_store_listing_builder`

앱스토어 설명·키워드·스크린샷 구성·업데이트 문구 초안을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `beta_recruitment_planner`

베타 사용자 모집 조건·모집 문구·선별 질문·온보딩 계획을 작성한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: true_if_external_recruitment

### `growth_experiment_planner`

채널·메시지·기능·사용자 행동을 대상으로 성장 실험을 설계한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `campaign_tracker`

성장 실험의 기간·비용·채널·성과·다음 액션을 관리한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `acquisition_funnel_analyzer`

노출·방문·가입·활성화·재방문 퍼널을 분석한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: depends_on_analytics_provider
- `approval_required`: false

### `referral_flow_planner`

사용자 추천·공유·초대 기능의 흐름과 실험을 설계한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

### `content_channel_adapter`

하나의 검증된 제품 메시지를 채널별 형식으로 변환한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

이 도구는 원래 메시지의 사실·안전·광고 표시를 변경하지 않는다.

### `growth_report_generator`

채널·실험·전환·재방문 결과를 CEO·Product Manager·Business에 보고한다.

- `enabled`: false
- `status`: planned
- `requires_credentials`: false
- `approval_required`: false

## 채널 도구의 범위

향후 다음 채널을 필요에 따라 연결할 수 있다.

- Instagram
- YouTube
- 블로그
- 검색
- 커뮤니티
- 이메일
- 앱스토어
- 제휴 채널

특정 채널 연결은 Growth의 상위 목표인 사용자 획득과 제품 활성화에 기여할 때만 검토한다.

## 외부 서비스와 개인정보

성장 도구를 연결하기 전 다음을 검토한다.

- 수집·전송되는 데이터
- 광고 식별자 사용 여부
- 피부·건강정보 포함 여부
- 사용자 동의와 거부 방법
- 외부 서비스 보관 기간
- 국외 이전 여부
- 비용
- Legal & Privacy Advisor 검토 여부

## 승인 필요 행동

- Instagram·YouTube·블로그 외부 게시
- 광고 캠페인 집행
- 앱스토어 제출
- 이메일·메신저 발송
- 베타 사용자 모집과 연락
- 사용자 보상 지급
- 외부 제휴 요청
- 유료 성장 도구 사용
- 개인정보를 활용한 타깃팅
- 사용자 데이터의 외부 전송

## 안전 규칙

- 실제 제품 기능과 다른 홍보 문구를 만들지 않는다.
- 피부·건강·의료 효과를 보장하지 않는다.
- 광고·제휴·협찬을 숨기지 않는다.
- 개인정보와 피부 사진을 마케팅 자료에 불필요하게 포함하지 않는다.
- 모든 외부 행동은 `_agents/growth/activity.log`에 기록한다.
- 승인 대기 액션은 `approvals/pending/`에 저장한다.
