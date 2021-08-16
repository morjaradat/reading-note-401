# review: Intro to Serverless

***What is Serverless?***

* Serverless is a cloud computing execution model where the cloud provider dynamically manages the allocation and provisioning of servers.
* A serverless application runs in stateless compute containers that are event-triggered, ephemeral (may last for one invocation), and fully managed by the cloud provider.
* Pricing is based on the number of executions rather than pre-purchased compute capacity.
* Serverless applications are event-driven cloud-based systems where application development rely solely on a combination of third-party services, client-side logic and cloud-hosted remote procedure calls (Functions as a Service).
* some of the currently available cloud services:
  * AWS Lambda
  * Google Cloud Functions
  * Azure Functions
  * IBM OpenWhisk
  * Alibaba Function Compute
  * Iron Functions
  * Auth0 Webtask
  * Oracle Fn Project
 *Kubeless

***Traditional vs. Serverless Architecture***

* serverless don't need to be patch every year like the Traditional.
* Pricing - of serverless is more less than the traditional.
* Networking - The downside is that Serverless functions are accessed only as private APIs(To access these you must set up an API Gateway).
* 3rd Party Dependencies - Without system-level access, you must package these dependencies into the application itself (applications with few dependencies, Serverless is the winner; for anything more complex, Traditional Architecture is the winner).
* Environments - for Serverless is as easier than traditional way .
* Timeout - With Serverless computing, there’s a hard 300-second timeout limit and Too complex or long-running functions aren’t good for Serverless.
* Scale - Scaling process for Serverless is automatic and seamless, but there is a lack of control or entire absence of control.
* Functions as a Service (FaaS) - FaaS is an implementation of Serverless architectures where engineers can deploy an individual function or a piece of business logic ;They start within milliseconds (~100ms for AWS Lambda) and process individual requests within a 300-second timeout imposed by most cloud vendors.

----------------
***Principles of FaaS:***

1. Complete management of servers
2. Invocation based billing
3. Event-driven and instantaneously scalable

* Key properties of FaaS: Independent, server-side, logical functions
* FaaS are similar to the functions you’re used to writing in programming languages, small, separate, units of logic that take input arguments, operate on the input and return the result.

----------------

* Stateless - With Serverless, everything is stateless, you can’t save a file to disk on one execution of your function and expect it to be there at the next ; Any two invocations of the same function could run on completely different containers under the hood.
* Ephemeral - FaaS are designed to spin up quickly, do their work and then shut down again.
* Event-triggered - Although functions can be invoked directly, yet they are usually triggered by events from other cloud services such as HTTP requests, new database entries or inbound message notifications.
* Scalable by default - With stateless functions multiple containers can be initialised, allowing as many functions to be run.
* Fully managed by a Cloud vendor - offering typically supports a range of languages and runtimes e.g. Node.js, Python, .NET Core, Java.

***The Serverless App***

* A Serverless solution consists of a web server, Lambda functions (FaaS), * security token service (STS), user authentication and database.
* Client Application — The UI of your application is rendered client side in Modern Frontend Javascript App which allows us to use a simple, static web server.
* Web Server - Amazon S3 provides a robust and simple web server. All of the static HTML, CSS and JS files for our application can be served from S3.
* Lambda functions (FaaS) — They are the key enablers in Serverless architecture.
* Security Token Service (STS) - generates temporary AWS and are used by the client application to invoke the AWS API.
* User Authentication - AWS Cognito is an identity service which is integrated with AWS Lambda.
* Database - AWS DynamoDB provides a fully managed NoSQL database.

----------------

### Benefits of Serverless Architecture

***From business perspective***

1. The cost incurred by a serverless application is based on the number of function executions, measured in milliseconds instead of hours.
2. Process agility: Smaller deployable units result in faster delivery of features to the market, increasing the ability to adapt to change.
3. Cost of hiring backend infrastructure engineers goes down.
Reduced operational costs

***From developer perspective***

1. Reduced liability, no backend infrastructure to be responsible for.
2. Zero system administration.
3. Easier operational management.
4. Fosters adoption of Nano-services, Micro-services, SOA Principles.
5. Faster set up.
6. Scalable, no need to worry about the number of concurrent requests.
7. Monitoring out of the box.
8. Fosters innovation.

***From user perspective***

1. If businesses are using that competitive edge to ship features faster, then customers are receiving new features quicker than before.
2. It is possible that users can more easily provide their own storage backend(i.e Dropbox, Google Drive).
3. It’s more likely that these kinds of apps may offer client-side caching, which provides a better offline experience.

### Drawbacks of Serverless Architecture

***From business perspective***

1. Reduced overall control.
2. Vendor lock-in requires more trust for a third-party provider.
3. Additional exposure to risk requires more trust for a third party provider.
Security risk.
4. Disaster recovery risk.
5. Cost is unpredictable because the number of executions is not predefined.
6. All of these drawbacks can be mitigated with open-source alternatives but at the expense of cost benefits mentioned previously.

***From developer perspective***

1. Immature technology results in component fragmentation, unclear best-practices.
2. Architectural complexity.
3. The discipline required against function sprawl.
4. Multi-tenancy means it’s technically possible that neighbour functions could hog the system resources behind the scenes.
5. Testing locally becomes tricky.
6. Significant restrictions on the local state.
7. Execution duration is capped.
8. Lack of operational tools

***From user perspective***

1. Unless architected correctly, an app could provide a poor user experience as a result of increased request latency.

### Serverless Frameworks

* Serverless Framework (Javascript, Python, Golang)
* Apex (Javascript)
* ClaudiaJS (Javascript)
* Sparta (Golang)
* Gordon (Javascript)
* Zappa (Python)
* Up (Javascript, Python, Golang, Crystal)

## GraphQL @connection section

***Add relationships between types***

***@connection***

* The @connection directive enables you to specify relationships between @model types.
* supports one-to-one, one-to-many, and many-to-one relationships.

* Definition :

```
directive @connection(keyName: String, fields: [String!]) on FIELD_DEFINITION
```

* Relationships between types are specified by annotating fields on an @model object type with the @connection directive.
* The fields argument can be provided and indicates which fields can be queried by to get connected objects.
* The keyName argument can optionally be used to specify the name of secondary index.

*** Has one for one-to-one relationship***

* we can write it by add   team: Team @connection like :

```
type Project @model {
  id: ID!
  name: String
  team: Team @connection
}

type Team @model {
  id: ID!
  name: String!
}
```

* OR

```
 type Project @model {
  id: ID!
  name: String
  teamID: ID!
  team: Team @connection(fields: ["teamID"])
}

type Team @model {
  id: ID!
  name: String!
}
```

* The connection between them :

```
mutation CreateProject {
  createProject(input: { name: "New Project", teamID: "a-team-id"}) {
    id
    name
    team {
      id
      name
    }
  }
}
```

***Has many***

```
type Post @model {
  id: ID!
  title: String!
  comments: [Comment] @connection(keyName: "byPost", fields: ["id"])
}

type Comment @model
  @key(name: "byPost", fields: ["postID", "content"]) {
  id: ID!
  postID: ID!
  content: String!
}
```

```
mutation CreatePost {
  createPost(input: { id: "a-post-id", title: "Post Title" } ) {
    id
    title
  }
}

mutation CreateCommentOnPost {
  createComment(input: { id: "a-comment-id", content: "A comment", postID: "a-post-id"}) {
    id
    content
  }
}
```

* The connection between them :

```
query getPost {
  getPost(id: "a-post-id") {
    id
    title
    comments {
      items {
        id
        content
      }
    }
  }
}
```

***Belongs to represent one-to-many relationships***

```
type Post @model {
  id: ID!
  title: String!
  comments: [Comment] @connection(keyName: "byPost", fields: ["id"])
}

type Comment @model
  @key(name: "byPost", fields: ["postID", "content"]) {
  id: ID!
  postID: ID!
  content: String!
  post: Post @connection(fields: ["postID"])
}
```

```
mutation CreatePost {
  createPost(input: { id: "a-post-id", title: "Post Title" } ) {
    id
    title
  }
}

mutation CreateCommentOnPost1 {
  createComment(input: { id: "a-comment-id-1", content: "A comment #1", postID: "a-post-id"}) {
    id
    content
  }
}

mutation CreateCommentOnPost2 {
  createComment(input: { id: "a-comment-id-2", content: "A comment #2", postID: "a-post-id"}) {
    id
    content
  }
}
```

* The connection between them :

```
query GetCommentWithPostAndComments {
  getComment( id: "a-comment-id-1" ) {
    id
    content
    post {
      id
      title
      comments {
        items {
          id
          content
        }
      }
    }
  }
}
```

***Many-to-many connections***

* You can implement many to many using two 1-M @connections, an @key, and a joining @model.

```
type Post @model {
  id: ID!
  title: String!
  editors: [PostEditor] @connection(keyName: "byPost", fields: ["id"])
}

# Create a join model and disable queries as you don't need them
# and can query through Post.editors and User.posts
type PostEditor
  @model(queries: null)
  @key(name: "byPost", fields: ["postID", "editorID"])
  @key(name: "byEditor", fields: ["editorID", "postID"]) {
  id: ID!
  postID: ID!
  editorID: ID!
  post: Post! @connection(fields: ["postID"])
  editor: User! @connection(fields: ["editorID"])
}

type User @model {
  id: ID!
  username: String!
  posts: [PostEditor] @connection(keyName: "byEditor", fields: ["id"])
}
```

* bidirectional many-to-many which is why two @key calls are needed on the PostEditor model. You can first create a Post and a User, and then add a connection between them with by creating a PostEditor object .

```
mutation CreateData {
  p1: createPost(input: { id: "P1", title: "Post 1" }) {
    id
  }
  p2: createPost(input: { id: "P2", title: "Post 2" }) {
    id
  }
  u1: createUser(input: { id: "U1", username: "user1" }) {
    id
  }
  u2: createUser(input: { id: "U2", username: "user2" }) {
    id
  }
}

mutation CreateLinks {
  p1u1: createPostEditor(input: { id: "P1U1", postID: "P1", editorID: "U1" }) {
    id
  }
  p1u2: createPostEditor(input: { id: "P1U2", postID: "P1", editorID: "U2" }) {
    id
  }
  p2u1: createPostEditor(input: { id: "P2U1", postID: "P2", editorID: "U1" }) {
    id
  }
}
```

* The query :

```
query GetUserWithPosts {
  getUser(id: "U1") {
    id
    username
    posts {
      items {
        post {
          title
        }
      }
    }
  }
}
```

***Alternative definition***

* The above definition is the recommended way to create relationships between model types in your API.
* This involves defining index structures using @key and connection resolvers using @connection.

```
directive @connection(name: String, keyField: String, sortField: String, limit: Int) on FIELD_DEFINITION
```

***Limit***

* The default number of nested objects is 100. You can override this behavior by setting the limit argument.

***Generates***

* In order to keep connection queries fast and efficient, the GraphQL transform manages global secondary indexes (GSIs) on the generated tables on your behalf when using @connection.
