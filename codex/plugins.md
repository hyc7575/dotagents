# Codex Skills & Plugins

Codex는 `~/.agents/skills/`를 시작 시 스캔해 SKILL.md frontmatter를 파싱하고 on-demand로 스킬을 로드한다.
플러그인 매니페스트가 아니라 **native skill discovery (symlink 기반)** 방식이다.

> 행동 원칙(Think Before Coding, Simplicity First, Surgical Changes 등)은 루트 `AGENTS.md`로 단일화.
> karpathy-skills는 AGENTS.md와 내용이 겹쳐 미설치.

---

## 1. superpowers

- **소스**: obra/superpowers
- **방식**: clone + symlink (native discovery)
- **설치**:

```bash
  git clone https://github.com/obra/superpowers.git ~/.codex/superpowers
  mkdir -p ~/.agents/skills
  ln -s ~/.codex/superpowers/skills ~/.agents/skills/superpowers
```

설치 후 Codex 재시작.

- **subagent 스킬 활성화 (선택)**: `subagent-driven-development`, `dispatching-parallel-agents`는 multi-agent 기능 필요. `~/.codex/config.toml`에 추가:

```toml
  collab = true
```

- **업데이트**:

```bash
  cd ~/.codex/superpowers && git pull
```

symlink을 통해 즉시 반영. 재시작 불필요.

- **검증**:

```bash
  ls -la ~/.agents/skills/superpowers   # symlink 확인
  ls ~/.codex/superpowers/skills        # 스킬 목록 확인
```

> 구버전 bootstrap 방식에서 마이그레이션하는 경우, `~/.codex/AGENTS.md`의 기존 bootstrap 블록을 제거할 것.

---

## 2. ralph-loop → Codex 네이티브 `/goal`

- **소스**: Codex 내장 기능 (별도 설치 불필요)
- **방식**: config 설정 후 `/goal` 명령 사용
- **설명**: ralph-loop(Ralph Wiggum 패턴)은 "목표 → 행동 → 관찰 → 다음 행동"을 완료 조건까지 자율 반복하는 패턴.
  Codex는 이를 `/goal` 명령으로 first-party 지원한다.
- **활성화**: `~/.codex/config.toml`에서 goals 기능 플래그 설정 (버전에 따라 다름, `/goal` 입력 시 안내 따름).
- **주의**: `/goal` 실행 중에는 스킬을 추가 설치할 수 없다. 루프가 필요로 하는 스킬(예: superpowers)은 **반드시 실행 전에 설치**할 것.

> 별도 bash 스크립트형 ralph-loop를 쓰고 싶으면 PageAI-Pro/ralph-loop 또는 Th0rgal/open-ralph-wiggum 참고.
> 단, Codex 환경에서는 네이티브 `/goal`이 goal 추적 + 토큰 budget 제어를 first-party로 제공하므로 우선 검토.

---

## config.toml 통합 예시

```toml
# ~/.codex/config.toml
collab = true                       # superpowers subagent 스킬용
model_reasoning_effort = "high"     # 복잡한 스킬 워크플로우 권장
```
