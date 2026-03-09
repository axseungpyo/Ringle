# 프로젝트 전체 파일 검토 보고서

- 작성일: 2026-03-03
- 검토 대상: 프로젝트 내 전체 파일(텍스트 파일 전수 + 바이너리 메타/추출 가능한 범위 확인)
- 검토 파일 수: 23개
  - 텍스트 검토: `*.md`, `*.html`, `*.json`, `ringle_report_ui`
  - 바이너리 확인: `report/링글 AI 스피킹 개선 공모전 리서치.docx`, `report/링글 AI 스피킹 개선 공모전 리서치.pdf`, `*.png`

## 검토 범위/한계

- `report/링글 AI 스피킹 개선 공모전 리서치.docx`는 텍스트 추출 후 본문 검토함.
- `report/링글 AI 스피킹 개선 공모전 리서치.pdf`는 로컬 도구로 본문 텍스트 추출이 불가하여, 메타데이터/링크 단서만 확인함.
- `*.png`는 이미지 메타데이터(해상도/포맷)만 확인함.

## 주요 문제점 (심각도 순)

### 1) [높음] 핵심 지표/출처의 문서 간 불일치

- 동일 주제(시장 성장률/시장 정의/근거 출처)가 문서마다 서로 다른 수치로 제시됨.
  - `docs/06_ppt_outline.md:89` → CAGR `32.2%`
  - `ringle_report_ui:54` → CAGR `14.3%`
  - `ringle_report_ui:90-92` → CAGR `12.5%`
  - `report/ringle_report_competition_2026-02-26.md:67-71` → `16.6% / 27.5% / 14.62% / 16.15% / 11.05%`
- 위험: 심사 단계에서 "숫자 신뢰도"가 무너지고, 발표-문서-Q&A 간 정합성이 깨짐.

### 2) [높음] KPI 목표치 충돌 (동일 메트릭)

- `사용자 발신 비율` 목표가 문서마다 다름.
  - `docs/01_market_analysis.md:375` → `22.3% → 50%+`
  - `docs/04_feature_spec.md:396`, `docs/04_feature_spec.md:412` → `22.3% → 35%`
  - `docs/06_ppt_outline.md:409` → `22.3% → 35%`
- 위험: 우선순위 및 성공기준 혼선, 실험 설계/성과판단 기준 붕괴.

### 3) [높음] 접수 링크가 2개로 병기되어 운영 혼선 가능

- `ringle_competition_notice.md`에 접수 관련 링크가 2개 노출됨.
  - `ringle_competition_notice.md:177`
  - `ringle_competition_notice.md:179`
- 위험: 잘못된 폼 제출, 제출 누락, 팀 내 혼선.

### 4) [중간] 결과물 파일 중복/분기(드리프트) 구조

- 동일 HTML이 서로 다른 경로로 중복 저장됨.
  - `ringle_report_ui`
  - `report/ringle_report_ui.html`
- 실제 해시는 현재 동일하지만, 구조상 향후 한쪽만 수정될 가능성이 큼.

### 5) [중간] 문서 이식성(포터빌리티) 저하 요소

- Notion `attachment:` 스킴 이미지 참조로 로컬/깃 렌더링 시 깨질 수 있음.
  - `ringle_competition_notice.md:13`
- 절대경로 하드코딩 존재.
  - `memory/MEMORY.md:10`
  - `CLAUDE.md:225`

### 6) [중간] 근거 출처의 신뢰도 계층이 혼재

- 핵심 판단 근거에 위키/개인 후기/2차 요약 출처가 혼재함.
  - `docs/01_market_analysis.md:386-387` (나무위키)
  - `docs/02_ringle_service_analysis.md:280-281`, `:286-287` (개인 후기성 블로그)
- 위험: 반박 가능성 상승, 심사 질의 대응력 저하.

### 7) [중간] 용어/표기 일관성 저하

- `롤플레이`와 `롤플레잉` 혼용, `Top 2`/`TOP 2` 혼용.
- 대표 예시:
  - `docs/02_ringle_service_analysis.md:26` (롤플레잉)
  - `docs/05_wireframe_spec.md:18` (롤플레이)
  - `ringle_competition_full_content.md:14` (TOP 2)
  - `ringle_competition_full_content.md:119` (Top 2)
- 위험: 문서 완성도/브랜드 톤 일관성 저하.

### 8) [낮음] 저장소 위생 및 협업성 저하 요소

- 불필요 시스템 파일 포함: `.DS_Store`
- 권한이 `600`으로 잠겨 있는 파일 다수(협업 환경에서 접근 이슈 가능)
  - 예: `ringle_competition_notice.md`, `ringle_competition_full_content.md`, `report/ringle_platform_brainstorm.md`
- HTML 리포트가 CDN 의존(오프라인/보안 정책 환경에서 렌더 실패 가능)
  - `report/ringle_report_ui.html:7-10`

## 보완점 (우선 적용 권장)

### A. 데이터 정합성 기준 문서 1개로 통합

- `docs/00_data_registry.md` 신설 권장.
- 항목: 지표명, 정의, 기준일, 값, 출처 URL, 관측일, 신뢰도 등급(A/B/C), 사용 가능 슬라이드 번호.
- 원칙: 발표/PPT/보고서 모든 수치는 Registry 단일 원천에서만 인용.

### B. KPI 타깃 단일화

- `사용자 발신 비율` 목표를 하나로 확정(예: `35%` 또는 `50%+` 중 하나).
- 확정 후 `docs/01`, `docs/04`, `docs/06` 동시 정리.

### C. 제출/운영 링크 Canonical 처리

- 접수 폼 URL 1개만 `정본`으로 표기하고, 나머지는 "폐기/이전 링크"로 주석 처리.
- FAQ/접수 섹션의 링크 중복 제거.

### D. 파일 구조 정리

- `ringle_report_ui`는 삭제 또는 `ringle_report_ui.html`로 명확히 변경.
- `report/ringle_report_ui.html` 하나만 기준 파일로 유지.

### E. 출처 품질 기준 수립

- Tier-A(공식/1차): 기업 공식, 앱스토어 공식 지표, 공신력 있는 리서치 원문
- Tier-B(보조): 언론 기사
- Tier-C(참고): 블로그/커뮤니티/위키
- 핵심 결론은 Tier-A/B 중심으로 재기술.

## 추가 개선사항 (완성도 향상)

### 1) 문서 품질 자동 점검 스크립트 도입

- 링크 유효성(상대경로), 용어 통일, 긴 줄(예: 200자+) 경고, 중복 파일 체크를 자동화.
- 최소 `make lint-docs` 또는 `scripts/lint_docs.sh` 형태 권장.

### 2) 용어 스타일 가이드 파일 추가

- 예: `docs/STYLE_GUIDE.md`
- 표준어 지정: `롤플레잉`(또는 `롤플레이`) 1개 선택, `Top` 표기 규칙 통일.

### 3) 시간 민감 정보에 기준일 강제 표기

- 앱 순위/리뷰수/평점 등 변동 지표는 항상 `관측일` 표기.
- 오래된 수치(예: `2025.05 기준`)는 최신 관측치로 갱신 또는 "히스토리 데이터"로 명확히 분리.

### 4) 제출 직전 체크리스트 분리

- `docs/99_submission_checklist.md`에 아래 항목 고정:
  - 수치 정합성 확인
  - 링크 클릭 테스트
  - 파일명/용량/포맷 규격 확인
  - 저작권/AI 활용 표기 확인

## 빠른 실행 우선순위 (오늘 바로 가능)

1. 접수 폼 링크 정본화(중복 제거)
2. KPI 목표치 단일화(`22.3%→35%` vs `50%+` 결정)
3. 중복 파일 정리(`ringle_report_ui` 계열)
4. `attachment:` 이미지 링크 로컬 파일 경로로 교체
5. `.DS_Store` 제거 및 제외 처리

---

필요하면 다음 단계로, 위 이슈 중 **즉시 수정 가능한 항목(링크/중복/표기 통일)**부터 실제 파일에 반영해 드릴 수 있습니다.
