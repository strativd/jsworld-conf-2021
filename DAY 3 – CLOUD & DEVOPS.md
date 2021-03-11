# DAY 3 – CLOUD & DEVOPS


* [Developer Experience: Your documentation deserves more love!](#developer-experience-your-documentation-deserves-more-love)
  + [Four Pillars of Great Documentation](#four-pillars-of-great-documentation)
    - [Clear Structure](#clear-structure)
    - [Search Analytics](#search-analytics)
    - [Interactivity](#interactivity)
    - [User feedback](#user-feedback)
* [Build a social network with Serverless and GraphQL](#build-a-social-network-with-serverless-and-graphql)
  + [GraphQL](#graphql)
* [Security is not a Feature!](#security-is-not-a-feature)
  + [Vulnerabilities are everywhere](#vulnerabilities-are-everywhere)
* [Dungeons, Dragons, and Graph Databases](#dungeons-dragons-and-graph-databases)
  + [First, What's a Graph?](#first-whats-a-graph)
  + [Now, What's a Graph Database?](#now-whats-a-graph-database)
  + [Cypher Queries](#cypher-queries)
* [Containerized Deployments for your SPA and API](#containerized-deployments-for-your-spa-and-api)
  + ["Single Page Applications" & APIs](#single-page-applications--apis)
  + [Deplying with Dockerfiles](#deplying-with-dockerfiles)
  + [Deplyment Techniques](#deplyment-techniques)
  + [Okay, which deploy should I choose?](#okay-which-deploy-should-i-choose)
  + [Examples](#examples)



## Developer Experience: Your documentation deserves more love!

**▶️ [Watch video](https://www.youtube.com/watch?v=I4UkWp_mSUY)**

> Tech: Documentation
>
> We often treat documentation as a by-product of our offering. But wait a second. Where do developers spend most of their time? You’re right, digging your documentation to find an answer to their question. So, why not spend some time improving our documentation? In the end, developer experience matters more than ever before. Developers often choose between products based on the user-friendliness of the docs you offer. This talk provides you with love-filled ideas to take your documentation to the next level.
>
> **Michiel Mulders**
> Developer Advocate at Humanitec

- Where do developers spend most of their time...?
- The Four Pillars of Developer Documentation

### Four Pillars of Great Documentation

1. Clear Structure
2. Search Analytics
3. Interactivity
4. User Feedback

#### Clear Structure

1. Tutorials – learning from the start. A Complete solution! Example: Quickstart.
2. How-to Guides – problem guides (not a complete solution).
3. Explanations – don't deviate in your tutorials. Explanations should deviate.
4. Reference – to easily find more detailed information.
5. Glossary (optional) for more complex applications.

#### Search Analytics

Important for continuous improvement.

Success metrics:

- Searches per keyword
- Successful searches
- Unsuccessful searches are more important though!
- Click position – which result is showing up where?

Tools:

- [MeiliSearch](https://www.meilisearch.com/)
- [Algolia](https://www.algolia.com/)

#### Interactivity

Allow for safe exploration!

- Code playground or sandbox
- Provide test data or default accounts
- Advanced: allow developers to play with real data.

Example: Stripe Code Playground.

#### User feedback

Try to gather feedback from users **while they're using your product**.

- Feedback buttons or forms
- Comments section
- "Productboard" to capture user feedback, feature and content requests, and allow upvoting, etc.
- Advanced: User testing



## Build a social network with Serverless and GraphQL

**▶️ [Watch video](https://www.youtube.com/watch?v=9n_Hca0XsOk)**

> Tech: Serverless, GraphQL, AppSync, Lambda, Algolia
>
> Building a social network in under 4 weeks with Serverless and GraphQL
>
> You get great velocity without sacrificing quality and reliability when you combine Serverless and GraphQL. It’s really the best of both worlds.
>
> In this talk, Yan Cui shares his experience of building a new social network for university students in just 4 weeks, using AppSync, Lambda and Algolia.
>
> **Yan Cui**
> Developer Advocate at Lumigo

### GraphQL

Query language that uses queries and mutations to fetch and manipulate data, respectively.

GraphQL queries on the server require a middle-man to accept queries as text – at a single endpoint, like /graphql – parse the query, and then fetch and return data to the frontend.

Makes it easy to fetch related data without making multiple requests. For example: fetch all products and then each of the collections that the product belongs.

- With a REST API, that could require 100s or requests to multiple endpoints.
- GraphQL can fetch all required data from multiple resources with one nested request.



## Security is not a Feature!

**▶️ [Watch video](https://www.youtube.com/watch?v=YmfPSgidMyo)**

> Tech: Web App Security, XSS, XSRF
>
> I know we are front end developers but is also our duty to take care and stop delegating (or relegating) the security of our web apps. We handle a lot of sensitive information, but more importantly, we handle the user’s trust and we have to make the commitment of taking it seriously. This talk is an introduction to Web Apps security. We are going to review fundamentals, best practices, scenarios for developing secure web apps from scratch, and stop thinking of security as a feature.
>
> **Ignacio Anaya**
> Lead Open Source Engineer at Checkly

No perfect solution, hacks will happen, but we can be ready.

- Mitigate risk by **sandboxing** features.
- Security should be the default.

### Vulnerabilities are everywhere

Know your **input vectors** – all the ways that your app can accept data (query strings, cookies, etc.)

- **Assume the worst** and consider how anyone can hack the input.
- Use HTTPS.
- LTS – long-term support.

**Dependencies**.

- Every dependency has bugs, and those are your bugs now.
- Use Dependabot.
- Use frontend frameworks.

**SQL / No-SQL Injections**.

- Always use server-side validation!
- Sanitize all queries.
- ORM / ODM

**XSS** – cross-site scripting

- Always use server-side validation!
- Sanitize all queries.
- HTML encoding
- Frameworks!
- HTTPS reponse headers – `content-security-policy`, etc.

**DoS**

- Rate limiting.
- Proper error handling.
- Explicit crashes.
- Exponential Regex can crash a site.
- IP Banning.

**Sessions & Token** – stealing customer data.

- They should expire!
- Alow list or Deny list
- OAuth – OpenID
- Single Sign on services

**Passwords**

- Hash + salt (bcrypt) on server
- Enforce strong passwords
- Multi-factor authentication

**Sensitive Data**

- Never expose it to the browser!
- Encrypt & disable caching of sensitive data.



## Dungeons, Dragons, and Graph Databases

**▶️ [Watch video](https://www.youtube.com/watch?v=WJogrXBEPy8)**

> Tech: Graph Database, SQL Query, Coding Demo
>
> A graph database allows you to model DB relationships simply and intuitively with nodes and edges. Being schema-free, you can evolve your graph as you encounter new things such as traps or secret doors. And, using the Cypher query language, you can write elegant and easy to understand queries that find the best routes to get the stuff adventures desire most.
>
> **Guy Royse**
> Developer Advocate at Redis Labs

https://github.com/guyroyse/dnd-and-graph-databases

### First, What's a Graph?

> Mathematical connection of "nodes" and "edges"

Picture a dice as a 3D graph 🎲

- **Edges** are the 90 degree edges where the faces touch.
- **Nodes** are the corners; where edges meet each other.

With nodes and edges there are connections (edges) between information stores (nodes).

**Nodes & Edges have relationships.**

- "Directional" – which way can data flow?
- "Degrees" – how many relationships does a node have?

### Now, What's a Graph Database?

**Nodes**

- Represent items – tend to be nouns!
- They can have labels and attributes.
- They can stand alone!

**Edges**

- Represent connections – connecting two nodes.
  - Must have a type
  - Must have a connection
  - Must have a direction
  - Can have attributes
- Cannot exist without Nodes!

Example:

`(Shop) -▻ :contains -▻ (Product)`

(Node) ▻ :edge ▻ (Node)

`(s:shop)-[:contains]->(p:product)`

### Cypher Queries

Used to query graph databases, like Redis Graph.

`(r:room)-[:contains]->(m:monster)`

- Now `r` and `m` are assigned an can be used in the rest of the query for advanced logic.

```sql
MATCH (r:room)-[:contains]->(:monster)-[:guards]->(:treasure) RETURN r
```

> Cypher is kind of neat because its queries look sort of like a graph. Since nodes are represented as circles, when we `CREATE` or MATCH them, we wrap them in parentheses to suggest a circle. This idea is carried forward when we create nodes with edges.
>
> https://redislabs.com/blog/redisgraph-and-redis/

**EXAMPLES**

```sql

CREATE (:room { name: 'The Den of the Ogre King' })-[:contains]->(:monster { name: 'Ralph the Ogre King', xp: 1200 })

# The Dungeon
MATCH (d:dungeon) RETURN d.name

# All the Rooms
MATCH (r:room) RETURN r.name

# All the Monsters
MATCH (m:monster) RETURN m.name

# All the Treasure
MATCH (t:treasure) RETURN t.name, t.gp

# Rooms and Treasures
MATCH (r:room)-[:contains]->(t:treasure) RETURN r.name, t.name, t.gp

# Find Longest Path
MATCH p = (:dungeon)-[:has_entrance]->(:room)-[:leads_to*]->(:room)-[:has_exit]->(:dungeon) RETURN nodes(p), relationships(p), length(p) as l ORDER BY l DESC LIMIT 1

# Shortest Path to the Most Gold
MATCH (max:treasure) WITH max(max.gp) as maxgp MATCH (r:room)-[:contains]->(t:treasure) WHERE t.gp = maxgp WITH id(r) as dest_id MATCH p = (start:room)-[:leads_to*]->(stop:room) WHERE id(start) = 1 AND id(stop) = dest_id RETURN nodes(p), length(p) as len ORDER BY len ASC LIMIT 1
```



## Containerized Deployments for your SPA and API
**▶️ [Watch video](https://www.youtube.com/watch?v=_9oJeltLIg4)**

> Tech: SPA, API, Vue CLI, dotnet CLI, Kubernetes
>
> You've built a SPA and an API backend, and you're now looking to deploy with ease. Kubernetes is the natural fit, but where do we begin?
>
> We'll use the Vue CLI and the dotnet CLI to startup our codebases, then craft Dockerfiles to deploy these with ease in various configurations.
>
> Whether you'd rather deploy both parts together or scale different pieces separately, Docker can empower you to deploy your solutions at cloud scale.
>
> [**Rob Richardson**](https://robrich.org)
> Developer Evangelist at SingleStore

### "Single Page Applications" & APIs

Great separation of concerns! But more difficult to glue together...

### Deplying with Dockerfiles

- **What is Docker?** Docker is an ecosystem around Container Virtualization.
- **What are Containers?** Light-weight kernel virtualization.

**Docker**: A suite of command-line tools for creating, running, and managing containers.

Dockerfiles are "containers" that separate our concerns (frontend and backend) to connect to in development or production.

`$ docker run -p 3000` – to run docker containers on specified port.

### Deplyment Techniques

In each folder, we demonstrate one approach:

- **1-container-1-domain** - Deploy both SPA and back-end into a single container, using the back-end to host the front-end's static files.
- **2-containers-2-domains** - We put our website on https://www.example.com/ and our api on https://api.example.com/.
- **2-containers-1-domain** - We put both front-end and back-end into separate containers, but stitch them together into a single URL via a Kubernetes Ingress controller.
- **server-rendered-spa** - Visual Studio's New Project template hosts both pieces together and includes server-side processing for SPA pages.

___

### A – 1 container, 1 domain

SPA lives as static files within the same server as the API.

**PRODUCTION IMPLIMENTATION**

1. API adds static file hosting
2. **Single Dockerfile** builds both pieces
3. Final step copies SPA files into static folder. Example: /public

![1-container-1-domain](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/1-container-1-domain.png)

**DEVELOPMENT IMPLIMENTATION**

1. Webpack dev server proxies `/api` to the backend server

![2-containers-1-domain-dev](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/2-containers-1-domain-dev.png)

**HELPFUL WHEN...**

- Hosting on Heroku or Azure Web App
- Don't have an orchestrator
- Backend is a single monolyth

| PROS                                              | CONS                                          |
| ------------------------------------------------- | --------------------------------------------- |
| Easily deploy whole app to single hosting account | Can't scale front end and back end seperately |

___

### B – 2 containers, 2 domains

1. SPA is on `www.example.com`
2. API is on `api.example.com`

**IMPLIMENTATION**

1. API has white-list of allowed domains
2. SPA has hard-coded API domain
3. SPA app makes AJAX request
4. SPA browser makes OPTIONS request
5. API answers with CORS header
6. SPA browser validates CORS header
7. SPA browser completes real request

```
headers: {
  Access-Control-Allow-Origin: http://www.example.com
}
```

![2 containers 2 domains](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/2-containers-2-domains.png)

**HELPFUL WHEN...**

- Separate front-end and back-end teams
- Solid naming conventions between environments
- Consistent development tools

| PROS                                                      | CONS                                                         |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| Scale containers separately<br />Evolve pieces separately | Need different urls for each environment<br/>Developer settings may differ<br/>Rebuild images to inject new setting<br/>CORS headers are surprisingly difficult |

___

### C – 2 containers, 1 domain

1. SPA is on `www.example.com`
2. API is on `www.example.com/api/*`

**PRODUCTION IMPLIMENTATION**

**"Orchestrator"** controller proxies requests to each container.

- EX: Kubernetes (K8s) ingress controller orchestrating requests using a YAML file.

![2 containers 1 domain](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/2-containers-1-domain.png)

**DEVELOPMENT IMPLIMENTATION**

1. Webpack dev server proxies `/api` to backend Server

![2 containers 1 domain](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/2-containers-1-domain-dev.png)

_Similar to 1 container, 1 domain development setup_

**HELPFUL WHEN...**

- You have Kubernetes
- The SPA reaches out to one API
  - may be an API Gateway

| PROS                                                         | CONS                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Scale containers separately<br/>No hard-coded urls<br/>No CORS headers | Need kubernetes or other proxy<br/>Entire backend must be on one sub-<br/>domain or proxied to other services |

___

### D – Server-rendered SPA

1. SPA source lives in-process with API

EX: Next.js for React, and Nuxt for Vue.js

**IMPLIMENTATION**

1. API pre-renders SPA page
2. Browser boots SPA
3. SPA (on browser) picks up from there

![1 container 1 domain](https://robrich.org/slides/create-robust-deployments-for-spa-and-api/img/1-container-1-domain.png)

**HELPFUL WHEN...**

- You need Search Engine Optimization
- You don't want to keep up with the SPA tech
- You have a compatible back-end (usually Node.js)

| PROS                                                         | CONS                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Great for performance<br/>Great for SEO: full html delivered to browser | Best with a Node.js (JavaScript) back-end<br/>Generally doesn't use SPA's CLI |



### Okay, which deploy should I choose?

|               | 2 CONTAINERS                                                 | 1 CONTAINER                                                  |
| :------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| SINGLE DOMAIN | **K8s Ingress**<br />many microservices<br />"Kubernetes"    | **SPA in API folder**<br />few microservices or monolyth app<br />No orchestrator<br />*Heroku or Azure Web Apps* |
| SUBDOMAINS    | **BASE_URL + CORS**<br />separate teams<br />solid naming conventions |                                                              |



### Examples

[Example repo for each implementation](https://github.com/robrich/create-robust-deployments-for-spa-and-api)

- `dotnet` MVC API on the backend
- `vue` SPA on the frontend

https://robrich.org/presentation/2021/02/24/containerized-deployments-for-spa-and-api.aspx