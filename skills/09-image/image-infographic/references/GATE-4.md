# 관문 4: 강의 준비 완료 검증 (파이프라인 최종)

image-infographic 종료 시점에 실행하는 파이프라인 최종 관문. 이 관문 통과 = 강의 준비 완료.

## 파이프라인 위치

lecture-plan [관문 1] → lecture-research [관문 2] → lecture-slides [관문 3] → **image-infographic [관문 4]**

## 실행 시점

image-infographic의 모든 이미지 프롬프트 생성이 완료된 직후, 최종 전달 전에 실행한다.

## 입력 조건 확인 (실행 전)

image-infographic 시작 시 lecture-slides 산출물의 YAML에서 아래를 확인한다.

- [ ] `gate_3_passed: true` 플래그 존재
- [ ] `color_key` 지정됨
- [ ] `text_layout_default` 지정됨
- [ ] `image_slot_count` 명시됨

하나라도 미충족이면 **lecture-slides로 회귀**하여 관문 3을 먼저 통과시킨다.

## 관문 4 체크리스트 (6개 항목, 모두 충족)

### 프롬프트 규칙 준수 (3개)

- [ ] **모든 이미지 프롬프트가 한국어로 작성되었는가**
  - 영문 프롬프트 혼입 금지
  - 고유명사(제품명·기업명)는 예외

- [ ] **배경·폰트·캐릭터 규칙을 준수하는가**
  - 배경: #FFFFFF (solid pure white, flat color, no shadows)
  - 폰트: Noto Sans KR
  - 캐릭터: 스틱맨 고정

- [ ] **금지 요소가 없는가**
  - 매거진 헤더 없음
  - 영문 부제 없음
  - 장식 라인 없음
  - 그라데이션·그림자 없음

### 파이프라인 일관성 (2개)

- [ ] **컬러 키가 관문 3 지정과 일치하는가**
  - lecture-slides의 `color_key`와 모든 이미지 프롬프트의 컬러가 동일
  - 7종 컬러 키 중 1개로 고정 (꼭지별 변경 X)

- [ ] **레이아웃 유형이 관문 3 지정과 일치하는가**
  - 각 이미지 슬롯의 레이아웃이 관문 3에서 지정한 유형(중앙/2분할/카드그리드/타임라인/방사형) 그대로
  - 변경이 필요하면 lecture-slides 관문 3 재검증 후 진행

### 사양 분리 (1개)

- [ ] **콘텐츠와 사양이 분리되어 있는가**
  - 사양 텍스트(배경색·폰트·레이아웃)가 이미지에 노출되지 않도록 별도 블록으로 분리
  - 콘텐츠(메시지·키워드)만 이미지에 반영

## 통과 기준

**6/6 모두 충족**

## 실패 시 대응

### 항목 1~3 실패 (프롬프트 규칙)
- 해당 프롬프트만 규칙에 맞게 재작성
- 여러 프롬프트에서 동일 위반이 반복되면 사용자 요구사항 재확인

### 항목 4~5 실패 (파이프라인 일관성)
- 관문 3 산출물(color_key, 레이아웃)을 다시 로드해 재매핑
- 관문 3 값 자체가 부적절하면 lecture-slides로 회귀

### 항목 6 실패 (사양 분리)
- 사양 블록을 프롬프트 상단 별도 섹션으로 분리
- 이미지 생성 지시 본문에서 사양 텍스트 제거

### 2회 연속 전체 실패
- image-infographic Phase 1부터 재실행
- 근본 원인이 lecture-slides에 있으면 관문 3부터 재검증

## 출력 YAML 추가 항목

관문 4 통과 후 최종 산출물에 아래를 기록한다.

```yaml
gate_1_passed: true   # lecture-plan 상속
gate_2_passed: true   # lecture-research 상속
gate_3_passed: true   # lecture-slides 상속
gate_4_passed: true
gate_4_score: 6/6
gate_4_checked_at: {YYYY-MM-DD}
pipeline_complete: true
total_image_prompts: {N}
lecture_ready: true
```

`pipeline_complete: true`와 `lecture_ready: true`가 기록되면 **파이프라인 4단계가 모두 통과된 상태**이며, 강의 준비가 완료되었음을 의미한다.

## 완료 리포트

관문 4 통과 시 아래 형식의 완료 리포트를 사용자에게 제시한다.

```
■ 파이프라인 4단계 통과 완료

강의명: {lecture_title}
대상: {target_profile.job}
시간: {lecture_duration_minutes}분

[관문 1] 기획안 검증         : {gate_1_score}
[관문 2] 리서치 검증         : {gate_2_score} (A·B 사례 {ab_case_ratio}%)
[관문 3] 슬라이드 검증       : {gate_3_score} (슬라이드 {slide_count}장)
[관문 4] 이미지 프롬프트 검증 : {gate_4_score} (프롬프트 {total_image_prompts}개)

산출물:
- LP_*.md   (기획안)
- RL_*.md   (리서치 노트)
- *.pptx    (슬라이드)
- 이미지 프롬프트 {N}개

다음 단계: 나노바나나 프로에서 이미지 생성 → 슬라이드 삽입 → 리허설
```

## Harness 블록 (관문 4 전용)

| 항목 | 값 |
|------|-----|
| **평가 분리** | image-infographic 본 프로세스와 분리된 최종 검증 |
| **통과 기준** | 6/6 모두 충족 |
| **실패 시 대응** | 항목별 보완 → 2회 실패 시 Phase 1 회귀 |
| **최종 플래그** | `pipeline_complete`, `lecture_ready` 기록 |

## 실행 원칙

- 관문 4는 image-infographic 본 프로세스 **종료 직후** 실행
- 입력 조건(gate_3_passed)이 false면 lecture-slides로 회귀
- 통과 시 완료 리포트 자동 생성
- `lecture_ready: true` 플래그가 기록되어야 파이프라인 종료로 간주
- 실패 시 항목별 대응 경로 명시적 출력
- 관문 4는 다른 관문보다 간결하게 (6개 항목) 설계되어 있으며, 본질은 규칙 준수 재확인
