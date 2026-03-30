# Territory Wars

Multiplayer territory game built with [Yjs](https://yjs.dev) CRDTs on [Durable Streams](https://electric-sql.com/primitives/durable-streams). Players claim cells by moving over them. Each cell is a Yjs CRDT entry — last-writer-wins resolves contention. Encircle an area to fill it. First to 50% wins.

Built with React, TypeScript, and [Electric Cloud](https://electric-sql.com/cloud).

## Setup

1. Sign up at [Electric Cloud](https://dashboard.electric-sql.com)
2. Create a **Yjs** service and a **Durable Streams** service
3. Copy `.env.example` to `.env` and fill in your service URLs and tokens:

```sh
cp .env.example .env
```

4. Install and run:

```sh
npm install
npm run dev
```

## How it works

- **Cells** are stored in a [Yjs Y.Map](https://docs.yjs.dev/api/shared-types/y.map) — each key is a grid coordinate, each value records the owner. When two players claim the same cell, Yjs LWW resolves the conflict.
- **Territory fill** — when your cells form a closed boundary around empty space, the enclosed area is automatically claimed.
- **Room registry** and **presence** use [StreamDB](https://electric-sql.com/docs/api/durable-streams/stream-db) on Durable Streams.
- **No WebSockets** — all sync happens over plain HTTP via the [Yjs Durable Streams Protocol](https://github.com/durable-streams/durable-streams/blob/main/packages/y-durable-streams/YJS-PROTOCOL.md).

## Controls

- **Keyboard**: arrow keys or WASD
- **Mouse**: click on the board to move toward the click
- **Touch**: tap or swipe on the board

## License

MIT
