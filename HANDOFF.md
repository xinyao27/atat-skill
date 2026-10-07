# Publish the AtAt plugin & skills

Everything in this directory is generated from the AtAt repository by
`pnpm publish:skill`. Nothing has been pushed anywhere — the steps below are yours, because
they need your GitHub account, your Claude plan, and your OpenAI developer account.

## 0. What is here

| Directory / File | Target | State |
| --- | --- | --- |
| `atat-skill/` | GitHub public repo `xinyao27/atat-skill` | ready to push |
| `atat-plugin.zip` | OpenAI Plugin Directory submission | ready to upload |

One repository serves Claude Code, ChatGPT, Codex, and Cursor:

- two **skills** — the AtAt command skill at `SKILL.md` and `skills/atat/SKILL.md`, plus the
  Memory skill at `skills/atat-memory/SKILL.md`; both are copied from `apps/AtAt/Resources/Skills/`;
- a **plugin** — `.claude-plugin/plugin.json`;
- a **marketplace** — `.claude-plugin/marketplace.json`, whose one plugin is the repository
  root itself (`source: "./"`).

The shape passes Claude Code strict validation (`claude plugin validate --strict`) and
conforms to OpenAI's Agent Plugins 1.0.0 specification for Skills-Only plugins.

---

## 1. Push the repository to GitHub

```bash
cd ~/work/atat-skill
git init -b main
git add -A && git commit -m "feat: release AtAt plugin and skills"
gh repo create xinyao27/atat-skill --public --source . --push
```

You can check it locally before or after creating the remote repo:

```bash
claude plugin validate --strict ~/work/atat-skill
claude plugin marketplace add ~/work/atat-skill
claude plugin install atat@atat
claude plugin list                     # atat@atat, Status: ✔ enabled
claude plugin details atat@atat      # Skills (2): atat, atat-memory
```

---

## 2. Submit to Claude Directory (Anthropic)

1. Run the local validator:
   ```bash
   claude plugin validate --strict ~/work/atat-skill
   ```
2. Open https://claude.ai/directory/manage
3. Click **Submit new → Plugin bundle**
4. Fill in the form:
   - **Repository**: `xinyao27/atat-skill`
   - **Plugin path**: `.` (root of repository)
   - **Data Access & Privacy**: Declare that the plugin touches user screen content (Screen Recording) and Clipboard History.
   - **Documentation URL**: https://atatapp.com/manual
5. Submit for review. Anthropic reviews the listing and pins the release to your published commit.

---

## 3. Submit to OpenAI Plugin Directory (ChatGPT & Codex)

OpenAI's universal Plugin Directory accepts Skills-Only plugins packaged as a ZIP:

1. Confirm your OpenAI developer account:
   - Log in at https://developers.openai.com/plugins
   - Verify you have **Apps Management Write** permissions in your organization.
   - Ensure your personal or organization developer identity verification is complete.
2. Create the draft:
   - Go to **Plugins** → **Upload new or existing plugin**.
   - Select your **Verified Developer Identity**.
   - Choose **Skills only** (do NOT choose With MCP, since this plugin delegates directly to the local macOS companion CLI).
   - Upload `~/work/atat-skill/atat-plugin.zip`.
3. Review automated checks:
   - The portal runs automated checks and automatically parses `.claude-plugin/plugin.json` and `skills/`.
   - Verify all checks in **Metadata & Skills** turn green.
4. Fill submission details:
   - **Display Name**: AtAt
   - **Homepage / Docs**: https://atatapp.com/manual
   - **Privacy Policy**: https://atatapp.com
   - **Terms of Service**: https://atatapp.com
5. Submit for review:
   - Note: Skills-only plugins do NOT require demo videos or test case matrices.
   - Click **Submit for review**.

---

## 4. End-to-End User Experience Verification

Once published, test what happens for a fresh user who does NOT have AtAt installed:

1. In Claude Code: `claude plugin install atat@atat`
2. Ask: "Capture my active window and inspect it"
3. The skill instructions detect that `atat` is missing, politely ask the user for permission,
   and install the companion app:
   `brew install --cask xinyao27/tap/atat`
4. Once installed, it runs `open -a AtAt` to guide macOS permissions (Screen Recording and Accessibility),
   verifies `atat status`, and fulfills the user's initial request.
