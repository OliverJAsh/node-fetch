
node-fetch-task
==========

[`node-fetch`](https://github.com/bitinn/node-fetch) fork, implemented using the [`Task`
type](https://github.com/rpominov/fun-task), which [allows cancellation amongst
other things](https://github.com/rpominov/fun-task#what-is-a-task).

Currently WIP.

Also see the [browser version of `fetch` implemented via `Task`](https://github.com/OliverJAsh/fun-task-fetch).

## Example

``` js
const cancellableFetch = require('./lib/index');

const url = 'https://jsonplaceholder.typicode.com/posts'
const task = cancellableFetch(url, { method: 'GET' })

const cancel = task
    .chain(response => response.json())
    .run({
        success(result) {
            console.log('success', { result })
        },
        failure(result) {
            console.log('failure', { result })
        }
    })

setTimeout(cancel, 100)
```
