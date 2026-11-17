# 🧪 AI 에이전트 333 부트캠프 — 실습 키트

> 코딩알려주는 누나 · AI 에이전트 333 부트캠프 1기

이 폴더 하나로 6주 동안 실험합니다.
매 PART가 끝날 때마다 `notebooks/` 안에 새 폴더가 추가돼요. (지금은 **PART1**)

**오늘의 목표:** `00_setup_check.ipynb` 마지막 셀에서
👉 **"AI Agent 실습 환경설정 완료"** 한 줄을 받으면 성공!

---

## 📁 폴더 구조

```text
agent-333-bootcamp/
├─ README.md              ← 지금 보는 파일
├─ .env                   ← 🔑 여기에 API 키 붙여넣기
├─ .env.example           ← .env 원본 양식 (건드리지 않아도 됨)
├─ requirements.txt       ← 설치할 패키지 목록
├─ data/
│  ├─ company_brief.md     ← 실습 케이스: 신규 AI 회의록 서비스 브리프
│  └─ competitor_db.json   ← 가짜 사내 검색 DB (경쟁사 3곳)
├─ notebooks/
│  └─ PART1/
│     ├─ 00_setup_check.ipynb                 ← ① 환경설정 확인
│     ├─ 01_chatgpt_vs_workflow_vs_agent.ipynb ← ② Single LLM vs Workflow vs Agent
│     └─ 02_prompt_engineering_for_agents.ipynb← ③ Agent에게 일 시키는 프롬프트
└─ outputs/               ← 실행 결과(보고서 txt)가 쌓이는 곳
```

---

## ✅ 세팅 체크리스트 (순서대로!)

- [ ] 1. Python 3.11 또는 3.12 설치
- [ ] 2. VS Code + 확장(Python, Jupyter) 설치
- [ ] 3. 이 폴더를 VS Code로 열기
- [ ] 4. 가상환경 만들고 패키지 설치
- [ ] 5. `.env`에 API 키 붙여넣기
- [ ] 6. `00_setup_check.ipynb` 실행 → 성공 메시지 확인
- [ ] 7. Claude Code 설치

---

## 1. Python 설치

**Windows**
1. https://www.python.org/downloads/ 에서 **3.12.x** 설치 파일 받기
2. 설치 첫 화면에서 **☑ Add python.exe to PATH 꼭 체크!** ← 제일 많이 놓치는 부분
3. 확인 (새 터미널에서)
   ```powershell
   python --version
   ```

**macOS**
```bash
brew install python@3.12
python3 --version
```
(Homebrew가 없으면 python.org에서 설치 파일로 설치해도 돼요)

---

## 2. VS Code 설치

1. https://code.visualstudio.com 설치
2. 왼쪽 **확장(Extensions)** 탭에서 두 개 설치
   - **Python** (Microsoft)
   - **Jupyter** (Microsoft)

---

## 3. 폴더 열기

1. 받은 zip 파일 **압축 풀기** (zip 안에서 바로 열면 안 돼요!)
2. 바탕화면 등 **한글·공백 없는 경로**에 두기를 추천 (예: `C:\dev\agent-333-bootcamp`)
3. VS Code → `File > Open Folder` → `agent-333-bootcamp` 폴더 선택
4. 상단 메뉴 `Terminal > New Terminal`

---

## 4. 가상환경 + 패키지 설치

**Windows (PowerShell)**
```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

**macOS**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

터미널 맨 앞에 **`(.venv)`** 가 보이면 성공 🎉

> ⚠️ Windows에서 `activate` 할 때 "스크립트를 실행할 수 없습니다" 에러가 나면
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
> ```
> 입력 후 `Y` → 다시 activate

---

## 5. `.env`에 API 키 넣기 🔑

1. https://platform.openai.com/api-keys 에서 **Create new secret key** → 복사
   (결제수단 등록 + 크레딧 충전이 되어 있어야 동작해요. 실습 전체 비용은 소액이에요)
2. VS Code 왼쪽 파일 목록에서 **`.env`** 열기
3. `sk-여기에_본인_키_붙여넣기` 부분을 본인 키로 바꾸고 저장 (`Ctrl+S` / `Cmd+S`)

```env
OPENAI_API_KEY=sk-proj-abc123...
OPENAI_MODEL=gpt-4.1-mini
```

> 🍎 Mac에서 `.env`가 안 보이면 Finder에서 `Cmd + Shift + .` (숨김 파일 보기)
> 🚫 **`.env`는 절대 깃허브·단톡방·커뮤니티에 올리지 마세요.** 키가 털리면 요금이 나갑니다.

---

## 6. 환경설정 확인

1. `notebooks/PART1/00_setup_check.ipynb` 열기
2. 우측 상단 **Select Kernel → Python Environments → `.venv`** 선택
3. 위에서부터 셀마다 `Shift + Enter`

| 결과 | 의미 |
|---|---|
| `API KEY: ✅ 설정됨` + 한 줄 응답 | 🎉 완료! 성공 화면 캡처해서 인증 |
| `API KEY: ❌ 없음` | `.env` 저장 안 했거나, 이름이 `.env.txt`로 바뀜 |
| `ModuleNotFoundError` | 커널이 `.venv`가 아님 → 커널 다시 선택 |
| `AuthenticationError` | 키 오타 / 앞뒤 공백 / 따옴표 확인 |
| `RateLimitError`, `insufficient_quota` | OpenAI 크레딧 충전 필요 |

---

## 7. Claude Code 설치

**Windows (PowerShell)**
```powershell
irm https://claude.ai/install.ps1 | iex
```

**macOS / Linux**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

설치 후 **터미널을 껐다 켜고**
```bash
claude --version
claude
```
처음 실행하면 브라우저 로그인 창이 떠요 (Claude 계정 필요).

> Windows는 Git for Windows(https://git-scm.com/downloads/win) 설치를 권장해요.

첫 대화로 테스트 👇
```
이 폴더 구조 설명해주고, notebooks/PART1 노트북 3개가 각각 뭘 하는지 한 줄씩 알려줘
```

---

## 📒 노트북 실행 순서

| 순서 | 노트북 | 하는 것 |
|---|---|---|
| ① | `00_setup_check` | 환경이 잘 깔렸는지 확인 |
| ② | `01_chatgpt_vs_workflow_vs_agent` | 같은 경쟁사 분석을 3가지 방식으로 → 누가 다음 행동을 정하나 |
| ③ | `02_prompt_engineering_for_agents` | 업무 지시서 6요소 · JSON 출력 · 완료 기준 실험 |

---

## 📝 Day 1 과제

1. **환경설정 인증** — `00_setup_check` 성공 화면 + `01_chatgpt_vs_workflow_vs_agent` 마지막 비교표(정확도) 캡처
2. **내 업무를 자율성 사다리 0~4 중 어디에?** — "고르기 전 4가지 질문"으로 근거 3줄
   - 경로를 그릴 수 있나? / 다음 행동이 상황마다 다른가? / 하위 작업이 서로 독립인가? / 결과물 하나에 여럿이 쓰나?
3. **실험 노트 1장** — 아래 4줄 양식으로

```text
가설:        예) Workflow에 reviews/security 검색을 추가하면 Agent만큼 정확도가 오른다
바꾼 변수:    예) Agent의 max_steps 30 → 5   (한 번에 하나만!)
측정값:      맞힌 사실 수(정확도 %) / Agent STEP 수
배운 점:      예) 필요한 정보가 고정이면 Workflow로도 충분했다
```

---

## 🆘 막히면 여기부터 (90%는 이 다섯 개)

1. **PATH** — Python 재설치하면서 "Add to PATH" 체크
2. **커널** — VS Code 우측 상단에서 `.venv` 선택
3. **`.env.txt`** — 탐색기 "파일 확장명 표시" 켜고 이름 확인
4. **실행 정책** — `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`
5. **재시작** — 설치 후 터미널(또는 VS Code) 껐다 켜기

그래도 안 되면 👉 **에러 메시지 전체 스크린샷** + 운영체제(Windows/Mac)를 같이 올려주세요!

---

> **오늘의 한 문장**
> Agent란 다음 행동을 스스로 결정하는 AI. 쓸지 말지는, 측정해서 정한다.
