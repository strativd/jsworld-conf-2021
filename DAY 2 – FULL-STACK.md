# DAY 2 – FULL-STACK

* [Introduction to Fastify.io for Node.js](#introduction-to-fastifyio-for-nodejs)
  + ["Monolithic" architecture](#monolithic-architecture)
  + [Fastify architecture](#fastify-architecture)
  + [Serverless functions](#serverless-functions)
* [Testing Legacy Frontend Apps](#testing-legacy-frontend-apps)
  + [Why implement tests?](#why-implement-tests)
  + [How to start testing?](#how-to-start-testing)
  + [When do we test?](#when-do-we-test)
  + [How do we test?](#how-do-we-test)
* [Magic Authentication: The Missing LEGO Piece](#magic-authentication-the-missing-lego-piece)
  + [No Password Auth](#no-password-auth)
* [Headless eCommerce with Next.js](#headless-ecommerce-with-nextjs)
  + [Headless](#headless)
  + [Headless Commerce](#headless-commerce)
  + [Example](#example)
  + [Why Headless?](#why-headless)

## Introduction to [Fastify.io](https://www.fastify.io/) for Node.js
> Tech: Fastify, Node.js, Live-Coding
>
> Fastify is a web framework for Node.js that has a great satisfaction across developers with a 89% rating in the last state of javascript. Fastify combines an amazing developer experience with top of the class performance, with minimal reduction on top of Node.js core.
>
> **Matteo Collina**
> Technical Director at Nearform

### "Monolithic" architecture

- Ex: MEAN, MERN, Ruby on Rails
- Often three layers on the backend: **Model, View, Controller**.
- "Monolithic" architecture – very difficult to migrate architecture and Models often grow rapidly.

### Fastify architecture

- NO MVC; microservices instead – **features as plugins**!
- Each feature can be decomposed into its own plugin!
- Virtual Machine for Plugins. Plugins/features wach have separate context.
- Request "Lifecycles" (for example: authentication, parsing, response handlers).

### [Serverless functions](https://www.fastify.io/docs/latest/Serverless)

Run serverless applications and REST APIs using your existing Fastify application.

- [AWS Lambda](https://www.fastify.io/docs/latest/Serverless/#aws-lambda)
- [Google Cloud Run](https://www.fastify.io/docs/latest/Serverless/#google-cloud-run)
- [Netlify Lambda](https://www.fastify.io/docs/latest/Serverless/#netlify-lambda)
- [Vercel](https://www.fastify.io/docs/latest/Serverless/#vercel)

**Google Cloud Run**

> Google Cloud Run is a serverless **container** environment. It's primary purpose is to provide an infrastructure-abstracted environment to run arbitrary containers. As a result, Fastify can be deployed to Google Cloud Run with little-to-no code changes from the way you would write your Fastify app normally.

```js
function build() {
  const fastify = Fastify({ trustProxy: true })
  return fastify
}

async function start() {
  // Google Cloud Run will set this environment variable for you, so
  // you can also use it to detect if you are running in Cloud Run
  const IS_GOOGLE_CLOUD_RUN = process.env.K_SERVICE !== undefined

  // You must listen on the port Cloud Run provides
  const port = process.env.PORT || 3000

  // You must listen on all IPV4 addresses in Cloud Run
  const address = IS_GOOGLE_CLOUD_RUN ? "0.0.0.0" : undefined

  try {
    const server = build()
    const address = await server.listen(port, address)
    console.log(`Listening on ${address}`)
  } catch (err) {
    console.error(err)
    process.exit(1)
  }
}

module.exports = build

if (require.main === module) {
  start()
}
```



## Testing Legacy Frontend Apps
> Tech: Frontend Testing, Page Speed, YSlow, Cypress, Jasmine
>
> Nobody wants to work with Legacy Code. Yet it’s what many of us do. Complexity in frontend development grew rapidly in the last years. The habit of writing tests did not. Now they are everywhere: massive software systems without any tests in the frontend.
>
> **Mirjam Bäuerlein**
> Frontend Developer at BRYTER

### Why implement tests?

**BENEFITS**

- Futureproof
- Extensibilty
- Refactor easier
- Reduce bugs long-term
- Find bugs before users
- *Add new features quickly and safely!*

### How to start testing?

**SELLING TESTING**

- **Make writing tests easy.** Provide examples to work with. Dive in and own the project!
- **Make a business case.** It saves money! Reduces downtime.

**GETTING STARTED**

- **Component library.** Move reusable code into a shared repo.
- **Faster UI tests.** Run more tests (upon build, efor example).
- **Error tracking.** Find bugs before your users.

**WORKFLOW**

- Tests before commit.
- Tests before build.
- Tests as part of code review.
- Create issues for refactoring.

### When do we test?

- **Test when you find a bug** to make sure it doesn't happen again in the future.
- **Test before you start coding** to have a clear definiton of your goal.
- Create tests when your team is idle.

### How do we test?

New feature time, woo! (╯°o°)╯

1. Create a failing test. ⛔
2. Create a success test. ✅
3. Refactor required code first.
4. Export functionality for your new feature if you can to separate concerns.

**TIPS**

- Separate new code from old code if possible. Keep testing separate.
- **Characterising / Pinning Test**: create your tests before you code to clearly define what you want to return.
- Testing won't feel worth it right away, but it pays off over time with more and more tests!



## [Magic Authentication](https://magic.link/), The Missing LEGO Piece
> Tech: JamStack, Magic Authenticaiton
>
> Sean will be giving an introduction to Magic passwordless authentication and how it enables developers to effortlessly build more feature-rich Jamstack applications with just a few lines of code.
>
> **Sean Li**
> CEO at Magic

### No Password Auth

- Magic: One SDK for passwordless login, fully customizable:
  - Email login – click link in email
  - Social login – Google, Github, etc.
  - WebAuthn – log in with your web app or with biometrics (Touch ID)

[How to Build Magic Link in 5 Minutes](https://magic.link/posts/hello-world)

```html
<!-- Install Magic SDK -->
<script src="https://cdn.jsdelivr.net/npm/magic-sdk/dist/magic.js"></script>
```

```js
/* Initialize Magic Instance */
const magic = new Magic('YOUR_LIVE_PUBLISHABLE_API_KEY');
```

```jsx
/* Implement Login Handler */
const handleLogin = async e => {
  e.preventDefault();
  const email = new FormData(e.target).get('email');
  const redirectURI = `${window.location.origin}/callback`; // 👈 This will be our callback URI
  if (email) {
    /* One-liner login 🤯 */
    await magic.auth.loginWithMagicLink({ email, redirectURI }); // 👈 Notice the additional parameter!
    render();
  }
};

/* Implement Logout Handler */
const handleLogout = async () => {
  await magic.user.logout();
  render();
};
```



## Headless eCommerce with Next.js
> Tech: Storyblok CMS, Next.js Commerce, Headless CMS
>
> Imagine combining a world-class editing experience with a beautiful eCommerce storefront. The result? Everyone is happy:
>
> - Customers experience a fast and seamless experience
> - Managers get rapid and reusable development
> - Editors are able to edit content easily any time they want
> - Developers can code without technical constraints
>
> This talk will show how to connect Next.js commerce with Storyblok CMS and deliver value to all of these players. It will explain the advantages of connecting two headless systems for creating flexible storefronts that work for everyone.
>
> **Lisi Linhart**
> Developer Experience Engineer at Storyblok

### Headless

"Separating the backend from the frontend"

- Return data only so that any frontend can be used to consume the backend.
- API-first approach

### Headless Commerce

[Headless commerce explained in 5 minutes](https://www.storyblok.com/mp/headless-commerce)

> In this approach, the data (products, blogs, etc.) is created only once in the back-end, which then can be delivered to any number of front-ends (websites, apps, IoT, etc.) through APIs.

**Headless commerce** provides content management dashboard to update the shop with an API that returns content to the frontend view.

- **3 layers**: Ecommerce Platform (shop logic) + CMS (editing content) + frontend (customer UI)

**Monolithic commerce** where the front-end and the back-end are locked together.

- Generally speaking, this means the presentational layer (front-end) usually has limited customization capabilities as it is tied to the back-end. 

### Example

*Storyblok supports a Shopify integration as well.*

> [How to Build a Storefront with Next.js and BigCommerce](https://www.storyblok.com/tp/storefront-next-bigcommerce)
>
> In this tutorial, you will build a Storefront connecting the **Storyblok, BigCommerce and [Next.js Commerce](https://nextjs.org/commerce) systems**. Take a look at the end result demo: [nextjs-bigcommerce-starter.vercel.app](https://nextjs-bigcommerce-starter.vercel.app/)

1. Add Storyblok (CMS & live editor) to Next.js (frontend)
2. Create dynamic components for content editing
3. Add products in Storyblok from commerce provider

### Why Headless?

- Manage shop on multiple channels
- Use any tech stack you feel comfortable with – just consume the content
- Performance & security with JAMstack (static assets)
- Flexible customization

