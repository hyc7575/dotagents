# dotagents

에이전트 코딩 툴들의 user-scope 설정을 버전 관리하는 dotfiles 스타일 레포.

## 구조

```
dotagents/
├── AGENTS.md        # 모든 에이전트 공용 행동 원칙 (툴 독립적)
├── claude/          # Claude Code 설정
│   ├── plugins.md   # 설치된 플러그인 목록과 설치 커맨드
└── README.md
```

## AGENTS.md

툴/언어/프레임워크에 독립적인 공용 행동 원칙. Claude Code, Codex CLI, Cursor, Gemini CLI 등 어디서나 동일하게 적용된다.

새 프로젝트 시작 시 루트에 복사해서 사용한다:

```bash
curl -O https://raw.githubusercontent.com/<username>/dotagents/main/AGENTS.md
```

Claude Code에서 `CLAUDE.md`로 인식시키려면 symlink:

```bash
ln -s AGENTS.md CLAUDE.md
```

프로젝트별 규칙(빌드 명령, 디렉토리 구조, 스택 가이드)은 복사한 `AGENTS.md` 아래에 섹션으로 추가한다. 도메인별 세부 규칙은 하위 디렉토리에 별도 `AGENTS.md`를 둔다 (예: `src/api/AGENTS.md`).

### 설계 원칙

- 언어/프레임워크 독립적
- 약 250단어, 한 화면에 들어오는 분량
- Superpowers 같은 워크플로우 프레임워크와 충돌하지 않음
- 이직, 회사 이동, 도구 교체 후에도 그대로 사용 가능

## claude/

Claude Code의 user-scope 설정 파일들을 관리한다.

- `CLAUDE.md` - 전역 CLAUDE.md 설정
- `plugins.md` - 설치된 플러그인 목록 및 복원 커맨드
- `skills/` - 직접 작성한 커스텀 스킬 파일들

## 향후 계획

Cursor, Windsurf 등 다른 에이전트 코딩 툴의 user-scope 설정도 동일한 방식으로 추가될 수 있다. 공용 원칙은 루트 `AGENTS.md`에 두고, 툴 특화 설정만 각 폴더에 분리한다.

```
dotagents/
├── AGENTS.md
├── claude/
├── cursor/
├── windsurf/
└── ...
```
