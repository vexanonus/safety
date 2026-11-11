# How it checks

Safety reviews files before publication. This page explains the method. The code is in this repo, open for anyone to inspect.

## The principle

Many places restrict identifying children, victims, patients or people in proceedings. Careful publishers keep real people's private details out unless the piece needs them, and write so that a fair-minded public figure could quote them.

## The checks

1. **Words.** A list the publisher keeps privately: names, numbers and places that should not appear.
2. **Hidden data.** Photos and documents can carry GPS, author and device data. It is found and can be removed.
3. **Vulnerable-person read.** An AI asks whether a child, patient, victim or party to proceedings could be identified next to private details.
4. **Legal read.** An AI reads the file as a newsroom lawyer would, and quotes any line a lawyer would use.
5. **Public read.** An AI asks whether a careful public figure could quote the piece as a respectable view.

Before a folder or repo is made public, `safety reveal` reads all of it, git history included, as a suspicious stranger would, and lists what it gives away about the author.

## When they run

- **Before publishing:** `safety check` on the piece.
- **On commit,** in a repo with a remote: the word and hidden-data checks run, and anything flagged gets the AI reads. A file that fails cannot be committed.

## Why AI

An AI reads every line of every file, the same way each time, and writes down what it found. Its verdict and reasons are kept in the log.

## The record

Each check is one line in a private log: date, file, fingerprint, result and which checks ran. A file that passes is recorded by its fingerprint. If it changes, it is checked again.
