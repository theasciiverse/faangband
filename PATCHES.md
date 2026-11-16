# Changes from upstream

This is the Asciiverse packaging of FAangband (First Age Angband) by Nick
McConnell, from [NickMcConnell/FAangband](https://github.com/NickMcConnell/FAangband)
(the `upstream` remote). Branch `asciiverse` starts at upstream's tag
`2.0.1-1103-gc4ee2ce24` (commit `c4ee2ce24`, 2026-10-14), the newest of
the builds upstream publishes on its releases page: 2.0.1 (2021) with
five years of fixes, most of them carried over from Angband 4.2. The
commits below are ours.

Licence: FAangband is under either the GNU GPL version 2 or the "Angband
licence" (non-commercial), at the user's choice (`docs/copying.rst`). The
text says "version 2" with no "or later", so this edition is taken under
GPL-2.0-only, as our Angband is. `asciiverse/GPL-2` is the licence text
(upstream ships none), copied from theasciiverse/angband.

## Removed

- The Shockbolt tileset (`lib/tiles/shockbolt/`, its entries in
  `lib/tiles/list.txt`, `lib/tiles/Makefile` and `src/Makefile.std`):
  Raymond Gaustadnes' terms forbid modifying it or using it with other
  projects, so it is not free. It is still in upstream's history, which
  this repository carries. The other tilesets, the sounds and the fonts
  stay in the tree but are neither built nor shipped.

## Code

- Paths (`src/main.c`, `src/init.c`): on Unix the game reads its data
  (`gamedata`, `customize`, `help`, `screens`, `ghost`) from a `lib`
  folder beside the running program when there is one, found through
  `/proc/self/exe` on Linux and `_NSGetExecutablePath()` on macOS, so
  av's symbolic link in `~/.local/bin` still finds it; otherwise from
  the configured `/usr/share/faangband`. The data is only read. The
  player's folder, `~/.angband/FAangband` upstream, is
  `$XDG_STATE_HOME/faangband` (else `~/.local/state/faangband`), holding
  options, keymaps, character dumps and the `save`, `scores`, `panic`,
  `archive` and `bone` folders. Upstream's `-d<dir>=<path>` options
  still override any of these.

## Packaging (new files)

- `asciiverse/build.sh`: autotools build of the curses (GCU) frontend
  only (`--enable-curses --disable-x11 --disable-sdl --disable-sdl2`, no
  sound), `--with-private-dirs` (no setgid, no shared score file) and
  `--sysconfdir=/usr/share` so the whole read-only lib is
  `/usr/share/faangband`. Fully static in Alpine (musl, static ncursesw);
  on macOS it links the system ncurses through upstream's own
  `NCURSES_CONFIG` workaround from its `mac.yaml`. Git is hidden from
  the build and a `version` file gives upstream's build name, so the
  game shows `2.0.1-1103-gc4ee2ce24`, not a `git describe` of our
  commits.
- `asciiverse/stage.sh`: puts the program,
  `lib/{gamedata,customize,help,screens,ghost}` without the build files,
  `docs/copying.rst`, `GPL-2`, our README and this file in `stage/`, the
  av archive's contents. No tiles, fonts, sounds or icons are shipped.
- `asciiverse/nfpm.yaml`: .deb, .rpm, .apk and Arch packages:
  `/usr/bin/faangband`, `/usr/share/faangband`, the licence in
  `/usr/share/doc/faangband`. No `.desktop` file or icon. The package
  version is upstream's build with dots (`2.0.1.1103`).
- `asciiverse/README.md`: the README in each archive.
- `asciiverse/record-preview.py` and `asciiverse/faangband.cast`: the
  catalog preview, a scripted Beorning Warrior who starts in Gladden
  Fields Town and sets out into the Anduin Vale as a bear cub (best of
  several takes).
- `asciiverse/faangband.toml`, `asciiverse/faangband.md`: the catalog
  manifest and store page, as drafts for hub.
- `.github/workflows/asciiverse-release.yml`: builds all of it on a
  `*-av.*` tag. Upstream's own workflows run only on pushes to `main`
  and on pull requests, which this repository does not have.

## Not built

- Windows: upstream's Windows edition is its own GUI frontend
  (`main-win.c`). A Windows console build would take upstream's CMake
  route against MSYS2's ncurses plus a Windows branch of our path change,
  and has not been tried.
- X11, SDL, SDL2, sound, tiles, the Nintendo and DOS ports, the stats
  and test frontends.
