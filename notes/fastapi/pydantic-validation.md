[FastAPI] Pydantic 모델과 검증 (Pydantic Model & Validation)

- 한 줄 정의:
  서버에 들어오는 데이터가 정해 둔 양식에 맞는지 입구에서 자동으로 검수해 주는 도구.

- 비유:
  은행 창구 신청서 양식 + 경비원.
  신청서(MemoCreate)에는 이름 · 금액만 적고, 접수 번호(id)는 창구가 찍어 준다(Memo).
  칸이 빠지거나 숫자 칸에 글자를 쓰면 경비원이 창구까지 가기 전에 돌려보낸다(422).

- 왜 필요한가:
  검사가 없으면 이상한 데이터가 그대로 저장되고, 나중에 다른 곳에서 에러가 터진다.
  직접 검사하려면 칸마다 if문을 써야 하는데, Pydantic은 `text: str` 한 줄로 끝낸다.

- 어떻게 동작하나:
  POST {"text": "..."} 보냄
    → FastAPI: 함수 괄호에 memo: MemoCreate가 있네 → Pydantic에 검사 맡김
    → Pydantic: text 칸 있나? 글자인가?
       통과 → 함수 실행 → 201
       탈락 → 함수 실행 안 됨 → 422 + 이유 메시지

- 최소 코드 (직접 실행함):
  from pydantic import BaseModel

  class MemoCreate(BaseModel):      # 보낼 때 양식 (id 없음)
      text: str

  class Memo(BaseModel):            # 돌려줄 때 양식 (서버가 id 붙임)
      id: int
      text: str

  @app.post("/memos", status_code=201)
  def create_memo(memo: MemoCreate) -> Memo:   # ← 여기서 Pydantic 검사
      ...

  | 보낸 것 | 결과 |
  |---|---|
  | {"text": "Pydantic 배우기"} | 201, id 6번 |
  | {"title": "이름이 틀림"} | 422 text: Field required |
  | {"text": 123} | 422 Input should be a valid string |

- 면접 질문 1개와 내 답 (3문장):
  Q. FastAPI에서 Pydantic은 어떤 역할을 하나요?
  A. json 양식에 맞추어서 인풋이 되었는지 검사한다. 틀리면 422로 응답한다. "text":"str"일 때 int 형식을 입력하거나 text 대신 title로 입력하는 등을 하면 422로 답이 온다.
  A. 들어온 JSON이 미리 정해 둔 양식(Pydantic 모델)에 맞는지 함수 실행 전에 자동으로 검사한다. 틀리면 422로 응답한다. 예를 들어 text: str인데 숫자를 넣거나 text 대신 title로 보내면 422가 온다.

- 내 프로젝트에서 쓰는 곳:
  fastapi-memo: MemoCreate · Memo (POST /memos)
  W3 llm-playground: LLM한테 "이 양식대로 JSON으로 답해"라고 시킬 때 (구조화 출력)
  W10 VOC 에이전트: 민원 분류 결과(category, urgency)를 양식으로 받아 이상한 값 거르기

- 헷갈렸던 점:
  Pydantic이 어디서 쓰이는지 몰랐다 → POST로 내용을 보낼 때 text 칸 대신 title을 보내거나
  숫자를 넣으면 422가 뜬다. 함수에 memo: MemoCreate라고 적어 두면 Pydantic이 자동으로 검수해 준다.