# 5월 13일주차 CEO 보고자료

> 작성 기준일: 2026-05-13 (5월 둘째주)
> 위치: `Desktop/대표님 보고자료/5월 13일주차 CEO 보고자료/`
> 디자인: CEO 선호 패턴 적용 (KARINA EDITION VOL.2 기반)

---

## 1. 폴더 구성

```
5월 13일주차 CEO 보고자료/
├── INDEX_DASHBOARD.html   # 통합 대시보드 (4개 탭 iframe 로드)
├── tab1.html              # 패턴 라이브러리 포함 (참고용 + 콘텐츠 영역)
├── tab2.html              # 클린 스타터 (hero + section + card)
├── tab3.html              # 클린 스타터
├── tab4.html              # 클린 스타터
├── assets/                # 이미지/영상 자산
└── README.md              # 본 가이드
```

대시보드 열기: `INDEX_DASHBOARD.html` 브라우저로 더블클릭.

---

## 2. 디자인 시스템 (CEO 선호 패턴)

전임자 산출물(KARINA EDITION VOL.2, MLB VALIRAM) 분석 결과 CEO가 선호한 디자인 요소:

- **폰트**: `Outfit` (sans, 본문) + `DM Serif Display` (serif, 헤딩·숫자)
- **컬러**: Sky blue 메인 (`--s0~s5`) + Dark navy 헤로 그라디언트
- **위계**: Hero → Section 라벨 → Card → Insight 박스
- **장식 최소화**: 둥근 모서리 + soft shadow + 1px 보더. 무지개 그라디언트·sparkle 등 화려한 장식은 빼고 정돈된 톤 유지.

### 2.1 색상 토큰 (CSS 변수)

| 토큰 | 값 | 용도 |
|------|-----|------|
| `--s0` ~ `--s5` | #F0F8FD → #1A7FAA | 스카이블루 (메인) |
| `--bg` | #F4F9FD | 페이지 배경 |
| `--t1~t4` | #0F2733 → #A0BCC8 | 텍스트 (어두움 → 옅음) |
| `--bdr` | rgba(58,164,205,.18) | 보더 |
| `--grn` / `--grn-bg` | #2EAA78 / #E8F7F1 | 긍정 |
| `--red` / `--red-bg` | #E05A6B / #FEF0F2 | 부정·리스크 |
| `--amb` / `--amb-bg` | #D4882A / #FDF3E3 | 주의 |
| `--lav` | #7B68D4 | 포인트 |
| `--rad` | 14px | 카드 둥근 모서리 |
| `--sh` | 0 2px 18px rgba(58,164,205,.10) | Soft shadow |

---

## 3. 패턴 라이브러리 (tab1.html에 모두 구현됨)

### 3.1 Hero 섹션
다크 그라디언트 + radial overlay + 3컬럼 핵심 인사이트.
```html
<div class="hero">
  <div class="hero-eye">TAB 1 · 핵심 인사이트</div>
  <div class="hero-title">메인 헤드라인</div>
  <div class="hero-body">서브 카피 (b 태그로 강조)</div>
  <div class="h3">
    <div class="h3c"><div class="h3c-icon">📌</div><div class="h3c-t">제목</div><div class="h3c-b">본문</div></div>
    ...
  </div>
</div>
```

### 3.2 Section 라벨
`01 · SECTION TITLE` + 우측 가로선.
```html
<div class="sec">01 · KEY METRICS</div>
```

### 3.3 KPI 4카드 (상단 액센트 스트라이프)
```html
<div class="kpi4">
  <div class="kpi">
    <div class="kl">지표명</div>
    <div class="kv">0.0M</div>
    <div class="kn">단위·비고</div>
    <span class="kb kb-g">+0.0% YoY</span>  <!-- kb-g 긍정 / kb-s 중립 -->
  </div>
</div>
```

### 3.4 Insight 박스 (4종)
| 클래스 | 용도 |
|--------|------|
| `.ins`   | 일반 인사이트 (blue) |
| `.ins-g` | 긍정 신호 (green) |
| `.ins-a` | 주의·관찰 (amber) |
| `.ins-r` | 부정·리스크 (red) |

```html
<div class="ins"><b>관전 포인트:</b> 본문…</div>
```

### 3.5 Numbered cards (Strategy / Next step)
```html
<div class="sg">
  <div class="sc">
    <div class="sn">01</div>
    <div class="st">제목</div>
    <div class="sb">설명</div>
  </div>
</div>
```

### 3.6 이미지 클래스 (V11+ 시스템)
| 클래스 | 용도 |
|--------|------|
| `.portrait` | aspect-ratio 3/4 — 인물 |
| `.wide-ratio` | aspect-ratio 16/9 — 공간 |
| `.contain-img` | object-fit:contain — 캡처/스크린샷 안전 (잘림 방지) |

---

## 4. 작성 순서

1. **콘텐츠 기획 확정** — 이번 주 4개 탭 주제 결정
2. **INDEX_DASHBOARD.html 헤더/탭명 수정**
   - `.hdr-logo`, `.hdr-sub` (헤더 카피)
   - `.hdr-pills` (상단 우측 뱃지)
   - 4개 `.tab-btn` 라벨
   - 4개 `.loading-text` 라벨
3. **tab1.html → tab4.html 콘텐츠 작성**
   - hero `.hero-eye`, `.hero-title`, `.hero-body`, `.h3c` 교체
   - 필요한 section만 남기고 패턴 라이브러리에서 복사·붙여넣기
   - 이미지는 `assets/` 폴더에 저장 후 `<img src="assets/파일명">` 참조
4. **브라우저 검증** — `INDEX_DASHBOARD.html` 열고 4개 탭 모두 정상 렌더링 확인

---

## 5. 다음 주차 작업 시

1. 새 폴더 생성: `Desktop/대표님 보고자료/5월 20일주차 CEO 보고자료/`
2. 본 폴더 전체 복사 → 기준일 변경
3. 위 작성 순서대로 콘텐츠 갱신

> 큰 구조 변경(레이아웃·탭 개수 변동)은 새 버전 폴더로 분리해 이전 버전을 보존합니다.
