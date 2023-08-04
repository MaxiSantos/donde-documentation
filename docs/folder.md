# Project Folder

## Frontend

- app

  - components: all ui related code

    - elements: single elements like buttons, grid, form
    - sections: pieces of code that can be considered its own view and can be placed in more than one place like footer, header, sidebar, ErrorMessage
    - pageTemplate: react view built with elements, sections and more to be loaded by `pages`

  - config: configuration related to the project such as setting up which pages are protected by authorization and role

  - graphql: all graphlq related code

    - fragments
    - mutations
    - queries

  - hooks: react hooks

  - lib: some helpers

  - common: this folder is intended to have common code to be shared with user and admin project. We have common code that belongs to folders such as components, config, graphql, hooks, and pages plus other folders
    - components
      - layout: here we define the layouts to be used. Basically user will use default layout (header, container and footer) and admin will use sidebarLayout (same as default but with sidebar manu for dashboard navigation)
    - scripts: some script like bumping version
    - styles: setting up mui theme and some other css styles like normalization.css
    - constants: TODO: this should be in shared repo.. it contains some contants variables and types

- pages: nextjs pages using `layout` and `pageTemplate` plus related code to backend like `getStaticProps`.

- public: public nextjs folder

  - locales: inext18 translation folders

- middleware.ts: middleware that controlls access to pages and also check for jwt plus refresh-token

## Backend

- prisma
  - seedData: seed data for development purpose
  - seed.ts: script for seed database operation
  - schema.prisma: file generated with prisma (**can not** be modified manually)
- src
  - api: need to be refactored
    - context.ts: context file from apollo
    - db.ts: prisma instance
  - config: some constants
  - graphql: all typegraphl related code
    - decorator
      - Authorization.ts: in charge of validating user existance, correct role and correct status. We add this decorator in all those places where we need to check authorization and authentication when defining the schema in `server.ts`
    - errors: Apollo and Graphql custom errors
    - middleware
      - ErrorInterceptor.ts: logs erros with more details and it can change the message to be more friendly
    - resolvers: this is where all the graphql api belongs divided by models it contains `types`, `args` and the `resolver` itself
    - service: example of typegraphql services like a logger that is injected into ErrorInterceptor
    - server.ts: Apollo server configuration plus suscription
  - scripts: some scripts like bumping up backend and web version
  - templates: html templates for sending emails
  - utils: helpers like logging, time, mailer
  - index.ts: it initialize the server, a cron job and it contains some REST apis like refresh-token
