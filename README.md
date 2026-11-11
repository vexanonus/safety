# Safety: check it before it goes online

LAST UPDATED: 11 November 2026

Once something is published, you can't take it back. A real name left in a draft, a photo with a street address in its hidden data, or a line that reads badly out of context can all cause lasting harm to real people.

Safety reads every file before it leaves your computer, the way a newsroom lawyer reads a story before it runs. It's for journalists, researchers, advocates and small publishers who write about real people and have no legal desk. It blocks what would cause harm and lets the rest through, on every commit.

## What it checks

1. **Words.** Your own list of names, numbers and places. The list stays on your machine.
2. **Hidden data.** GPS, author, camera and original file name in photos, PDFs and video. `safety strip` removes it.
3. **Vulnerable-person read.** An AI checks whether a child, patient, victim or party to proceedings could be identified next to private details.
4. **Legal read.** An AI looks for lines a lawyer would quote: defamation, unneeded private detail, statements that read badly.
5. **Public read.** An AI asks whether a careful public figure, such as a minister or editor, could quote the piece as a respectable view, whether or not they agree.

Each read quotes the line, says why, and suggests a fix. `safety reveal FOLDER` reads a whole folder or repo, git history included, as a suspicious stranger would, and lists what it gives away about you. Run it before making a repo public.

Each file that passes is recorded by its fingerprint, and each check gets a line in a private log. Change the file and it is checked again.

## Run it

```
./run setup                 put `safety` on your PATH, make the private settings folder
safety check FILE|FOLDER    all five checks
safety reveal FOLDER        what a stranger learns about you from a folder or repo
safety scan FILE|FOLDER     words and hidden data only (no AI, instant)
safety strip PHOTO          remove hidden data
safety log                  the last 20 checks
./run test                  prove it works (./run test --ai includes the AI reads)
```

**On every commit:** add `safety staged || exit 1` to a pre-commit hook. It checks staged files in repos that have a remote. A file the word check flags gets the AI reads straight away, so a false alarm passes by itself.

**Private settings** go in `~/.config/safety/` (or `$SAFETY_CONFIG`), never in this repo:
- `terms.txt`: one term per line. `~term` counts only alongside another hit; `re:PATTERN` is a regex.
- `harmless.txt`: phrases containing a term that belong to someone else, such as a common phrase.
- `context.md`: anything the AI readers should know, such as pen names you've approved.

Needs Python 3, exiftool and pdftotext, plus the Claude Code CLI for the AI reads. The model is set with `SAFETY_MODEL` (default `opus`) and costs about 2–3 cents per file read.

How the checks work: [docs/HOW-WE-CHECK.md](docs/HOW-WE-CHECK.md). Start here to change it: [docs/START.md](docs/START.md).

## Repo

https://github.com/vexanonus/safety · MIT licence
