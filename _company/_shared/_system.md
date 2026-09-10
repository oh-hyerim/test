# 🧬 1인 기업 OS — 자가 매뉴얼

## 이 폴더는 무엇인가요?
당신의 1인 기업의 두뇌입니다. 7명의 AI 에이전트가 여기서 일합니다.

## 폴더 구조
- `_shared/` — 모든 에이전트가 매번 읽는 공동 메모리
  - `identity.md` — 회사 정체성 (이름, 톤, 가치)
  - `goals.md` — 목표
  - `decisions.md` — 의사결정 로그 (자가학습이 자동 누적)
  - `_system.md` — 이 파일
- `_agents/<id>/` — 각 에이전트 개인 공간
  - `memory.md` — 자가학습 (자동, append-only)
  - `prompt.md` — 페르소나 디테일 (사용자가 편집)
  - `config.md` — API 키·시크릿 (`.gitignore`로 보호)
- `sessions/<ts>/` — 세션별 산출물 (자동)
- `_cache/` — API 응답 캐시 (sync 제외)

## 메모리 위계 (충돌 시 우선순위)
1. `decisions.md` — 가장 강한 신뢰
2. `identity.md`
3. `goals.md`
4. 개인 메모리
5. 지식 베이스 (`10_Wiki/`)

## 다른 PC로 옮길 때
1. 새 PC에 Connect AI 설치
2. 👔 모드 ON → "📥 다른 PC에서 가져오기" 선택
3. GitHub URL 입력 → 자동 clone
4. 끝.

## 동기화 정책
- `_shared/`, `_agents/*/memory.md`, `_agents/*/prompt.md`, `sessions/` → git sync ✅
- `_agents/*/config.md`, `_cache/` → git sync ❌ (시크릿·캐시)

## 18명의 에이전트
- 🧭 **CEO**: 오케스트레이션, 작업 분해, 종합 판단, 다음 액션 결정
- 💼 **Business**: 수익화 모델, 가격 전략, 시장·경쟁·ROI·KPI 분석
- 📋 **Product Manager**: 고객 문제, MVP 범위, 요구사항, 우선순위, 수용 기준
- 🔍 **Researcher**: 시장·경쟁·공개 자료·논문 조사와 사실 확인
- 🧑‍🤝‍🧑 **Customer Research**: 인터뷰·설문·사용성 테스트와 고객 문제 검증
- 🧴 **Skin & Cosmetic Advisor**: 피부·화장품·성분·논문 전문 자문
- 🗃️ **Knowledge Curator**: 출처·지식 버전·충돌·업데이트 상태 관리
- 🤖 **AI & Recommendation Specialist**: AI 분석·추천 기준·평가·변경 관리
- 🎨 **Designer**: UX/UI·사용자 흐름·디자인 시스템
- 💻 **Developer**: 앱 개발·API·데이터·테스트·배포 준비
- ✍️ **Writer**: UX 라이팅·제품 문서·사용자 안내
- 🛡️ **QA & Safety**: 기능·보안·개인정보·피부 안전·출시 검수
- ⚖️ **Legal & Privacy Advisor**: 법률·개인정보·의료·플랫폼 정책 검토
- 📊 **Data & Experimentation Analyst**: 제품 지표·퍼널·실험·행동 데이터 분석
- 🤝 **Customer Success**: 베타 사용자 지원·문의·피드백·이탈 신호
- 📈 **Growth**: 출시·사용자 획득·채널·성장 실험
- 📱 **Secretary**: 일정·업무·보고·알림 관리
- 🎵 **Editor**: 전체 산출물 품질·일관성 및 편집 검수

> Instagram과 YouTube는 새 Growth 구조가 검증될 때까지 기존 폴더와 설정을 유지하지만, 현재 기본 업무 배정에서는 제외한다.
