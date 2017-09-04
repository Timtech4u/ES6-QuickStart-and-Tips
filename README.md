ES6: QuickStart and Tips
------------------------

ES6: quick experience, and practical tips

> 2016 is ES6 vigorously promote and popularize the golden age, but also this year's fashion trends,
> On a [ES6] (https://github.com/search?o=desc&q=ES6&s=stars&type=Repositories&utf8=✓) keywords,
> There are so many search results on GitHub. (Keep up with big troops!)

! [It's very hot!] (Images / github-search-results.png)


## Introduction

ES6 is short for ECMAScript 6 **, [EC6-262, version 6] (http://www.ecma-international.org/ecma-262/6.0/index.html).


* ES5, ES2015 / ES6, ES2016 / ES7, ES2017 / ES8 What do these keywords mean?

  [ES5] was released in 2009.

  [ES6], compared to ES5, is the first major update, released in 2015-06, so also known as ES2015.

  [ES7 and ES8] collectively referred to as ECMAScript Next.

  [ES7] released at 2016-06, also known as ES2016.

  ES8 released in 2017-06, also known as ES2017.

* What is the relationship between ECMAScript and JavaScript?

  The former is the latter's language standard, the latter is an implementation of the former.

* ES6 in the browser, Node.js support how suitable for development, production?

  - Browser: [ECMAScript Compatibility List] (http://kangax.github.io/compat-table/es6/)

  - Node.js: [ES2015 Support] (http://node.green)

  - Performance: ES6 features relative to the ES5 baseline operations per second] (https://kpdecker.github.io/six-speed/)

  - Tools: Using some conversion tools, you can put ES6 => ES5


* Why learn new grammar?

  Many libraries, frameworks, and tools are currently being developed using ** ES6 + **, typically React and Vue, using the advantages of new grammar features for rapid development, and then deploying production code using conversion build tools.


## ES6 new features


### Arrows and Lexical This

  "Arrow" function (`=>`) and `this`:

  > Use the "arrow" function we can experience the functional programming "beauty", efficient, simple, of course, also pay attention to the context `this`.
  
   * e.g.

    ```js
    // old
    var sum = function (a, b) { return a + b }
    ```

    ```js
    // new
    var sum = (a, b) => a + b
    ```
    
    * Guess guess
    
    0. *a.js*

      ```js
      var PI = 3.14

      var c = r => 2 * PI * r

      // c(2) = ?
      ```

    0. *b.js*

      ```js
      var PI = 3.14

      var circle = {
        PI: 3.14159,
        c: r => 2 * this.PI * r
      }

      // circle.c(2) = ?
      ```

    0. *c.js*

      ```js
      var PI = 3.14

      var circle = {
        PI: 3.14159,
        c (r) {
          return 2 * this.PI * r
        }
      }

      // circle.c(2) = ?
      ```



### Classes

class:

   > Based on the syntax of the prototype chain sugar, simple, clear; object-oriented programming more easily.
   > Will not be any other language Tucao!
   
   
  * e.g.

    ```js
    // old
    function Cat () {
      this.voice = 'miao'
    }
    Cat.prototype.speak = function () {
      console.log(this.voice)
    }

    function Lion () {
      this.voice = 'roar'
    }

    Lion.prototype = Cat.prototype

    var c = new Cat()
    var l = new Lion()
    c.speak()
    l.speak()
    ```

    ```js
    // new
    class Cat {
      constructor () {
        this.voice = 'miao'
      }

      speak () {
        console.log(this.voice)
      }
    }

    class Lion extends Cat {
      constructor () {
        super()

        this.voice = 'roar'
      }
    }
    var c = new Cat()
    var l = new Lion()
    c.speak()
    l.speak()
    ```

  * Guess guess

    0. *cat.js*

      ```js
      class Cat {
        constructor () {
          this.voice = 'miao'
        }

        speak () {
          console.log(this.voice)
        }

        static type () {
          return Cat.name.toLowercase()
        }
      }

      // Cat.prototype= ?
      ```

    0. *getters-setters.js*

      ```js
      class Cat {
        constructor (options) {
          this.voice = 'miao'
          this.options = options || {}
        }

        speak () {
          console.log(this.voice)
        }

        get name () {
          return this.options.name
        }

        set name (name) {
          this.options.name = name
        }
      }

      var a = new Cat({ name: 'Garfield' })
      // a.name ?
      // a.name = 'Tom'
      // a.name ?
      ```

    0. *[mixins.js](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)*

      ```js
      var CalculatorMixin = Base => class extends Base {
        calc() { }
      }

      var RandomizerMixin = Base => class extends Base {
        randomize() { }
      }

      class Foo { }
      class Bar extends CalculatorMixin(RandomizerMixin(Foo)) { }

      // Bar.prototype ?
      ```

### Enhanced Object Literals

   Improved object declaration:

   > Significantly reduces the amount of code, creating objects more concise.

   - attribute abbreviation

   - function abbreviation

   - attribute name calculation
   
   
  * e.g.

    ```js
    // old
    var a = 1
    var b = 2
    var c = 3

    var o = {
      a: a,
      b: b
      c: c,
      d: function () {
        return this.a + this.b + this.c
      }
    }
    ```

    ```js
    // new
    var o = {
      a,
      b,
      c,
      d () {
        return this.a + this.b + this.c
      }
    }
    ```

  * Guess guess

    0. *returns.js*

      ```js
      var generate = (name, age) => ({ name, age })

      // generate('github', 5) ?
      ```

    0. *cumputed-properties.js*

      ```js
      var create = (path, verb) => {
        return {
          path,
          verb,
          ['is' + verb[0].toUpperCase() + verb.substring(1)]: true
        }
      }

      // create('/', 'get') ?
      ```

    0. *complicated.js*

      ```js
      var path = '/'
      var verb = 'get'
      var root = {
        path,
        verb
      }

      var route = {
        root
      }
      ```



### Template Strings

   Template string:

   > Finally, you can write more comfortable lines, and this function until the flowers are thanked!

   - support multiple lines

   - Supports variable binding

   - also support the string is not escaped, not parsed
   
     * e.g.

    ```js
    // old
    var first = 1
    var second = 2
    var third = 3

    var str = 'No.' + first + '\n' +
      'No.' + second +'\n' +
      'No.' + third
    ```

    ```js
    // new
    var first = 1
    var second = 2
    var third = 3

    var str = `No. ${first}
    No. ${second}
    No. ${third}
    `
    ```

  * Guess Guess

    0. *raw-tag.js*

      ```js
      var t0 = `In ES5 "\n" is a line-feed.`
      var t1 = String.raw`In ES5 "\n" is a line-feed.`

      // console.log(t0)
      // console.log(t1)
      ```

    0. *expression.js*

      ```js
      var a = 5
      var b = 10

      // console.log("Fifteen is " + (a + b) + " and\nnot " + (2 * a + b) + ".")
      // console.log(`Fifteen is ${a + b} and\nnot ${2 * a + b}.`)
      ```

    0. *custom-tag.js*

      ```js
      var generatePath = (strings, ...values) => {
        return strings[0] + values.reduce((prev, curr) => `${prev}/${curr}`, '')
      }

      var user = 'user'
      var id = '233'
      var profile = 'profile'
      // generatePath`GET: ${user}${id}${profile}`
      ```

### Destructuring

   Parsing assignment

   > You can easily get objects, arrays, and so on, and assign values to the specified variable

   - Array Array object, etc., with an iterator interface object
   
     * e.g.

    ```js
    // old
    var arr = [1, 2, 3, 4]

    var a0 = arr[0]
    var a1 = arr[1]
    var a2 = arr[2]

    var obj = {
      name: 'github',
      age: 5
    }

    var name = obj.name
    var age = obj.age
    ```

    ```js
    // new
    var arr = [1, 2, 3, 4]

    var [a0, a1, a2] = arr

    var obj = {
      name: 'github',
      age: 5
    }

    var { name, age } = obj
    ```

  * Guess guess

    0. *print.js*

      ```js
      var print = ({ name, age }) => console.log(name, age)

      // print({ name: 'ES6', age: 2015 }) ?
      ```

    0. *alias.js*

      ```js
      var js = { name: 'ES6', age: 2015 }

      var { name: es, age } = js
      // name, es, age?
      ```

    0. *defaults.js*

      ```js
      var js = { name: 'ES6', age: 2015 }
      var date = [2015, 9, 14]

      var { version = '6' } = js
      // version ?

      var { fullname: f = 'ECMAScript 6' } = js
      // fullname, f ?

      var [y, m, d, h = 9] = date
      // y, m, d, h ?
      ```

### Default + Rest + Spread

   Default, the remaining parameters (Rest), array expansion (Spread)

   - Default: Reduces the amount of code that checks the input parameters, ie, it is readable and concise

   - Rest: more flexible for parameter array operations

   - Spread: can be seen as Rest anti-operation, more convenient for the operation of the array
   
   
  * e.g.

    ```js
    // old
    function bar (a) {
      a = a || 5
    }

    function sum (a) {
      a = a || 5
      var l = arguments.length
      var i = 1
      for (; i < l; ++i) {
        a += arguments[i]
      }
      return a
    }

    function apply () {
      function fn () {}
      var l = arguments.length
      var args = new Array(l)
      for (var i = 0; i < l; ++i) {
        args[i] = arguments[i]
      }
      fn.apply(null, args)
    }
    ```

    ```js
    // new
    function bar(a = 5) {
    }

    function sum (a = 5, ...args) {
      var l = args.length
      var i = 0
      for (; i < l; ++i) {
        a += args[i]
      }
      return a
    }

    function apply (...args) {
      function fn () {}
      fn.apply(null, args)
    }
    ```

  * Guess Guess

    0. *string.js*

      ```js
      var str = '1234567890'

      // [...str] ?
      ```

    0. *concat.js*

      ```js
      var a = [1, 2, 3]
      var b = [6, 5, 4]

      var c = [...a, ...b]
      // c ?
      ```

    0. *parse-args.js*

      ```js
      /**
       * Parse the parameters and return to a specific format
       *
       * @return {Array} [arr, options, cb]
       */

      function parseArgs (...args) {
        const last = args[args.length - 1]
        const type = typeof last
        let opts
        let cb

        if ('function' === type) {
          cb = args.pop()
          if ('object' === typeof args[args.length - 1]) {
            opts = args.pop()
          }
        } else if ('object' === type && !Array.isArray(last)) {
          opts = args.pop()
        } else if ('undefined' === type) {
          args.pop()
          return parseArgs(...args)
        }

        if (Array.isArray(args[0])) {
          args = args[0]
        }
        return [args, opts || {}, cb]
      }

      // parseArgs('users') ?
      // parseArgs('users', {}) ?
      // parseArgs('users', () => {}) ?
      // parseArgs('users', {}, () => {}) ?
      // parseArgs('users', 'books') ?
      // parseArgs(['users', 'books']) ?
      ```

### Let + Const

   Variable, constant definition statement:

   > When the world is `var` time, variable management is a god pit!

   - Block level

   - const: one-time statement

   * e.g.

     `` `js
     // old
     / / Function scope under the coverage of the global scope
     var bar = 1
     var bar = 3
     function method () {
       console.log (bar) // undefined
       var bar = 2
     }

     // variable leaks
         for (var i = 0; i < s.length; i++) {
      console.log(s[i]);
    }
    console.log(i); // 5
    ```

    ```js
    // new
    let bar0 = 1
    let bar1 = 3

    function method () {
      console.log(bar0)
      let bar3 = 2
    }

    var s = 'hello';
    for (let i = 0; i < s.length; i++) {
      console.log(s[i]);
    }
    ```

  * Guess guess

    0. *global.js*

      ```js
      var a = 1
      let b = 2
      const c = 3

      // this.a ?
      // this.b ?
      // this.c ?
      ```

    0. *for.js*

      ```js
      var s = 'hello';
      for (let i = 0; i < s.length; i++) {
        console.log(s[i]);
      }
      console.log(i); // ?
      ```

### Iterators + For..Of

   Iterator and `for..of`

   > Like `[... arr]` is a good example of the iterator.

   - Iterative protocol: ES6 defines a set of uniform standards that allow JavaScript objects to customize their iterative behavior.

   - The built-in iterable types are String, Array, TypedArray, Map, Set, because the `[Symbol.iterator]` method already exists on their prototype objects.
     * e.g.

    ```js
    // old
    var arr = [1, 2, 3]

    for (let i in arr) {
      console.log(i)
    }
    ```

    ```js
    // new
    var arr = [1, 2, 3]

    for (let i of arr) {
      console.log(i)
    }
    ```

  * Guess guess

    0. *for-loops.js*

      ```js
      Array.prototype.arrCustom = function () {}
      var arr = [1, 2, 3]
      arr.isArray = true

      for (let i in arr) {
        console.log(i) // ?
      }

      for (let i of arr) {
        console.log(i) // ?
      }
      ```

    0. *iterable.js*

      ```js
      var iterable = {
        [Symbol.iterator]() {
          return {
            i: 0,
            next () {
              return {
                done: this.i === 10,
                value: this.i++
              }
            }
          }
        }
      }

      for (const i of iterable) {
        console.log(i) // ?
      }

      // [...iterable] ?
      ```

    0. *iterator.js*

      ```js
      var iterable = {
        [Symbol.iterator]() {
          return {
            i: 0,
            next () {
              const done = this.i === 10
              const value = done ? undefined : this.i++
              return { done, value }
            }
          }
        }
      }

      const iterator = iterable[Symbol.iterator]()

      iterator.next() // ?
      iterator.next() // ?
      iterator.next() // ?
      // ...

      const iterator2 = iterable[Symbol.iterator]()

      iterator2.next() // ?
      iterator2.next() // ?
      iterator2.next() // ?
      // ...
      ```


### Generators

   Builder:

   > Generator big kill device!

   - [iterable] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#iterable)

   - [follow the iterator protocol] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#iterator)

   - can be in a single function `GeneratorFunction` custom iteration logic, can replace the iterator, more powerful

   - can be interrupted

   - can be assigned
   
     * e.g.

    ```js
    // old
    var iterable = {
      [Symbol.iterator]() {
        return {
          i: 0,
          next () {
            const done = this.i === 10
            const value = done ? undefined : this.i++
            return { done, value }
          }
        }
      }
    }
    const iterator = iterable[Symbol.iterator]()
    ```

    ```js
    // new
    function* generatable () {
      for (let i = 0, l = 10; i < l; ++i) {
        yield i
      }
    }
    const iterator = generatable()
    ```

  * Guess guess

    0. *generatable.js*

      ```js
      function* generatable () {
        for (let i = 0, l = 10; i < l; ++i) {
          yield i
        }
      }
      const iterator = generatable()

      for (const i of generatable()) {
        console.log(i) // ?
      }
      // [...generatable()] ?
      ```

    0. *next.js*

      ```js
      function* range(min = 0, max = 10, step = 1) {
        for (; min < max; min += step) {
          let rest = yield min
          if (rest) min = step * -1
        }
      }

      const iterator = range()

      iterator.next() // ?
      iterator.next() // ?
      iterator.next() // ?
      iterator.next(true) // ?
      iterator.next() // ?
      iterator.next() // ?
      iterator.next() // ?

      const iterator2 = range(0, 100, 2)

      [...iterator2] // ?
      iterator.next() // ?
      ```

    0. *return.js*

      ```js
      function* range(min = 0, max = 10, step = 1) {
        for (; min < max; min += step) {
          let rest = yield min
          if (rest) min = step * -1
        }
      }

      const iterator = range()
      iterator.next()
      iterator.next(true)
      iterator.next()
      iterator.return() // ?
      iterator.next() // ?
      iterator.return(1) // ?
      iterator.next() // ?
      ```

    0. *yield.js*

      ```js
      function* g() {
        yield 1
        yield 2
        yield 3
        yield* [4, 5, 6]
        yield* 'Hello World!'
        yield 7
      }

      [...g()] // ?
      ```

### Unicode

   Unicode

   - Enhanced support for Unicode, and extended string objects

   * e.g.

     `` `js
     // same as ES5.1
     "𠮷" .length == 2

     // new RegExp behaviour, opt-in 'u'
     "𠮷" .match (/./ u) [0] .length == 2

     // new form
     "\ u {20BB7}" == "𠮷" == "\ uD842 \ uDFB7"

     // new String ops
     "𠮷" .codePointAt (0) == 0x20BB7

     // for-of iterates code points
     for (var c of "𠮷") {
       console.log (c);
     }
     `` ``


### Modules?

   Modular system is not yet available!


### Subclassable Built-ins

   Subclasses can inherit from built-in data types

   > Really too convenient, such as want to expand the Array, and now no need to modify the `Array.prototype`,` extends Array` on it.

   - Array Boolean String Number Map Set Error RegExp Function Promise
   
     * e.g.

    ```js
    // old
    // This is danger.
    Array.prototype.sum = function () {
      return this.reduce((t, curr) => t + curr, 0)
    }

    var a = [1, 2, 3]
    a.sum()
    ```

    ```js
    // new
    class CustomArray extends Array {
      constructor (...args) {
        super(...args)
      }

      sum () {
        return this.reduce((t, curr) => t + curr, 0)
      }
    }

    var a = CustomArray.from([1, 2, 3])
    a.sum()
    ```

  * Guess guess

    0. *[middleware.js](https://github.com/trekjs/middleware)*

      ```js
      const SYMBOL_ITERATOR = Symbol.iterator

      class Middleware extends Array {

        [SYMBOL_ITERATOR] () {
          return this
        }

        next (i = 0, context, nextFunc) {
          const fn = this[i] || nextFunc

          return {
            done: i === this.length,
            value: fn && fn(context, () => {
              return this.next(i + 1, context, nextFunc).value
            })
          }
        }

        compose (context, nextFunc) {
          return this[SYMBOL_ITERATOR]().next(0, context, nextFunc).value
        }

      }

      const middleware = new Middleware()

      middleware.push((ctx, next) => {
        ctx.arr.push(1)
        next()
        ctx.arr.push(6)
      })

      middleware.push((ctx, next) => {
        ctx.arr.push(2)
        next()
        ctx.arr.push(5)
      })

      middleware.push((ctx, next) => {
        ctx.arr.push(3)
        next()
        ctx.arr.push(4)
      })

      const ctx = { arr: [] }
      middleware.compose(ctx)
      console.log(ctx.arr) // ?
      ```

### Map + Set + WeakMap + WeakSet

   Add `Map``set`` WeakMap`` WeakSet` several efficient data types
   
     * e.g.

    ```js
    // Sets
    var s = new Set();
    s.add("hello").add("goodbye").add("hello");
    s.size === 2;
    s.has("hello") === true;

    // Maps
    var m = new Map();
    m.set("hello", 42);
    m.set(s, 34);
    m.get(s) == 34;

    // Weak Maps
    var wm = new WeakMap();
    wm.set(s, { extra: 42 });
    wm.size === undefined

    // Weak Sets
    var ws = new WeakSet();
    ws.add({ data: 42 });
    // Because the added object has no other references, it will not be held in the set
    ```

### Proxies

   > `Proxies` is the best solution when we do not want to expose the objects and do not want to operate them directly.
   > But when the increase in the `Proxies` this layer, the performance will still be affected.
   
     * e.g.

    ```js
    // old
    const inner = {
      name: 'ES6'
    }

    var outer = {
      inner,
      get name () {
        return this.inner.name
      },
      set name (name) {
        this.inner.name = name
      }
    }

    // outer.name
    ```

    ```js
    // new
    const inner = {
      name: 'ES6'
    }

    var p = new Proxy(inner, {
      get (target, name) {
        return target[name]
      },

      set (target, name, value) {
        if ('string' !== typeof value) throw new TypeError('value must be String!')
        target[name] = value
      }
    })

    p.name
    p.name = 2
    p.name = 'ES2015'
    ```

  * Guess guess

    0. *[delegate-proxy.js](https://github.com/fundon/delegate-proxy)*

      ```js
      function delegateProxy (target, origin) {
        return new Proxy(target, {
          get (target, key, receiver) {
            if (key in target) return Reflect.get(target, key, receiver)
            const value = origin[key]
            return 'function' === typeof value ? function method () {
              return value.apply(origin, arguments)
            } : value
          },
          set (target, key, value, receiver) {
            if (key in target) return Reflect.set(target, key, value, receiver)
            origin[key] = value
            return true
          }
        })
      }

      const bar = {
        n: 1,

        add (i) {
          this.n += i
        }
      }

      const foo = {

        set (n) {
          this.n = n | 0
        },

        sub (i) {
          this.n -= i
        }

      }

      const p = delegateProxy(foo, bar)

      bar
      foo
      p

      p.n       // ?
      p.add(1)
      p.n       // ?

      p.sub(2)
      p.n       // ?

      p.set(1)
      p.n       // ?

      p.n = 233
      p.n       // ?
      ```

### [Symbols] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

   symbol:

     - Uniqueness

     - immutable

     - Object.getOwnPropertyNames (obj) `and` Object.keys (obj) `that are not included in the object

     - safe (in some cases can be used as a private property `key`)

   > Want to give the object a signal, no longer difficult!
   
     * e.g.

    ```js
    // old
    let obj = {
      id: 1
    }

    obj.id      // 1
    obj.id = 2
    obj.id      // 2
    ```

    ```js
    // new
    let obj = {
      [Symbol('id')]: 1
    }

    obj[Symbol('id')]      // undefined
    obj[Symbol('id')] = 2
    obj[Symbol('id')]      // undefined

    for (const k of Object.getOwnPropertySymbols(obj)) {
      console.log(obj[k])
    }
    ```


### Math + Number + String + Array + Object APIs

  New APIs, data manipulation is more convenient.

  * e.g.

    ```js
    Number.EPSILON
    Number.isInteger(Infinity) // false
    Number.isNaN("NaN") // false

    Math.acosh(3) // 1.762747174039086
    Math.hypot(3, 4) // 5
    Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

    "abcde".includes("cd") // true
    "abc".repeat(3) // "abcabcabc"

    Array.from(document.querySelectorAll("*")) // Returns a real Array
    Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
    [0, 0, 0].fill(7, 1) // [0,7,7]
    [1,2,3].findIndex(x => x == 2) // 1
    ["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
    ["a", "b", "c"].keys() // iterator 0, 1, 2
    ["a", "b", "c"].values() // iterator "a", "b", "c"

    Object.assign(Point, { origin: new Point(0,0) })
    ```


### Binary and Octal Literals

  Binary `b`, octal` o` literally

  * e.g.

    ```js
    0b111110111 === 503 // true
    0o767 === 503 // true
    0x1f7 === 503 // true
    ```

### Promises

   Promises: more elegant asynchronous programming. To see more clearly the implementation of `Promise`, you can see this visual tool [promisees] (https://github.com/bevacqua/promisees).

   > In the face of asynchronous programming, `callback-hell` is the biggest criticism of JavaScript!
   
     * e.g.

    ```js
    // old
    getProfileById(233, (err, res) => {
      if (err) throw err
      getFollowing(233, (err, following) => {
        if (err) throw err
        getFollowers(233, (err, followers) => {
          if (err) throw err
          getStarred(233, (err, starred) => {
            if (err) throw err
            // ....
          })
        })
      })
    })
    ```

    ```js
    // new
    getProfileById(233)
      .then(res => getFollowing(233))
      .then(res => getFollowers(233))
      .then(res => getStarred(233))
      .catch(err => console.log(err))
      // ...
    ```

  * Guess guess

    0. *simple-promise.js*

      ```js
      function loadImage (url) {
        return new Promise((resolve, reject) => {
          const img = new Image()

          img.onload = function () {
            resolve(img)
          }

          img.onerror = function () {
            reject(new Error('Could not load image at ' + url))
          }

          img.url = url
        })
      }

      loadImage('https://nodejs.org/static/images/logo-header.png')
        .then(img => document.body.appendChild(img))
        .catch(err => console.log(err))
      ```

    0. *all.js*

      ```js
      function delay(value, duration = 0) {
        return new Promise((resolve, reject) => {
          setTimeout(() => resolve(value), duration)
        })
      }

      let res = Promise.all([
        delay(10, 1),
        delay(8, 2),
        delay(6, 3),
        delay(4, 4),
        delay(2, 5),
        delay(0, 6),
      ])

      res.then(arr => {
        console.log(arr) // ?
      })
      ```

    0. *race.js*

      ```js
      function delay(value, duration = 0) {
        return new Promise((resolve, reject) => {
          setTimeout(() => resolve(value), duration)
        })
      }

      let res = Promise.race([
        delay(10, 1),
        delay(8, 2),
        delay(6, 3),
        delay(4, 4),
        delay(2, 5),
        delay(0, 6),
      ])

      res.then(arr => {
        console.log(arr) // ?
      })
      ```

    0. *reduce.js*

      ```js
      const reduce = (arr, cb, initialValue = 0) => {
        return arr.reduce(cb, Promise.resolve(initialValue))
      }

      const cb = (prev, curr) => prev.then(v => v + curr)

      reduce([1, 2, 3, 4, 5, 6, 7, 8, 9], cb)
        .then(res => {
          console.log(res) // ?
        })
      ```


### [Reflect API] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

   Reflective API: exposes the object's meta operations, with the opposite of the proxy API
   
     * e.g.

    ```js
    var O = {a: 1};
    Object.defineProperty(O, 'b', {value: 2});
    O[Symbol('c')] = 3;

    Reflect.ownKeys(O); // ['a', 'b', Symbol(c)]

    function C(a, b){
      this.c = a + b;
    }
    var instance = Reflect.construct(C, [20, 22]);
    instance.c; // 42
    ```

### Tail Calls

  Optimize the tail recursive algorithm to ensure that the stack will not grow indefinitely, making the tail recursive algorithm safe.


## Quick experience

> For more than the new features, experience some of the environment, including the browser and Node.js environment


## Advanced application

> In-depth learning characteristics, application production

* http://ramdajs.com/

* https://github.com/cujojs/most

* https://lodash.com/

* `fs.readdir` problem

  - https://github.com/nodejs/node/issues/583

  - https://github.com/w3c/filesystem-api

* https://github.com/kriskowal/gtor/#asynchronous-generator-functions


## compatible, transcoding

> Use the conversion tool to convert the ES6 + code to fit the browser or Node <v6


## other

* http://es6.ruanyifeng.com

* https://github.com/lukehoban/es6features

* https://babeljs.io/docs/learn-es2015/

* https://ponyfoo.com/articles/tagged/es6-in-depth

* https://github.com/bevacqua/es6

* https://github.com/DrkSephy/es6-cheatsheet

* https://github.com/ericdouglas/ES6-Learning

* https://github.com/addyosmani/es6-tools

* https://github.com/bevacqua/promisees


## License

Authorization: [signed - non-commercial use] (https://creativecommons.org/licenses/by-nc/4.0/)

---

> [fundon.me] (https://fundon.me) & nbsp; & middot; & nbsp;
> GitHub [@fundon] (https://github.com/fundon) & nbsp; & middot; & nbsp;
> Twitter [@_fundon] (https://twitter.com/_fundon)

[ES5]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_5_support_in_Mozilla

[ES6]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla

[ES7 and ES8]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_Next_support_in_Mozilla

[ES7]: http://www.ecma-international.org/ecma-262/7.0/index.html
