# rekcod

> docker inspect -> docker run

A simple module to reverse engineer a `docker run` command from a `docker inspect` command. Just pass in the container names or ids that you want to reverse engineer.

This is not super robust, but it should hopefully cover most arguments needed.

This module calls `docker inspect` directly, and the user running it should be able to as well.

## Install and Usage

### CLI

```
npm i -g rekcod
```

```sh
# single container
rekcod container-name
# multiple containers
rekcod another-name 6653931e39f2 happy_torvalds
```

### Module

```
npm i --save rekcod
```

```js
const rekcod = require('rekcod')
// single container
rekcod('container-name', (err, run) => {
  if (err) return console.error(err)
  console.log(run[0].command)
})
// multiple containers
rekcod(['another-name', '6653931e39f2', 'happy_torvalds'], (err, run) => {
  if (err) return console.error(err)
  run.forEach((r) => {
    console.log('\n', r.command)
  })
})
```
