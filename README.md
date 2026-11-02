# til

AI · AX 엔지니어 16주 공부 기록 (2026.11 – 2027.02)

## 폴더 규칙

```
til/
├── worklog/YYYY-MM/YYYY-MM-DD.md    # 작업 노트 (하루 1개)
├── notes/<태그>/<개념-영문-kebab>.md  # 기술 노트 (개념 1개 = 파일 1개)
└── templates/
    ├── worklog.md                   # 작업 노트 빈 양식
    └── note.md                      # 기술 노트 빈 양식
```

- **작업 노트**: `worklog/2026-11/2026-11-02.md`처럼 월 폴더 아래 날짜 파일로 만든다. 하루에 1개.
- **기술 노트**: `notes/fastapi/http-status-code.md`처럼 태그 폴더 아래 개념 이름(영문 kebab-case)으로 만든다. 개념 1개 = 파일 1개.
- **태그 폴더**는 아래 목록에서만 쓴다.
  `python` · `fastapi` · `llm` · `sql` · `devops` · `rag` · `eval` · `agent` · `deploy` · `llmops` · `ml` · `ax` · `cert` · `coding-test`
- 새 노트는 `templates/`의 양식을 복사해서 시작한다.

## 노트 2종의 차이

- **기술 노트** = 무엇을 아는가. 주제별로 정리하고, 계속 고쳐 쓴다.
- **작업 노트** = 무엇을 했고 어디서 막혔나. 날짜별로 남긴다.

## 목차 (notes/)

<!-- 기술 노트를 만들면 태그별로 여기에 링크를 추가한다. -->

## 주의

- API 키 · 개인 연락처 · 실제 회사/사람 정보는 올리지 않는다.
