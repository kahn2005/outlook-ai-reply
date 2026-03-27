# Outlook AI Reply Assistant

> Outlook 수신 이메일을 AI가 분석하여 자동으로 답변 초안을 생성하는 Outlook Add-in

## 프로젝트 소개

Microsoft 365 Outlook에서 수신된 이메일(한국어/일본어)을 Claude AI가 분석하고, 적절한 답변 초안을 생성하여 Outlook 답장 창에 자동으로 삽입해주는 생산성 도구입니다.

## 주요 기능

- 수신 이메일 내용 자동 분석
- 한국어 / 일본어 언어 자동 감지
- Claude AI 기반 비즈니스 답변 초안 생성
- Outlook 답장 창에 초안 자동 삽입

## 문서

| 문서 | 설명 |
|------|------|
| [개발자 가이드](docs/DEVELOPER_GUIDE.md) | 아키텍처, API 명세, 설치 방법 등 개발 전반 레퍼런스 |
| [PRD](docs/02_PRD.md) | 제품 요구사항 문서 |
| [아키텍처](docs/05_architecture.md) | 시스템 구조 및 Mermaid 다이어그램 |
| [개발 계획](docs/04_development_plan.md) | GitHub Issues 기반 개발 로드맵 |
| [목업](docs/03_mockup.html) | 동작하는 HTML 프로토타입 |
| [튜토리얼](docs/06_tutorial_guide.md) | 비개발자용 바이브코딩 가이드 |

## 빠른 시작

```bash
# 의존성 설치
npm install

# 개발 서버 실행
npm start
```

자세한 내용은 [개발자 가이드](docs/DEVELOPER_GUIDE.md)를 참조하세요.

## 기술 스택

- **Add-in**: Office.js (Microsoft 365)
- **언어**: TypeScript
- **AI**: Claude API (claude-sonnet-4-6)
- **빌드**: webpack

## 담당자

- kahn@directcloud.co.jp
