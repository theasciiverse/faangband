# FAangband

**Beleriand in the days of the War of the Jewels.**

Morgoth sits in Angband with the Silmarils in his crown, and the free
peoples of the First Age are losing. You start where your people live: a
Grey-Elf in Menegroth, the thousand caves of Doriath, a Dwarf in the
great halls of Belegost, a Longbeard of Khazad Dum, an Easterling in
little Eriador Town, a Green-Elf in Ossiriand, even an Ent. From there
the whole of Beleriand is open to you, from the plains of West Beleriand
to the mountains of Ered Luin, and none of it is safe.

FAangband is First Age Angband. Between the towns lies wilderness made
fresh every time you walk into it: plains, forests, mountains, deserts,
swamps and valleys, with day and night passing over them and a choice of
roads at every edge. Four dungeons wait at the end of those roads, each
with a guardian at the bottom: Mîm, Betrayer of Turin, in Amon Rudh;
Glaurung, Father of the Dragons, in Nargothrond; Sauron the Sorcerer on
Tol-in-Gaurhoth; and Morgoth himself, a hundred levels down in Angband.
Ungoliant, the Unlight, broods in the valley of Nan Dungortheb.

- **Thirteen races and nine classes**: Easterlings and Edain, Green-,
  Grey-, High- and Dark-Elves, Hobbits, Dwarves, Petty-Dwarves and
  Longbeards, the Drúedain, Beornings who take the shape of a bear, and
  Ents; Warriors, Mages, Druids, Priests, Necromancers, Paladins, Rogues,
  Rangers and Blackguards
- **Specialties**, special abilities you choose as you grow; slaying a
  guardian earns you more
- **The Silmarillion's own treasures**: Ringil, Anguirel, Gurthang, the
  dagger of Maedhros, sets of artifacts that grow stronger together
- **Four ways to play** the world: the standard wilderness, an extended
  one, a hybrid with portals between dungeons, or a classic Angband
  dungeon under a single town
- **Monster traps**, recall points you set yourself, and a house you can
  move to another town once you have walked there

## Playing

Run `faangband` from this folder, with its `lib` folder beside it. It
needs a UTF-8 terminal of at least 80x24; a bigger one shows more of
the map.

- **Arrow keys** or **1** to **9**: move; walk into a monster to attack
- **<** and **>**: take a path or staircase up or down; standing on the
  edge of a wilderness map, they lead on to the next
- **g** pick up, **i** inventory, **e** equipment, **w** wear or wield
- **q** quaff, **r** read, **E** eat, **a** aim, **u** use a staff,
  **z** zap a rod, **f** fire, **v** throw
- **m**: cast a spell; **S**: specialties; **!**: change shape
  (Beornings)
- **+**: set a monster trap; **$**: move house; **#**: the time of day
- **C**: character sheet, **l**: look, **M**: map, **~**: knowledge
- **=**: options (a roguelike keyset is there too); **?**: help
- **Ctrl-S**: save; **Ctrl-X**: save and quit

Your game, options, character dumps and scores are kept in the state
folder, `$XDG_STATE_HOME/faangband` (else `~/.local/state/faangband`),
and FAangband carries on from your save the next time you start it.

## Credits

- FAangband: Nick McConnell, https://github.com/NickMcConnell/FAangband,
  with Si Griffin (0.3.6) and the contributors in `docs/thanks.rst`
- Before it: Oangband by Leon Marrick and Bahman Rabii, Angband by the
  Angband Dev Team, Moria by Robert Alan Koeneke and Umoria by James E.
  Wilson
- Licence: GNU GPL version 2 or the Angband licence (`copying.rst`,
  `GPL-2`)
- This package: Asciiverse, for the av launcher and the catalog at
  https://asciiverse.sh. What we changed is in PATCHES.md.

## Building

`sh asciiverse/build.sh` builds `./faangband` with the curses frontend
only (statically in Alpine for the release, against the system curses
on macOS), and `sh asciiverse/stage.sh` gathers the program, its `lib`
and these files into `stage/`. The release workflow
(`.github/workflows/asciiverse-release.yml`) builds Linux and macOS
archives and Linux system packages. Upstream's own README and docs
cover the other frontends.
