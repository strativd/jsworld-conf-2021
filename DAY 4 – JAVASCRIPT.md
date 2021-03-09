# DAY 4 – JavaScript


* [JavaScript/Web tooling now and tomorrow](#javascript-web-tooling-now-and-tomorrow)
  + [Developer Dilemma](#developer-dilemma)
  + [Solutions](#solutions)
* [The modern DXP](#the-modern-dxp)
  + [Digital Experience Platform](#dxp-digital-experience-platform)
  + [Drawbacks for Developers](#drawbacks-for-developers)
  + [Solution: JAMstack DXP](#solution-jamstack-dxp)
* [Third Age of Javascript](#third-age-of-javascript)
* [Composable components using React Context](#composable-components-using-react-context)
* [Building Considerate React Component APIs with TypeScript](#building-considerate-react-component-apis-with-typescript)
  + [Considerate React Component APIs](#considerate-react-component-apis)
  + [TypeScript](#typescript)
  + [Considerate TypeScript](#considerate-typescript)
  + [Tips](#tips)
* [The Rule of Least Power #ROLP](#the-rule-of-least-power-rolp)
  + [Rule of Least Power](#rule-of-least-power)
  + [Depower by Abstraction](#depower-by-abstraction)
  + [Depower by Convention](#depower-by-convention)
  + [Depower by Types](#depower-by-types)

## JavaScript/Web tooling now and tomorrow

> Tech: JavaScript Tooling, Web Tooling, Browser tooling
>
> We live in amazing times when it comes to browser tooling and open web tooling. Browsers aren't only a thing for end users, but also power our editors and can be automated to do a lot of work for us. In this session we'll take a look how the developer tools in browsers work, how to contribute and what's cooking to make developers more effective and prevent us from making mistakes before we make them.
>
> **Christian Heilmann**
> Principal Program Manager at Microsoft

### Developer Dilemma

**LOTS OF TOOLS TO ADOPT**

- Editor/IDE – development
- Browser – testing and tweaking
- Terminal – CI/CD, version control, build scripts

*None of this has to do with the actual code we WANT to learn...*

**SO WHAT?**

- web developers often get caught up in what tools to use instead of building great things.
- endless context switching between development tools which causes developer fatigue.
- we rely on our tools instead of learning the *why* behind differnet development techniques.

### Solutions

- **Console filtering** to only show what we're interested in
- **Issues panel** which houses development messages and suggestions
  - Also provides context on each issue with links to solutions and lines of code
- **Problems pane in VS Code** to catch problems before build
- **Live linting in VS Code** with links to more details
- `debugger` & `breakpoints` – provide the live state as your code changes the browser.
- Inspect > *Right-click element* > **"Break on..."** – pauses code execution when the DOM changes!
- **CSS browser tools**. For example, dedicated CSS flexbox debugging tool with illustrations.
- **"Microsoft Edge Tools for VS Code" extension**
  - IDE, browser, terminal together – combines all development tools!
  - Live browser (mostly): inspect, edit DOM & CSS, Network tab, etc.
- Network tab: *right-click* > **"Edit and resend..."** – UI to edit network requests live.
- **Dev Tools for Dev Tools** – see how Dev Tools are build and where bugs are coming from.



## The modern DXP

> Tech: DXP, JAMstack
>
> The Modern Digital Experience Platform - How JAMstack will change the world.
>
> **Tim Benniks**
> Principal Developer Advocate at Uniform

### Digital Experience Platform

- Combine multiple tools and services to create a platform.
  - Content management
  - email services
  - asset management
  - A/B Testing
  - Analytics
- Enterprise software (usually) chosen by marketing teams.

**EXAMPLES**: Drupal, Wordpress, Sitecore, Adobe AEM, **Shopify (for commerce)**

### Drawbacks for Developers

- **Origin based** – content delivery server that houses all other services – which make iteration tough.
- **High effort** – everything gets **deployed at once** which takes a long time and makes it tough to customzie.
- **Error prone** when we can't iterate often or quickly.
- **Vendor lock-in** so there's less choice.
  - Professionsl sevices and certifications are required to use their platform (ex: Salesforce)
- **EXPENSIVE** 💸

### Solution: JAMstack DXP

**Composed DXP** using "best of breed" – gather the best piece and host them together.

- Why buy a pre-made 🥪 when you can pick your own ingredients?

![https://screenshot.click/2021-54-1p2f7-abojy.png](https://screenshot.click/2021-54-1p2f7-abojy.png)

Composing our own stack with an assortment of tools – whatever works best for us or the client – stitching them together and delivering frontends using a CDN for the benefits of JAMstack.

*Sponsored: [Uniform](https://uniform.dev/) is an app that can orchestrate this process and stitch together other services.*



## Third Age of Javascript

> Tech: ES Modules, Polyglot Tooling, ES5, Node, ActionScript
>
> Every 10 years there is a changing of the guard in JavaScript.
>
> 1. The First Age started with Brendan Eich and ended with ActionScript.
> 2. The Second Age started in 2009 when npm, Node, and ES5 all gave new life to JavaScript.
> 3. In the Third Age we will see the confluence of a few megatrends – ES Modules, polyglot tooling, collapsing layers, and the slow death of IE.
>
> **Shawn Wang**
> Senior Developer Advocate at AWS Amplify

**"JavaScript modules will allow libraries to collapse into singular tools"**

- Faster for developers
- Less decision fatigue
- Less config for developers.

Examples:

[**Rome**](https://rome.tools/) – "Unifying the frontend development toolchain"

- "Rome is a linter, compiler, bundler, and [more](https://rome.tools/#development-status) for JavaScript, TypeScript, JSON, HTML, Markdown, and CSS."

[**Deno**](https://deno.land/) – "A secure runtime for JavaScript and TypeScript."

**"The death of JS"**

- More javascript tools are not using javascript – they're built with Rust, GO, etc.
- JavaScript tools build in other languages limits the amount of devs that can contribute to open source.



## Composable components using React Context

> Tech: reusable React Component, React Context
>
> If you've ever created a complex reusable React component one of the first questions you probably got asked is how can it be extended, right? The immediate solution will be to provide props as extension points but soon we will realize that no matter the amount of props we provide there is always going to be a case we forgot to cover. There is a better way ▻ React Context.
>
> **Danail Hadjiatanasov**
> Software Engineer at Material-UI

- **[Slides](https://slides.com/danailh/composable-components-using-react-context)**
- **[Code Demo](https://github.com/DanailH/jsworldconference-2021)**

`/App.jsx`

```jsx
import React from 'react';
import './App.css';
import {
  TabsProvider,
  TabHeader,
  TabContent
} from './components/Tabs';

function App() {
  return (
    <div className="container">
      <h2>Context demo</h2>
      <TabsProvider value="one">
        <div className="tabs">
          <div className="tab-list">
            <TabHeader value="one">
              one
            </TabHeader>
            <TabHeader value="two">
              two
            </TabHeader>
          </div>
          <div className="tab-content">
            <TabContent value="one">
              This is tab <em>ONE</em>!
            </TabContent>
            <TabContent value="two">
              This is tab <em>TWO</em>!
            </TabContent>
          </div>
        </div>
      </TabsProvider>
    </div>
  );
}

export default App;
```

`/components/Tabs.jsx`

```jsx
import * as React from 'react';
import PropTypes from 'prop-types';
import { TabsProvider, useTabsState } from './TabsContext';
import { TabsStateless } from './TabsStateless';

export const Tabs = React.memo(function Tabs(props) {
  const state = useTabsState();

  if (state !== null) {
    throw new TypeError('TabContext provided. Please use TabHeader and TabContent directly.');
  }

  return (
    <TabsProvider value={props.defaultTab}>
      <TabsStateless {...props} />
    </TabsProvider>
  )
});

Tabs.propTypes = {
  children: PropTypes.array.isRequired,
  defaultTab: PropTypes.string.isRequired,
};
```

`/components/TabsContext.jsx`

```jsx
import * as React from 'react';
import PropTypes from 'prop-types';

const TabsStateContext = React.createContext(null);
const TabsDispatchContext = React.createContext(null);

function tabsReducer(state, action) {
  switch (action.type) {
    case 'CHANGE_TAB': {
      return { activeTab: action.payload || state.activeTab };
    }
    default: {
      throw new Error(`Unhandled action type: ${action.type}`)
    }
  }
};

export function useTabsState() {
  return React.useContext(TabsStateContext);
};

export function useTabsDispatch() {
  return React.useContext(TabsDispatchContext);
};

export function TabsProvider(props) {
  const {
    children,
    value,
  } = props;
  const [ state, dispatch ] = React.useReducer(tabsReducer, {activeTab: value});

  return (
    <TabsStateContext.Provider value={state}>
      <TabsDispatchContext.Provider value={dispatch}>
        {children}
      </TabsDispatchContext.Provider>
    </TabsStateContext.Provider>
  );
};

TabsProvider.propTypes = {
  children: PropTypes.object.isRequired,
  value: PropTypes.string.isRequired,
};
```



## Building Considerate React Component APIs with TypeScript

> Tech: TypeScript, React Component API
>
> Perhaps we can shift our perspective about TypeScript from a bug catching tool to a developer experience tool that enables us to write reasonable and intuitive code interfaces. In this talk, you will learn how to think like a consumer and take advantage of basic and advanced TypeScript types to enhance the readability of your React component APIs.
>
> [**Daria Caraway**](https://www.dariacaraway.com/speaking/)
> Software Engineer at Workday

- **[Slides](https://github.com/darcar31/slides/blob/master/2021/JSWorld/BuildingConsiderateReactComponentAPIswithTypeScript-JSWorld2021.pdf)**

### Considerate React Component APIs

The Componenet API (calling components) should **reveal as much context as possible**.

- Avoid hidden context!
- Use proper naming for properties.
- Helpful for future developers – that could be you when you have to revisit the codebase later...

### TypeScript

- "Superset of JavaScript" which means it doesn't change the Javascript – it adds types during development.
- Types help catch bugs at build time instead of run time, so that you catch bugs before your users.

***It's a great communication tool for Developers!***

- IDE / code editors now provide auto-complete in development if used properly...

### Considerate TypeScript

Type script can be loose or strict. It's important to **provide as much context as possible** when naming and typing your properties.

- avoid primitive types and short forms wherever possible
- replace primitive types (`string`) with unions for more context (`'large' | 'medium' | 'small'`)
- `Partial<T>` Type – returns parts of the parent type. Ex: only some properties.
- `Omit<T>` Type – returns the parent type without specific details. Ex: omit some properties.
  - `<T>` is a generic type and provides more context to functions.

*Incorrect or misleading types can be worse than no types at all!*

### Tips

- Complex Type structures is a good sign that you should rethink the data needs instead.
- Be considerrate: test your componenets like a consumer.
  - Think of your code as a consumable API. How will your "users" figure out what the API requires?



## The Rule of Least Power #ROLP

> Tech: ROLP, Code Writing
>
> When writing computer programs, one is often faced with a choice between multiple ways to express a condition, or to perform an operation, or to solve some problem. The "Rule of Least Power" (extended) suggests choosing the least powerful way suitable for a given purpose.
>
> **Jason Yu**
> Frontend Engineer at Attest

### Rule of Least Power

How to choose technologies when solving a problem.

> "Power is directly related to the number of ways that you can express the same thing."
>
> *[OPINION – take this article with a pinch of salt...](https://dev.to/ycmjason/writing-cleaner-code-with-the-rule-of-least-power-rolp-4kkk)*

For example: You can write JavaScript (powerful) many ways to build a simple (less powerful) JSON structure.

**THE TRADE OFF**

More issues can be introduced with more power (options === complexity).

Depowering – removing complexity – is **often more readable** as well.

### Examples

```js
// More powerful: RegExp.prototype.test
/hi/.test(str)
// Less powerful: String.prototype.includes
str.includes('hi')
```

```js
// More powerful: Array.prototype.reduce
['a', 'b', 'c'].reduce((acc, key) => ({
  ...acc,
  [key]: null
}), {})
// Less powerful: Object.fromEntries + Array.prototype.map
Object.fromEntries(['a', 'b', 'c'].map(key => [key, null]))

```

```js
// More powerful: RegExp.prototype.test
/^hi$/.test(str)
// Less powerful: ===
str === 'hi'

// More powerful: RegExp.prototype.test
/^hi/.test(str)
// Less powerful: String.prototype.startsWith
str.startsWith('hi')

// More powerful: RegExp.prototype.test
/hi$/.test(str)
// Less powerful: String.prototype.endsWith
str.endsWith('hi')


/// More powerful: Array.protype.reduce
xs.reduce((x, y) => x > y ? x : y, -Infinity)
// Less powerful: Math.max
Math.max(...xs)

// More powerful: Array.prototype.reduce
parts.reduce((acc, part) => ({ ...acc, ...part }), {})
// Less powerful: Object.assign
Object.assign({}, ...parts)


// More powerful: Object.assign - can mutate first object
Object.assign({}, a, b)
// Less powerful: Object spread
{ ...a, ...b }


// More powerful: function - have its own `this`
function f() { ... }
// Less powerful: arrow function
const f = () => {...}

// More powerful: without destructure - who knows what the function will
//                                      do with the universe
const f = (universe) => { ... }
// Less powerful - f only needs earth
const f = ({ earth }) => { ... }

```

![https://screenshot.click/2021-20-1k8ky-tm75u.png](https://screenshot.click/2021-20-1k8ky-tm75u.png)

![https://screenshot.click/2021-21-6w2tc-ntg2p.png](https://screenshot.click/2021-21-6w2tc-ntg2p.png)

### Depowering

Take the "power" out of your code to make it more readable and less error-prone.

#### Depower by Abstraction

Basically reducing your code to functions.

```js
const sum = (xs) => xs.reduce((x1, x2) => x1 + x2, 0))
```

```js
const minBy = (xs, getN) => {
  const ns = xs.map(x => getN(x));
  return xs[ns.indexOf(
    Math.min(...ns);
  )]
}
```

```js
/* MODULES */
pathToRegExp('/hello/:name'); //=> compiled to: /^\/hello\/(?:([^\/]+?))\/?$/i
```

`!!x && f(x)` is common pattern to make sure `x` is truthy before calling `f(x)`.

```js
// Maybe a = Just a | Nothing
const Maybe = x => !!x ? Just(x) : Nothing()

const Just = x => ({
  map: f => Maybe(f(x))
})

const Nothing = () => ({
  map: f => Nothing()
})

return Maybe(x).map(f).map(g)
```



#### Depower by Convention

Ie. Styleguides – [Shopify Javascript Guide](https://github.com/Shopify/javascript)

- Establish **code conventions** across development teams
- Example: only use `map / filter / reduce` if you're going to use the value returned.
  - Otherwise use `forEach` and developers know what to expect.

#### Depower by Types

The last example is depowering via types.

```ts
/* TypeScript Depowering JavaScript */
type Person = {
  name: string
  age: number
  height: number
  weight: number
}

// More powerful - is f going to do anything with the person?
const f = (person: Person) => { ... }
// Less powerful - f only needs the name. But will it mutate it?
const f = (person: Pick<Person, 'name'>) => { ... }
// Even less powerful - f only reads the name from the person
const f = (person: Readonly<NamedThing>) => { ... }
```


