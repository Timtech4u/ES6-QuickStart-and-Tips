ES6: QuickStart and Tips
------------------------

ES6: fast experience, and practical tips

 >2016 is ES6 vigorously promote and popularize the golden age, but also this year's fashion trends, on an ES6 keyword, there are so many search results on GitHub. 
>(Keep up with big troops!)

![It's very hot!](images/github-search-results.png)


## Introduction

ES6 is short for ECMAScript 6 **, [EC6-262, version 6] (http://www.ecma-international.org/ecma-262/6.0/index.html)。


* ES5, ES2015 / ES6, ES2016 / ES7, ES2017 / ES8 What do these keywords mean?

   [ES5] was released in 2009.

   [ES6], compared to ES5, is the first major update, released in 2015-06, so also known as ES2015.

   [ES7 and ES8] collectively referred to as ECMAScript Next.

   [ES7] released in 2016-06, also known as ES2016.

   ES8 released in 2017-06, also known as ES2017.

* What is the relationship between ECMAScript and JavaScript?

   The former is the latter's language standard, the latter is an implementation of the former.

* ES6 in the browser, Node.js support how, suitable for development, production?

   - Browser: [ECMAScript Compatibility List] (http://kangax.github.io/compat-table/es6/)

   - Node.js: [ES2015 Support] (http://node.green)

   - Performance: ES6 features relative to the ES5 baseline operations per second] (https://kpdecker.github.io/six-speed/)

   - Tools: Using some conversion tools, you can put ES6 => ES5


* Why learn new grammar?

   Many libraries, frameworks, and tools are currently being developed using ** ES6 + **, typically React and Vue, using the advantages of new syntax features for rapid development, and then deploying production code using conversion build tools.


## ES6 new features


### Arrows and Lexical This

  "Arrow" function (`=>`) and `this`:

  > Use the "arrow" function we can experience the functional programming "beauty", efficient, simple, of course, also pay attention to the context `this`.

  * E.g.

    `` `Js
    // old
    Var sum = function (a, b) {return a + b}
    `` ``

    `` `Js
    // new
    Var sum = (a, b) => a + b
    `` ``

  Guess guess

    0. * a.js *

      `` `Js
      Var PI = 3.14

      Var c = r => 2 * PI * r

      // c (2) =?
      `` ``

    0. * b.js *

      `` `Js
      Var PI = 3.14

      Var circle = {
        PI: 3.14159,
        C: r => 2 * this.PI * r
      }

      // circle.c (2) =?
      `` ``

    0. * c.js *

      `` `Js
      Var PI = 3.14

      Var circle = {
        PI: 3.14159,
        C (r) {
          Return 2 * this.PI * r
        }
      }

      // circle.c (2) =?
      `` ``


### Classes

  class:

  > Based on the syntax of the prototype chain sugar, simple, clear; object-oriented programming more easily.
  > Will not be any other language Tucao!

  * E.g.

    `` `Js
    // old
    Function cat () {
      This.voice = 'miao'
    }
    Cat.prototype.speak = function () {
      Console.log (this.voice)
    }

    Function Lion () {
      This.voice = 'roar'
    }

    Lion.prototype = Cat.prototype

    Var c = new Cat ()
    Var l = new Lion ()
    C.speak ()
    L.speak ()
    `` ``

    `` `Js
    // new
    Class Cat {
      Constructor () {
        This.voice = 'miao'
      }

      Speak () {
        Console.log (this.voice)
      }
    }

    Class Lion extends Cat {
      Constructor () {
        Super ()

        This.voice = 'roar'
      }
    }
    Var c = new Cat ()
    Var l = new Lion ()
    C.speak ()
    L.speak ()
    `` ``

  Guess guess

    0. * cat.js *

      `` `Js
      Class Cat {
        Constructor () {
          This.voice = 'miao'
        }

        Speak () {
          Console.log (this.voice)
        }

        Static type () {
          Return Cat.name.toLowercase ()
        }
      }

      // Cat.prototype =?
      `` ``

    0. * getters-setters.js *

      `` `Js
      Class Cat {
        Constructor (options) {
          This.voice = 'miao'
          This.options = options || {}
        }

        Speak () {
          Console.log (this.voice)
        }

        Get name () {
          Return this.options.name
        }

        Set name (name) {
          This.options.name = name
        }
      }

      Var a = new Cat ({name: 'Garfield'})
      // a.name?
      // a.name = 'Tom'
      // a.name?
      `` ``

    0. * [mixins.js] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) *

      `` `Js
      Var CalculatorMixin = Base => class extends Base {
        Calc () {}
      }

      Var RandomizerMixin = Base => class extends Base {
        Randomize () {}
      }

      Class Foo {}
      Class Bar extends CalculatorMixin (RandomizerMixin (Foo)) {}

      // Bar.prototype?
      `` ``


### Enhanced Object Literals

  Improved object declaration:

  > Greatly reduces the amount of code, creating objects more concise.

  - attribute abbreviation

  - function abbreviation

  - attribute name calculation

  * E.g.

    `` `Js
    // old
    Var a = 1
    Var b = 2
    Var c = 3

    Var o = {
      A: a,
      B: b
      C: c,
      D: function () {
        Return this.a + this.b + this.c
      }
    }
    `` ``

    `` `Js
    // new
    Var o = {
      A,
      B,
      C,
      D () {
        Return this.a + this.b + this.c
      }
    }
    `` ``

  Guess guess

    0. * returns.js *

      `` `Js
      Var generate = (name, age) => ({name, age})

      // generate ('github', 5)?
      `` ``

    0. * cumputed-properties.js *

      `` `Js
      Var create = (path, verb) => {
        Return {
          Path,
          Verb,
          ['Is' + verb [0] .toUpperCase () + verb.substring (1)]: true
        }
      }

      // create ('/', 'get')?
      `` ``

    0. * complicated.js *

      `` `Js
      Var path = '/'
      Var verb = 'get'
      Var root = {
        Path,
        Verb
      }

      Var route = {
        Root
      }
      `` ``

### Template Strings

  Template string:

  > Finally can be comfortable to write multi-line string, and this function until the flowers are grateful!

  - support multiple lines

  - Supports variable binding

  - also support the string is not escaped, no resolution

  * E.g.

    `` `Js
    // old
    Var first = 1
    Var second = 2
    Var third = 3

    Var str = 'No.' + first + '\ n' +
      'No.' + second + '\ n' +
      'No.' + third
    `` ``

    `` `Js
    // new
    Var first = 1
    Var second = 2
    Var third = 3

    Var str = `No. $ {first}
    No. $ {second}
    No. $ {third}
    `
    `` ``

  Guess guess

    0. * raw-tag.js *

      `` `Js
      Var t0 = `In ES5" \ n "is a line-feed.`
      Var t1 = String.raw`In ES5 "\ n" is a line-feed.`

      // console.log (t0)
      // console.log (t1)
      `` ``

    0. * expression.js *

      `` `Js
      Var a = 5
      Var b = 10

      // console.log ("Fifteen is" + (a + b) + "and \ nnot" + (2 * a + b) + ".")
      // console.log (`Fifteen is $ {a + b} and \ nnot $ {2 * a + b} .`)
      `` ``

    0. * custom-tag.js *

      `` `Js
      Var generatePath = (strings, ... values) => {
        Return strings [0] + values.reduce ((prev, curr) => `$ {prev} / $ {curr}`, '')
      }

      Var user = 'user'
      Var id = '233'
      Var profile = 'profile'
      // generatePath`GET: $ {user} $ {id} $ {profile} `
      `` ``


### Destructuring

  Parsing assignment

  > You can easily get the elements of an object, array, and so on, and assign it to the specified variable

  - Array ArrayObjects, etc, objects with an iterator interface

  * E.g.

    `` `Js
    // old
    Var arr = [1, 2, 3, 4]

    Var a0 = arr [0]
    Var a1 = arr [1]
    Var a2 = arr [2]

    Var obj = {
      Name: 'github',
      Age: 5
    }

    Var name = obj.name
    Var age = obj.age
    `` ``

    `` `Js
    // new
    Var arr = [1, 2, 3, 4]

    Var [a0, a1, a2] = arr

    Var obj = {
      Name: 'github',
      Age: 5
    }

    Var {name, age} = obj
    `` ``

  Guess guess

    0. * print.js *

      `` `Js
      Var print = ({name, age}) => console.log (name, age)

      // print ({name: 'ES6', age: 2015})?
      `` ``

    0. * alias.js *

      `` `Js
      Var js = {name: 'ES6', age: 2015}

      Var {name: es, age} = js
      // name, es, age
      `` ``

    0. * defaults.js *

      `` `Js
      Var js = {name: 'ES6', age: 2015}
      Var date = [2015, 9, 14]

      Var {version = '6'} = js
      // version?

      Var {fullname: f = 'ECMAScript 6'} = js
      // fullname, f?

      Var [y, m, d, h = 9] = date
      // y, m, d, h?
      `` ``### Default + Rest + Spread
Default value, the remaining parameters (Rest), array expansion (Spread)

  - Default: Reduces the amount of code that checks the input parameters, ie, it is readable and concise

  - Rest: more flexible for parameter array operations

  - Spread: can be seen as Rest anti-operation, more convenient for the operation of the array

  * E.g.

    `` `Js
    // old
    Function bar (a) {
      A = a || 5
    }

    Function sum (a) {
      A = a || 5
      Var l = arguments.length
      Var i = 1
      For (; i <l; ++ i) {
        A + = arguments [i]
      }
      Return a
    }

    Function apply () {
      Function fn () {}
      Var l = arguments.length
      Var args = new Array (l)
      For (var i = 0; i <l; ++ i) {
        Args [i] = arguments [i]
      }
      Fn.apply (null, args)
    }
    `` ``

    `` `Js
    // new
    Function bar (a = 5) {
    }

    Function sum (a = 5, ... args) {
      Var l = args.length
      Var i = 0
      For (; i <l; ++ i) {
        A + = args [i]
      }
      Return a
    }

    Function apply (... args) {
      Function fn () {}
      Fn.apply (null, args)
    }
    `` ``

  Guess guess

    0. * string.js *

      `` `Js
      Var str = '1234567890'

      // [... str]?
      `` ``

    0. * concat.js *

      `` `Js
      Var a = [1, 2, 3]
      Var b = [6, 5, 4]

      Var c = [... a, ... b]
      // c?
      `` ``

    0. * parse-args.js *

      `` `Js
      / **
       * Parse the parameters to return to a particular format
       *
       * @return {Array} [arr, options, cb]
       * /

      Function parseArgs (... args) {
        Const last = args [args.length - 1]
        Const type = typeof last
        Let opts
        Let cb

        If ('function' === type) {
          Cb = args.pop ()
          If ('object' === typeof args [args.length - 1]) {
            Opts = args.pop ()
          }
        } Else if ('object' === type &&! Array.isArray (last)) {
          Opts = args.pop ()
        } Else if ('undefined' === type) {
          Args.pop ()
          Return parseArgs (... args)
        }

        If (Array.isArray (args [0])) {
          Args = args [0]
        }
        Return [args, opts || {}, cb]
      }

      // parseArgs ('users')?
      // parseArgs ('users', {})?
      // parseArgs ('users', () => {})?
      // parseArgs ('users', {}, () => {})?
      // parseArgs ('users', 'books')?
      // parseArgs (['users', 'books'])?
      `` ``


### Let + Const

  Variable, constant definition statement:

  > When the world is `var` time, variable management is a god pit!

  - Block level

  - const: one-time statement

  * E.g.

    `` `Js
    // old
    // function scope to override the global scope
    Var bar = 1
    Var bar = 3
    Function method () {
      Console.log (bar) // undefined
      Var bar = 2
    }

    // variable leaks
    Var s = 'hello';
    For (var i = 0; i <s.length; i ++) {
      Console.log (s [i]);
    }
    Console.log (i); // 5
    `` ``

    `` `Js
    // new
    Let bar0 = 1
    Let bar1 = 3

    Function method () {
      Console.log (bar0)
      Let bar3 = 2
    }

    Var s = 'hello';
    For (let i = 0; i <s.length; i ++) {
      Console.log (s [i]);
    }
    `` ``

  Guess guess

    0. * global.js *

      `` `Js
      Var a = 1
      Let b = 2
      Const c = 3

      // this.a?
      // this.b?
      // this.c
      `` ``

    0. * for.js *

      `` `Js
      Var s = 'hello';
      For (let i = 0; i <s.length; i ++) {
        Console.log (s [i]);
      }
      Console.log (i); //?
      `` ``


### Iterators + For..Of

  Iterators and `for..of`

  > Like `[... arr]` is a good example of the iterator.

  - Iterative protocol: ES6 defines a set of uniform standards that allow JavaScript objects to customize their iterative behavior.

  - The built-in iterable types are String, Array, TypedArray, Map, Set, because the `[Symbol.iterator]` method already exists on their prototype objects.

  * E.g.

    `` `Js
    // old
    Var arr = [1, 2, 3]

    For (let i in arr) {
      Console.log (i)
    }
    `` ``

    `` `Js
    // new
    Var arr = [1, 2, 3]

    For (let i of arr) {
      Console.log (i)
    }
    `` ``

  Guess guess

    0. * for-loops.js *

      `` `Js
      Array.prototype.arrCustom = function () {}
      Var arr = [1, 2, 3]
      Arr.isArray = true

      For (let i in arr) {
        Console.log (i) //?
      }

      For (let i of arr) {
        Console.log (i) //?
      }
      `` ``

    0. * iterable.js *

      `` `Js
      Var iterable = {
        [Symbol.iterator] () {
          Return {
            I: 0,
            Next () {
              Return {
                Done: this.i === 10,
                Value: this.i ++
              }
            }
          }
        }
      }

      For (const i of iterable) {
        Console.log (i) //?
      }

      // [... iterable]?
      `` ``

    0. * iterator.js *

      `` `Js
      Var iterable = {
        [Symbol.iterator] () {
          Return {
            I: 0,
            Next () {
              Const done = this.i === 10
              Const value = done? Undefined: this.i ++
              Return {done, value}
            }
          }
        }
      }

      Const iterator = iterable [Symbol.iterator] ()

      Iterator.next () //?
      Iterator.next () //?
      Iterator.next () //?
      // ...

      Const iterator2 = iterable [Symbol.iterator] ()

      Iterator2.next () //?
      Iterator2.next () //?
      Iterator2.next () //?
      // ...
      `` ``
### Generators

  Builder:

  > Generator big killer!

  - [iterable] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#iterable)

  - [follow the iterator protocol] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#iterator)

  - can be in a single function `GeneratorFunction` custom iteration logic, can replace the iterator, more powerful

  - can be interrupted

  - can be assigned

  * E.g.

    `` `Js
    // old
    Var iterable = {
      [Symbol.iterator] () {
        Return {
          I: 0,
          Next () {
            Const done = this.i === 10
            Const value = done? Undefined: this.i ++
            Return {done, value}
          }
        }
      }
    }
    Const iterator = iterable [Symbol.iterator] ()
    `` ``

    `` `Js
    // new
    Function * generatable () {
      For (let i = 0, l = 10; i <l; ++ i) {
        Yield i
      }
    }
    Const iterator = generatable ()
    `` ``

  Guess guess

    0. * generatable.js *

      `` `Js
      Function * generatable () {
        For (let i = 0, l = 10; i <l; ++ i) {
          Yield i
        }
      }
      Const iterator = generatable ()

      For (const i of generatable ()) {
        Console.log (i) //?
      }
      // [... generatable ()]?
      `` ``

    0. * next.js *

      `` `Js
      Function * range (min = 0, max = 10, step = 1) {
        For (; min <max; min + = step) {
          Let rest = yield min
          If (rest) min = step * -1
        }
      }

      Const iterator = range ()

      Iterator.next () //?
      Iterator.next () //?
      Iterator.next () //?
      Iterator.next (true) //?
      Iterator.next () //?
      Iterator.next () //?
      Iterator.next () //?

      Const iterator2 = range (0, 100, 2)

      [... iterator2] //?
      Iterator.next () //?
      `` ``

    0. * return.js *

      `` `Js
      Function * range (min = 0, max = 10, step = 1) {
        For (; min <max; min + = step) {
          Let rest = yield min
          If (rest) min = step * -1
        }
      }

      Const iterator = range ()
      Iterator.next ()
      Iterator.next (true)
      Iterator.next ()
      Iterator.return () //?
      Iterator.next () //?
      Iterator.return (1) //?
      Iterator.next () //?
      `` ``

    0. * yield.js *

      `` `Js
      Function * g () {
        Yield 1
        Yield 2
        Yield 3
        Yield * [4, 5, 6]
        Yield * 'Hello World!'
        Yield 7
      }

      [... g ()] //?
      `` ``

### Unicode

  Unicode

  - 加强对 Unicode 的支持，并且扩展了字符串对象

  * e.g.

    ```js
    // same as ES5.1
    "𠮷".length == 2

    // new RegExp behaviour, opt-in ‘u’
    "𠮷".match(/./u)[0].length == 2

    // new form
    "\u{20BB7}" == "𠮷" == "\uD842\uDFB7"

    // new String ops
    "𠮷".codePointAt(0) == 0x20BB7

    // for-of iterates code points
    for(var c of "𠮷") {
      console.log(c);
    }
    ```


### Modules ?

  模块化系统目前还未实现！


### Subclassable Built-ins

  子类可继承自内置数据类型

  > 真的太方便了，比如想对 Array 进行扩展，现在无需修改 `Array.prototype`，`extends Array` 就可以了。

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

  * 猜猜猜

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
### Unicode

  Unicode

  - 加强对 Unicode 的支持，并且扩展了字符串对象

  * e.g.

    ```js
    // same as ES5.1
    "𠮷".length == 2

    // new RegExp behaviour, opt-in ‘u’
    "𠮷".match(/./u)[0].length == 2

    // new form
    "\u{20BB7}" == "𠮷" == "\uD842\uDFB7"

    // new String ops
    "𠮷".codePointAt(0) == 0x20BB7

    // for-of iterates code points
    for(var c of "𠮷") {
      console.log(c);
    }
    ```


### Modules ?

  模块化系统目前还未实现！


### Subclassable Built-ins

  子类可继承自内置数据类型

  > 真的太方便了，比如想对 Array 进行扩展，现在无需修改 `Array.prototype`，`extends Array` 就可以了。

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

  * 猜猜猜

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

  Added `Map``set`` WeakMap`` WeakSet` Several efficient data types

  * E.g.

    `` `Js
    // Sets
    Var s = new Set ();
    ("Hello"). Add ("goodbye"). Add ("hello");
    S.size === 2;
    S.has ("hello") === true;

    // Maps
    Var m = new Map ();
    M.set ("hello", 42);
    M.set (s, 34);
    M.get (s) == 34;

    // Weak Maps
    Var wm = new WeakMap ();
    Wm.set (s, {extra: 42});
    Wm.size === undefined

    // Weak Sets
    Var ws = new WeakSet ();
    Ws.add ({data: 42});
    // Because the added object has no other references, it will not be held in the set
    `` ``


### Proxies

  > `Proxies` is the best solution when we do not want to expose the objects and do not want to operate them directly.
  > But when the increase in the `Proxies` this layer, the performance will still be affected.

  * E.g.

    `` `Js
    // old
    Const inner = {
      Name: 'ES6'
    }

    Var outer = {
      Inner,
      Get name () {
        Return this.inner.name
      },
      Set name (name) {
        This.inner.name = name
      }
    }

    // outer.name
    `` ``

    `` `Js
    // new
    Const inner = {
      Name: 'ES6'
    }

    Var p = new Proxy (inner, {
      Get (target, name) {
        Return target [name]
      },

      Set (target, name, value) {
        If ('string'! == typeof value) throw new TypeError ('value must be String!')
        Target [name] = value
      }
    })

    P.name
    P.name = 2
    P.name = 'ES2015'
    `` ``

  Guess guess

    0. * [delegate-proxy.js] (https://github.com/fundon/delegate-proxy) *

      `` `Js
      Function delegateProxy (target, origin) {
        Return new Proxy (target, {
          Get (target, key, receiver) {
            If (key in target) return Reflect.get (target, key, receiver)
            Const value = origin [key]
            Return 'function' === typeof value? Function method () {
              Return value.apply (origin, arguments)
            }: Value
          },
          Set (target, key, value, receiver) {
            If (key in target) return Reflect.set (target, key, value, receiver)
            Origin [key] = value
            Return true
          }
        })
      }

      Const bar = {
        N: 1,

        Add (i) {
          This.n + = i
        }
      }

      Const foo = {

        Set (n) {
          This.n = n | 0
        },

        Sub (i) {
          This.n - = i
        }

      }

      Const p = delegateProxy (foo, bar)

      Bar
      Foo
      P

      P.n //?
      P.add (1)
      P.n //?

      P.sub (2)
      P.n //?

      P.set (1)
      P.n //?

      P.n = 233
      P.n //?
      `` ``
### [Symbols] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

  symbol:

    - Uniqueness

    - immutable

    - not included in the object 'object.getOwnPropertyNames (obj) `and` object.keys (obj) `

    - safe (in some cases can be used as a private property `key`)

  > Want to give the object a signal, no longer difficult!

  * E.g.

    `` `Js
    // old
    Let obj = {
      Id: 1
    }

    Obj.id // 1
    Obj.id = 2
    Obj.id // 2
    `` ``

    `` `Js
    // new
    Let obj = {
      [Symbol ('id')]: 1
    }

    Obj [Symbol ('id')] // undefined
    Obj [Symbol ('id')] = 2
    Obj [Symbol ('id')] // undefined

    For (const k of Object.getOwnPropertySymbols (obj)) {
      Console.log (obj [k])
    }
    `` ``


### Math + Number + String + Array + Object APIs

  New APIs, data manipulation is more convenient.

  * E.g.

    `` `Js
    Number.EPSILON
    Number.isInteger (Infinity) // false
    Number.isNaN ("NaN") // false

    Math.acosh (3) // 1.762747174039086
    Math.hypot (3, 4) // 5
    Math.imul (Math.pow (2, 32) - 1, Math.pow (2, 32) - 2) // 2

    "Abcde" .includes ("cd") // true
    "Abc" .repeat (3) // "abcabcabc"

    Array.from (document.querySelectorAll ("*")) // Returns a real Array
    Array.of (1, 2, 3) // Similar to new Array (...), but without special one-arg behavior
    [0, 0, 0] .fill (7, 1) // [0,7,7]
    [1,2,3] .findIndex (x => x == 2) // 1
    ["A", "b", "c"]. Entries () // iterator [0, "a"], [1, "b"], [2, "c"
    ["A", "b", "c"]. Keys () // iterator 0, 1, 2
    ["A", "b", "c"]. Values ​​() // iterator "a", "b", "c"

    Object.assign (Point, {origin: new Point (0,0)})
    `` ``


### Binary and Octal Literals

  Binary `b`, octal` o` literally

  * E.g.

    `` `Js
    0b111110111 === 503 // true
    0o767 === 503 // true
    0x1f7 === 503 // true
    `` ``

### Promises

  Promises: more elegant asynchronous programming. To see more clearly the implementation of `Promise`, you can see this visual tool [promisees] (https://github.com/bevacqua/promisees).

  > In the face of asynchronous programming, `callback-hell` is the biggest criticism of JavaScript!

  * E.g.

    `` `Js
    // old
    GetProfileById (233, (err, res) => {
      If (err) throw err
      GetFollowing (233, (err, following) => {
        If (err) throw err
        GetFollowers (233, (err, followers) => {
          If (err) throw err
          GetStarred (233, (err, starred) => {
            If (err) throw err
            //
          })
        })
      })
    })
    `` ``

    `` `Js
    // new
    GetProfileById (233)
      .then (res => getFollowing (233))
      .then (res => getFollowers (233))
      .then (res => getStarred (233))
      .catch (err => console.log (err))
      // ...
    `` ``

  Guess guess

    0. * simple-promise.js *

      `` `Js
      Function loadImage (url) {
        Return new Promise ((resolve, reject) => {
          Const img = new Image ()

          Img.onload = function () {
            Resolve (img)
          }

          Img.onerror = function () {
            Reject (new Error ('Could not load image at' + url))
          }

          Img.url = url
        })
      }

      LoadImage ('https://nodejs.org/static/images/logo-header.png')
        .then (img => document.body.appendChild (img))
        .catch (err => console.log (err))
      `` ``

    0. * all.js *

      `` `Js
      Function delay (value, duration = 0) {
        Return new Promise ((resolve, reject) => {
          SetTimeout (() => resolve (value), duration)
        })
      }

      Let res = Promise.all ([
        Delay (10, 1),
        Delay (8, 2),
        Delay (6, 3),
        Delay (4, 4),
        Delay (2, 5),
        Delay (0, 6),
      ])

      Res.then (arr => {
        Console.log (arr) //?
      })
      `` ``

    0. * race.js *

      `` `Js
      Function delay (value, duration = 0) {
        Return new Promise ((resolve, reject) => {
          SetTimeout (() => resolve (value), duration)
        })
      }

      Let res = Promise.race ([
        Delay (10, 1),
        Delay (8, 2),
        Delay (6, 3),
        Delay (4, 4),
        Delay (2, 5),
        Delay (0, 6),
      ])

      Res.then (arr => {
        Console.log (arr) //?
      })
      `` ``

    0. * reduce.js *

      `` `Js
      Const reduce = (arr, cb, initialValue = 0) => {
        Return arr.reduce (cb, Promise.resolve (initialValue))
      }

      Const cb = (prev, curr) => prev.then (v => v + curr)

      Reduce ([1, 2, 3, 4, 5, 6, 7, 8, 9], cb)
        .then (res => {
          Console.log (res) //?
        })
      `` ``

### [Reflect API] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

  Reflective API: the object of the operation of the yuan, the effect of the opposite with the Proxy API

  * E.g.

    `` `Js
    Var O = {a: 1};
    Object.defineProperty (O, 'b', {value: 2});
    O [Symbol ('c')] = 3;

    Reflect.ownKeys (O); // ['a', 'b', Symbol (c)]

    Function C (a, b) {
      This.c = a + b;
    }
    Var instance = Reflect.construct (C, [20, 22]);
    Instance.c; // 42
    `` ``


### Tail Calls

  Optimize the tail recursive algorithm to ensure that the stack will not grow indefinitely, making the tail recursive algorithm safe.


## Quick experience

> For more than the new features, experience some of the environment, including the browser and Node.js


## Advanced application

> In-depth learning characteristics, application production

* Http://ramdajs.com/

* Https://github.com/cujojs/most

* Https://lodash.com/

* `Fs.readdir` problem

  - https://github.com/nodejs/node/issues/583

  - https://github.com/w3c/filesystem-api

* Https://github.com/kriskowal/gtor/#asynchronous-generator-functions


## compatible, transcoding

> Use the conversion tool to convert the ES6 + code to fit the browser or Node <v6


## other

* Http://es6.ruanyifeng.com

* Https://github.com/lukehoban/es6features

* Https://babeljs.io/docs/learn-es2015/

* Https://ponyfoo.com/articles/tagged/es6-in-depth

* Https://github.com/bevacqua/es6

* Https://github.com/DrkSephy/es6-cheatsheet

* Https://github.com/ericdouglas/ES6-Learning

* Https://github.com/addyosmani/es6-tools

* Https://github.com/bevacqua/promisees


## License

Authorization: [signed - non-commercial use] (https://creativecommons.org/licenses/by-nc/4.0/)

---

> [Fundon.me] (https://fundon.me) & nbsp; & middot; & nbsp;
> GitHub [@fundon] (https://github.com/fundon) & nbsp; & middot; & nbsp;
> Twitter [@_fundon] (https://twitter.com/_fundon)

[ES5]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_5_support_in_Mozilla

[ES6]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Mozilla

[ES7 and ES8]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_Next_support_in_Mozilla

[ES7]: http://www.ecma-international.org/ecma-262/7.0/index.html
