# 구현 계획 요약 (Research)

## 프로젝트 구조

```
my_grade/
├── index.html   — 과목 선택 랜딩
├── ds.html      — 자료구조 계산기
├── cpp.html     — C++ 프로그래밍 계산기
├── db.html      — 데이타베이스 계산기
├── wcc.html     — 웹클라이언트컴퓨팅 계산기  ← NEW
└── style.css    — 공통 스타일
```

---

## 공통 요소

- **디자인 토큰**: CSS 변수 (라이트/다크 자동 전환)
- **Nav**: 사이트명(index) + 자료구조/C++ 링크, 현재 페이지 active
- **입력 카드**: bg(white/dark), border 0.5px, radius-md
- **숫자 입력**: 모노 폰트, 80px, right-align, 스핀버튼 제거
- **결과 카드**: 총점 48px 모노 + 등급 뱃지 30px
- **바 차트**: 6px 트랙, 색상별 fill, 0.35s 트랜지션
- **등급 뱃지**: 9가지 색상 클래스 (style.css 1회 정의)
- **clamp 입력 보호** + 페이지 로드 즉시 `calc()` 호출

---

## ds.html 핵심 로직

```
총점 = (mid/91×100)×0.35 + (fin/91×100)×0.40 + (hw/100)×0.20 + att + pcceBonus
pcceBonus = pcce <= 100 ? 0 : (pcce-100)/900 * 10
```

- 입력: mid(0-91,기본75), fin(0-91,기본0), hw(0-100,기본100), att(0-5 step0.5,기본5), pcce(0-1000,기본0)
- mid/fin 아래 100점 환산값 표시
- PCCE 아래 보너스 환산값 표시
- getGrade: 80↑A+, 70↑A0, 60↑B+, 50↑B0, 나머지 C+/C0/D+/D0/F (ABF는 50↓=F)
- 힌트: A+(80) 달성여부 + 다음 등급까지 거리

## cpp.html 핵심 로직

```
midTotal = mid-short + mid-code
finTotal = fin-short + fin-code
bonus = max(0, finTotal - midTotal) × 0.5
총점 = midTotal×0.20 + finTotal×0.20 + bonus + (hw/100)×35 + (proj/100)×15 + (att/5)×5 + (pcce/1000)×5
```

- 입력: mid-short(0-40,기본22), mid-code(0-60,기본60), fin-short(0-40,기본0), fin-code(0-60,기본0)
- 기타: pcce(0-1000,기본1000), proj(0-100,기본100), hw(0-100,기본100), att(0-5 step0.1,기본5)
- 향상분 보너스 최대 10점 (바차트 max=10)
- getGrade: 90↑A+, 80↑A, 70↑B+, 60↑B, 50↑C+, 40↑C, 30↑D+, 20↑D, F

---

## wcc.html 핵심 로직

```
총점 = mid×0.20 + fin×0.20 + proj×0.35 + hw×0.15 + att×0.10
```

- 입력 5개: mid/fin(0-100,기본0), proj(0-100,기본0), hw(0-100,기본0), att(0-100,기본100)
- 등급: A+(95↑) A0(90↑) B+(85↑) B0(80↑) C+(75↑) C0(70↑) D+(65↑) D0(60↑) F(60미만)
- 절대평가, 외부 라이브러리 없음
- 결과 카드: 총점 + 등급 뱃지 + 바 차트 5항목 + A+ 힌트
- 목표 역산 섹션: A+/A0/B+/B0 세그먼트 버튼, 부족 점수 + 0점 항목 만점 가정 예상
- 등급 기준표: 현재 해당 등급 행 하이라이트
- 연동: index.html 카드 추가 + 전체 nav에 "웹클라이언트" 링크 추가

---

## 주의사항

- 외부 라이브러리 금지 (순수 HTML/CSS/JS)
- toFixed(2) or toFixed(1)로 표시
- 모든 input에 addEventListener('input', calc)
- 배포: git init → gh repo create → gh api로 Pages 설정
