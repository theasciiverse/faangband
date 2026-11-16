# FAangband (Asciiverse packaging)

Nick McConnell's First Age Angband (C, curses, GPL-2.0 or the Angband
licence), packaged for the Asciiverse catalog (id `faangband`, kind
`game`, genre `roguelike`). Not our code: the game stays as its author
made it; list every change in PATCHES.md.

- `upstream` is github.com/NickMcConnell/FAangband (branch `main`, weekly
  pre-release tags like `2.0.1-1103-gc4ee2ce24`); ours is branch
  `asciiverse`, `origin` github.com/theasciiverse/faangband (private).
- Build: `sh asciiverse/build.sh` (static in alpine:3.22 under docker in
  CI; locally it links the host's ncursesw), then `sh asciiverse/stage.sh`
  for `stage/`: the program with `lib/` beside it. Set `UPSTREAM_VERSION`
  in build.sh when moving to a newer upstream build.
- Release: tag `v<upstream build>-av.<n>` (first `v2.0.1-1103-av.1`) and
  push it; `.github/workflows/asciiverse-release.yml` builds Linux, macOS
  and the Linux system packages. No Windows build (PATCHES.md).
- Player files live in `$XDG_STATE_HOME/faangband`. Tests and scripted
  runs always set a scratch `XDG_STATE_HOME` and `HOME` in the same
  command and run under `systemd-run --user --scope -p MemoryMax=4G`.
  No sound is built.
- Preview: `python3 asciiverse/record-preview.py` after stage.sh (needs
  pyte and asciinema 3). Catalog drafts: `asciiverse/faangband.toml` and
  `.md`; copies go in hub/catalog, the cast in hub/site/casts.
