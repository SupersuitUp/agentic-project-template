# agentic-project-template

A forkable repo for **one real project with a deliverable and a deadline** — a
thesis, a book, a filing, a launch, a move. It holds every piece of context the
project has, plus a state machine an agent reads to answer "what is next", so
closing the laptop costs nothing and reopening it costs one command.

Pattern: https://appliedai.wiki/concepts/agentic-project-management

## What is in here

| Path | What it is |
|---|---|
| `template/` | The thing you copy. This becomes the project repo. |
| `BOOMERANG.md` | Paste-into-any-AI interview that returns a filled `PROJECT.md` + `STATE.md`. For when the project owner is not in the room. |
| `run-tests.sh` | The regression suite. Six cases: five attacks that must fail, one good-faith fill that must pass. |

## Start a project

```bash
# NOT YET PUSHED TO A REMOTE. Local only, as of 2026-07-29.
cp -R <this-repo>/template ~/projects/<project-slug>
cd ~/projects/<project-slug>
git init && git add -A && git commit -m "init: <project> as an agentic project"
python3 check.py     # zero of everything, no dates yet. That is correct.
```

Then fill `PROJECT.md` and `STATE.md` and re-run `check.py`. It will name the
date that actually binds.

## Start someone ELSE'S project

Send them `BOOMERANG.md`. They paste it into whatever AI they use, it interviews
them for ten minutes, and it hands back two finished files that drop straight
into `template/`. They start populated instead of staring at `<PROJECT NAME>`.

This is the right path more often than it looks. The alternative is you guessing
at their deliverable and their deadline, and a scaffold built on a guess is worse
than no scaffold.

## The honest part

`check.py` asserts content rather than counting filenames. A directory is not a
source, a touched file is not an annotation, and a heading with its own authoring
instructions still under it is not a filled-in section. It reads every milestone
date and reports the nearest FUTURE one as what binds, whether or not that date
is self-imposed, because the decision you must make before the work can start is
usually the thing that actually catches people out.

It prints its template version on line one. **If you are reviewing a project repo,
check that line against this repo before you trust anything you conclude.** A cold
review once spent an hour producing a confident, thorough, wrong report against a
two-generations-stale copy that had no way to announce itself. That is why the
version is printed and why the suite exists.

## Changing the template

```bash
bash run-tests.sh          # must be ALL GREEN
```

Every case in the suite is a defect a cold review actually found. Add a case
whenever a new one is found, and bump `TEMPLATE_VERSION` in `template/check.py`
in the same commit. A checker you have not attacked is a checker you have not
tested.

## Canonical home

This repo is the published home. The `start-agentic-project` skill carries a
working copy at `~/.agents/skills/start-agentic-project/`. **They must not
drift.** After changing either one:

```bash
diff -r ~/.agents/skills/start-agentic-project/template ./template
```

If that ever prints anything unexpected, the version stamp is the tiebreaker:
higher `TEMPLATE_VERSION` wins, and the loser gets overwritten rather than
merged by hand.
