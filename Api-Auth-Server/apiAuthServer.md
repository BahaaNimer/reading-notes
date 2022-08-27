# API-AUTH-Server

## Dynamic API Server

An `Express/Node.js` based server designed to be a “model agnostic” REST API server, which can perform CRUD operations on any data model

## Support all REST/HTTP methods

- GET: Retrieve record(s) from a data source
  - All
  - One (by id)
  - Some (by filtering)
- POST: Create a new record in a data source
- PUT: Update a single full record in a data source
- PATCH: Update part of a single record in a data source
- DELETE: Delete a record in a data source

## Obey a standard routing structure

`i.e. http://amazingapi.com/api/v1/products/12345`

- `/api/v#` where # is the version number of our API

  - /model where ‘model’ is the name of the data model to operate on
    - /id where ‘id’ is the id number of a specific entity in the data model

- Allow for Query String parameters for filtering

  - `i.e. http://amazingapi.com/api/v1/products?category=electronics`

  - This would GET every entry in our products data model where the category is ‘electronics’

## Obey a standard output format

- Results will be returned in JSON format

- Results will be served with the correct HTTP header - `application/json`

- The GET Route, when not retrieving by ID, must return a full header, with count ,pages, and a results array

- All other routes must return a single object, representing the state of the entity following the operation

## Technical Requirements

The application will be created with the following overall architecture and methodologies

1. Node.js.
2. ES6 Classes and best practices.
3. ExpressJS Web Server, built modularly.

   - Middleware for handling 404 and 500 conditions

   - Middleware for handling the dynamic loading of the correct data model as specified in the route

     - Inspect the route, looking for the model name

     - `require()` the correct module model (i.e. if the model is categories, `require('src/models/categories/categories-model.js')`)

   - Use a single router (`v1.js`) to handle the ReST methods for CRUD for any model

     - `express.params` middleware

4. Persistence using a Mongo Database (NoSQL).

5. Mongoose Schemas (data models) to define and model data.

6. Mongoose Model “wrapper” class to serve as the API between the express server and the data models themselves.

7. Test Driven Development, using Jest.

- Tests will be runnable locally
- Tests will auto-execute (CI) in your repo using GitHub actions
- Tests will use a 3rd party library called `supergoose` to:
  - “mock” the mongo running database
  - “mock” the running Express server
    Deployment to Heroku

## Data Models

## Application Structure

## Development Process, Milestones

### Phase 1: API Basics

- Use JSON Server (non-express) to mock the routes for testing purposes

### Phase 2: Basic API

- Create CRUD/ReST endpoints for categories and products
- Separate route modules for each data model type
- Store user created data in memory (no persistence)
- Integrates with an online CI framework

### Phase 3: Persistence

- Replace the in-memory data store with mongo
- Use Mongo Collections for each data model type

### Phase 4: Dynamic Models

- Create a single model class that all data models can inherit from to keep the interface simple
- Use middleware to load models based on param
  - i.e. Replace `app.get('/api/v1/categories')` and `app.get('/api/v1/products')` with `app.get('/api/v1/:model')`
- API is Fully Documented
- API is deployed and running live

## Authentication Server

An Express/Node.js based server using a custom “authentication” module that is designed to handle user registration and sign in using Basic, Bearer, or OAuth along with a custom “authorization” module that will grant/deny users access to the server based on their role or permissions level.

1. Users can create an account, associated with a “role”
2. User Roles will be pre-defined and will each have a list of allowed capabilities
   - `admin` can read, create, update, delete
   - `editor` can read, create, update
   - `writer` can read, create
   - `user` can read
3. Users can then login with a valid username and password
4. Alternatively, users can login using an OAuth provider such as `Google` or `GitHub`
   - In this case, users should be automatically assigned the role of `user`
5. Once logged in, Users can then access any route on the server, so long as they are permitted by the capabilities that match their role.
   - For example, a route that deletes records should only work if your user role is `“admin”`

## Technical Requirements For Server

The application will be created with the following overall architecture and methodologies

1. Node.js

2. ES6 Classes and best practices

3. ExpressJS Web Server, built modularly

   - “Auth” routes for handling the login and authentication system
     - POST `/signup` to create an account
     - POST `/signin` to login with Basic Auth
     - GET `/oauth`
   - Middleware for handling 404 and 500 conditions
   - Middleware for handling each type of authentication
     - Basic (username + password) to be used on the `/signin` route only
       - i.e. `app.post('/signin', basicAuthentication, (req, res) => { ... })`
     - OAuth (3rd Party) to be used on the `/oauth` route only
       - i.e. `app.get('/oauth', OAuth, (req, res) => { ... })`
       - Handles the handshake process from a 3rd party OAuth system
     - Bearer (token) to be used on any other route in the server that requires a logged in user
       - i.e. `app.get('/secretstuff', tokenAuthentication, (req, res) => { ... })`
   - Middleware for handling authorization
     - To be run after Bearer Middleware on routes to be protected
     - Accepts a “capability” as a parameter
     - i.e. `app.delete('/secretstuff', tokenAuthRequired, capability('delete'), (req, res) => { ... })`

4. User Persistence using a Mongo Database (NoSQL)
   - Mongoose Schemas (data models) to define and model data
5. Test Driven Development, using Jest
   - Tests will be runnable locally
   - Tests will auto-execute (CI) in your repo using GitHub actions
   - Tests will use a 3rd party library called `supergoose` to:
     - “mock” the mongo running database
     - “mock” the running Express server
6. Deployment to Heroku

## Data Model

## Application Structure For Server

## Development Process, Milestones For Server

1. Phase 1: Basic Authentication

   - Create a basic express server with the following features:
     - Users Model (Mongoose Schema)
     - `/signup` route that creates a user
     - `/signin` route that attempts to log a user in
     - `BasicAuth` middleware that validates the user as a part of the `/signin` process
   - Implement: Modularize and Test a starter server

2. Phase 2: Bearer Authentication
   - Re-Authenticate Users
   - Accepts a TOKEN in the Authorization: Bearer header
   - Validates the user
   - Allows or Denies access to the route handler
   - Implement: Debug, Extend Token Security
3. Phase 3: Authorization
   - Role Based Authorization System
   - Combines the Bearer Token with User roles to give fine grained access control
   - Implement: Protect API Routes, Write tests
