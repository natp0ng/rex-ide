# rex-ide notes

A fork of [Zed](https://github.com/zed-industries/zed) built for very large codebases.

## Goals
1. Fix indexing and the language servers so huge projects open without hanging.
2. Open the full AOSP tree and jump to file / go to definition across languages: Mojo, Java, Kotlin, Rust.
3. Later: a UI editor for Android apps inside AOSP.

The first scope is **AOSP + Chromium for Android** only.

## Git
| | |
|---|---|
| `origin` | `natp0ng/rex-ide` (SSH alias `github.com-personal`) |
| `upstream` | `zed-industries/zed` (fetch only, push disabled) |
| `main` | mirrors `upstream/main`, **never edit** |
| `rex` | our working branch |

Git identity is set only in this repo (personal email). The global config belongs to the office account.

### Pulling in a Zed update
```sh
git fetch upstream
git switch main && git merge --ff-only upstream/main
git switch rex && git merge main
```

## Rules for keeping merges easy
- New code goes in new crates: `crates/rex_*`
- Edit Zed's own crates as little as possible. Add only a thin hook that calls into a `rex_*` crate.
- Mark every spot that touches Zed code with `// REX:` so it's easy to find (`rg "REX:"`).
- Do branding, name and icon changes last, because they conflict often.
- Don't edit Zed's files `CLAUDE.md`, `AGENTS.md` or `README.md`. Put our notes here instead.
- Keep test projects (AOSP, Chromium) outside this repo, e.g. `~/aosp`, `~/chromium`.

## Progress
- [x] Fork + clone + remote/branch setup
- [ ] Build stock Zed
- [ ] Open AOSP and find where it hangs
