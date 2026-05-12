# 세션 인계 문서 (Session Handoff)

> 작성일: 2026-04-27
> 목적: 다른 컴퓨터에서 진행 중인 작업을 이어서 진행하기 위한 핸드오프 문서
> 사용자: ynot@fnfcorp.com
> 프로젝트 루트: `C:\Users\AD1215\dcsai` (다른 PC도 동일 경로 권장)

---

## 1. 진행 중인 프로젝트 요약

| # | 프로젝트 | 상태 | 최신 산출물 |
|---|---------|------|------------|
| 1 | **DX 26SS 대표님 보고자료** | V15 대시보드로 대표님 보고 완료 (2026-04-21). AI 점수 Q&A 방어 성공 | `src/output/dx_mkt_v15_dashboard/` |
| 2 | **MLB 26SS Summer 보고자료** | PPT 초안 12슬라이드 + Dashboard V11 완성, 수정 대기 중 | `src/output/MLB_26SS_Dashboard_V11/`, `src/output/mlb_summer_ai_report.pptx` |

---

## 2. 다른 PC 환경 셋업

### 2.1 필수 사전 조건
- **OS**: Windows 11 권장 (현재 PC와 동일 환경 유지 시 경로 이슈 최소화)
- **Python**: 3.13 (uv로 설치)
- **Claude Code**: 최신 버전 (DCS AI 플러그인 포함)
- **OneDrive**: 동일 계정 로그인 → `보고자료`, `워딩` 폴더 동기화 필요

### 2.2 프로젝트 클론/복사
```bash
# 옵션 A: OneDrive로 dcsai 폴더 동기화 (권장)
# C:\Users\<NEW_USER>\dcsai 가 OneDrive 동기화 폴더 안에 있으면 자동 동기화

# 옵션 B: 직접 복사 (USB/네트워크 드라이브)
# 복사 대상:
#   - C:\Users\AD1215\dcsai\.claude\
#   - C:\Users\AD1215\dcsai\CLAUDE.md
#   - C:\Users\AD1215\dcsai\src\
```

### 2.3 가상환경 셋업
```bash
cd C:\Users\<NEW_USER>\dcsai

# uv 설치 (없는 경우)
# https://github.com/astral-sh/uv#installation

uv venv --python 3.13 .venv
uv pip install polars duckdb python-pptx matplotlib plotly kaleido pyarrow pillow
```

### 2.4 메모리 동기화
```
원본: C:\Users\AD1215\.claude\projects\C--Users-AD1215-dcsai\memory\
대상: C:\Users\<NEW_USER>\.claude\projects\C--Users-<NEW_USER>-dcsai\memory\

복사 파일:
- MEMORY.md
- project_dx_mkt_report.md
- project_mlb_mkt_report.md
```

### 2.5 Claude Code 플러그인 캐시 (DCS AI)
```
경로: ~/.claude/plugins/cache/dcs-ai/
재설치: /dcs-ai-common:Init 슬래시 명령어 실행 (새 PC에서 첫 진입 시)
```

---

## 3. DX 26SS 프로젝트 상세

### 3.1 핵심 스토리라인 (V3 확정, 변경 금지)
```
AI 아젠다 정의 → 닝닝 실행 → 실측 성과 검증 →
AI 브릿지(하이라이트) → 변우석 행사 AI 설계 → 웨이브 제인 전략·로드맵
```

### 3.2 절대 변경 금지 — 실측 데이터
**원본 PPT 실측:**
- PR 보도자료: POST 15, TTL 노출 264만, AVG IMP 14.7만
- 메가·파워페이지: POST 18
- 인플루언서: POST 240, TTL IMP 856.2만, AVG IMP 3.6만, TTL ENG 41.9만, AVG ENG 1,748

**DCS AI 지식그래프 실측 (BRD_CD='X', 3/1~4/17):**
- 웨이브 제인 26SS: 3.82억원 · 4,158 qty (운동화 3위)
- 웨이브 제인 25SS: 1.04억원 · 1,156 qty (운동화 17위)
- **YoY +266% 매출, +260% 수량, ▲14단계**

### 3.3 사용 금지 (허위/샘플 수치)
- ❌ 12.8M 도달, 4.7% 인게이지먼트, 8.2억원 PR 광고환산가
- ❌ Instagram/YouTube/TikTok/Weibo/RED 채널별 분해
- ❌ "업계 평균 2.1% 대비 2.2x", "92pt 감성 일치도"
- → `src/service/dx_mkt_report/sample_data.py` 출처. 절대 실수치로 인용 금지

### 3.4 산출물 위치
| 항목 | 경로 |
|------|------|
| PPT v3 (최종) | `src/output/dx_mkt_ai_report_v3.pptx` |
| PPT 빌드 스크립트 | `src/service/dx_mkt_report/build_pptx_v2.py` |
| **HTML V15 (최신)** | `src/output/dx_mkt_v15_dashboard/DX_26SS_V15_DASHBOARD.html` |
| V15 배포 ZIP | `src/output/dx_mkt_v15_dashboard/DX_V15_DEPLOY.zip` |
| 보존 버전 | `dx_mkt_v3_dashboard` ~ `dx_mkt_v14_dashboard` (롤백/비교용) |
| 사용자 canonical base | V6 (`dx_mkt_v6_dashboard` — 느좋남 단일 통합) |

### 3.5 V14 대비 V15 보정 내역
- Tab1: 닝닝 썸머 릴리즈 3컷 `max-width:720px`로 축소
- Tab3 Section 1: 캡처 이미지 → 원본 포토(`slide07_img056/062/066`) 교체
- Tab3 Zone 카드: `wide-ratio` → `contain-img` (잘림 방지)
- Tab3 느좋남: 변우석 앰버서더 컷 복원 + 4컷 + 카드 컴팩트화
- Tab4 25SS GOOD/BAD: 카드 내부에 gy1~gy4 임베드
- Tab4 PHASE 3: 제휴몰 기획전 이미지(`slide17_img132.png`) 추가
- Tab4 CAD: 1장 → 6장 그리드(`cad12~17.png`)

### 3.6 스타일 시스템 (V11+)
`tab*.html` 내부 inline CSS:
- `.portrait` — aspect-ratio 3/4 (인물)
- `.wide-ratio` — aspect-ratio 16/9 (공간, 세로 잘림 가능)
- `.contain-img` — object-fit:contain (원본 비율 유지, 캡처/스크린샷 안전)

### 3.7 다음 작업 시 원칙
- 큰 구조 변경 → V16 신규 폴더 생성 (V15 보존)
- 작은 텍스트/이미지 교체 → V15 내부 직접 수정 가능
- 실측 수치(264만·856.2만·+266%) 절대 변경 금지
- 이미지 잘림 이슈 → `contain-img` 클래스로 해결

---

## 4. MLB 26SS Summer 프로젝트 상세

### 4.1 핵심 스토리라인
```
26SS AI 핵심 인사이트(힙페미닌 × K-POP × 페스티벌) →
1차 카리나 릴리즈 성과 →
AI 2차 분석(페스티벌/워터밤/메가 인플루언서) →
3단 파동 2차 전략 로드맵
```

### 4.2 12 슬라이드 구성
| # | 슬라이드 |
|---|---------|
| S01 | Cover |
| S02 | Agenda |
| S03 | 26SS AI 핵심 인사이트 |
| S04 | 카리나 썸머 릴리즈 |
| S05 | 1차 성과 KPI |
| S06 | 힙페미닌 무드 확산 |
| S07 | AI 2차 분석 |
| S08 | 워터밤 심층분석 |
| S09 | 메가 인플루언서 선정 |
| S10 | 3단 파동 로드맵 |
| S11 | 워터밤 실행 상세 |
| S12 | 기대효과·다음액션 |

### 4.3 산출물 위치
| 항목 | 경로 |
|------|------|
| **PPT 초안** | `src/output/mlb_summer_ai_report.pptx` (17.8MB, 12슬) |
| 원본 PPT (로컬) | `src/service/mlb_mkt_report/source.pptx` (69MB, 11슬) |
| 추출 이미지 (200개) | `src/service/mlb_mkt_report/pptx_images/slideNN_imgXXX.{png,jpg}` |
| **Dashboard V11 (최신)** | `src/output/MLB_26SS_Dashboard_V11/index.html` |
| V11 배포 ZIP | `src/output/MLB_26SS_Dashboard_V11.zip` |
| Dashboard 초기 (V1/V2) | `src/output/mlb_summer_dashboards/MLB_26SS_AI_DASHBOARD.html`, `_V2.html` |
| 빌드 스크립트 | `src/service/mlb_mkt_report/build_pptx.py`, `build_v7.py`, `build_v8.py` |
| 이미지 추출 | `src/service/mlb_mkt_report/extract_images.py` |
| 사용자 피드백 PPT | `src/output/[MLB] 26SS 카리나 썸머 1차 결과 및 페스티벌 보고_AI 수정 요청!.pptx` |

### 4.4 결정사항/규칙
- "셀럽 PPL" 워딩 금지 → **메가 인플루언서** 사용
- 컬러 테마: MLB_NAVY(#0C2040) + MLB_RED(#C8102E) + 핑크 액센트
- 기존 PPT 이미지 최대한 활용 (카리나 얼굴컷, 힙페미닌 무드컷, 워터밤 레퍼런스)

### 4.5 재사용 패턴 (DX 프로젝트와 공통)
- `src/util/pptx_utils.py` 헬퍼 함수 활용
- 로컬 헬퍼: `_ai_badge()`, `_kpi_row()`, `_img()`
- `add_bullet_box(positive=True/False)` 인사이트 박스
- 한글 경로 이슈: OneDrive 파일은 로컬 복사 후 처리, `PYTHONUTF8=1` 필요

---

## 5. 실행 환경 & 명령어 치트시트

### 5.1 PYTHONPATH (Windows)
```bash
# src/ 패키지 임포트하는 스크립트 실행 시
PYTHONPATH=. .venv/Scripts/python src/service/dx_mkt_report/build_pptx_v2.py
PYTHONPATH=. .venv/Scripts/python src/service/mlb_mkt_report/build_pptx.py
```

### 5.2 한글 경로 처리
```bash
PYTHONUTF8=1 PYTHONPATH=. .venv/Scripts/python <script>
```

### 5.3 dcs-ai-cli (DCS AI API 호출)
```bash
dcs-ai-cli fetch --endpoint /api/kg/execute --method POST \
  --body '{"data_type":"list","..."}' --name sales_data
# 결과: %TEMP%\dcs-ai-cli\sales_data_<timestamp>.json
```

### 5.4 결과물 저장 위치 규칙
| 상황 | 위치 |
|------|------|
| 사용자 명시적 다운로드 | `src/download/` |
| 토큰 큰 데이터 자동 저장 | `%TEMP%\dcs-ai-cli\` |
| 분석 결과물 (PPT/HTML/차트) | `src/output/` |

---

## 6. 다음 세션 재개 포인트

### 6.1 DX 26SS
- ✅ 대표님 보고 완료 (2026-04-21)
- ⏳ 추가 수정 요청 시 V16 폴더 생성 후 작업
- 🔒 실측 수치 변경 금지

### 6.2 MLB 26SS
- ⏳ 사용자 피드백 PPT(`[MLB] 26SS 카리나 썸머 1차 결과 및 페스티벌 보고_AI 수정 요청!.pptx`) 반영 작업 대기
- ⏳ Dashboard V11 → V12 보정 가능

### 6.3 첫 명령어 추천 (다른 PC에서)
```
1. Claude Code 진입
2. cd C:\Users\<NEW_USER>\dcsai
3. claude (또는 IDE 통합)
4. 아래 메시지 입력:
   "MEMORY.md 확인하고 DX/MLB 프로젝트 현재 상태 알려줘.
    src/output/SESSION_HANDOFF.md 가 인계 문서야."
```

---

## 7. 체크리스트

### 새 PC 셋업 체크리스트
- [ ] Python 3.13 + uv 설치
- [ ] `dcsai/` 폴더 동기화 (OneDrive 또는 직접 복사)
- [ ] `.venv` 생성 + 필수 라이브러리 설치
- [ ] `~/.claude/projects/.../memory/` 메모리 파일 복사
- [ ] DCS AI 플러그인 `/dcs-ai-common:Init` 실행
- [ ] `dcs-ai-cli` 인증 확인
- [ ] OneDrive `보고자료`, `워딩` 폴더 동기화 확인
- [ ] V15 대시보드 브라우저로 정상 열림 확인
- [ ] V11 MLB 대시보드 브라우저로 정상 열림 확인

### 작업 재개 시 확인사항
- [ ] CLAUDE.md 규칙 (`.claude/rules/`) 숙지
- [ ] DX 실측 수치 변경 금지 인지
- [ ] "셀럽 PPL" 금지, "메가 인플루언서" 사용 인지
- [ ] V14/V15 같은 버전 보존 원칙 인지

---

*인계 끝. 새 PC에서도 동일한 산출물 품질로 작업 이어가실 수 있습니다.*
