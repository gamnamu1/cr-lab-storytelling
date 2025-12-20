# 멀티에이전트 소설 창작 시스템 - 프로젝트 요약

## 프로젝트 개요

CR(Checking the News Reliability) 프로젝트의 일환으로, **소설을 통해 언론 개혁의 당위를 전달**하기 위한 멀티에이전트 소설 창작 시스템을 구축했습니다.

- **목표**: 직접적 홍보가 아닌, 서사적 공감을 통해 "왜 시민 주도 언론 검증이 필요한가"를 느끼게 함
- **도구**: Claude Code (Sonnet 4.5) 기반 멀티에이전트 워크플로우
- **참조 자료**: 23권의 소설작법/스토리텔링 서적에서 추출한 지침

## 완료된 단계

| 단계 | 내용 | 상태 |
|------|------|------|
| 1단계 | 23권 서적 분석 → 5개 에이전트별 지침서 추출 | ✅ 완료 |
| 2단계 | 멀티에이전트 워크플로우 구현 (run.py) | ✅ 완료 |
| 3단계 | 도메인 전문가 + 재작성 기능 추가 | ✅ 완료 |
| 3-1단계 | 리서처 에이전트 페르소나 방식으로 수정 | ✅ 완료 |
| 3-2단계 | 리서처 에이전트 관점 중립성 보강 | ✅ 완료 |
| 4단계 | 프로젝트 컨텍스트 및 CR 지식 베이스 구축 | ✅ 완료 |

## 시스템 구조
```
workflow/
├── project_context.md          ← CR 프로젝트 핵심 철학 (모든 에이전트 공유)
├── references/cr-knowledge/    ← 언론 현실 상세 자료 (선택적 참조)
│   ├── 01-problem-awareness.md
│   ├── 02-journalism-reality.md
│   ├── 03-problematic-patterns.md (119개 문제적 보도 패턴)
│   └── 04-citizen-solution.md
├── agents/
│   ├── 00-orchestration.md
│   ├── 00-researcher.md        ← 도메인 전문가 (페르소나 기반, 관점 중립)
│   ├── 00-diagnostician.md     ← 진단자 (재작성용)
│   ├── 01-philosopher.md       ← 화두 도출
│   ├── 02-novelist-creator.md  ← 시놉시스/본문 작성
│   ├── 03-novelist-critic.md   ← 구조적 비평
│   ├── 04-editor.md            ← 문장 다듬기
│   └── 05-literary-critic.md   ← 문학적 비평
├── outputs/                    ← 단계별 산출물
└── run.py
```

## 기본 파이프라인
```
사용자 입력 (input.txt)
  ↓
[0] 리서처 → 도메인 지식 (--domain 옵션 사용 시)
  ↓
[1] 철학자 → theme.md (화두/문제의식)
  ↓
[2] 소설가 A → synopsis_v1.md
  ↓
[3] 소설가 B → feedback.md (구조적 비평)
  ↓
[4] 소설가 A → draft_v1.md (피드백 반영)
  ↓
[5] 편집자 → edit_notes.md
  ↓
[6] 소설가 A → draft_v2.md
  ↓
[7] 비평가 → critique.md
  ↓
[8] 소설가 A → final.md
```

## 실행 방법
```bash
# 기본 실행
python run.py --input "소재.txt"

# 도메인 전문가 모드 (언론 관련 시 CR 지식 자동 로드)
python run.py --input "소재.txt" --domain "언론/탐사보도"

# 대화형 모드 (체크포인트에서 확인)
python run.py --input "소재.txt" --domain "언론/탐사보도" --interactive

# 재작성 모드
python run.py --revise "outputs/08-final.md" --feedback "주인공 동기가 약해요"
```

## 등록된 도메인 페르소나

| 키워드 | 페르소나 |
|--------|---------|
| 언론/탐사보도 | 20년차 탐사보도 기자 |
| 언론/방송뉴스 | 18년차 방송기자 겸 앵커 |
| 의료/응급의학 | 15년차 응급의학 전문의 |
| 의료/외과 | 20년차 외과 전문의 |
| 법조/형사변호 | 18년차 형사전문 변호사 |
| 법조/검찰 | 17년차 검사 |
| 교육/고등학교 | 22년차 고등학교 교사 |
| 기업/스타트업 | 12년차 창업자 겸 CTO |

미등록 도메인도 일반 템플릿으로 자동 처리됩니다.

## CR 프로젝트 핵심 (소설에 반영할 문제의식)

> **언론인 스스로 만든 '언론윤리규범'을 근거로, 시민들이 직접 뉴스의 품질을 묻고 확인한다.**

- 한국 뉴스 신뢰도 28% (OECD 최하위)
- 언론은 자정능력을 상실
- 전문가 비평만으로는 한계
- 시민이 주도하는 새로운 감시/견제 방식 필요

## 창작 원칙

1. **프로파간다가 아닌 문학**: CR을 직접 홍보하지 않음
2. **현실의 충실한 재현**: 다층적, 균형 있는 묘사
3. **인간에 대한 공감**: 선악 이분법을 넘어 구조적 딜레마
4. **열린 결말**: 답보다 질문을 남김

## 다음 단계 (이번 세션에서 문의할 내용)

이제 실제로 이 시스템을 **활용**하여 소설을 창작하려 합니다.

예상 문의:
- input.txt에 어떤 형식으로 소재를 적으면 좋을까?
- 어떤 인물, 어떤 배경, 어떤 문제의식을 어떻게 지정하면 좋을까?
- 도메인 선택은 어떻게 하면 효과적일까?
- 결과물이 마음에 안 들 때 재작성은 어떻게 활용하나?

---

**작업 디렉토리**: `/Users/gamnamu/Downloads/cr-lab-storytelling/workflow/`
**참조 서적**: `/Users/gamnamu/Downloads/cr-lab-storytelling/[References] books-about-storytelling/`
**CR 프로젝트 원본**: `/Users/gamnamu/Downloads/cr-project-main/`
