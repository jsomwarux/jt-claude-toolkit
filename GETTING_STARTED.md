# Getting Started: JT Claude Toolkit

This guide takes you from "I downloaded a zip" to "I use this every day." Follow the parts in
order the first time. After that, Part 5 is the part you live in.

The whole point: stop re-tuning a giant CLAUDE.md in every repo. The reusable how-to now
lives in skills and agents that install once and work everywhere. Each project's CLAUDE.md or
AGENTS.md stays thin and only holds facts about that one project.

---

## Part 0: Before you start (check these once)

You need:
- Claude Code installed and on the latest version. If `/plugin` does not exist when you type
  it, update Claude Code first.
- `git` installed, and a GitHub account. (Your handle looks like `jsomwarux` based on your
  existing repos. Confirm yours, you will use it below.)
- Python 3 available (the proposal skill installs `weasyprint` itself the first time).

How to know you are ready: open a terminal, run `claude --version` and `git --version`. Both
print a number.

---

## Part 1: Put it on your machine and in GitHub (one time, about 10 minutes)

**Step 1.1.** Unzip the toolkit somewhere permanent, for example your code folder:
```bash
cd ~/code
unzip ~/Downloads/jt-claude-toolkit.zip
cd jt-claude-toolkit
```

**Step 1.2.** Turn it into a git repo:
```bash
git init
git add -A
git commit -m "Initial toolkit"
```

**Step 1.3.** Create an empty repo on GitHub named `jt-claude-toolkit`, then push. Replace
`jsomwarux` with your real handle if different:
```bash
git remote add origin https://github.com/jsomwarux/jt-claude-toolkit.git
git branch -M main
git push -u origin main
```

**Step 1.4 (optional).** If your GitHub handle is not `jtsomwaru`, open
`consulting-toolkit/.claude-plugin/plugin.json` and `product-builder/.claude-plugin/plugin.json`
and fix the `repository` line to your real handle. This field is only for attribution, so it
does not break anything if you skip it. Commit and push again if you change it.

How to know it worked: your repo shows up at `github.com/<your-handle>/jt-claude-toolkit`.

---

## Part 2: Install it into Claude Code (one time per computer, about 3 minutes)

**Step 2.1.** Validate the toolkit first (catches typos before install):
```bash
claude plugin validate .
```
It should report no errors.

**Step 2.2.** Start Claude Code in any folder and add the marketplace. For your own machine,
the GitHub form is best because it auto-updates later:
```
/plugin marketplace add jsomwarux/jt-claude-toolkit
```
(If you have not pushed yet, you can test locally instead with
`/plugin marketplace add ~/code/jt-claude-toolkit`.)

**Step 2.3.** Install both plugins:
```
/plugin install consulting-toolkit@jt-toolkit
/plugin install product-builder@jt-toolkit
```

**Step 2.4.** Reload so they load right now without restarting:
```
/reload-plugins
```

How to know it worked: type `/plugin` and you see both plugins listed and enabled.

Note: plugins install at the user level, so once installed they are available in every folder
you open Claude Code in. You do not reinstall per project.

---

## Part 3: Confirm every piece works (smoke test, about 5 minutes)

**Step 3.1.** See the agents are loaded:
```
/agents
```
You should see `workflow-strategist`, `n8n-builder`, and `quality-pass`.

**Step 3.2.** Test an auto-skill. In a chat, type a normal request, no slash:
```
Research a mid-size NYC residential property manager and rank the top automation opportunities.
```
The `opportunity-research` skill should kick in and return a ranked list.

**Step 3.3.** Test a user-skill (these only fire when you call them by name):
```
/consulting-toolkit:new-client Aya Property Group
```
It should scaffold a `clients/aya-property-group/` folder and run research into `brief.md`.

**Step 3.4.** Test the proposal skill:
```
Make a proposal PDF for that client with two use cases and a total.
```
The first run installs weasyprint, then produces a branded PDF. Open it and confirm the blue
accent line and right-aligned prices look right.

How to know it worked: each step produced what it promised. If an auto-skill did not trigger,
phrase the request a bit more specifically; if it still does not, that skill's description may
need tightening (see Part 6).

---

## Part 4: Wire it into your real projects (this is the high-payoff step)

The plugins are global. The only per-project work is dropping in the right thin template and
deleting any old generic methodology you were carrying in that project's CLAUDE.md.

**Step 4.1. Make one home for client work.** Create a single folder where all client
engagements live and where you run Claude Code for consulting:
```bash
mkdir -p ~/code/consulting && cd ~/code/consulting
git init && mkdir clients
```
From now on, run `/consulting-toolkit:new-client ...` from inside this folder so the
`clients/<name>/` folders all land here.

**Step 4.2. Altmark (do this first, fastest return).** Copy the client template into your
Altmark repo and fill the blanks (most are already filled with your real Beelink details):
```bash
cp ~/code/jt-claude-toolkit/templates/client-CLAUDE.md /path/to/altmark/CLAUDE.md
```
Then open it and delete anything that is generic how-to (how to write a proposal, how to design
a workflow). That knowledge now lives in the skills. Keep only Altmark facts: infra, paths,
Sheet IDs, credentials references, open items.

**Step 4.3. Action Arena (and any repo Codex and Claude Code both touch).** Use AGENTS.md so
both tools read one file:
```bash
cp ~/code/jt-claude-toolkit/templates/app-AGENTS.md /path/to/action-arena/AGENTS.md
cd /path/to/action-arena
ln -s AGENTS.md CLAUDE.md
```
The symlink means Claude Code (which looks for CLAUDE.md) and Codex (which looks for AGENTS.md)
see the exact same content. Fill in the real stack, scripts, and quality gates.

**Step 4.4. Nash Satoshi and Glow Index.** Drop the ensemble guide into each ensemble repo:
```bash
cp ~/code/jt-claude-toolkit/templates/ensemble-CLAUDE.md /path/to/nash-satoshi/CLAUDE.md
```
Fill in the exact request fields, model dict shape, and callback payload from the real code.

**Step 4.5. Decide where the format-on-save hook should run.** `product-builder` ships a hook
that runs prettier on files you edit. It is fail-safe (it does nothing in repos without
prettier), but if you do not want it firing in your consulting folder, open `/plugin`, select
`product-builder`, and disable it for that project. Leave it on in your app repos.

How to know it worked: open Claude Code in your Altmark repo and ask "what infra constraints
apply here?" It should answer from your thin CLAUDE.md without you re-explaining.

---

## Part 5: Daily-driver workflows (the part you actually use)

### A. Land a new client
1. `cd ~/code/consulting`
2. `/consulting-toolkit:new-client <Company name or website>`
3. Review the ranked opportunities it wrote into `clients/<slug>/brief.md`.
4. Ask: "Draft a proposal PDF for the top three." (proposal skill runs.)
5. Send the PDF. Done.

### B. Build a workflow for a client
1. From `~/code/consulting`, run `/consulting-toolkit:build-workflow <slug> <workflow-name>`.
2. The `workflow-strategist` agent designs the full node-by-node blueprint.
3. Review it, then it produces a child-simple playbook with the exact prompts for your n8n
   builder agent.
4. Hand those prompts to your n8n builder, or invoke the `n8n-builder` agent to implement.
5. Test with the sample payloads in the blueprint before touching real client data.

### C. Send a proposal on its own
Just ask in plain language: "Proposal for <client>: <use case> at <price>, <use case> at
<price>, monthly support <price>." The `proposal-pdf` skill builds the branded PDF.

### D. Tailor your resume for a role
1. Open Claude Code anywhere.
2. "Tailor my resume for this role:" then paste the job description.
3. The `resume-tailor` skill produces a two-page docx with clients anonymized, consultant
   framing, no stray em dashes. Review and send.

### E. Build or ship a product feature
1. In the app repo: "Build <feature>." The `build-phases` skill drives plan, implement, test,
   LARP check, slop cleanup, and production validation.
2. When ready: `/product-builder:ship "<commit message or PR title>"`. The `quality-pass`
   agent runs a real verification, then it commits, pushes, and opens a PR.

---

## Part 6: Keep it sharp (the flywheel that compounds)

This is your core habit, now made mechanical:

1. **Promote, do not repeat.** Any time you catch yourself explaining the same how-to in a
   project's CLAUDE.md a second time, that is the signal to move it into a skill here instead.
   Add a folder under the right plugin's `skills/`, write a `SKILL.md`, commit, push.
2. **Tighten triggers.** If an auto-skill fires when you did not want it, or fails to fire when
   you did, edit its `description` line (the first lines of its `SKILL.md`). The description is
   the only thing that controls triggering. Make it more specific or a bit more insistent.
3. **Bump and propagate.** When you change a plugin, raise its `version` in `plugin.json`, then
   `git commit` and `git push`. On any machine, run `/plugin marketplace update jt-toolkit`
   then `/reload-plugins` to pull the new version.
4. **Guard quality with CI.** Add a GitHub Action that runs `claude plugin validate .` on every
   push so a broken manifest never reaches your other machines.

---

## Quick reference (the commands you will actually type)

```
/plugin marketplace add jsomwarux/jt-claude-toolkit   # one time per machine
/plugin install consulting-toolkit@jt-toolkit
/plugin install product-builder@jt-toolkit
/reload-plugins

/consulting-toolkit:new-client <company>              # scaffold + research
/consulting-toolkit:build-workflow <slug> <workflow>  # blueprint + playbook
/product-builder:ship "<message>"                     # quality pass + commit + PR

/agents        # see your agents
/plugin        # enable, disable, browse
```

Auto-skills (no slash, just ask): proposal-pdf, opportunity-research, n8n-blueprint,
build-playbook, resume-tailor, build-phases.
