# JavaScript

⭐️ [Practical Ways to Write Better JavaScript](https://dev.to/taillogs/practical-ways-to-write-better-javascript-26d4)

[Array Distinct](https://codeburst.io/javascript-array-distinct-5edc93501dc4)
```
const arrayUniq = arrayNotUniq.filter((value, index, self) => {
        return self.indexOf(value) === index
    })
// es6
const arrayUniq = [...new Set(arrayNotUniq)]
```



## Node.js

Node.js has a built-in debug log method [stefanjudis](https://www.stefanjudis.com/today-i-learned/node-js-has-a-built-in-debug-method/) [Node.js](https://nodejs.org/api/util.html#util_util_debuglog_section)
