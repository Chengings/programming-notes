# JavaScript

⭐️ [Practical Ways to Write Better JavaScript](https://dev.to/taillogs/practical-ways-to-write-better-javascript-26d4)

[Array Distinct](https://codeburst.io/javascript-array-distinct-5edc93501dc4)
```javascript
const arrayUniq = arrayNotUniq.filter((value, index, self) => {
        return self.indexOf(value) === index
    })
// es6
const arrayUniq = [...new Set(arrayNotUniq)]
```

⭐️ [JavaScript & Node.js Testing Best Practices](https://github.com/goldbergyoni/javascript-testing-best-practices)

[Writing a Simple MVC App in Plain JavaScript](https://www.taniarascia.com/javascript-mvc-todo-app/)

[void in JavaScript and TypeScript](https://fettblog.eu/void-in-javascript-and-typescript/) | [void operator
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void)

[The JavaScript Survival Guide](https://www.youtube.com/watch?v=9emXNzqCKyg)
// Highlight: closures and this

⭐️ [A Re-Introduction To Destructuring Assignment](https://www.smashingmagazine.com/2019/09/reintroduction-destructuring-assignment/)

⭐️ [Fireship's Javascript Iteration and Loops](https://fireship.io/snippets/javascript-loops-pro-tips/)

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
```
let nestedProp = obj.first && obj.first.second;
let nestedProp = obj.first?.second; // optional chaining
// equivalent
let temp = obj.first;
let nestedProp = ((temp === null || temp === undefined) ? undefined : temp.second);
```

Use `Intl.DateTimeFormat().resolvedOptions().timeZone` to get timezone. https://stackoverflow.com/a/34602679

## Node.js

📦
 - https://github.com/sindresorhus/awesome-nodejs#packages
 - pm2: process manager https://github.com/Unitech/pm2

---
Node.js has a built-in debug log method [stefanjudis](https://www.stefanjudis.com/today-i-learned/node-js-has-a-built-in-debug-method/) | [Node.js](https://nodejs.org/api/util.html#util_util_debuglog_section)

[It’s about time to embrace Node.js Streams](https://slides.com/lucianomammino/its-about-time-to-embrace-streams-node-manchjs)

## React

[Life cycle](https://busypeoples.github.io/post/react-component-lifecycle/)
