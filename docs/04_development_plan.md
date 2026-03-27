# 🗺️ 개발 계획 문서

**프로젝트**: Outlook AI 답변 자동 초안 생성기
**작성일**: 2026-03-27

---

## 이슈 기반 개발 계획 (GitHub Issues)

---

### 🏁 마일스톤 1: 기반 구축 (1~2주)

#### Issue #1: [SETUP] 프로젝트 환경 세팅
**레이블**: `setup`, `priority:high`

- [ ] Node.js 프로젝트 초기화 (`npm init`)
- [ ] Outlook Add-in 프로젝트 스캐폴딩 (Office Add-in Yeoman Generator)
- [ ] Claude API 키 설정 및 테스트
- [ ] GitHub 리포지토리 생성 및 README 작성
- [ ] `.env` 파일 구성 (API 키 관리)

---

#### Issue #2: [FEATURE] Claude API 연동 모듈 개발
**레이블**: `feature`, `backend`, `priority:high`

- [ ] `@anthropic-ai/sdk` 패키지 설치
- [ ] 이메일 텍스트를 받아 답변 초안을 반환하는 함수 개발
- [ ] 언어 감지 로직 구현 (일본어/한국어 자동 판별)
- [ ] 프롬프트 템플릿 작성 (비즈니스 경어체 지시 포함)
- [ ] 단위 테스트 작성

**예시 프롬프트 구조:**
```
시스템: 당신은 비즈니스 이메일 답변 전문가입니다.
수신 언어에 맞춰 답변을 작성하세요.

사용자: 아래 이메일에 대한 답변 초안을 작성해주세요.
[이메일 내용]
```

---

#### Issue #3: [FEATURE] Outlook Add-in UI 개발
**레이블**: `feature`, `frontend`, `priority:high`

- [ ] Office.js를 사용한 사이드 패널 UI 구현
- [ ] 메일 본문 텍스트 읽기 (`Office.context.mailbox.item`)
- [ ] "초안 생성" 버튼 구현
- [ ] 로딩 상태 표시 (스피너/진행바)
- [ ] 생성된 초안 표시 영역 구현

---

### 🚀 마일스톤 2: 핵심 기능 구현 (3~4주)

#### Issue #4: [FEATURE] 메일 분석 및 초안 자동 입력
**레이블**: `feature`, `core`, `priority:high`

- [ ] 수신 메일 본문 파싱 (HTML → 순수 텍스트 변환)
- [ ] 발신자 이름 추출 (인사말 자동 생성용)
- [ ] 생성된 초안을 답장 창에 자동 삽입
  - `Office.context.mailbox.item.body.setAsync()`
- [ ] 초안 적용 전 미리보기 기능

---

#### Issue #5: [FEATURE] 언어별 프롬프트 최적화
**레이블**: `feature`, `ai`, `priority:medium`

- [ ] 일본어 전용 프롬프트 (경어체, 관용 표현 반영)
- [ ] 한국어 전용 프롬프트 (존댓말, 비즈니스 표현)
- [ ] 이메일 유형별 템플릿 (문의/요청/확인/감사)
- [ ] A/B 테스트로 최적 프롬프트 선정

---

#### Issue #6: [FEATURE] 사용자 설정 기능
**레이블**: `feature`, `ux`, `priority:medium`

- [ ] 자동 생성 ON/OFF 토글
- [ ] 서명(사인오프) 자동 추가 설정
- [ ] 이름/직함 등 사용자 정보 저장

---

### ✅ 마일스톤 3: 품질 개선 (5~6주)

#### Issue #7: [BUG] 엣지 케이스 처리
**레이블**: `bug`, `priority:medium`

- [ ] 첨부파일만 있는 메일 처리
- [ ] 매우 긴 메일 (토큰 제한) 처리
- [ ] 언어 혼용 메일 처리
- [ ] API 오류 시 사용자 알림

---

#### Issue #8: [DOC] 문서화 및 배포 준비
**레이블**: `documentation`, `priority:low`

- [ ] 설치 가이드 작성
- [ ] 사용자 매뉴얼 작성
- [ ] Microsoft AppSource 배포 준비 (선택)
- [ ] 비개발자용 튜토리얼 작성

---

## 개발 타임라인

```
주차  1  2  3  4  5  6
#1   ████
#2   ████
#3      ████
#4         ████
#5            ████
#6               ██
#7                  ████
#8                     ██
```

---

## 기술 스택 상세

| 구성 | 기술 | 이유 |
|------|------|------|
| Add-in 프레임워크 | Office.js | Outlook 공식 지원 |
| AI API | Claude API (claude-sonnet-4-6) | 다국어 성능 우수 |
| 런타임 | Node.js + TypeScript | 타입 안전성 |
| 번들러 | webpack | Office Add-in 표준 |
| 테스트 | Jest | 단위/통합 테스트 |
