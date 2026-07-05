# john-skills

A personal Claude Code plugin marketplace bundling all of John's skills into one
installable package, so the exact same skill set is available on **every machine
and account** — and can be shared with teammates.

`~/.claude/skills/` is machine-local and does not sync anywhere. Packaging the
skills as a plugin published through this marketplace (a git repo) is the
supported way to make them portable across devices/accounts and shareable with a
team.

## What's inside

One plugin, `john-skills`, whose `skills/` directory holds every skill (see
`skills/`). Skills invoke under the plugin namespace, e.g. `/john-skills:triage`,
`/john-skills:tdd`, `/john-skills:ask-matt`.

## Publish (once)

```bash
cd ~/claude-skills-marketplace
git remote add origin git@github.com:<your-org-or-user>/john-skills.git
git push -u origin master
```

## Install on any machine / account (once per device)

```bash
/plugin marketplace add <your-org-or-user>/john-skills
/plugin install john-skills@john-skills
```

## Update after adding/changing a skill

```bash
# author side
git add skills/ && git commit -m "…" && git push
# every other device
/plugin marketplace update john-skills
/reload-plugins
```

## Adding a skill that currently lives only on your web/team account (e.g. Deslop)

Export or copy the skill's folder (must contain `SKILL.md`) into `skills/`,
then commit and push:

```bash
cp -r /path/to/deslop ~/claude-skills-marketplace/skills/deslop
git add skills/deslop && git commit -m "Add deslop" && git push
```
