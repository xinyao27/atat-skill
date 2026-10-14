# AtAt skills

This repository packages AtAt's CLI, Memory, and extension-authoring skills as a plugin for Claude Code and Codex. The local ZIP is only an archive and does not imply eligibility for any external directory.

## Install

The installer lets you choose skills, agents, and scope:

```bash
npx skills add xinyao27/atat-skill
```

Claude Code plugin:

```bash
claude plugin marketplace add xinyao27/atat-skill
claude plugin install atat@atat
```

Codex plugin:

```bash
codex plugin marketplace add xinyao27/atat-skill
codex plugin add atat@atat
```

Sources: atat and atat-memory are maintained in AtAt; atat-extension is maintained in atat-extensions. Generated with pnpm publish:skill.

Manual: https://atatapp.com/manual
