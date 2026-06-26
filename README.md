# 🦀 claudemgr/rust

Rust project specification for Claude AI — the single source of truth for building CasjaysDev Rust projects.

## 📄 What's Here

| File | Purpose |
|------|---------|
| `API.md` | Complete ~40,000-line Rust project specification (34 PARTs) |
| `IDEA.md` | Project-scope description and variables |
| `CLAUDE.md` | Short loader — reads `API.md` at session start |

## 📦 What API.md Covers

All 34 PARTs of the Rust project specification:

| PART | Topic |
|------|-------|
| 0–6 | Project structure, Cargo.toml, release profile, binary naming |
| 7–9 | Makefile pattern (local dev), Docker build, cache scheme |
| 10–13 | Error handling, `?` operator, logging, tracing |
| 14–18 | HTTP server, routing, middleware, request/response types |
| 19–22 | Authentication, authorization, session management |
| 23–25 | CLI flags, NO_COLOR, clap derive API |
| 26–28 | CI/CD — GitHub/GitLab/Gitea/Forgejo workflows |
| 29–31 | Release workflow, binary artifacts, Docker image publishing |
| 32–34 | Testing, Docker/Incus dev workflow, security hardening |

## 🏗️ Build Model

```
Local development / AI work → make build / make test / make release
CI/CD pipelines            → cargo build --release / cargo test (direct)
```

**Makefile is a local development tool only.** CI/CD workflow files always use direct `cargo` commands — never `make`.

All builds run inside Docker via `casjaysdev/rust:latest` — never on the host machine.

### Cache Scheme

| Variable | Local Default | Container Path |
|----------|--------------|----------------|
| `CARGO_CACHE` | `~/.cargo` | `/usr/local/share/cargo` |
| `RUSTUP_CACHE` | `~/.rustup` | `/usr/local/share/rustup` |
| `SCCACHE_CACHE` | `~/.cache/sccache` | `/root/.cache/sccache` |

## ⚙️ Required Release Profile

```toml
[profile.release]
opt-level      = "z"
lto            = true
codegen-units  = 1
strip          = true
panic          = "abort"
```

All five fields are non-negotiable.

## 🏷️ Binary Naming

Schema: `{name}-{os}-{arch}`

| Term | Valid values |
|------|-------------|
| OS | `linux` `macos` `windows` `freebsd` |
| Arch | `x86_64` `aarch64` |

Never use Go terms (`darwin`, `amd64`, `arm64`) or a `-musl` suffix.

## 🤖 AI Quick Start

```text
You are working in the current project directory.

The project specification is ./API.md. It is the single source of truth.

Before doing anything else:
1. Fully read ./API.md from the top through PART 5.
2. Follow ./API.md exactly as written.
3. Do not guess or assume when ./API.md says to detect, read, verify, or ask.
4. If ./TODO.AI.md exists, review and update it as needed.
5. Commit all COMMIT, NEVER, and MUST rules from ./API.md to memory.
6. Before making changes, read the relevant section of ./API.md and follow it exactly.

If any file conflicts with ./API.md, ./API.md wins.
```

## 👤 Author

**Jason Hempstead** · [GitHub](https://github.com/casjay) · [Casjays Developments](https://casjaysdev.pro)

## 📄 License

MIT — see [LICENSE.md](LICENSE.md)
