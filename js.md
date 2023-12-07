# JavaScript

📚
 * The Modern JavaScript Tutorial https://javascript.info
 * [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
 * [Intl Explorer is a tool for experimenting and trying out the ECMAScript Internationalization API](https://www.intl-explorer.com/)

---

⭐️ [Practical Ways to Write Better JavaScript](https://dev.to/taillogs/practical-ways-to-write-better-javascript-26d4)

⭐️ [JavaScript & Node.js Testing Best Practices](https://github.com/goldbergyoni/javascript-testing-best-practices)

[Writing a Simple MVC App in Plain JavaScript](https://www.taniarascia.com/javascript-mvc-todo-app/)

[void in JavaScript and TypeScript](https://fettblog.eu/void-in-javascript-and-typescript/) | [void operator
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void)

[The JavaScript Survival Guide](https://www.youtube.com/watch?v=9emXNzqCKyg)
// Highlight: closures and this

⭐️ [A Re-Introduction To Destructuring Assignment](https://www.smashingmagazine.com/2019/09/reintroduction-destructuring-assignment/)

[Clone array](https://www.samanthaming.com/tidbits/35-es6-way-to-clone-an-array)
```javascript
const sheeps = ['🐑', '🐑', '🐑'];

// Old way
const cloneSheeps = sheeps.slice();

// ES6 way
const cloneSheepsES6 = [...sheeps];
```

[Compound values are always assigned/passed by reference-copy](https://stackoverflow.com/a/34522073)

Use `repeat` and `padStart` to solve Hackerrank's stairCase problem.
```javascript
for (let i = 1; i <= n; i++) {
    console.log("#".repeat(i).padStart(n));
}
````

Optional chaining `?.`, instead of causing an error if a reference is nullish (null or undefined), the expression short-circuits with a return value of `undefined`.
```javascript
let nestedProp = obj.first && obj.first.second;
let nestedProp = obj.first?.second; // optional chaining
// equivalent
let temp = obj.first;
let nestedProp = ((temp === null || temp === undefined) ? undefined : temp.second);
```

Use `Intl.DateTimeFormat().resolvedOptions().timeZone` to get timezone. https://stackoverflow.com/a/34602679

⭐️ [Natively Format JavaScript Numbers](https://elijahmanor.com/blog/format-js-numbers)

[The most modern Javascript I know](https://jott.live/markdown/new_js) // ⬇ new > es6 features at a glance
```js
class Thing {

  constructor(data) {
    this.data_ = data
    this.show_thing = true
    this.display_loop()
  }

  async display_loop() {
    while (this.show_thing) {

      this.display_thing()

      await new Promise((resolve) => {
        requestAnimationFrame(resolve)
      })
    }
  }

  display_thing() {
    const canvas = document.querySelector('#output_canvas')
    // ...
  }

  get data() {
    return this.data_
  }

}

const d = new Float32Array(128)
d.fill(11) // fill with the number 11
let t = new Thing(d)
```

### null vs. undefined

`null` represents the intentional absence of any object value. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null), [ECMAScript® 2022 Language Specification](https://tc39.es/ecma262/#sec-null-value)

`undefined` is used when a variable has not been assigned a value. [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined), [ECMAScript® 2022 Language Specification](https://tc39.es/ecma262/#sec-undefined-value)

[Dr. Axel Rauschmayer's undefined vs. null revisited](https://2ality.com/2021/01/undefined-null-revisited.html) // including weird 🙃 js behaviour, fun to read

### Loop & List

[Dr. Axel Rauschmayer's Looping over Arrays: for vs. for-in vs. .forEach() vs. for-of](https://2ality.com/2021/01/looping-over-arrays.html) // use "forEach" or "for of" if possible.

⭐️ [Fireship's Javascript Iteration and Loops](https://fireship.io/snippets/javascript-loops-pro-tips/)

[Array Distinct](https://codeburst.io/javascript-array-distinct-5edc93501dc4)
```javascript
const arrayUniq = arrayNotUniq.filter((value, index, self) => {
        return self.indexOf(value) === index
    })
// es6
const arrayUniq = [...new Set(arrayNotUniq)]
```

[Use `Object.entries()` to loop object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)
```javascript
for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}
```

---

## Node.js

📦
 - https://github.com/sindresorhus/awesome-nodejs#packages
 - pm2: process manager https://github.com/Unitech/pm2

---

Node.js has a built-in debug log method [stefanjudis](https://www.stefanjudis.com/today-i-learned/node-js-has-a-built-in-debug-method/) | [Node.js](https://nodejs.org/api/util.html#util_util_debuglog_section)

[It’s about time to embrace Node.js Streams](https://slides.com/lucianomammino/its-about-time-to-embrace-streams-node-manchjs)

⭐️ [How To Set Up An Express API Backend Project With PostgreSQL](https://www.smashingmagazine.com/2020/04/express-api-backend-project-postgresql/)
## React

[Life cycle](https://busypeoples.github.io/post/react-component-lifecycle/)

## Asynchronous

Script loading
- https://stackoverflow.com/a/52177827
- [Patterns for a Promises based initialization](https://jeremenichelli.io/2016/04/patterns-for-a-promise-based-initialization/) https://ghostarchive.org/archive/ZvdZS https://archive.today/2Al6g

## Web APIs

### Events

Pointer events are the modern method to handle input from a range of pointing devices, such as touchscreen, mouse, stylus etc.
- https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events
- https://javascript.info/pointer-events
- [Touch/pointer tests and demos](https://patrickhlauke.github.io/touch/)

Bubbling
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling
- https://javascript.info/bubbling-and-capturing#summary
