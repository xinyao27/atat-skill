# Publish AtAt skills and plugin

Generated from maintained AtAt and atat-extensions sources by pnpm publish:skill. The local ZIP is an archive only; confirm external directory eligibility with its operator.

Install with npx skills add xinyao27/atat-skill. Generate with pnpm publish:skill. The extension source defaults to ~/work/atat-extensions; set ATAT_EXTENSIONS_REPO to another verified checkout root when needed.

Validate with claude plugin validate --strict ~/work/atat-skill, then install it from a temporary CLAUDE_CONFIG_DIR and CODEX_HOME as the release-atat skill describes. The plugin version is the app's MARKETING_VERSION, so publish once per release.
