# rossoctl Agent Skills

Agent Skills for automated maintenance of GitHub organizations. Each skill teaches an AI agent how to perform a specific task using shell scripts and structured instructions.

Built to the [Agent Skills specification](https://agentskills.io/specification).

## Skills

| Skill | Description |
|-------|-------------|
| [repoman](skills/repoman/) | The RepoMan entrypoint — first-time setup, enabling a program, enrolling repos or an org, or running a program across enrolled repos; a single intent-dispatching skill |
| [link-health-scanner](skills/link-health-scanner/) | Scan repos for broken links, create GitHub issues for findings |
| [link-health-fixer](skills/link-health-fixer/) | Re-verify and fix broken links, open PRs for fixes |
| [dep-bump-scanner](skills/dep-bump-scanner/) | Monitor Dependabot PRs, classify by severity, flag SLA breaches |
| [dep-bump-fixer](skills/dep-bump-fixer/) | Analyze stale Dependabot PRs and post commentary to accelerate review |
| [automation-health-dashboard](skills/automation-health-dashboard/) | Generate executive-facing dashboard combining all program metrics |
| [github-weekly-report](skills/github-weekly-report/) | Generate weekly org activity reports with merged PRs, CI health, and active-epic tracking |
| [github-pr-review](skills/github-pr-review/) | Automated PR review: conventions, security, CI status, inline comments |
| [byo-rossoctl-cortex](skills/byo-rossoctl-cortex/) | Bring up a local rossoctl cortex (AuthBridge plugin pipeline) to host an agent; per-agent LiteLLM budget tracking isolated by env var |
| [repo-sync](skills/repo-sync/) | Keep local clones of the enrolled repos current: clone missing ones, fast-forward pull the rest, read-only toward GitHub |
| [hypershift](skills/hypershift/) | Full HyperShift (hosted OpenShift on AWS) cluster lifecycle across 7 skills — setup, preflight, quotas, create/destroy, debug, TTL-based cleanup; also needs `aws`, `oc`, `ansible` |

## Installation

### Claude Code (plugin marketplace)

```
/plugin marketplace add rossoctl/agent-skills
/plugin install <plugin-name>@rossoctl-agent-skills
```

Install one plugin at a time. Replace `<plugin-name>` with a plugin name such as
`repoman`, `link-health`, `dep-bump`, `pr-review`, `automation-health`, or
`repo-sync`. Plugin names are the ones declared in the marketplace, which can
differ from the per-skill directory names in the [Skills](#skills) table. For
example, the `link-health` plugin bundles the `link-health-scanner` and
`link-health-fixer` skills. Run `/plugin` after adding the marketplace to browse
the authoritative list. Installing one plugin does **not** pull in the others,
so repeat the `install` line per plugin you want.

### Updating

To pick up new changes after they land upstream, refresh the marketplace and
update any installed plugins (a Claude Code restart applies plugin updates):

```
/plugin marketplace update rossoctl-agent-skills
/plugin update <plugin-name>@rossoctl-agent-skills
```

### Manual

Copy the desired skill directory into your project's `.claude/skills/` directory:

```bash
cp -r skills/link-health-scanner /path/to/project/.claude/skills/
```

## Prerequisites

All skills in this repo require:

- `bash` 4+
- `gh` (GitHub CLI, authenticated)
- `jq`

Individual skills may have additional requirements documented in their `SKILL.md`.

## License

Apache-2.0. See [LICENSE](LICENSE).
