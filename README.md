# RING LOOP — 링글 AI 스피킹 개선 프로젝트

> 제5회 링글 서비스 기획 & 마케팅 공모전 출품작

---

## 프로젝트 개요

**RING LOOP**는 링글 AI 전화영어의 수신 거절률(40%)을 해결하고, 결제 전환율을 높이기 위한 서비스 기획안입니다.

핵심 컨셉은 **"준비(Ready) → 통화(In) → 성장(Grow)"** 루프를 통해 사용자의 학습 습관을 자동 형성하는 것입니다.

### 핵심 솔루션

| 구분 | 내용 |
|---|---|
| **AI 톡 (Ready)** | 메신저형 AI 대화로 사용자 맥락 수집 + 영어 표현 코칭 + 전화 전환 유도 |
| **AI 전화 (In)** | 톡에서 수집된 맥락 기반 맞춤형 롤플레이 시나리오로 준비된 전화 학습 |
| **RING LOOP** | Ready(AI 톡) → In(AI 전화) → Grow(피드백) 순환 루프 |
| **스마트 거절 UX** | 거절 = 끊김이 아닌, 재스케줄링 옵션으로 학습 연속성 유지 |
| **롤플레잉 온보딩** | 레벨테스트 직후 3분 롤플레잉 → AHA Moment → 결제 전환 |

### 목표 KPI

| 지표 | 현재 | 목표 (보수적/낙관적) |
|---|---|---|
| AI 전화 수신 거절률 | 40% | 25% / 20% |
| 사용자 발신 비율 | 22.3% | 30% / 35% |
| 롤플레잉 온보딩 경험률 | ~35% | 70% / 80% |
| 결제 전환율 | 기준치 | ×2.0 / ×2.4 |

---

## 프로젝트 구조

```
Ringle/
├── README.md                          ← 프로젝트 개요 (현재 파일)
├── CLAUDE.md                          ← AI Agent 팀 공통 컨텍스트
│
├── docs/                              ← 기획 산출물
│   ├── 00_data_registry.md            ← 수치 기준표 (Single Source of Truth)
│   ├── 01_market_analysis.md          ← 시장 분석 · 경쟁사 벤치마킹
│   ├── 02_ringle_service_analysis.md  ← 링글 서비스 심층 분석
│   ├── 03_problem_definition.md       ← 문제 정의 · 솔루션 방향
│   ├── 04_feature_spec.md             ← RING LOOP MVP 기능 스펙
│   ├── 05_wireframe_spec.md           ← 와이어프레임 스펙 (10개 화면)
│   ├── 06_ppt_outline.md              ← PPT 스토리라인
│   ├── 07_concept_board.md            ← 컨셉보드 기획
│   ├── 08_review_report.md            ← 리뷰 리포트
│   └── 09_cross_check.md             ← 문서 간 교차검증
│
├── prototype/                         ← 인터랙티브 프로토타입
│   ├── index.html                     ← RING LOOP MVP 전체 플로우 (9개 화면)
│   ├── chat.html                      ← AI 톡 실제 채팅 (OpenAI GPT 연동)
│   └── voice-demo.html                ← 실시간 음성 데모 (OpenAI Realtime API)
│
├── concept_board.html                 ← 컨셉보드 시안 (A4 세로, HTML)
├── sample_board.html                  ← 컨셉보드 참고 시안
│
├── image/                             ← 이미지 리소스
│   ├── ringle_rogo.webp               ← 링글 로고
│   └── ringle-rogo1.png               ← 링글 로고 (원형)
│
├── report/                            ← 기존 리서치 (읽기 전용)
│   ├── 링글 AI 스피킹 개선 공모전 리서치.pdf
│   ├── 링글 AI 스피킹 개선 공모전 리서치.docx
│   ├── ringle_report_ui.html
│   └── ringle_report_competition_2026-02-26.md
│
├── ringle_competition_notice.md       ← 공모전 공식 안내문
├── ringle_competition_full_content.md ← 비즈니스 케이스 가이드라인
└── 제5회_링글서비스기획&마케팅공모전_포스터_일반.png
```

---

## 프로토타입

### 1. MVP 플로우 프로토타입 (`prototype/index.html`) — 통합 버전

전체 RING LOOP 플로우를 경험할 수 있는 통합 인터랙티브 프로토타입:

| 화면 | 내용 |
|---|---|
| WF-06 온보딩 | 레벨테스트 완료 → 3분 롤플레잉 → AHA Moment |
| **WF-09 AI 톡** | **OpenAI GPT 실시간 채팅 통합** — 한/영 혼용 대화, 영어 표현 코칭, 전화 전환 CTA |
| WF-01/02 브리핑 | 전화 10분 전 톡 내 브리핑 카드 |
| WF-03 전화 수신 | 캐릭터 표시 + 스마트 거절 바텀시트 |
| **WF-04 통화 중** | **GPT 실시간 통화** — AI HR 디렉터(Jennifer Park)와 영어 면접 롤플레이, 실시간 STT/TTS |
| WF-05 Grow 리포트 | CAFP 레이더 차트 + 표현 교정 + 내일 예약 |

**두 가지 모드:**
- **라이브 모드**: ⚙ 설정 → API 키 입력 → 실제 GPT 대화 + 실시간 음성 인식
- **데모 모드**: API 키 없이 "데모 모드" 버튼 → 정적 시나리오

**추가 기능:**
- **다크/라이트 모드**: 좌하단 토글 버튼으로 전환 (설정 유지)
- **iPhone 16 상태바**: SVG 기반 시그널/WiFi/배터리 아이콘 + 실시간 시계

**실행**: `prototype/index.html`을 브라우저에서 열기

### 2. AI 톡 독립 채팅 (`prototype/chat.html`) — 독립 개발용

GPT 채팅 기능만 분리된 독립 인터페이스 (기능 단위 개발/테스트용):

- **모델**: GPT-4o-mini (기본) / GPT-4.1-nano / GPT-4o 등 선택 가능
- **기능**: 한/영 혼용 대화, 비즈니스 영어 표현 코칭, AI 전화 연습 제안
- **API 키**: 설정 화면에서 직접 입력 (로컬 저장, 코드 노출 없음)

**실행**: `prototype/chat.html`을 브라우저에서 열고 → ⚙ 설정에서 OpenAI API 키 입력

### 3. 실시간 음성 데모 (`prototype/voice-demo.html`) — 음성 기능 테스트용

OpenAI Realtime API(WebSocket)를 활용한 실시간 음성 인식 독립 데모:

- **실시간 STT**: OpenAI Realtime API WebSocket 스트리밍 — 말하는 동안 텍스트가 실시간 표시
- **TTS**: OpenAI GPT-4o-mini-TTS — AI 응답을 음성으로 재생
- **GPT 채팅**: 음성 입력 → GPT 대화 → 음성 출력 풀사이클
- **Server VAD**: 서버측 음성 활동 감지로 자동 발화 구간 인식

**실행**: `prototype/voice-demo.html`을 브라우저에서 열고 → API 키 입력

---

## 기술 스택

| 용도 | 기술 |
|---|---|
| 프로토타입 UI | HTML + Tailwind CSS (CDN) + Vanilla JS |
| AI 채팅 | OpenAI GPT-4o-mini API (스트리밍) |
| 실시간 STT | OpenAI Realtime API (WebSocket, gpt-4o-mini-transcribe) |
| STT (배치) | OpenAI GPT-4o Mini Transcribe ($0.003/분) |
| TTS (텍스트→음성) | OpenAI GPT-4o-mini-TTS |
| 차트 | Canvas API (CAFP 레이더 차트) |
| 음성 처리 | Web AudioContext + ScriptProcessor (PCM16 24kHz) |

---

## 팀 구성

| 역할 | 담당 | 산출물 |
|---|---|---|
| Lead (PM) | 전체 조율, 문제 정의, 솔루션 방향 | `03_problem_definition.md` |
| Market Analyst | 경쟁사 분석, 포지셔닝, 트렌드 | `01_market_analysis.md` |
| Service Analyst | 서비스 분석, Pain Point, 유저 여정 | `02_ringle_service_analysis.md` |
| UX Designer | 기능 스펙, 유저 플로우, 와이어프레임 | `04`, `05` |
| Doc Writer | PPT 스토리라인, 컨셉보드 | `06`, `07` |

---

## 변경 이력

| 버전 | 날짜 | 내용 |
|---|---|---|
| v0.1.0 | 2026-03-09 | 초기 커밋: 전체 기획 문서 + 리서치 보고서 |
| v0.2.0 | 2026-03-09 | MVP 인터랙티브 프로토타입 (9개 화면) |
| v0.3.0 | 2026-03-09 | AI 톡 실시간 채팅 독립 버전 (chat.html, OpenAI GPT 연동) |
| v0.4.0 | 2026-03-09 | index.html 통합: Screen 2(AI 톡)에 GPT 라이브 채팅 교체 + 데모 모드 |
| v0.5.0 | 2026-03-09 | 음성 대화 기능: STT (GPT-4o Mini Transcribe) + TTS (GPT-4o-mini-TTS) — chat.html + index.html 동시 적용 |
| v0.6.0 | 2026-03-09 | 실시간 STT: OpenAI Realtime API (WebSocket) 기반 실시간 음성 인식 — voice-demo.html 독립 데모 |
| v0.7.0 | 2026-03-09 | index.html 대규모 통합: chat.html+voice-demo.html 기능 통합, Screen 5 GPT 실시간 통화, iPhone 16 상태바, 다크/라이트 모드 |
| v0.8.0 | 2026-03-13 | 컨셉보드 시안 확정 (A4 세로, 퍼플 그라디언트 헤더 + 라이트 바디), 기획 문서 RING LOOP 용어 통일 |

---

## 라이선스

본 프로젝트는 제5회 링글 서비스 기획 & 마케팅 공모전 출품 목적으로 제작되었습니다.
