# dotagents

에이전트 코딩 툴들의 user-scope 설정을 버전 관리하는 dotfiles 스타일 레포.

## 구조

```
dotagents/
├── claude/          # Claude Code 설정
│   ├── CLAUDE.md    # user-scope CLAUDE.md
│   ├── plugins.md   # 설치된 플러그인 목록과 설치 커맨드
│   └── skills/      # 커스텀 스킬 파일들
└── README.md
```

## claude/

Claude Code의 user-scope 설정 파일들을 관리한다.

- `CLAUDE.md` - 전역 CLAUDE.md 설정
- `plugins.md` - 설치된 플러그인 목록 및 복원 커맨드
- `skills/` - 직접 작성한 커스텀 스킬 파일들

## 향후 계획

Cursor, Windsurf 등 다른 에이전트 코딩 툴의 설정도 동일한 방식으로 추가될 수 있다.

```
dotagents/
├── claude/
├── cursor/
├── windsurf/
└── ...
```
