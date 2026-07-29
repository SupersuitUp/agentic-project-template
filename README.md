# agentic-project-template

A forkable repo for **one real project with a deliverable and a deadline**: a
thesis, a book, a filing, a launch, a move. It holds every piece of context the
project has, plus a state machine an agent reads to answer "what is next", so
closing the laptop costs nothing and reopening it costs one command.

Pattern: https://appliedai.wiki/concepts/agentic-project-management

## What is in here

| Path | What it is |
|---|---|
| `template/` | The thing you copy. This becomes the project repo. |
| `SKILL.md` | The `start-agentic-project` skill: hand it to an AI and it runs the interview and stands the whole thing up for you. |
| `template/.claude/skills/interview/` | The interview as a verb. Run it in Claude Code on a fresh copy and it writes your `PROJECT.md` and `STATE.md`. |
| `BOOMERANG.md` | The same interview as a paste-into-any-AI prompt. For no Claude Code, or when the project owner is not in the room. |
| `run-tests.sh` | The regression suite. Six cases: five attacks that must fail, one good-faith fill that must pass. |

## Start a project

```bash
git clone https://github.com/SupersuitUp/agentic-project-template.git
cp -R agentic-project-template/template ~/projects/<project-slug>
cd ~/projects/<project-slug>
git init && git add -A && git commit -m "init: <project> as an agentic project"
python3 check.py     # zero of everything, no dates yet. That is correct.
```

Or press **Use this template** on GitHub, which gives you your own private repo
with the history already started.

Then **open it in Claude Code and run `interview`.** It asks you questions for
about ten minutes and writes `PROJECT.md` and `STATE.md` for you. Re-run
`check.py` after and it will name the date that actually binds.

Filling those two files by hand is supported and is not the intended path. The
blank ontology is where people stop.

## No Claude Code, or the project is someone else's

Send them `BOOMERANG.md`. They paste it into whatever AI they already use, it
runs the same interview, and it hands back two finished files that drop straight
into `template/`. They start populated instead of staring at `<PROJECT NAME>`.

Reach for this whenever the person who can answer the questions is not the person
at the keyboard. The alternative is you guessing at their deliverable and their
deadline, and a scaffold built on a guess is worse than no scaffold.

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

**This repo is the only copy of all of it**, including `SKILL.md`. Anything
elsewhere (an installed skill under `~/.agents`, a file served by a wiki) is a
deployment of this, not a peer, and is overwritten from here rather than merged.

Two copies existed for about one day and diverged inside that day, which is the
entire reason this section exists. If you find another, delete it.
