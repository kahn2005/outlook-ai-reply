# 📘 비개발자용 바이브코딩 튜토리얼

**프로젝트**: Outlook AI 답변 자동 초안 생성기
**대상**: 코딩 경험이 없는 업무 사용자
**작성일**: 2026-03-27

---

## 이 가이드에서 배우는 것

코딩을 몰라도 Claude와 대화하면서 나만의 업무 도구를 만드는 방법을 배웁니다. "바이브코딩"은 AI에게 원하는 것을 말하면 AI가 코드를 만들어주는 방식입니다.

---

## 🚀 시작하기 전에 준비할 것

### 필요한 도구 목록

| 도구 | 다운로드 링크 | 설명 |
|------|-------------|------|
| Node.js | https://nodejs.org | 프로그램 실행 환경 |
| VS Code | https://code.visualstudio.com | 코드 편집기 |
| Git | https://git-scm.com | 버전 관리 도구 |
| Claude 계정 | https://claude.ai | AI 어시스턴트 |

> 💡 **설치가 어려우면?** 각 설치 파일을 내려받아 "다음" 버튼만 계속 누르면 됩니다.

---

## 📁 Git 기본 사용법

Git은 내 작업을 안전하게 저장하고 버전을 관리하는 도구입니다.

### 자주 쓰는 Git 명령어

```bash
# 1. 내 컴퓨터에 프로젝트 폴더 만들기 (처음 한 번만)
git init

# 2. 변경된 파일 모두 저장 준비
git add .

# 3. 저장 (메모 남기기)
git commit -m "오늘 작업한 내용 설명"

# 4. GitHub에 올리기
git push

# 5. 현재 상태 확인
git status
```

> 💡 **명령어가 두렵다면?** VS Code를 열고 왼쪽 아이콘 중 "소스 제어"(갈림길 모양)를 클릭하면 버튼으로 할 수 있습니다.

---

## 🤖 Claude와 함께 만드는 법 (바이브코딩)

### Step 1: 문제를 대화로 설명하기

Claude에게 이렇게 말해보세요:

```
"Outlook Add-in을 만들고 싶어.
수신된 이메일을 읽어서 Claude API로 답변 초안을 만들고
Outlook 답장 창에 자동으로 넣어주는 기능이야.
일본어/한국어 이메일 모두 지원해야 해."
```

### Step 2: 코드 받기

Claude가 코드를 만들어 줍니다. 코드를 이해할 필요 없이 복사해서 사용하면 됩니다.

### Step 3: 오류가 나면 오류 메시지 그대로 붙여넣기

```
"이런 오류가 났어: [오류 메시지]
어떻게 고치면 돼?"
```

Claude가 바로 해결해 줍니다.

---

## 🛠️ 실제 설치 단계별 가이드

### 단계 1: 프로젝트 폴더 만들기

1. 바탕화면에 `outlook-ai-reply` 폴더를 만드세요
2. VS Code를 열고 이 폴더를 엽니다 (파일 → 폴더 열기)
3. VS Code 상단 메뉴 → 터미널 → 새 터미널

### 단계 2: 필요한 패키지 설치

터미널에 아래를 복사해서 붙여넣기 후 Enter:

```bash
npm install -g yo generator-office
yo office
```

선택지가 나오면 이렇게 선택하세요:
- Project type: **Taskpane Add-in**
- Script language: **JavaScript**
- Add-in name: **AI Reply Assistant**
- Which Office client: **Outlook**

### 단계 3: Claude API 키 설정

1. https://console.anthropic.com 에서 API 키 발급
2. 프로젝트 폴더에 `.env` 파일 생성:

```
CLAUDE_API_KEY=여기에_발급받은_키_붙여넣기
```

> ⚠️ API 키는 비밀번호와 같으니 다른 사람과 공유하지 마세요!

### 단계 4: AI 기능 코드 추가

Claude에게 이렇게 요청하세요:

```
"아래 파일에 Claude API를 연동하는 코드를 추가해줘.
수신 이메일 텍스트를 받아서 답변 초안을 반환하는
aiService.ts 파일을 만들어줘."
```

### 단계 5: 테스트 실행

```bash
npm start
```

브라우저가 열리면서 Outlook Add-in이 실행됩니다.

---

## 🔧 자주 발생하는 문제와 해결법

| 문제 | 해결 방법 |
|------|----------|
| `npm: command not found` | Node.js가 설치되지 않음. nodejs.org에서 재설치 |
| API 키 오류 | `.env` 파일의 키 값 확인, 앞뒤 공백 제거 |
| Outlook에 Add-in이 안 보임 | `npm start`가 실행 중인지 확인 |
| 일본어가 깨져 보임 | 파일 저장 시 UTF-8 인코딩 선택 |

---

## 💬 Claude에게 효과적으로 요청하는 법

### 좋은 요청 예시 ✅

```
"Outlook Add-in에서 이메일 본문을 읽어오는 코드를 써줘.
Office.js의 mailbox.item.body.getAsync를 사용해야 해."
```

### 효과 없는 요청 예시 ❌

```
"코드 만들어줘"  ← 너무 막연함
```

### 팁
- 구체적으로 말할수록 좋습니다
- 오류 메시지가 나면 전체를 복사해서 붙여넣으세요
- "더 간단하게 만들어줘", "주석을 추가해줘" 처럼 수정 요청도 가능합니다

---

## 📚 참고 자료

- [Office Add-in 공식 문서](https://learn.microsoft.com/ko-kr/office/dev/add-ins/)
- [Claude API 문서](https://docs.anthropic.com)
- [Git 기초 튜토리얼 (한국어)](https://git-scm.com/book/ko/v2)

---

> 🎉 **기억하세요**: 코드를 이해하지 못해도 괜찮습니다. 원하는 것을 명확히 설명하고, 오류가 나면 Claude에게 물어보면 됩니다. 이것이 바이브코딩의 핵심입니다!
