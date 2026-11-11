# Spec

## Shape

One Python file with no dependencies beyond the standard library. It calls three outside tools: `exiftool` (hidden data), `pdftotext` and `textutil` (text out of PDF and Word), and the Claude Code CLI (`claude -p`) for the AI reads.

## Decisions

- **Code and private settings live apart.** The repo is public so anyone can inspect the method. The words, context, log and approved list sit in `$SAFETY_CONFIG` and never enter the repo. The alternative, a private repo, would hide the method we want people to see.
- **Approved by fingerprint, not by folder.** A file passes once, and its sha256 goes in `approved.tsv`. If it changes, it is checked again. We weighed a copy-into-`approved/` folder: it duplicates files, and the copies drift from what is actually published.
- **AI reads only where needed on commit.** The word check is instant and runs on every staged file. The AI reads cost money and time, so on commit they run only on files the word check flags. `safety check` runs them on everything.
- **Fail closed.** If an AI read errors, the file fails. Being blocked is better than publishing unchecked.
- **One AI call per file covers both reads**, returning structured JSON (`--json-schema`). Settings, tools and MCP servers are turned off so the call is cheap and only sees the file. A picture is read with the Read tool from a throwaway copy, because a staged version may not exist on disk.
- **Repos with no remote are skipped.** They never leave the machine.

## Limits

- The words check finds only words that are on the list.
- The AI reads judge. They can miss things and they can over-flag. The prompt tells them to pass most pieces and to fail only on a line they can quote.
- Video and audio get the hidden-data check only. Their content is not read.
