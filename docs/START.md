# Start here

**What it is:** one Python script, `safety`, that checks files before they are published. See [README](../README.md).

**Layout**
- `safety`: the whole tool (words, hidden data, AI reads, git hook, log)
- `prompts/read.md`: what the AI readers are told. Edit this to change what gets flagged.
- `test`: proves it works in a throwaway folder with made-up words
- `run`: `run setup`, `run test`, or `run check PATH`
- `docs/`: this page, [SPEC](SPEC.md), [HOW-WE-CHECK](HOW-WE-CHECK.md), [CHANGELOG](CHANGELOG.md)

**Set up:** `./run setup`, then put your words in `~/.config/safety/terms.txt`.

**First change:** edit `prompts/read.md` or `safety`, run `./run test` (and `./run test --ai` if you touched the AI reads), then commit.

Nothing private goes in this repo. Words, context, the log and the approved list live in `$SAFETY_CONFIG`.
