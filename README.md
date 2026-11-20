# github-core-clone-01

A standalone, GitHub-compatible git forge in one Node 22 process, stdlib only
(`node:http`, `node:zlib`, `node:crypto` — no dependencies, no internet, no git
binary). It serves, from a single in-memory store:

- git smart HTTP: protocol v2 `ls-refs`/`fetch` and v0 `receive-pack`, packfile
  read/write (full objects, OFS/REF delta resolution), pkt-line and sideband
  framing, shallow fetch and deepen;
- REST v3: repositories, branches, commits, contents, issues, comments, labels,
  pull requests, files and squash merges;
- GraphQL v4: the documents `gh` and `github-mcp-server` send, plus
  introspection, `node(id:)` and operation batching;
- MCP over streamable HTTP: `server/discover`, `initialize`, `tools/list`,
  `tools/call` for six tools, JSON-RPC 2.0 errors.

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
