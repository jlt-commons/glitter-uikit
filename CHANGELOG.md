# Changelog

Notable changes to glitter-uikit, newest first. The format follows
[babashka's changelog](https://github.com/babashka/babashka/blob/master/CHANGELOG.md):
one bullet per user-visible change, written as what a reader would notice
rather than what a commit did.

Nothing has been released yet, so there is a single `Unreleased` section.

## Unreleased

### Dependencies

- **Dropped the GTK4/GLib requirement.** This renderer never called a
  single GTK function, but depending on the full `glitter` package
  pulled GTK4/GLib in transitively via its `:jolt/native` declaration —
  jolt hard-fails in `load-natives!` before any namespace loads if a
  declared native is missing, and an `:aliases`-scoped `:jolt/native`
  was verified to be silently ignored, so there was no way to scope it
  away from this side. Fixed by depending on
  [`glitter-core`](https://github.com/jlt-commons/glitter-core) (the
  natives-free extraction of `glitter.core`/`glitter.protocols`/
  `glitter.alias`, same names, no `:jolt/native` anywhere in its own
  `deps.edn`) directly instead, plus
  [`nexus-jolt`](https://github.com/jlt-commons/nexus-jolt) (the
  `nexus.core`/`nexus.registry` dispatch engine `flights`/`temperature`/
  `todo` use — renamed from `glitter.nexus`/`glitter.nexus.registry`,
  the pre-extraction names those three examples used to require).
  `weavejester/hiccup` and `clojure.tools.logging`, previously arriving
  transitively through `glitter`, are declared here directly now that
  `glitter` is no longer in the dependency graph. See
  [glitter's own changelog entry](https://github.com/jlt-commons/glitter/blob/main/CHANGELOG.md)
  for the extraction this depends on.

### Documentation

- **Corrected stale licensing/attribution claims about upstream
  glimmer-uikit.** `README.md`, `NOTICE.md`, and
  `docs/guide/porting-and-attribution.md` all stated, in the present
  tense, that upstream `jolt-lang/glimmer-uikit` ships no LICENSE file.
  That was true of the commit this project actually ported from
  (`8f1c6a4`, tag `v0.1.0`, 2026-08-20 arc), but the live repository at
  that URL was recreated from scratch on 2026-09-13 as an entirely
  different, unrelated codebase (30 commits, all by a different author,
  imported from a separate project) — commit `8f1c6a4` no longer exists
  there, and the new repo now ships an MIT `LICENSE` that covers only
  the new, unrelated code. All three files now say so explicitly, so a
  reader doesn't visit the URL, see a LICENSE, and wrongly conclude the
  originally-ported material is now licensed. Also removed a duplicate,
  stale `## Licence` section in `README.md` that still said "MIT for
  this project's own code" after the 2026-09-05 EPL-2.0 relicense.
