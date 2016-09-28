
# hypercore-index

Linear asynchronous stateful indexing of a
[hypercore](https://github.com/mafintosh/hypercore) feed.

[![build status](https://travis-ci.org/juliangruber/hypercore-index.svg?branch=master)](http://travis-ci.org/juliangruber/hypercore-index)

Traverses a hypercore feed in chronologic order and lets you consume each
entry via some asynchronous function. Remembers where you left inside the
feed's db and continues there on later runs.

## Example

```js
const hypercore = require('hypercore')
const index = require('hypercore-index')

const core = hypercore(db)
const feed = core.createFeed()

index({
  feed: feed,
  db: db
}, function onentry (entry, next) {
  console.log('entry', entry.toString())
  next()
}, function ondone (err) {
  if (err) throw err
  console.log('Done!')
})
```

## Installation

```bash
$ npm install hypercore-index
```

## API

### index(opts, onentry, [ondone])

Options:

- `feed`: The hypercore feed. Required.
- `db`: A level db. Required.
- `start`: The first index. Default: `0`
- `end`: The last index. Default: `Infinity`
- `live`: Whether to keep scanning. Default: `true`, unless you pass `opts.end`

## license

MIT
