# JavaScript Conventions and Code Style

These are the conventions we teach at [PunchCode](https://punchcode.org/).

Some code snippets below are marked `YES` or `NO` — these are answering the question: _**Does this piece of code fall in line with the conventions we teach at PunchCode?**_ The right answer to how you should write code is ultimately how your company writes code. The consensus from members in our community is that if you write code the way we illustrate below, you should be accepted into and able to adapt to any workplace.

We use the default configurations of Prettier and ESLint (from create-react-app), except we add the following to our `.prettierrc` file:

```js
{ tabWidth: 3 }
```

𝒟𝑜𝓃'𝓉 𝒽𝒶𝓉𝑒 𝓂𝑒 𝒸𝓊𝓏 𝐼'𝓂 𝒷𝑒𝒶𝓊𝓉𝒾𝒻𝓊𝓁.

## Const vs Let vs Var

When you are first learning JavaScript, it is okay to use `var`, since many tutorials use `var`. Once you learn about `let` and `const` you should only use those two declarations exclusively.

**Use `const` for everything**... except if you know you want to update the value of that variable, then use `let`.

For example, we use `let` in this `for` loop because we are constantly incrementing the index, `i`:

```javascript
for (let i = 0; i < 10; i++) {
   // loop 10 times, incrementing the index (i) each time
}
```

You can realistically use `const` for every variable until you try to do something and get thrown an error and must use `let`. `const` prevents you from accidentally overwriting the value of a variable which is a common beginner bug.

## ES6 (Arrow) Functions vs Function Declarations

If your function has a name, use function declarations like this:

```javascript
function getBlogPostsByUser(userId) { } // YES
```

Not like this:

```javascript
const getBlogPostsByUser = (userId) => { } // NO
```

The function declaration above is shorter. But more importantly, it uses JavaScript's [function hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) language feature. The ES6 (arrow) function is not hoisted and must be declared before using it elsewhere in the code and is therefore more fragile—in this case, dependent on being in a certain position in the code in order to work. (A common beginner bug is declaring a `const` after the function is called earlier in the code—something that works with function declarations.)

Only use ES6 function syntax (once you've learned it) when used as an anonymous function. The following ES6 anonymous function inside of the filter method:

```javascript
const filteredPasswords = passwords.filter((password) => { // YES
   // do stuff here
})
```

Is preferable to this:

```javascript
const filteredPasswords = passwords.filter(function(password) { // NO
   // do stuff here
})
```

The ES6 syntax is shorter and easier to read here.

# How to name your variables

_This is also the convention for naming parameters in functions (which can be thought of and used as variables in that function)._

First, ask yourself, "what is the **data type** of the value I am storing?"

Consider these data types:

- String
- Object
- Number
- Array*
- Boolean
- Date*
- Function

## Strings and Objects

Name the variable something meaningful, narrow, and specific. What are you storing in this variable? Be specific. Try to reflect things that exist in the real world or would make sense to a layperson. Never write a single-letter variable or abbreviation. (Exceptions at the bottom.) Never write a variable that anyone would have the slightest difficulty interpreting—including you 6 months from now.

```javascript
const firstName = "Mike"
const user = {
   id: "16672b8b-6946-4016-b7b8-f450b911f69e",
   email: "test@gmail.com",
   password: "74ABC516649DFF36BE66F8D3D1AAB621022B6A4A",      
}
```

## Numbers

Use "number words": `total`, `length`, `width` `min`, `max`, `count`, or `numOf`.

```javascript
const minParticipants = 4
const tabWidth = 3
const totalChars = 240
const numOfRegistrants = 6
```

## Booleans

Prefix these variables with `is`, `can`, or `has`.

```javascript
const isErrorDisplayed = true
const canEdit = true
const hasAdminStatus = true
```

## Arrays

Give them a meaningful and specific name, but in plural form.

```javascript
const mostCommonPasswords = [
   "qwerty",
   "password",
   "111111",
   "12345678", 
   "abc123",
   "1234567",
   "password1",
]

const users = [
   {
      id: "16672b8b-6946-4016-b7b8-f450b911f69e",
      email: "test@gmail.com",
      password: "74ABC516649DFF36BE66F8D3D1AAB621022B6A4A",      
   },
   {
      id: "a575d85c-3907-4467-9512-b63d2dec8b20",
      email: "example@yahoo.com",
      password: "4B2B79B6F371CA18F1216461CFFEADDF6848A50E",      
   },
]

const activeMembers = [
   [
      "Mike", "Zetlow", 39
   ],
   [
      "Andrew", "Yasso", 35
   ],
   [
      "John", "Campbell", 44
   ]
]
```

### Iterating over arrays

Use the singular version of the array variable name in the function. For example when mapping over an array of objects that represents `users`, you are iterating over each `user`.

```javascript
const userFirstNames = users.map((user) => {
   return user.firstName
})
```

## Timestamps

When storing a JavaScript Date object or any date and time (often called a "timestamp") represented by a number or string, you can name it with the `At` suffix. The fact that this convention can be used on multiple data types is okay. It is primarily a convention to help you understand what it is you are working with.

```javascript
createdAt: 1591425642
updatedAt: "Fri Jun 05 2020 23:43:22 GMT-0700 (Pacific Daylight Time)"
nextEventAt: 202007101200
```

## Function names

As a general rule, function names should begin with a verb, followed by a noun. They should be meaningful, narrow, and specific like variable names.

```js
function resetTasks(date) { }
```

If a function does multiple things it is okay to describe those things. It is better to have a long and specific name than a short and ambiguous one.

From [Elements of Clojure](https://leanpub.com/elementsofclojure/read_sample):

>If a function takes an id and returns a binary payload, it should be called `getPayload`. If it takes an id and deletes the payload, it should be called `deletePayload`. If it takes an id, replaces the payload with a compressed version, and returns the result, it should be called `compressAndGetPayload`.

If you find your function name is too long and is doing too many things, break it into smaller functions that can be reused.

Functions that return the following data types:

 - String
 - Object
 - Number
 - Array
 - Boolean
 - Date

can use the conventions discussed earlier for variable names. Examples:

### Functions that return a string or object

```javascript
function getUserStatus(user) { }
function getUser(userId) { }
```
### Functions that return a number
Use your "number words" again: `total`, `length`, `width` `min`, `max`, `count`, or `num`. Prefix it with `get`

```javascript
function getNumOfBlogPosts(userId) { }
```

### Functions that return an array

Use a plural noun in the function name.

```js
function getTodaysUsers(date) { }
```

### Functions that return a boolean

Name the function like you do booleans, but prefix it with `check`

```javascript
function checkIsErrorDisplayed(errorMsg) { return }
function checkHasAdminStatus(user) { return }
function checkCanEdit(pageMode) { return }
```

### Functions that return a timestamp

Use the same `At` suffix convention we use in variable names.

```js
function getCreatedAt(blogPost) { }
```

### More function conventions

#### Functions that transform data

```javascript
function toSlug(str) { return str}
function toFriendlyDate(date) { return str }
function toDollars(num) { return num }
```

#### Functions that set state

```javascript
function setOpenModal() { }
```

## For loops

You can use `i` to represent the index of a `for` loop.
If you must use `for` loops inside of `for` loops, add a single digit, starting with the number 2. `i2` for example.

```javascript
for (let i = 0; i < users.length) {
   const user = users[i]
   for (let i2 = 0; i2 < user.length ) {
      const char = user[i2]
      const charCode = char.charCodeAt()
      console.log(charCode)
   }
}
```

## Abbreviations

You should try to name variables with a meaningful, narrow, and specific name that reflects what it is. But sometimes you will write utility functions that accept any string or any number, etc. and you can use the following abbreviations.

`char` - a single character, pluralized: `chars`
`str` - string, pluralized: `strings`
`num` - number, pluralized: `nums`
`obj` - object, pluralized: `objs`
`arr` - array, pluralized: `arrs`
`func` - function, pluralized: `funcs`
`bool` - boolean, pluralized: `bools`
`i` - index in a for loop
`e` - DOM event or [SyntheticEvent](https://reactjs.org/docs/events.html) wrapper in React

Avoid including these abbreviations on otherwise understandable variable names. For example:

```javascript
const firstNameStr = "Mike" // NO
const firstName = "Mike" // YES

const userObj = {} // NO
const user = {} // YES

const totalBlogPostsNum = 6 // NO
const totalBlogPosts = 6 // YES
const numOfBlogPosts = 6 // YES
```
## Id vs ID, Json vs JSON, and other acronyms

This is the most hotly contested style decision. It also matters least. Below we illustrate how and why we use one over the other in JavaScript.

Here is the convention we use:

```javascript
const userId = "a575d85c-3907-4467-9512-b63d2dec8b20" // YES
function toSafelyParsedJson(str) { } // YES
function getHtml(file) { } // YES
```

We do not do this:

```javascript
const userID = "a575d85c-3907-4467-9512-b63d2dec8b20" // NO
function toSafelyParsedJSON(str) { } // NO
function getHTML(file) { } // NO
```
Nerds [have battled](https://softwareengineering.stackexchange.com/questions/186277/should-the-variable-be-named-id-or-id) over this convention since the dawn of camelCase. We come down on the side of `Id` in JavaScript because a mistake many learners make is writing `document.getElementById()` as `document.getElementByID()` [which won't work](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById#Usage_notes).

Also, [if two acronyms are ever next to each other](https://en.wikipedia.org/wiki/Camel_case#Programming_and_coding) in a variable name (for whatever ungodly reason), you have a more readable and less mistake-prone variable name.

```js
function parseDBMXML(key) { } // NO
function parseDbmXml(key) { } // YES
```

We use this pattern for all acronyms to reinforce consistency.

## Beyond camelCase

We write variable in camelCase in JavaScript except for when we are working with non-JavaScript web development technologies. Instead of camelCase, write these names in kebab-case. This includes HTML, CSS, SCSS, file names, folder names.

```html
<input id="login-email-input">
```

```css
#brand-logo {
   width: 100px;
}
```

```
scrape-pages.js
```

React components are written in PascalCase, a requirement of the React library.
```javascript
import AppTemplate from "../uis/AppTemplate"
```

Development constants are variables that use the `const` syntax and are set by the developer, and are not altered by the program during execution. They often hold "[magic numbers](https://www.quora.com/What-is-a-magic-number-in-programming)" or other hard-coded values. They are written in SCREAMING_SNAKE_CASE.

```javascript
const SERVER_PORT: 3000
const SERVER_URL: "https//api.developers.vegas"
```
## References

These conventions were written with the help of [Las Vegas Developers](https://www.developers.vegas/) and the following resources:

- [The art of naming variables](https://hackernoon.com/the-art-of-naming-variables-52f44de00aad)
- [Good Variable Names](https://wiki.c2.com/?GoodVariableNames)
- [Naming your variables!](https://blog.usejournal.com/naming-your-variables-f9477ba002e9)
- [How to name variables](https://stackoverflow.com/questions/203618/how-to-name-variables)

## Notes
<sub>\* Yes, Array and Date are technically "constructed object instances" but it doesn't do anyone any good to know that. Rather, it's better to think of Array and Date as data types alongside the others.</sub>

<sub>Also, we can ignore `null` and `undefined` because we'll never/rarely create a variable to store only those values.</sub>


