# CLAUDE.md

이 저장소는 연구 프로젝트를 위한 작업 하네스이다.

핵심 흐름은 다음과 같다.

1. 데이터 수집 및 정리
2. 필요 시 build 단계 수행
3. downstream analysis 수행
4. 결과 정리 및 산출물 생성
5. manuscript 작성
6. review 및 revision

이 저장소에서 작업할 때는 반드시 아래 규칙을 따른다.

---

## 1. 먼저 읽기

작업을 시작하기 전에 다음 위치를 우선 확인한다.

1. `README.md`
2. `00_docs/research-plan/`
3. `00_docs/build-plan/`
4. `00_docs/analysis-plans/active/`
5. `00_docs/experiment-log/`

문서가 비어 있거나 부족하면, 먼저 필요한 문서를 만들거나 업데이트한 뒤 작업을 진행한다.

---

## 2. 폴더 역할

### `00_docs/`
프로젝트의 공식 문서 기록 공간이다.

- `research-plan/`: 연구 질문, 범위, 가설, 마일스톤
- `build-plan/`: assembly/annotation/build 전략과 기준
- `analysis-plans/active/`: 현재 진행 중인 분석 계획
- `experiment-log/`: 실제 실행 기록
- `eda-reports/`: 데이터 탐색 보고서

### `01_data/`
입력 데이터를 보관한다.

- `raw/`: 원본 데이터
- `processed/`: 전처리된 데이터

### `02_build/`
필요한 경우에만 사용하는 build 작업 공간이다.

예:
- assembly 생성
- annotation 생성
- build 관련 QC

이 폴더는 프로젝트에 따라 비워둘 수 있다.

### `03_analysis/`
build 결과 또는 기존 reference/annotation을 기반으로 수행하는 downstream analysis 공간이다.

### `04_outputs/`
최종 산출물 보관 공간이다.

- `figures/`
- `tables/`
- `final_datasets/`

### `05_manuscript/`
논문 초안 작성 공간이다.

### `06_review/`
검토 결과와 revision 계획을 보관하는 공간이다.

---

## 3. 작업 원칙

### 3-1. 먼저 계획을 문서화한다
새로운 build 작업이나 analysis 작업을 시작하기 전에 먼저 관련 계획 문서를 작성한다.

- build 작업 전: `00_docs/build-plan/`
- analysis 작업 전: `00_docs/analysis-plans/active/`

작업을 먼저 하고 문서를 나중에 맞추는 방식은 피한다.

### 3-2. 입력과 출력의 경로를 명확히 한다
각 작업은 다음을 명확히 해야 한다.

- 입력 데이터가 어디에 있는가
- 어떤 스크립트/도구/파라미터를 사용하는가
- 결과가 어디에 저장되는가
- 어떤 기준으로 성공/실패를 판단하는가

### 3-3. 실행 후 반드시 기록을 남긴다
실행이 끝나면 `00_docs/experiment-log/`에 기록을 남긴다.

기록에는 최소한 아래 항목이 포함되어야 한다.

- 날짜
- 작업 목적
- 입력 데이터
- 사용 도구 또는 스크립트
- 주요 파라미터
- 출력 위치
- 핵심 결과
- 문제점 또는 특이사항
- 다음 단계

### 3-4. 결과와 해석을 분리한다
결과는 결과대로 정리하고, 해석은 manuscript나 review 단계에서 신중하게 확장한다.

데이터가 직접 보여주지 않는 내용을 단정적으로 쓰지 않는다.

### 3-5. 최종 산출물은 별도로 정리한다
논문, 발표, 공유에 사용하는 figure, table, final dataset은 반드시 `04_outputs/` 아래에 정리한다.

작업 중간 산출물과 최종 산출물을 섞지 않는다.

---

## 4. 데이터 관련 규칙

### 4-1. 새 데이터가 들어오면 바로 분석하지 않는다
새 파일이나 새 데이터셋이 들어오면 먼저 `01_data/raw/` 또는 `01_data/processed/`에 정리한다.

그다음 필요하면 exploratory data analysis를 먼저 수행한다.

EDA가 필요할 경우:
- 파일 구조 확인
- 품질 확인
- 누락값/형식/기본 통계 확인
- 결과를 `00_docs/eda-reports/`에 저장

### 4-2. 원본 데이터는 보존한다
`01_data/raw/`의 원본 데이터는 직접 수정하지 않는다.  
전처리 결과는 `01_data/processed/`에 둔다.

---

## 5. build 단계 규칙

`02_build/`는 프로젝트에 따라 비워둘 수 있다.

다음과 같은 경우에만 `02_build/` 아래에 필요한 하위 폴더를 만든다.

- raw sequencing data로부터 assembly를 생성해야 할 때
- repeat/gene/functional annotation을 새로 생성해야 할 때
- build 관련 QC를 별도로 관리해야 할 때

예시 하위 폴더:
- `assembly/`
- `annotation/`
- `qc/`

build 작업을 시작하기 전에는 먼저 `00_docs/build-plan/`에 전략 문서를 작성한다.

예:
- 어떤 입력을 쓸 것인지
- 어떤 도구를 쓸 것인지
- 어떤 버전과 파라미터를 쓸 것인지
- 어떤 QC 기준으로 채택할 것인지

---

## 6. analysis 단계 규칙

`03_analysis/`에서는 build 결과 또는 기존 reference/annotation을 기반으로 downstream analysis를 수행한다.

새 analysis를 시작하기 전에는 반드시 `00_docs/analysis-plans/active/`에 계획 문서를 작성한다.

analysis 계획에는 최소한 아래가 포함되어야 한다.

- 분석 목표
- 연구 질문과의 연결
- 입력 데이터
- 방법
- 기대 결과
- 생성할 figure/table 후보
- 성공 조건

analysis 결과 중 중요한 내용은 `04_outputs/`에 정리하기 전에 먼저 문서와 로그로 기록한다.

---

## 7. manuscript 작성 규칙

`05_manuscript/`는 논문 초안 작성 공간이다.

작성 원칙:
- methods는 실제 build/analysis 기록에 근거해 작성한다
- results는 `04_outputs/`의 figure/table과 일치해야 한다
- discussion은 결과를 넘어서 과장하지 않는다
- 한계점과 불확실성을 명시한다

논문 초안은 섹션별로 나누어 관리해도 되고, 필요하면 full draft를 따로 둘 수 있다.

---

## 8. review 규칙

`06_review/`에는 다음을 저장한다.

- cross-check 결과
- reviewer-style 피드백
- revision plan
- 제출 전 확인 메모

논문 초안이 어느 정도 작성되면 review 단계를 수행한다.

---

## 9. 스킬 사용 규칙

이 저장소에서 사용할 수 있는 주요 스킬은 다음과 같다.

### exploratory-data-analysis
다음 상황에서 사용한다.
- 새 데이터 파일을 처음 받았을 때
- 파일 형식/구조/품질을 파악해야 할 때
- 분석 전에 데이터 특성을 문서화해야 할 때

결과는 `00_docs/eda-reports/`에 저장한다.

### cross-verify
다음 상황에서 사용한다.
- build 계획이 타당한지 점검할 때
- analysis 계획과 연구 질문의 정합성을 점검할 때
- 결과 정리나 manuscript 초안 전 구조적 문제를 확인할 때

결과는 필요 시 `06_review/` 또는 `00_docs/` 아래 메모로 남긴다.

### paper-review
다음 상황에서 사용한다.
- manuscript 초안이 어느 정도 완성되었을 때
- reviewer 관점의 피드백이 필요할 때
- 문헌, 수치 일관성, 주장 강도 등을 점검할 때

결과는 `06_review/`에 저장한다.

---

## 10. 출력 원칙

작업 결과를 보고할 때는 가능하면 아래 형식을 따른다.

- 수행한 작업
- 읽은 문서/참고한 자료
- 수정하거나 생성한 파일
- 핵심 결과
- 남은 문제
- 다음 단계

---

## 11. 금지 사항

다음은 피한다.

- 계획 문서 없이 바로 큰 분석을 시작하는 것
- raw data를 직접 수정하는 것
- build 산출물과 downstream analysis 산출물을 섞는 것
- figure/table과 본문 결과가 불일치한 상태로 manuscript를 진행하는 것
- 결과 이상의 해석을 사실처럼 쓰는 것
- 실험 로그 없이 작업을 끝내는 것

---

## 12. 기본 운영 철학

이 저장소는 단순한 파일 보관함이 아니다.

이 저장소의 목적은 다음을 일관되게 유지하는 것이다.

- 연구 질문
- 데이터 출처와 상태
- build 전략
- analysis 계획
- 실행 기록
- 결과와 산출물
- 논문 초안
- review 및 revision

모든 작업은 재현 가능하고, 추적 가능하고, 다음 단계로 이어질 수 있어야 한다.

## Codex 활용 규칙

이 프로젝트는 Claude를 리드로 사용하되, 필요할 때 Codex CLI를 적극적으로 활용한다.

Codex는 이 프로젝트에서 외부 기술 검토자이자 실행 가능성 비평 도구로 사용한다.
Codex의 역할은 프로젝트 내부 기록을 대신하는 것이 아니라, 현재 계획, 코드, 구조, 원고에 대해 외부 관점의 비판과 보완점을 제공하는 것이다.

최종 판단은 항상 프로젝트 문서, 실행 기록, 산출물, manuscript 상태를 함께 검토하여 내린다.

### 1. Codex를 사용하는 주요 상황

다음과 같은 경우 `codex-orchestrator`를 사용한다.

#### 1-1. Build 계획 검토
다음 상황에서 Codex 검토를 우선 고려한다.
- assembly 전략을 정했을 때
- annotation 전략을 정했을 때
- QC 기준이 충분한지 점검하고 싶을 때
- build 단계가 복잡하거나 선택지가 많을 때

목적:
- 빠진 단계 확인
- QC 누락 확인
- 실행 가능성 점검
- 취약한 가정 확인

#### 1-2. Analysis 계획 검토
다음 상황에서 Codex 검토를 우선 고려한다.
- 새로운 downstream analysis plan을 작성했을 때
- comparative / repeat / functional analysis 설계를 점검하고 싶을 때
- figure/table 생성 계획이 부족한지 확인하고 싶을 때
- 분석 흐름이 연구 질문과 잘 연결되는지 외부 시각이 필요할 때

목적:
- 계획의 빈틈 확인
- 방법과 목표의 연결성 점검
- 산출물 정의 보완
- 재현성 문제 예측

#### 1-3. 스크립트 및 코드 검토
다음 상황에서 Codex 검토를 사용한다.
- Python, R, bash 스크립트를 작성하거나 수정했을 때
- workflow 스크립트가 생겼을 때
- 입출력 경로, 파라미터, 재현성 문제가 걱정될 때
- 코드 품질이나 유지보수성을 점검하고 싶을 때

목적:
- 버그 가능성 탐지
- 재현성 문제 점검
- 경로 처리 문제 점검
- 유지보수성 향상

#### 1-4. 구조 및 정리 상태 점검
다음 상황에서 Codex 검토를 사용한다.
- 폴더 구조가 복잡해졌을 때
- outputs와 intermediate 결과가 섞이기 시작했을 때
- 어떤 파일을 어디에 둬야 할지 애매할 때
- 프로젝트 구조를 정리하기 전에 외부 비판이 필요할 때

목적:
- 구조적 혼란 탐지
- 역할이 모호한 폴더 식별
- traceability 개선
- 정리 방향 제안

#### 1-5. Manuscript 보조 검토
다음 상황에서 Codex 검토를 사용할 수 있다.
- methods가 실제 workflow와 맞는지 보고 싶을 때
- results가 outputs와 잘 연결되는지 점검하고 싶을 때
- manuscript 표현이 기술적으로 부정확한지 확인하고 싶을 때

주의:
- 이 경우 Codex는 보조 검토자로 사용한다.
- 문헌 검색, competing work 확인, reviewer-style 종합 평가는 `manuscript-review`가 우선이다.

---

### 2. Codex를 사용하기 전에 해야 할 것

Codex를 호출하기 전에 가능한 한 다음을 준비한다.

- 관련 계획 문서가 존재하는지 확인
- 입력 데이터 또는 입력 산출물이 명확한지 확인
- 목표가 한 문장으로 설명 가능한지 확인
- 필요한 문맥 파일만 추려서 준비
- outputs 또는 manuscript의 관련 부분을 확인

Codex는 문맥이 불충분하면 피상적인 검토를 할 가능성이 높다.
따라서 무조건 많은 파일을 넣기보다, **현재 질문에 꼭 필요한 문맥만 선별**해서 제공한다.

---

### 3. Codex 결과 해석 원칙

Codex의 결과는 외부 검토 의견으로 취급한다.

다음 원칙을 따른다.

- Codex의 지적은 그대로 기록할 수 있다
- Codex의 제안은 프로젝트 문서와 실행 기록에 비추어 검토한다
- Codex가 보지 못한 자료가 있다면 그 한계를 명시한다
- Codex 결과만으로 프로젝트 방향을 확정하지 않는다
- 최종 결정은 Claude가 프로젝트 전체 맥락을 반영해 내린다

즉, Codex는 강력한 비평 도구이지만 단독 의사결정자가 아니다.

---

### 4. Codex 결과 기록 위치

Codex 검토 결과는 필요에 따라 다음 위치에 기록한다.

- `06_review/`
- 또는 관련 문서 옆의 review note

예시:
- build plan 검토 결과 → `06_review/codex_build_review_YYYY-MM-DD.md`
- analysis plan 검토 결과 → `06_review/codex_analysis_review_YYYY-MM-DD.md`
- script review 결과 → `06_review/codex_script_review_YYYY-MM-DD.md`
- structure review 결과 → `06_review/codex_structure_review_YYYY-MM-DD.md`

Codex 결과를 저장할 때는 다음을 함께 기록하는 것이 좋다.

- 무엇을 Codex에 보여줬는지
- 어떤 질문을 던졌는지
- 핵심 지적이 무엇이었는지
- 실제로 반영할 것과 반영하지 않을 것을 어떻게 판단했는지

---

### 5. Codex와 다른 스킬의 역할 구분

#### `data-intake-review`
- 새 데이터의 구조와 품질을 본다
- build 또는 analysis 시작 전의 데이터 입구 점검이다

#### `research-consistency-check`
- 연구 질문, 계획, 실행, 결과, manuscript 사이의 내부 정합성을 본다
- 프로젝트 내부 기록 기준의 점검이다

#### `codex-orchestrator`
- 외부 기술 검토를 수행한다
- 계획, 코드, 구조, methods/results 연결을 비판적으로 본다

#### `manuscript-review`
- 문헌 검색, competing work 확인, 수치 일관성 검토, reviewer-style 피드백을 수행한다
- 논문 단계의 본격 리뷰다

즉, `codex-orchestrator`는 다른 스킬을 대체하는 것이 아니라 보완한다.

---

### 6. Codex 호출 우선순위

다음 경우에는 Codex 호출을 강하게 권장한다.

- build 계획이 새롭거나 복잡할 때
- analysis plan이 크거나 여러 단계로 이어질 때
- 중요한 스크립트를 처음 작성했을 때
- 폴더 구조가 커지면서 혼란이 생길 때
- manuscript methods/results가 실제 workflow와 맞는지 의심될 때

다음 경우에는 Codex 호출이 선택 사항이다.

- 작은 문장 수정
- 단순한 파일 이동
- 이미 검토된 계획의 사소한 보완
- 논문 문체 교정만 필요한 경우

---

### 7. 실패 시 처리 원칙

Codex CLI를 사용할 수 없거나 오류가 발생하면:

- Codex를 사용하지 못했다고 명시한다
- 어떤 명령이 실패했는지 기록한다
- 가능한 경우 Claude가 자체 검토를 계속한다
- Codex 미사용 상태를 숨기지 않는다

Codex가 없는 상태에서 마치 Codex 검토를 한 것처럼 행동하지 않는다.

---

### 8. 기본 운영 철학

이 프로젝트에서 Codex는 “추가 의견”이 아니라, 중요한 단계에서 활용하는 정식 외부 검토 파트너다.

다만 다음 원칙을 유지한다.

- Codex는 외부 비판자
- Claude는 리드이자 최종 통합 판단자
- 공식 기록은 항상 프로젝트 문서와 로그에 남긴다
- Codex 결과는 기록되고 검토되어야 하며, 맥락 없이 맹목적으로 따르지 않는다