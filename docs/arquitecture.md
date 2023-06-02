# Arquitecture

## About the project

##### Frontend

1. **Nextjs**
   - ISR (on demand): stores pages are generated at build time. But stores can update their info so everytime there is an update we send a request from backend to nextjs api to trigger an on-demand update of that page using ISR
   - friendly url: all store pages are generated dinamically so we include a friendly url for SEO purposes
   - middleware: using middleware to validate jwt without needed to go to backend so we ensure that if client goes to a protected route then we will take actions if tokens are not valid. We also refresh tokens if needed.
   - api: just a single api endpoint for ISR on demand a store page when its updated (action triggered from backend when store admin update some store item)
   - translation (next-i18next): using this module to handle translation (we only have spanish for now)
2. **mui and emotionjs**: we use `mui` as our css component library and `emotionjs` as our style engine to build components. We attempeted to use `styled-components` but there were some issues with next build that coun't be solved so we moved to `emotionjs` as its also the default style engine for `mui`.
3. **graphql**: we use complex graphql query and mutations thanks to `typegraphql` that has already built many of them.

   - fragments: pieces of graphql that can be used in more than one place to avoid code repetition.

4. **apollo**
   - state management: we don't use redux for state managent but rather apollo cache and its local state strategy (https://www.apollographql.com/docs/react/local-state/local-state-management/)
   - suscription: we use apollo suscription with websocket for some feature
5. **other third party packages**
   - cloudinary: used to upload and host images in their services
   - react-hook-form: used to manage forms. Many form elements has been built with `mui + react-hook-form` to manage the form state
   - yup: used with `mui` and `react-hook-form` for form validation
   - amplitude: used to track some events for analytics

##### Backend

1. typegraphql
   - decorator: used to apply authentication and authorization on resolvers (graphlq api).
   - middleware: used to catch all errors and make adjustment if needed like changing a message to the user to be more friendly or make silent logs
   - resolvers: this is like the graphlq api that allows client to communicate with backend
   - service: piece of code that can be injected in some clases. This example includes a logger class that print logs in a custom way
2. graphql: most of the job is done by typegraphql by creating all CRUD resolvers and queries. Suscription and business logic code has been created following typegraphql examples
3. prisma: this is our ORM for database communication
   - seed: there is a script that uses `PrismaClient` to perform database queries. We have created arrays and objects with relations between them and then this script is in charge of reading them and apply all connections between those objects.
   - postgresql: in some cases prisma won't allow us to do complex `postgresql` query so we apply them manually with prisma by sendimg the `postgresql` query directly to prisma
   - schema.prisma: this is the file that contains all the relations between models and also includes some `enums` like `ROLE` and `STATUS`
4. apollo-server: we use apollo to manage graphlq server and suscription with websocket
5. mailer: we use sendgrid for production and nodemailer for development
6. cron job: some features allow admin stores to create some publications. Those publications has an expire time so we created a cron job that delete expired publications every day
7. jwt: we use jwt to identify an authenticated user
   - cookies & header: we choose to work with cookies on production but for development purposes there is change a new member won't have access to all projects. So if they start with frontend then he will use other method to transmit `jwt` between local frontend and hosted backend that involves cookies, headers and CORS plugin

## Repositories

The project is divided in 5 github repositories.

- Fronted: its divided into 3 repositories

  - **user**: repository where regular users can access the web page
    https://github.com/MaxiSantos/donde-frontend-next

  - **admin** repository where store admin can access the web page
    https://github.com/MaxiSantos/donde-frontend-admin

  - **common**: repository containing common folders and files between user and admin
    https://github.com/MaxiSantos/donde-frontend-common

- Backend: it contains only one repo

  https://github.com/MaxiSantos/donde-backend-p2-typegraphql

- Documentation

  https://github.com/MaxiSantos/donde-documentation

## Branches

3 main branches are used in all 4 repositories (user, admin, common and backend)

- main: for production

  - frontend: dondelobusco.com
  - backend: api.dondelobusco.com

- staging: for testing

  - frontend: test.dondelobusco.com
  - backend: api.test.dondelobusco.com

- development: for local development

All branches are protected and need pull-request approval to be merged. In case of critical bug to fix in production we will use `hot-fix` branch. All other branches should follow this convention `feat/feature_name`, `bug/short_bug_name` or your name
