# SRE Agent skills

Skills that teach AI agents how to connect to and use [SRE Agent](https://sreagent.app), published as a
[Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces).

The `sre-agent` plugin carries one skill, `sre-agent`: how to connect the MCP server (endpoint, API keys and
personal tokens, Claude Code, Claude Desktop and other MCP clients), which kind of tool to call for which job,
how deletes and scopes work, how to work a Fix with Claude handoff from brief to report, how plan gates and rate
limits show up, and how to reach the configuration API, inbound webhooks and Terraform export. It is a usage
guide. The full tool list lives in the [MCP reference](https://docs.sreagent.app/api-reference/mcp).

The MCP server and configuration API need the Business or Enterprise plan, and you need an API key or personal access token
from your SRE Agent organization.

## Install in Claude Code

```text
/plugin marketplace add segfaultpw/sre-agent-skills
/plugin install sre-agent@sre-agent-skills
```

The skill loads when a task mentions SRE Agent. Connecting the server itself is one command, with the key kept
in an environment variable:

```bash
claude mcp add --transport http sre-agent https://sreagent.app/api/mcp \
  --header "Authorization: Bearer $SRE_AGENT_API_KEY"
```

## Update

A third-party marketplace does not update in the background by default. To pick up the newest skill, run:

```text
/plugin marketplace update sre-agent-skills
```

or enable auto-update for the marketplace from the `/plugin` menu. Each commit here is a new version, because the
plugin sets no `version`.

## Use it with another agent

The skill is plain Markdown. Copy
[`plugins/sre-agent/skills/sre-agent/SKILL.md`](plugins/sre-agent/skills/sre-agent/SKILL.md) into whatever your
agent reads for instructions (for example an `AGENTS.md`, or a Cursor rule).

## Layout

```text
.claude-plugin/marketplace.json                      the marketplace
plugins/sre-agent/.claude-plugin/plugin.json         the plugin
plugins/sre-agent/skills/sre-agent/SKILL.md          the skill
```

## How it is kept current

The three files under `.claude-plugin/` and `plugins/` are generated. SRE Agent renders them from the server's own
tool catalogue with `mix sre.skill.export`, and a release opens (or updates) one pull request from the
`skill-sync` branch here when anything changed. Edit the template in the SRE Agent source, not those files: a hand
edit is overwritten by the next release. This README and the LICENSE are maintained by hand in this repository.

## Report a problem

Open an issue here for a mistake in the skill's text. For a problem with SRE Agent itself, use the
`submit_feedback` tool or contact support.

## License

MIT, see [LICENSE](LICENSE).
