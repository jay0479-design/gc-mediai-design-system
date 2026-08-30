# 02. Figma MCP 기반 전수 분석 및 반응형 UI 구축 지침

제공된 Figma URL과 노드 ID를 읽어 들여, 피그마 내 정의된 디자인 시스템 토큰과
레이아웃 구조를 분석하고 반응형 웹 코드로 변환합니다.

---

## 1. 분석 대상 Figma 링크 및 노드

파일 키: `6eO6s3lH8TVv85FWgBekEh`
아래 3개의 지정된 피그마 노드와 그 하위에 포함된 모든 프레임(Frame),
레이어(Layer), 컴포넌트(Component)를 전수 분석합니다.

### [Component 기준점] — node-id `2031-6499`
- URL: https://www.figma.com/design/6eO6s3lH8TVv85FWgBekEh/?node-id=2031-6499
- 분석 내용: 타이포그래피 스타일(Font, Size, Line-height, Letter-spacing),
  컬러 토큰, 공통 버튼, 인풋, 아이콘, 칩 등 제반 컴포넌트 규격.

### [모바일(MO) 세부 페이지] — node-id `470-120`
- URL: https://www.figma.com/design/6eO6s3lH8TVv85FWgBekEh/?node-id=470-120
- 분석 내용: 모바일 환경에서의 오토 레이아웃(Auto Layout), 간격(Gap),
  여백(Padding/Margin), 컴포넌트 배치 순서.

### [PC 세부 페이지] — node-id `1374-2669`
- URL: https://www.figma.com/design/6eO6s3lH8TVv85FWgBekEh/?node-id=1374-2669
- 분석 내용: 데스크톱 환경에서의 그리드 시스템, 컬럼 구조,
  섹션 수평/수직 배치 및 반응형 전환 포인트.

---

## 2. 작업 순서 지침 (Strict Workflow)

### [1단계] UI 구조 선행 구축 (UI Construction Phase)
- 시각적 디자인 요소나 이미지 에셋 배치를 고려하기 전에, 시맨틱 HTML 태그 기반의
  문서 구조, DOM 계층, Grid 및 Flexbox 레이아웃 뼈대를 먼저 완성합니다.
- PC와 모바일 디자인을 대조하여, 단일 코드베이스에서 구현할
  반응형 UI 구조 및 컴포넌트 트리 구조를 우선적으로 정립합니다.

### [2단계] 시각적 고려 및 에셋 배치 (Visual Enhancement & Asset Placement Phase)
- 1단계 구조 구축 완료 이후, Figma MCP에서 추출한 스타일 정보를 적용합니다.
- `Component` 노드에 정의된 타이포그래피(폰트, 간격, 크기) 및 컬러 스킴을
  오차 없이 반영합니다.
- 이미지 및 그래픽 에셋의 배치, 둥근 모서리, 그림자 등 세부 스타일을 최종 결합합니다.

---

## 3. MCP 실무 규칙 (실측 검증된 패턴)

- **노드 ID 표기**: MCP 툴 파라미터에는 콜론 표기(`470:120`),
  Figma URL에는 하이픈 표기(`470-120`)를 사용한다.
- **에셋 URL 만료**: MCP가 반환하는 Figma 에셋 URL은 약 7일 후 만료된다.
  프로덕션 커밋 전 반드시 정적 에셋으로 교체한다.
- **크로스 파일 작업**: 소스 파일 읽기와 타겟 파일 쓰기는
  서로 다른 `fileKey`의 별도 MCP 호출로 분리한다.
- **미공개 컴포넌트**: `figma.importComponentByKeyAsync()`는 미공개 컴포넌트에서
  조용히 실패한다. 반드시 반환값을 확인하고, 대체 시 리포트에 명시한다.

---

## 4. 자체 검수 보고 (Self-Confirm Report)

코드 생성을 완료하기 전, 아래 3가지 항목을 스스로 검토하고 결과를 출력합니다.

1. **[구조 선행]** 시각적 요소 및 에셋 배치 전 UI 뼈대 구축을 먼저 처리했는가? (O/X)
2. **[스타일 일치성]** `Component` 노드의 폰트, 간격, 스타일 규칙이
   MO/PC 구현체 전체에 동일하게 적용되었는가? (O/X)
3. **[반응형 통합]** MO(`470-120`)와 PC(`1374-2669`) 디자인이
   하나의 코드 내에서 매끄럽게 대응되는가? (O/X)
