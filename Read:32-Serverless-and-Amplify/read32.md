# Read: 32 - Serverless and Amplify

## Intro to Serverless

**What is Serverless Architecture? What are its Pros and Cons?**

* Serverless - is a cloud computing execution model where the cloud provider dynamically manages the allocation and provisioning of servers.
* Serverless application - runs in stateless compute containers that are event-triggered, ephemeral, and fully managed by the cloud provider.
* They are event-driven cloud-based systems where application development rely solely on a combination of third-party services, client-side logic and cloud-hosted remote procedure calls.

***Traditional vs. Serverless Architecture***

* Traditionally - applications have run on servers which you had to patch, update, and continuously look after late nights and early mornings due to all the unimaginable errors that broke your production.
* Serverless :

1. no longer need to worry about the underlying servers, and can be worked on at anytime.
2. Serverless is reduced cost.

* ``Downside is that Serverless`` functions are accessed only as private APIs, and to access these you must set up an API Gateway.
* 3rd Party Dependencies - you rely on libraries that are not built into the language or framework you use, so you must package these dependencies into the application itself.
* Setting up different environments for Serverless is as easy as setting up a single environment.
* Serverless computing has a hard 300-second timeout limit.
* Scaling process for Serverless is automatic and seamless, but there is a lack of control or entire absence of control.
* Functions as a Service (FaaS) - n implementation of Serverless architectures where engineers can deploy an individual function or a piece of business logic.
  * Key properties of FaaS: independent, server-side, logical functions
* They are also stateless, ephemeral, event triggered, scalable by default, and fully managed by a cloud vendor.
* A Serverless solution consists of a web server, Lambda functions (FaaS), security token service (STS), user authentication and database.
* Serverless platforms need infrastructures where they can be executed, provider agnostic frameworks provide a platform agnostic way to define and deploy Serverless code on various cloud platforms or commercial services.

## AWS Amplify Kool-Aid

***AWS Amplify***

* AWS Amplify - set of tools and services that can be used together or on their own, to help front-end web and mobile developers build scalable full stack applications, powered by AWS.
* AWS Can configure app backend and connect your app in minutes, deploy static web apps in a few clicks, and easily manage app content outside the AWS console.
* Amplify supports popular web frameworks including JavaScript, React, Angular, Vue, Next.js, and mobile platforms including Android, iOS, React Native, Ionic, Flutter.
* Benefits :

1. configure backend fast
2. seamlessly connect frontend
3. deploy in a few clicks
4. and easily manage content.

* Features and tools :

1. develop
2. deliver
3. manage

* Develop :

1. configure backend
2. connect your app
3. integrate UI compenets.

* Deliver :

1. connect repository
2. configure build settings
3. deploy your app.

* Manage :

1. invite team members
2. manage users
3. and manage content.

* Use cases :

1. onboarding flows
2. real-time collaboration
3. AI/ML
4. targeted campaigns.

## GraphQL Intro

***API (GRAPHQL)***

* GraphQL Transform provides a simple to use abstraction that helps you quickly create backend for your web and mobile applications on AWS, and define your application’s data model using the GraphQL Schema Definition Language (SDL) and the library handles converting your SDL definition into a set of fully descriptive AWS CloudFormation templates that implement your data model.
* GraphQL Transform simplifies the process of developing, deploying, and maintaining GraphQL APIs.
* Define your API using the GraphQL Schema Definition Language (SDL) and can then use automation to transform it into a fully descriptive cloudformation template that implements the spec.
* The transform also provides a framework through which you can define your own transformers as @directives for custom workflows.
* Create a GraphQL API :

  1. Run this command amplify init
  2. Select GraphQl
  3. When asked if you have a schema, say No
  4. Select one of the default samples; you can change this later
  5. Choose to edit the schema and it will open the new schema.graphql in your editor
  6. Save the file and hit enter in your terminal window. if no error messages are thrown this means the transformation was successful and you can deploy your new API.

* Test the API - go to the AWS AppSync console or run amplify mock api to try some of these queries in your new API query page.
* Update schema - open your project’s file, and then compile it with the command: ``amplify api gql-compile``.
* To push the updated changes use the command: amplify push.
* The transform libraries take a schema defined in the GraphQL Schema Definition Language (SDL) and converts it into a set of AWS CloudFormation templates and other assets that are deployed as part of amplify push.

* The Amplify CLI provides GraphQL directives to enhance your schema with additional capabilities, such as custom indexes, authorization rules, function triggers and more.
* Object types that are annotated with @model are top-level entities in the generated API.
* Objects annotated with @model are stored in Amazon DynamoDB and are capable of being protected via @auth, related to other objects via @connection, and streamed into Amazon Elasticsearch via @searchable.
* @model directive that allows you to easily define top level object types in your API that are backed by Amazon DynamoDB.
