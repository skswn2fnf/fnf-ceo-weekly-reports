# DCS AI 프로젝트 작업 인수인계 가이드

> 작성일: 2026-04-27
> 대상: 다른 컴퓨터에서 동일한 작업 환경을 구성하고 이어서 진행하기 위한 가이드

---

## 1. 진행 중인 프로젝트 요약

현재 두 개의 대표님 보고자료 프로젝트가 진행 중입니다.

### 1-1. DX(Discovery) 26SS MKT 보고자료
- **상태**: V15 대시보드로 대표님 보고 완료 (2026-04-21)
- **핵심 스토리라인**: AI 아젠다 정의 → 닝닝 실행 → 실측 성과 검증 → AI 브릿지(하이라이트) → 변우석 행사 AI 설계 → 웨이브 제인 전략·로드맵
- **AI 점수 Q&A 스크립트 방어 성공** — 이후 추가 수정사항 발생 시 V15 기준으로 진행

### 1-2. MLB 26SS Summer 보고자료
- **상태**: 카리나 1차 성과 + AI 2차 전략(워터밤·메가 인플루언서) PPT 초안 12슬라이드 완성
- **핵심 스토리라인**: 26SS AI 핵심 인사이트(힙페미닌 × K-POP × 페스티벌) → 1차 카리나 릴리즈 성과 → AI 2차 분석 → 3단 파동 2차 전략 로드맵
- **현재 상태**: 수정 대기 중

---

## 2. 다른 컴퓨터에서 환경 구성하기

### 2-1. 사전 설치 필요
- **Claude Code**: https://claude.com/claude-code 설치
- **uv** (Python 패키지 매니저): https://github.com/astral-sh/uv
- **Git** (선택): 폴더 동기화용
- **OneDrive 동기화** 또는 **외장 디스크/USB**: 프로젝트 폴더 전체 복사

### 2-2. 프로젝트 폴더 복사
복사 대상 경로: `C:\Users\AD1215\dcsai\` (Windows 기준)

복사할 핵심 항목:
```
dcsai/
├── CLAUDE.md                       # 프로젝트 표준 (반드시 복사)
├── .claude/                        # 규칙·스킬·설정 (반드시 복사)
│   ├── rules/                      # dcsai-business-analysis.md, dcsai-tools.md, dcsai-visualization.md
│   ├── skills/                     # chart-visualization, data-processing, html-report, pptx-report 등
│   └── settings.local.json
├── .gitignore
├── src/
│   ├── util/                       # pptx_utils, chart_utils, plotly_utils, html_utils, data_stats_utils
│   ├── service/
│   │   ├── dx_mkt_report/          # DX 빌드 스크립트 + 추출 이미지
│   │   └── mlb_mkt_report/         # MLB 빌드 스크립트 + 추출 이미지 + source.pptx
│   └── output/                     # PPT·HTML 대시보드 결과물
│       ├── dx_mkt_v15_dashboard/   # DX 최신
│       ├── MLB_26SS_Dashboard_V11/ # MLB 최신
│       ├── dx_mkt_ai_report_v3.pptx
│       └── mlb_summer_ai_report.pptx
└── 보고자료/, 워딩/                  # 원본 자료 폴더
```

> **주의**: `.venv/` 폴더는 복사하지 말고, 새 컴퓨터에서 다시 생성합니다(아래 2-3 참조).

### 2-3. Python 가상환경 재구성
복사 후 새 컴퓨터에서 프로젝트 루트로 이동하여 실행:

```bash
# 1) Python 3.13 가상환경 생성
uv venv --python 3.13

# 2) 필수 라이브러리 설치
uv pip install polars duckdb python-pptx matplotlib plotly kaleido pyarrow

# 3) 동작 확인
PYTHONPATH=. .venv/Scripts/python -c "import polars, duckdb, pptx, matplotlib, plotly, kaleido, pyarrow; print('ok')"
```

> macOS/Linux에서는 `.venv/bin/python`을 사용합니다.

### 2-4. dcs-ai-cli 사용 가능 여부 확인
DCS AI API 호출은 `dcs-ai-cli`로만 합니다.
```bash
dcs-ai-cli --help
```
- 명령어가 없으면 사내에서 설치/인증 절차를 별도 진행해야 합니다.
- 결과 파일은 자동으로 `{TMPDIR}/dcs-ai-cli/`에 저장됩니다.

### 2-5. Claude Code에서 프로젝트 열기
```bash
cd C:\Users\AD1215\dcsai
claude
```
- 첫 실행 시 `CLAUDE.md`가 자동 로드되어 DCS AI 표준 규칙이 적용됩니다.
- 메모리 파일(`MEMORY.md`)은 컴퓨터별로 분리됩니다. 필요 시 `C:\Users\AD1215\.claude\projects\C--Users-AD1215-dcsai\memory\` 디렉토리도 함께 복사하세요.

---

## 3. 핵심 산출물 위치

### 3-1. DX 26SS
| 항목 | 경로 |
|------|------|
| PPT v3 (실측 데이터, 11슬라이드) | `src/output/dx_mkt_ai_report_v3.pptx` |
| PPT 빌드 스크립트 | `src/service/dx_mkt_report/build_pptx_v2.py` |
| **HTML 대시보드 V15 (최신)** | `src/output/dx_mkt_v15_dashboard/DX_26SS_V15_DASHBOARD.html` |
| 대시보드 보존 버전 | `dx_mkt_v3_dashboard` ~ `dx_mkt_v15_dashboard` (V3~V15 모두 보존) |
| 추출 이미지 | `src/service/dx_mkt_report/pptx_images/` |

### 3-2. MLB 26SS
| 항목 | 경로 |
|------|------|
| PPT 초안 (12슬라이드) | `src/output/mlb_summer_ai_report.pptx` |
| PPT 빌드 스크립트 | `src/service/mlb_mkt_report/build_pptx.py` |
| **HTML 대시보드 V11 (최신)** | `src/output/MLB_26SS_Dashboard_V11/index.html` |
| 추출 이미지 | `src/service/mlb_mkt_report/pptx_images/` (200개) |
| 원본 PPT 로컬 복사본 | `src/service/mlb_mkt_report/source.pptx` |

---

## 4. 절대 변경 금지 — 실측 데이터 (DX 프로젝트)

**원본 PPT 실측 (PR/콘텐츠 성과):**
- PR 보도자료: POST 15, TTL 노출 264만, AVG IMP 14.7만
- 메가·파워페이지: POST 18
- 인플루언서: POST 240, TTL IMP 856.2만, AVG IMP 3.6만, TTL ENG 41.9만, AVG ENG 1,748

**DCS AI 지식그래프 실측 (한국 상품 매출 분석, BRD_CD='X', 3/1~4/17):**
- 웨이브 제인 26SS: 3.82억원 · 4,158 qty (운동화 3위)
- 웨이브 제인 25SS: 1.04억원 · 1,156 qty (운동화 17위)
- **YoY +266% 매출, +260% 수량, ▲14단계** — 닝닝 착용 제품 실판매 증빙

### 절대 다시 사용하지 말 것 (sample_data.py에서 유래한 허위 수치)
- ❌ 12.8M 도달, 4.7% 인게이지먼트, 8.2억원 PR 광고환산가
- ❌ Instagram/YouTube/TikTok/Weibo/RED 채널별 분해
- ❌ "업계 평균 2.1% 대비 2.2x", "92pt 감성 일치도"

---

## 5. 작업 재개 시 원칙

### 5-1. 버전 관리 원칙
- **큰 구조 변경**: 새 폴더(V16, V12 등)를 생성하여 진행, 기존 버전 보존
- **작은 텍스트/이미지 교체**: 최신 버전 폴더 내부에서 직접 수정 가능
- 사용자의 canonical base는 DX의 경우 V6 (느좋남 단일 통합)

### 5-2. 스타일 시스템 (V11~V15에서 사용 중)
이미지 카드 클래스 (각 `tab*.html` 내부 inline CSS):
- `.portrait` — aspect-ratio 3/4 (인물 컷)
- `.wide-ratio` — aspect-ratio 16/9 (공간 컷, 단 세로 잘림 가능)
- `.contain-img` — object-fit:contain (원본 비율 유지, 캡처/스크린샷에 안전)

### 5-3. 워딩 규칙 (MLB)
- "셀럽 PPL" 워딩 금지 → **"메가 인플루언서"** 사용
- 컬러 테마: MLB_NAVY(#0C2040) + MLB_RED(#C8102E) + THEME_LIGHT 공통

---

## 6. DCS AI 코딩 표준 핵심 (반드시 준수)

> 상세 내용: `CLAUDE.md`, `.claude/rules/dcsai-*.md` 참조

### 6-1. 코드 작성 전
- `.claude/skills/` 와 `src/util/` 의 기존 유틸리티를 **먼저 확인**
- 기존 유틸리티가 있으면 직접 코드 작성 대신 활용

### 6-2. Python 실행
- 반드시 `.venv` 내의 python 사용
- `src/` 임포트 시 `PYTHONPATH=.` 설정
  - Windows: `PYTHONPATH=. .venv/Scripts/python src/service/xxx/script.py`
  - macOS/Linux: `PYTHONPATH=. .venv/bin/python src/service/xxx/script.py`
- Python 코드는 `.py` 파일로 저장 후 실행 (`bash -c` 멀티라인 금지)

### 6-3. 데이터 조회 규칙
- API 호출은 `curl` 금지 → 반드시 `dcs-ai-cli` 사용
- **1500토큰 미만**: `execute_kg_api_to_context` MCP로 context 로드
- **1500토큰 이상**: `dcs-ai-cli`로 파일 저장 후 코드 분석 (data-processing 스킬 활용)
- 사이즈 점검: `meta_info.data_size_only=true`로 먼저 토큰 크기 확인

### 6-4. 데이터 저장 위치
| 상황 | 저장 위치 |
|------|-----------|
| 사용자 명시적 "파일 다운로드" | `src/download/` |
| 토큰 큰 데이터 분석용 자동 저장 | `{TMPDIR}/dcs-ai-cli/` |
| 분석 결과물(리포트/차트) | `src/output/` |

### 6-5. 시각화 라이브러리 선택
- 단순 차트(bar/line/pie) + PPTX → `chart-visualization` 스킬 (matplotlib)
- 단순 차트 + HTML → `html-report` 스킬 (Chart.js)
- 복잡 차트(treemap/sankey/funnel/heatmap/multi_axis) → `chart-visualization-plotly` 스킬 (Plotly)

---

## 7. 다음 세션 재개 체크리스트

다른 컴퓨터에서 작업을 처음 시작할 때 다음 순서로 확인:

- [ ] 프로젝트 폴더 복사 완료 (`C:\Users\AD1215\dcsai\`)
- [ ] `.venv/` 재구성 + 필수 라이브러리 설치 확인
- [ ] `dcs-ai-cli` 명령어 동작 확인
- [ ] `CLAUDE.md` 가 자동 로드되는지 Claude Code 첫 실행 시 확인
- [ ] 메모리 파일 복사 또는 신규 작성 (`memory/MEMORY.md` + 개별 `.md`)
- [ ] DX V15 / MLB V11 대시보드 정상 렌더링 확인 (브라우저로 `index.html` 열기)
- [ ] PPT 파일 정상 열림 확인 (`dx_mkt_ai_report_v3.pptx`, `mlb_summer_ai_report.pptx`)

---

## 8. 참고 — 메모리 파일 위치

현재 컴퓨터의 메모리 위치:
```
C:\Users\AD1215\.claude\projects\C--Users-AD1215-dcsai\memory\
├── MEMORY.md                       # 인덱스
├── project_dx_mkt_report.md        # DX 프로젝트 상세 상태
└── project_mlb_mkt_report.md       # MLB 프로젝트 상세 상태
```

다른 컴퓨터로 이전 시 동일 사용자명일 경우 같은 경로, 다른 사용자명이면 `C:\Users\{user}\.claude\projects\` 하위에서 동일 구조로 생성됩니다.

---

> 본 가이드는 `src/output/WORK_HANDOVER_GUIDE.md`에 저장되어 있습니다.
> 작업 진행 사항이 변경될 때마다 이 문서도 함께 업데이트하시기 바랍니다.
