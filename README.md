# Proof of concept for [redwoodjs/redwood#279](https://github.com/redwoodjs/redwood/issues/279)

We've been experiencing an issue when attempting to update Prisma to `preview024` in Redwood. This repository serves to be a minimum replication case for this issue.

## Getting Started
- Clone the repo
- Run `yarn install` from the root of the repo
- Run `yarn rw dev`, and you'll see the issue.

## How did we build the PoC?

1. First, I followed [the Redwood tutorial](https://redwoodjs.com/tutorial/installation-starting-development), and used `yarn create redwood-app` to create a basic application. I tested this with `yarn rw dev` and it loaded properly.

2. Next, I manually installed `preview024` in the repo, by using the following command:

```sh
yarn add --ignore-workspace-root-check --dev prisma2@2.0.0-preview024 @prisma/client@2.0.0-preview024
```

This added the correct versions of `prisma2` and `@prisma/client` to the repo, as development dependencies. After running `yarn rw dev`, the error appears:

```
PS C:\Users\weave\Documents\redwood-279-poc> yarn rw dev
yarn run v1.22.4
$ C:\Users\weave\Documents\redwood-279-poc\node_modules\.bin\rw dev
  √ Generating the Prisma client...
$ C:\Users\weave\Documents\redwood-279-poc\node_modules\.bin\webpack-dev-server --config ../node_modules/@redwoodjs/core/config/webpack.development.js
$ C:\Users\weave\Documents\redwood-279-poc\node_modules\.bin\prisma2 generate --watch
$ C:\Users\weave\Documents\redwood-279-poc\node_modules\.bin\dev-server
12:37:16 api | C:\Users\weave\Documents\redwood-279-poc\node_modules\@redwoodjs\api\node_modules\@prisma\client\index.js:3
12:37:16 api |     throw new Error(
12:37:16 api |     ^
12:37:16 api |
12:37:16 api | Error: @prisma/client did not initialize yet. Please run "prisma2 generate" and try to import it again.
12:37:16 api | In case this error is unexpected for you, please report it in https://github.com/prisma/prisma-client-js/issues/390.
12:37:16 api |     at new PrismaClient (C:\Users\weave\Documents\redwood-279-poc\node_modules\@redwoodjs\api\node_modules\@prisma\client\index.js:3:11)
12:37:16 api |     at Object.<anonymous> (C:\Users\weave\Documents\redwood-279-poc\node_modules\@redwoodjs\api\src\dbInstance.ts:3:19)
12:37:16 api |     at Module._compile (internal/modules/cjs/loader.js:1158:30)
12:37:16 api |     at Module._compile (C:\Users\weave\Documents\redwood-279-poc\node_modules\pirates\lib\index.js:99:24)
12:37:16 api |     at Module._extensions..js (internal/modules/cjs/loader.js:1178:10)
12:37:16 api |     at Object.newLoader [as .js] (C:\Users\weave\Documents\redwood-279-poc\node_modules\pirates\lib\index.js:104:7)
12:37:16 api |     at Module.load (internal/modules/cjs/loader.js:1002:32)
12:37:16 api |     at Function.Module._load (internal/modules/cjs/loader.js:901:14)
12:37:16 api |     at Module.require (internal/modules/cjs/loader.js:1044:19)
12:37:16 api |     at require (internal/modules/cjs/helpers.js:77:18)
12:37:19  db |
12:37:19  db | Watching... C:\Users\weave\Documents\redwood-279-poc\api\prisma\schema.prisma
12:37:19  db |
12:37:20 web | i ｢wds｣: Project is running at http://localhost:8910/
12:37:20 web | i ｢wds｣: webpack output is served from /
12:37:20 web | i ｢wds｣: Content not from webpack is served from C:\Users\weave\Documents\redwood-279-poc\web
12:37:20 web | i ｢wds｣: 404s will fallback to /index.html
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```