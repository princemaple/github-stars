---
project: mande
stars: 1207
description: <700 bytes convenient and modern wrapper around fetch with smart extensible defaults
---

mande
=====

> Simple, light and extensible wrapper around fetch with smart defaults

**Requires `fetch` support.**

_mande_ has better defaults to communicate with APIs using `fetch`, so instead of writing:

// creating a new user
fetch('/api/users', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'Dio',
    password: 'irejectmyhumanityjojo',
  }),
})
  .then((response) \=> {
    if (response.status \>= 200 && response.status < 300) {
      return response.json()
    }
    // reject if the response is not 2xx
    throw new Error(response.statusText)
  })
  .then((user) \=> {
    // ...
  })

You can write:

const users \= mande('/api/users')

users
  .post({
    name: 'Dio',
    password: 'irejectmyhumanityjojo',
  })
  .then((user) \=> {
    // ...
  })

Installation
------------

npm install mande
yarn add mande

Usage
-----

Creating a small layer to communicate to your API:

// api/users
import { mande } from 'mande'

const users \= mande('/api/users', usersApiOptions)

export function getUserById(id) {
  return users.get(id)
}

export function createUser(userData) {
  return users.post(userData)
}

Adding _Authorization_ tokens:

// api/users
import { mande } from 'mande'

const todos \= mande('/api/todos', todosApiOptions)

export function setToken(token) {
  // todos.options will be used for all requests
  todos.options.headers.Authorization \= 'Bearer ' + token
}

export function clearToken() {
  delete todos.options.headers.Authorization
}

export function createTodo(todoData) {
  return todo.post(todoData)
}

// In a different file, setting the token whenever the login status changes. This depends on your frontend code, for instance, some libraries like Firebase provide this kind of callback but you could use a watcher on Vue.
onAuthChange((user) \=> {
  if (user) setToken(user.token)
  else clearToken()
})

You can also globally add default options to all _mande_ instances:

import { defaults } from 'mande'

defaults.headers.Authorization \= 'Bearer token'

To delete a header, pass `null` to the mande instance or the request:

const legacy \= mande('/api/v1/data', {
  headers: {
    // override all requests
    'Content-Type': 'application/xml',
  },
})

// override only this request
legacy.post(new FormData(), {
  headers: {
    // overrides Accept: 'application/json' only for this request
    Accept: null,
    'Content-Type': null,
  },
})

TypeScript
----------

All methods defined on a `mande` instance accept a type generic to type their return:

const todos \= mande('/api/todos', globalOptions)

todos
  .get<{ text: string; id: number; isFinished: boolean }\[\]\>()
  .then((todos) \=> {
    // todos is correctly typed
  })

SSR (and Nuxt in Universal mode)
--------------------------------

To make Mande work on Server, make sure to provide a `fetch` polyfill and to use full URLs and not absolute URLs starting with `/`. For example, using `node-fetch`, you can do:

export const BASE\_URL \= process.server
  ? process.env.NODE\_ENV !== 'production'
    ? 'http://localhost:3000'
    : 'https://example.com'
  : // on client, do not add the domain, so urls end up like \`/api/something\`
    ''

const fetchPolyfill \= process.server ? require('node-fetch') : fetch
const contents \= mande(BASE\_URL + '/api', {}, fetchPolyfill)

### Nuxt 2

Note: If you are doing SSR with authentication, Nuxt 3 hasn't been adapted yet. See #308.

When using with Nuxt **and SSR**, you must wrap exported functions so they automatically proxy cookies and headers on the server:

import { mande, nuxtWrap } from 'mande'
const fetchPolyfill \= process.server ? require('node-fetch') : fetch
const users \= mande(BASE\_URL + '/api/users', {}, fetchPolyfill)

export const getUserById \= nuxtWrap(users, (api, id: string) \=> api.get(id))

Make sure to add it as a buildModule as well:

// nuxt.config.js
module.exports \= {
  buildModules: \['mande/nuxt'\],
}

This prevents requests from accidentally sharing headers or bearer tokens.

#### TypeScript

Make sure to include `mande/nuxt` in your `tsconfig.json`:

{
  "types": \["@types/node", "@nuxt/types", "mande/nuxt"\]
}

API
---

Most of the code can be discovered through the autocompletion but the API documentation is available at https://mande.esm.is

### Cookbook

#### Timeout

You can timeout requests by using the native `AbortSignal`:

mande('/api').get('/users', { signal: AbortSignal.timeout(2000) })

This is supported by all modern browsers.

#### `FormData`

When passing Form Data, mande automatically removes the `Content-Type` header but you can manually set it if needed:

// directly pass it to the mande instance
const api \= mande('/api/', { headers: { 'Content-Type': null } })
// or when creating the request
const formData \= new FormData()
api.post(formData, {
  headers: { 'Content-Type': 'multipart/form-data' },
})

Most of the time you should let the browser set it for you.

Related
-------

-   fetchival: part of the code was borrowed from it and the api is very similar
-   axios:

License
-------

MIT