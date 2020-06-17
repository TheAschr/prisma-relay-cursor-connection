<!-- Title -->
<h1 align="center">
  prisma-relay-cursor-connection
</h1>

<!-- Description -->
<h4 align="center">
  Extend <a href="https://www.prisma.io/">Prisma's</a> <code>findMany</code> method to support <a href="https://relay.dev/graphql/connections.htm">Relay Cursor Connections</a>
</h4>

<!-- Badges -->
<p align="center">
  <a href="https://www.npmjs.com/package/@devoxa/prisma-relay-cursor-connection">
    <img
      src="https://img.shields.io/npm/v/@devoxa/prisma-relay-cursor-connection?style=flat-square"
      alt="Package Version"
    />
  </a>

  <a href="https://app.circleci.com/pipelines/github/devoxa/prisma-relay-cursor-connection?branch=master">
    <img
      src="https://img.shields.io/circleci/build/github/devoxa/prisma-relay-cursor-connection/master?style=flat-square"
      alt="Build Status"
    />
  </a>

  <a href="https://codecov.io/github/devoxa/prisma-relay-cursor-connection">
    <img
      src="https://img.shields.io/codecov/c/github/devoxa/prisma-relay-cursor-connection/master?style=flat-square"
      alt="Code Coverage"
    />
  </a>
</p>

<!-- Quicklinks -->
<p align="center">
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#contributors">Contributors</a> •
  <a href="#license">License</a>
</p>

<br>

## Installation

```bash
yarn add @devoxa/prisma-relay-cursor-connection
```

This module has a peer dependency on `@prisma/client@^2.0.0`.

## Usage

```ts
import { findManyCursorConnection, ConnectionArguments } from '@devoxa/prisma-relay-cursor-connection'

const result = await findManyCursorConnection(
  (args) => client.todo.findMany(args),
  () => client.todo.count(),

  // Relay Cursor Connection Arguments (one of [first] | [first, after] | [last] | [last, before])
  // Type: ConnectionArguments
  { first: 5, after: '5c11e0fa-fd6b-44ee-9016-0809ee2f2b9a' }
)
```

You can also use additional `FindManyArgs` while keeping type safety intact:

```ts
import { findManyCursorConnection } from '@devoxa/prisma-relay-cursor-connection'

const baseArgs = {
  select: { id: true, isCompleted: true },
  where: { isCompleted: true },
}

const result = await findManyCursorConnection(
  (args) => client.todo.findMany({ ...args, ...baseArgs }),
  () => client.todo.count(baseArgs),
  { first: 5, after: '5c11e0fa-fd6b-44ee-9016-0809ee2f2b9a' }
)

// Type error: Property text does not exist
result.edges[0].node.text
```

## Contributing

```bash
# Setup the test database
yarn prisma migrate up --experimental
yarn prisma generate

# Run the tests
yarn test
```

## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://www.david-reess.de"><img src="https://avatars3.githubusercontent.com/u/4615516?v=4" width="75px;" alt=""/><br /><sub><b>David Reeß</b></sub></a><br /><a href="https://github.com/devoxa/prisma-relay-cursor-connection/commits?author=queicherius" title="Code">💻</a> <a href="https://github.com/devoxa/prisma-relay-cursor-connection/commits?author=queicherius" title="Documentation">📖</a> <a href="https://github.com/devoxa/prisma-relay-cursor-connection/commits?author=queicherius" title="Tests">⚠️</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors)
specification. Contributions of any kind welcome!

## License

MIT
