---
project: clooney
stars: 1422
description: Clooney is an actor library for the web. Use workers without thinking about workers.
url: https://github.com/GoogleChromeLabs/clooney
---

Clooney
=======

Clooney is an actor (ayooo) library for the web. Classes given to Clooney will be instantiated and run in a worker, keeping the main thread responsive.

> ⚠️ **Caveat:** The class cannot rely on its surrounding scope, since it is executed in an isolated context. This might change once workers support ES6 modules.

Quickstart
----------

An example says more than 1000 words:

<script src\="/clooney.bundle.js"\></script\>
<script\>
  (async function() {
    class MyRemoteClass {
      doExpensiveCalculation(a, b) {
        return a + b;
      }
    }

    const instance \= await Clooney.spawn(MyRemoteClass);
    console.log(await instance.doExpensiveCalculation(5, 23));
  })();
</script\>

I’m collecting more examples of Clooney in action in this Glitch.

Browser support
---------------

Clooney uses Comlink under the hood, and so inherits its browser compatibility matrix.

Browsers without ES6 Proxy support can use the proxy-polyfill.

Events and Functions
--------------------

Functions and events are not transferable (i.e. can’t be sent from to a worker), but Clooney has special handling for them:

class MyRemoteClass {
  onClick(remoteEvent) {
    // … react to click …
  }
}

const instance \= await Clooney.spawn(MyRemoteClass);
const button \= document.querySelector('button');
button.addEventListener('click', instance.onClick.bind(instance));

The `remoteEvent` object is a mangled version of the original event to make it transferable:

const remoteEvent \= {
  targetId, // = event.target.id
  targetClassList, // = \[...event.target.classList\]
  detail, // = event.detail
  data // = event.data
};

Promises and async methods
--------------------------

Clooney handles promises (and therefore, async methods) automatically:

class Actor {
  timeoutThing() {
    return new Promise(resolve \=> setTimeout(\_ \=> resolve('ohai'), 1000));
  }
}

const instance \= await strategy.spawn(Actor);
alert(await instance.timeoutThing()); // Will alert() after 1 second

API
---

Clooney’s job is to take _actors_ (class definitions) and _spawn_ those actors in _containers_ (Web Workers). You can use that instance as if it was a local instance (this is magic provided by Comlink).

### `Clooney.spawn(class, constructorArgs)`

This call is equivalent to `Clooney.defaultStrategy.spawn(class, constructorArgs)`. Clooney creates an instance of `RoundRobinStrategy` as the default strategy.

### Strategies

Strategies decide how many containers are spun up and where a new instance is created.

export interface Strategy {
  /\*\*
   \* \`spawn\` instantiates the given actor in an actor container of the strategy’s choice.
   \* @returns The return type is the type as T, but every method is implicitly async.
   \*/
  spawn<T\>(actor: new () \=> T, constructorArgs: any\[\], opts: Object): Promise<T\>;
  /\*\*
   \* \`terminate\` calls \`terminate()\` on all existing containers of the strategy.
   \*/
  terminate(): Promise<void\>;
}

#### `Clooney.RoundRobinStrategy(opts)`

`RoundRobinStrategy` creates up to n containers and cycles through the containers with every `spawn` call. `RoundRobinStrategy` is the default strategy.

### Strategy Options

-   `maxNumContainers`: Maximum number of containers to create (default: 1)
-   `newWorkerFunc`: Asynchronous function that creates a new container (default: `new Worker(Clooney.defaultWorkerSrc)`)

### `Clooney.asRemoteValue(obj)`

`asRemoteValue` marks a value. If a marked value is used as an parameter or return value, it will not be transferred but instead proxied.

CDN
---

If you want to use Clooney from a CDN, you need to work around the same-origin restrictions that workers have:

<script src\="https://cdn.jsdelivr.net/npm/clooneyjs@0.7.0/clooney.bundle.min.js"\></script\>
<script\>
  async function newWorkerFunc() {
    const blob \= await fetch(Clooney.defaultWorkerSrc).then(resp \=> resp.blob())
    return new Worker(URL.createObjectURL(blob));
  }

  const strategy \= new Clooney.RoundRobinStrategy({newWorkerFunc});
  // Business as usual using strategy.spawn() ...
</script\>

* * *

License Apache-2.0
