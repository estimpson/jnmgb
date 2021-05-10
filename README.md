# jnmgb
## Jest, Nest, Mongoose, GraphQL, Blazor WASM

This repository serves as a demonstration project for a web-based line of business application.  It utilizes some of the more popular web technologies of today to deliver a dependable, scalable, and cohesive architecture, with end-to-end testing, SOLID object oriented coding practices, and suitability for large-scale projects as primary concerns.

A web-based line of business application has at minimum these three tiers:
1. Data repository
1. Web API
1. Client front end

This project relies on MongoDB as the data repository, hosted on Atlas.  Mongoose serves as the interface between pure JavaScript business logic (actually TypeScript) and the MongoDB, while GraphQL defines how the client front end can interact with the application data.  The Nest framework loosely couples the Mongoose and GraphQL components together, and provides additional tooling that minimizes the manual creation of much of the boilerplate code that these tools depend upon.  Nest encapsulates the Web API layer, routing requests to the various components, and wiring together addional tooling.  The front-end client is built using Blazor WASM and it talks to the Web API to retrieve and modify application data.  Finally, Jest is the testing framework that enables unit testing of each component, as well as end-to-end (E2E) testing of the overall applicaiton.

The guiding principles that led to these choices of building blocks (Jest, Nest, Mongoose, GraphQL, and Blazor) were:
1. Free - lots of things are free, but for this project free means more than not having to pay for a tool.  In this project free means that every slice of the application also has suitable free hosting options where it can be developed, tested, and *deployed* during development (and possily even production).
1. Popularity - the tooling should have a broad user base and ideally be a market leader in their particular segment.
1. Cohesive - each piece must work well with the others.

MongoDB's Atlas cloud service provides free hosting for the data repository suitable at least for development and quite possibly production deployments of a small to medium sized application.  The Nest-Mongoose-GraphQL Web API runs under node, which can be deloped and hosted entirely on Glitch or other Node cloud hosting services.  Meanwhile, the Blazor WASM front end is essentially a static website, suitable for deployment on GitHub Pages, Azure Static Pages, etc.

## Readme Driven Development Methodology

TDD, or test driven development, is a development methodology wherein you first develop tests for your application using a testing framework such as Jest, *before* impelementing the product code.  Readme driven development is a further refinement of this methodology, where you first describe a feature of the application in a readme file prior to writing your tests.  Thus the readme file for this project serves the purpose of providing basic documentation of what this project does and what this project will eventually do as it is being further developed and refined.

## API

Authentication and authorization to the API are provided by REST endpoints for creating a login, changing a password, and verifying credentials.  The rest of the API is implemented as GraphQL queries and mutations, secured by a JWT token provided by a successful login.

The following REST endpoints support user authentication:
Endpoint | Header | Body | Response
------------ | ------------- | ------------- | -------------
../auth/login | N/A | email: string, password: string | JWT token or error
../auth/register | JWT token (admin) | name: string, email: string (unique), password: string (complexity) | newUser (JSON) or error
../auth/setPassword | JWT token (admin) | email: string, password: string (complexity) | success or error

## Next steps
1. Create Nest application
    1. Add support for Mongoose
    1. Add support for GraphQL
    1. Connect to MongoDB
    1. Test GraphQL API
1. Add Blazor WASM
   1. Setup deployment to GitHub pages
   1. Test Blazor
1. Connect Blazor to API
   1. Implement CORS
   1. Test E2E
