# 멀티에이전트 소설 창작 시스템 - 실행 가이드

## 사전 준비

1. `inputs/input.md`에 소재를 작성하세요
2. 아래 프로세스를 순서대로 진행하세요

---

## 기본 프로세스 (8단계)

| 순서 | 프롬프트 파일 | 역할 | 산출물 |
|------|--------------|------|--------|
| 0 | `01-researcher.md` | 도메인 지식 (선택) | `00-domain_knowledge.md` |
| 1 | `02-philosopher.md` | 화두 도출 | `01-theme.md` |
| 2 | `03-novelist-synopsis.md` | 시놉시스 작성 | `02-synopsis.md` |
| 3 | `04-novelist-critic.md` | 구조적 비평 | `03-feedback.md` |
| 4 | `05-novelist-draft.md` | 초고 작성 | `04-draft_v1.md` |
| 5 | `06-editor.md` | 편집 노트 | `05-edit_notes.md` |
| 6 | `07-novelist-revision.md` | 수정고 | `06-draft_v2.md` |
| 7 | `08-literary-critic.md` | 문학적 비평 | `07-critique.md` |
| 8 | `09-novelist-final.md` | 최종본 | `08-final.md` |

---

## 실행 방법

### Step 0 (선택): 도메인 전문가
언론, 의료, 법조 등 전문 분야를 다룰 때만 실행
```
prompts/01-researcher.md를 읽고,
inputs/input.md의 소재에 대해 도메인 지식을 생성해줘.
도메인은 "언론/탐사보도"야.
결과물은 outputs/00-domain_knowledge.md에 저장해줘.
```

### Step 1: 철학자
```
prompts/02-philosopher.md를 읽고,
inputs/input.md와 (있다면) outputs/00-domain_knowledge.md를 참조해서
화두를 도출해줘.
결과물은 outputs/01-theme.md에 저장해줘.
```

### Step 2~8: 순차 실행
각 단계마다 해당 프롬프트 파일을 읽고 실행하도록 요청

---

## 간편 실행 (한 번에 요청)

전체 프로세스를 한 번에 요청할 수도 있습니다:
```
이 소설 창작 시스템의 전체 프로세스를 실행해줘.

1. inputs/input.md를 읽어줘
2. project_context.md를 읽어줘
3. prompts/ 폴더의 각 단계를 순서대로 실행해줘
4. 각 단계의 결과물을 outputs/에 저장해줘
5. 각 단계 완료 후 간략히 보고해줘

도메인은 "언론/탐사보도"로 설정해줘.
```

---

## 재작성 모드

기존 결과물에 피드백을 반영하고 싶을 때:
```
prompts/R1-revision-mode.md를 읽고,
outputs/08-final.md에 대해 다음 피드백을 반영해서 수정해줘:
"주인공의 동기가 약하고, 중반부 긴장감이 떨어져요"
```
