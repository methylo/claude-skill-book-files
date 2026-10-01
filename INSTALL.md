# 설치·호출·오류 해결

## 준비

| 항목 | 내용 |
|---|---|
| 계정 | 스킬 등록은 클로드 유료 플랜에서 할 수 있습니다(책 3장) |
| 설정 | **설정 → 기능**에서 "코드 실행 및 파일 생성"을 켭니다. .docx·.pptx를 만드는 스킬은 이 기능이 있어야 동작합니다 |
| 코워크 | 내 폴더의 파일을 직접 읽고 쓰는 실습(책 7부부터)은 클로드 데스크톱 앱이 필요합니다 |

## 설치

1. README 목록의 **받기** 링크에서 쓸 스킬의 `.skill` 파일을 내려받습니다.
2. 클로드에서 **사용자 지정 → 스킬**로 이동합니다.
3. **+ → 스킬 추가 → 스킬 업로드**를 누르고 `.skill` 파일을 선택합니다.
4. 스킬 목록에 이름이 나타나는지 확인합니다.

한 번 등록하면 모든 대화와 프로젝트에서 쓰입니다. `.skill` 파일은 압축(zip) 파일이라, 압축을 풀면 `SKILL.md`와 `references/` 등 하위 폴더를 직접 열어 볼 수 있습니다.

## 호출

- **자연어**: 요청 문장에 트리거 단어를 넣습니다. 예) "이 메모로 회의록 정리해 줘"
- **슬래시 명령**: 스킬 이름을 직접 부릅니다. 예) `/meeting-minutes`

## 오류가 날 때 3지점 점검

| 증상 | 점검 |
|---|---|
| 스킬이 아예 불리지 않음 | 스킬 목록에 등록되어 있는가, 등록 직후라면 잠시 뒤 다시 시도 |
| 일반 답변만 나옴 | 요청에 트리거 단어가 있는가. 없으면 `/스킬명`으로 직접 부름 |
| 다른 스킬이 불림 | 비슷한 스킬끼리 트리거가 겹치는가. 요청에 스킬 이름을 넣어 지정 |

## 함께 쓰는 순서가 있는 스킬

| 분류 | 순서 |
|---|---|
| 책쓰기 | book-planning → book-research → book-writing-pro → book-editing → book-feedback-reader·editor → book-citation |
| 강의 | lecture-plan → lecture-research → lecture-blueprint → lecture-slides → lecture-review → image-infographic |
| 사업계획서 | bizplan-research → bizplan-kstartup → bizplan-kstartup-pitch |
| LLM 위키 | wiki-research → wiki-ingest → wiki-activate → wiki-audit |

순서대로 쓰면 앞 스킬의 결과 파일을 다음 스킬이 이어받습니다. 하나만 따로 써도 동작합니다.
