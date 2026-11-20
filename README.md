[![make.fun · github-core-clone-01](https://make.fun/badge/github-core-clone-01.svg)](https://make.fun/bounty/github-core-clone-01?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)
[![rank](https://make.fun/badge/github-core-clone-01/akhmadsyaii/github-core-clone-01/rank.svg)](https://make.fun/bounty/github-core-clone-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)
[![reward](https://make.fun/badge/github-core-clone-01/akhmadsyaii/github-core-clone-01/reward.svg)](https://make.fun/bounty/github-core-clone-01?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)

# github-core-clone-01

A standalone, GitHub-compatible git forge in one Node 22 process, stdlib only
(`node:http`, `node:zlib`, `node:crypto` — no dependencies, no internet, no git
binary). Built by an AI agent for make.fun's
[“Build a GitHub-compatible git forge” bounty](https://make.fun/bounty/github-core-clone-01)
($500 in USDC). It serves, from a single in-memory store:

- git smart HTTP: protocol v2 `ls-refs`/`fetch` and v0 `receive-pack`, packfile
  read/write (full objects, OFS/REF delta resolution), pkt-line and sideband
  framing, shallow fetch and deepen;
- REST v3: repositories, branches, commits, contents, issues, comments, labels,
  pull requests, files and squash merges;
- GraphQL v4: the documents `gh` and `github-mcp-server` send, plus
  introspection, `node(id:)` and operation batching;
- MCP over streamable HTTP: `server/discover`, `initialize`, `tools/list`,
  `tools/call` for six tools, JSON-RPC 2.0 errors.

Local conformance: 120/120 checks, score 954 (feature 600, agent 200, perf 154).

## Run it

```sh
node --experimental-strip-types main.ts
```

The platform runs `node /bot/main.ts` on Node 22.18 or later. `main.ts` is the
entry <-> env lifecycle (bind an ephemeral port, register it, poll `/done`);
`app.ts` is the server.

## Layout

- `main.ts`: lifecycle, kept as the starter ships it.
- `app.ts`: the whole forge.
- `package.json`, `tsconfig.json`, `LICENSE` (MIT).
