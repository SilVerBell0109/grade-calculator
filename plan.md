# 구현 계획 (Plan)

## 파일별 구현 순서

1. `style.css` — 공통 토큰·컴포넌트
2. `index.html` — 랜딩 (과목 카드 2개)
3. `ds.html` — 자료구조 계산기
4. `cpp.html` — C++ 계산기
5. 배포 — git init → gh repo create → Pages 설정

---

## style.css 체크리스트

- [ ] CSS 변수 (--bg, --text 등) 라이트 모드
- [ ] CSS 변수 다크 모드 (`@media prefers-color-scheme: dark`)
- [ ] body, container 기본 스타일
- [ ] nav 스타일 (.nav, .nav-brand, .nav-links, .nav-link.active)
- [ ] .section-label (11px, uppercase, letter-spacing)
- [ ] .input-card (bg, border, radius-md, padding)
- [ ] input[type=number] 공통 스타일 + 스핀버튼 제거
- [ ] .result-card (bg, border-strong, radius-lg, padding)
- [ ] .score-total (48px, mono)
- [ ] .grade-badge (30px, mono, padding, radius-md)
- [ ] 등급 뱃지 색상 9종 (grade-ap ~ grade-f), 라이트/다크
- [ ] .bar-track (6px, bg-secondary, radius 3px)
- [ ] .bar-fill (transition 0.35s cubic-bezier)
- [ ] .bar-row 레이아웃 (항목명, 바, 값)
- [ ] .hint-text (text-secondary, font-size 13px)
- [ ] .convert-hint (11px, text-tertiary, mono)
- [ ] .footer-formula (text-tertiary, font-size 11px, mono)

---

## index.html 체크리스트

- [ ] nav (성적 계산기 / 자료구조 / C++)
- [ ] 페이지 타이틀 + 부제 (2026-1학기)
- [ ] 과목 카드 2개 (자료구조 / C++) — flex/grid로 나란히
  - [ ] 자료구조: 중간 35% / 기말 40% / 과제 20% / 출석 5점 / PCCE +10점
  - [ ] C++: 중간 20% / 기말 20% / 향상 보너스 / 과제 35% / 프로젝트 15% / 출석 5% / PCCE 5%
- [ ] 각 카드 → `계산하기 →` 버튼

---

## ds.html 체크리스트

- [ ] nav (C++ 링크 / 자료구조 active)
- [ ] 페이지 헤더 (이상환 교수 / 절대평가 ABF / 2026-1)
- [ ] 중간고사 입력 (id=mid, 0-91, 기본75) + 환산값 표시
- [ ] 기말고사 입력 (id=fin, 0-91, 기본0) + 환산값 표시
- [ ] 과제물 입력 (id=hw, 0-100, 기본100)
- [ ] 출석 입력 (id=att, 0-5 step0.5, 기본5)
- [ ] PCCE 입력 (id=pcce, 0-1000, 기본0) + 보너스 환산값 표시
- [ ] 결과 카드: 총점 + 등급 뱃지
- [ ] 힌트 텍스트 (A+ 달성 여부)
- [ ] 바 차트 5항목 (mid/fin/hw/att/pcce)
- [ ] 등급표 (ABF 기준) + ABF 제외 등급 주석
- [ ] footer 공식
- [ ] getGrade(), calc() 함수

---

## cpp.html 체크리스트

- [ ] nav (자료구조 링크 / C++ active)
- [ ] 페이지 헤더 (절대평가 / 2026-1)
- [ ] 중간고사: mid-short(0-40,기본22) + mid-code(0-60,기본60) + 합계 표시
- [ ] 기말고사 `6/11(목) 18:00`: fin-short(0-40,기본0) + fin-code(0-60,기본0) + 합계 표시
- [ ] 기타 2열 그리드: pcce / proj / hw / att
- [ ] 결과 카드: 총점 + 등급 뱃지
- [ ] 힌트 텍스트 (A+ 달성 여부)
- [ ] 바 차트 7항목 (mid/fin/bonus/hw/proj/att/pcce)
- [ ] 등급표 (절대평가 9단계)
- [ ] footer (향상분 공식)
- [ ] getGrade(), calc() 함수

---

## wcc.html 체크리스트

### HTML 구조
- [ ] nav (자료구조/C++/DB/논리회로 + 웹클라이언트 active)
- [ ] 헤더: `웹클라이언트컴퓨팅 성적 계산기` / `이다원 교수 · 국민대 소융대 · 2026-1학기`

### 입력 섹션
- [ ] 시험 섹션 레이블: `시험 ×20%` — **2열 그리드**
  - [ ] `mid`: 중간고사 0-100 기본0, 서브 `×20% · 7주차 4/14`
  - [ ] `fin`: 기말고사 0-100 기본0, 서브 `×20% · 14주차 6/2`
- [ ] 수행과제 섹션
  - [ ] `proj`: 프로젝트 0-100 기본0, 서브 `×35% · HTML/CSS/JS 웹 제작`
  - [ ] `hw`: 과제물 0-100 기본0, 서브 `×15% · 실습과제`
- [ ] 참여 섹션
  - [ ] `att`: 출석 0-100 기본100, 서브 안내 `100 = 결석 없음 기준`

### 결과 카드
- [ ] 상단: 총점(48px mono, toFixed(2)) + 최저항목 텍스트 + 등급 뱃지
- [ ] 구분선
- [ ] 바 차트 5항목 (mid/fin/proj/hw/att) — 각 max 점수 기준 비율
  - [ ] 중간고사 ×0.20 → max 20, 색상 `#378ADD`
  - [ ] 기말고사 ×0.20 → max 20, 색상 `#1D9E75`
  - [ ] 프로젝트 ×0.35 → max 35, 색상 `#7F77DD`
  - [ ] 과제물 ×0.15 → max 15, 색상 `#639922`
  - [ ] 출석 ×0.10 → max 10, 색상 `#BA7517`
- [ ] 힌트: A+(95) 달성 시 달성 메시지 / 미달 시 A+까지 N.NN점 + 다음 등급까지 N.NN점

### 목표 역산 섹션 (결과 카드와 등급표 사이)
- [ ] 세그먼트 버튼: A+ / A0 / B+ / B0 (기본 A0 선택)
- [ ] 부족 점수 표시
- [ ] 현재 0점 항목 목록
- [ ] 0점 항목 만점 가정 시 예상 총점 + 달성 가능 여부

### 등급 기준표 카드
- [ ] 9개 등급 행 (A+~F)
- [ ] 각 행: 뱃지 + 진행 바(현재 총점 위치) + 기준점
- [ ] 현재 해당 등급 행 `background: var(--bg-secondary)` 하이라이트

### 공통 연동
- [ ] index.html에 웹클라이언트컴퓨팅 subject-card 추가
- [ ] 모든 html 파일 nav에 `wcc.html` 링크 추가

### JS 함수
- [ ] `clamp(v, mn, mx)`
- [ ] `getGrade(total)` — GRADES 배열 기반
- [ ] `calc()` — 총점, 바 차트, 등급, 힌트, 역산, 등급표 하이라이트 동시 업데이트
- [ ] 모든 input에 `addEventListener('input', calc)` + 로드 시 즉시 `calc()`

### 검증 케이스
- [ ] 모든 0 → 총점 0.00, F
- [ ] 모든 100 → 총점 100.00, A+
- [ ] mid=80, fin=80, proj=90, hw=100, att=100 → 88.50, B+
- [ ] 목표 A0(90) 역산 정확도 확인

---

## 배포 체크리스트

- [ ] `git init`
- [ ] `git add .`
- [ ] `git commit -m "init: 성적 계산기 웹사이트"`
- [ ] `gh repo create kmu-grade-calculator --public --source=. --push`
- [ ] GitHub Pages 설정 (main 브랜치 루트)
- [ ] 배포 URL 확인 출력
