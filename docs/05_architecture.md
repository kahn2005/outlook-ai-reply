# 🏗️ 아키텍처 문서

**프로젝트**: Outlook AI 답변 자동 초안 생성기
**작성일**: 2026-03-27

---

## 시스템 아키텍처 개요

```mermaid
graph TB
    subgraph Outlook["📧 Microsoft Outlook (Microsoft 365)"]
        MAIL[수신 이메일]
        ADDIN[Outlook Add-in\nOffice.js]
        REPLY[답장 작성 창]
    end

    subgraph ADDIN_LOGIC["🔧 Add-in 로직"]
        PARSER[메일 파서\nHTML → Text]
        LANG[언어 감지\n일본어 / 한국어]
        PROMPT[프롬프트 빌더]
    end

    subgraph CLAUDE["✨ Claude API (Anthropic)"]
        API[claude-sonnet-4-6]
    end

    MAIL -->|메일 본문 읽기\nOffice.js| ADDIN
    ADDIN --> PARSER
    PARSER --> LANG
    LANG --> PROMPT
    PROMPT -->|API 요청| API
    API -->|답변 초안 반환| ADDIN
    ADDIN -->|초안 자동 삽입\nbody.setAsync()| REPLY
```

---

## 상세 시퀀스 다이어그램

```mermaid
sequenceDiagram
    actor 사용자
    participant Outlook
    participant AddIn as Outlook Add-in
    participant Parser as 메일 파서
    participant Claude as Claude API

    사용자->>Outlook: 이메일 수신/열기
    Outlook->>AddIn: 메일 열림 이벤트 트리거
    AddIn->>Outlook: 메일 본문 요청 (Office.js)
    Outlook-->>AddIn: 메일 본문 (HTML)
    AddIn->>Parser: HTML 파싱 요청
    Parser-->>AddIn: 순수 텍스트 + 언어 정보
    AddIn->>Claude: 답변 초안 생성 요청\n(언어별 프롬프트)
    Claude-->>AddIn: 생성된 답변 초안
    AddIn->>Outlook: 답장 창에 초안 삽입\n(body.setAsync)
    Outlook-->>사용자: 초안이 채워진 답장 창 표시
    사용자->>Outlook: 확인 후 수정 → 전송
```

---

## 컴포넌트 구조

```mermaid
graph LR
    subgraph Frontend["프론트엔드 (Office.js)"]
        UI[TaskPane UI\nHTML/CSS/JS]
        EVENT[이벤트 핸들러]
        STATE[상태 관리]
    end

    subgraph Backend["백엔드 로직 (TypeScript)"]
        MAIL_SVC[MailService\n메일 읽기/쓰기]
        LANG_SVC[LanguageService\n언어 감지]
        AI_SVC[AIService\nClaude API 연동]
        PROMPT_SVC[PromptService\n프롬프트 빌더]
    end

    subgraph External["외부 서비스"]
        GRAPH[Microsoft Graph API]
        CLAUDE[Claude API]
    end

    UI --> EVENT
    EVENT --> STATE
    STATE --> MAIL_SVC
    STATE --> AI_SVC
    MAIL_SVC --> GRAPH
    AI_SVC --> LANG_SVC
    AI_SVC --> PROMPT_SVC
    AI_SVC --> CLAUDE
```

---

## 데이터 흐름

```mermaid
flowchart LR
    A[📩 수신 이메일] --> B{언어 감지}
    B -->|일본어| C[일본어 프롬프트\n경어체 지시]
    B -->|한국어| D[한국어 프롬프트\n존댓말 지시]
    C --> E[Claude API]
    D --> E
    E --> F[답변 초안]
    F --> G{사용자 검토}
    G -->|수정 없이| H[✅ 전송]
    G -->|수정 후| I[✏️ 수정 → 전송]
    G -->|폐기| J[🗑️ 삭제]
```

---

## 보안 고려사항

| 항목 | 처리 방법 |
|------|----------|
| API 키 관리 | 환경변수로 관리, 코드에 하드코딩 금지 |
| 메일 내용 저장 | API 처리 후 즉시 폐기, 로컬 저장 없음 |
| 전송 암호화 | HTTPS/TLS 통신 |
| 인증 | Microsoft 365 OAuth 2.0 |

---

## 폴더 구조

```
outlook-ai-reply/
├── src/
│   ├── taskpane/          # UI 컴포넌트 (HTML/CSS/JS)
│   │   ├── taskpane.html
│   │   ├── taskpane.css
│   │   └── taskpane.ts
│   ├── services/
│   │   ├── mailService.ts      # 메일 읽기/쓰기
│   │   ├── languageService.ts  # 언어 감지
│   │   ├── aiService.ts        # Claude API
│   │   └── promptService.ts    # 프롬프트 관리
│   └── utils/
│       └── htmlParser.ts       # HTML → Text 변환
├── manifest.xml            # Office Add-in 매니페스트
├── .env                    # API 키 (git 제외)
├── package.json
└── README.md
```
