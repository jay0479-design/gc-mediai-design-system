# GC메디아이 디자인 시스템 — Claude Code 전용 워크플로우 템플릿

Figma MCP 기반 **디자인 자동화**(시안 생성·유지보수)를 위한 팀 공용 Git 저장소 템플릿입니다.
기본 산출물은 **Figma 시안 프레임**이며, 코드(퍼블리싱)는 명시 요청 시에만 진행합니다.
이 저장소를 클론(또는 프로젝트 루트에 복사)하는 것만으로
누구나 동일한 품질 기준의 Claude Code 작업 환경을 갖게 됩니다.

## 구조

```
├── CLAUDE.md                      # 최상위 절대 규범 (Claude Code가 자동 로드)
├── .claude/
│   ├── settings.json              # 팀 공유 권한 설정
│   └── commands/
│       ├── new-page.md            # /new-page [Figma 링크] — 신규 페이지 시안 생성(Figma)
│       └── maintain.md            # /maintain [Figma 링크] — 기존 시안 유지보수(Figma)
├── docs/                          # Claude가 작업 전 필독하는 컨벤션 문서
│   ├── 01_핵심_개발_원칙.md
│   ├── 02_Figma_MCP_분석_지침.md
│   ├── 03_디자인_토큰.md
│   └── 04_페이지_작업_요청_템플릿.md
└── src/                           # 생성 코드 출력 위치
```

## 시작하기

1. 이 저장소를 클론하거나, 기존 프로젝트 루트에 `CLAUDE.md`, `.claude/`, `docs/`를 복사합니다.
2. Figma MCP 서버가 Claude Code에 연결되어 있는지 확인합니다.
3. 프로젝트 루트에서 `claude`를 실행합니다.
4. 슬래시 커맨드 또는 자연어로 작업을 요청합니다.

```
/new-page https://www.figma.com/design/6eO6s3lH8TVv85FWgBekEh/?node-id=1374-2669
/maintain https://www.figma.com/design/6eO6s3lH8TVv85FWgBekEh/?node-id=470-120
```

자연어로 요청해도 Claude가 표준 3단계([분석]→[실행]→[확인]) 작업 계획을
먼저 제안한 뒤 진행합니다.

## 규칙 우선순위

`CLAUDE.md` > Figma `Component` 기준점(`2031-6499`) > `docs/` 개별 문서

## 주의

- MCP가 반환하는 Figma 에셋 URL은 약 7일 후 만료됩니다.
  프로덕션 커밋 전 반드시 정적 에셋으로 교체하세요.
- `docs/03_디자인_토큰.md`의 값은 작업 시작 시 Figma에서 재검증 후 사용합니다.
