# Setup

## Permission

You need to be added as collaborator in private repos to clone them. Then we suggest to use ssh to communicate with github

#### configure ssh

1. Generating ssh keys
   https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

2. Troubleshooting

- Connection timed out:
  -- create config file in ssh folder:
  https://gist.github.com/Tamal/1cc77f88ef3e900aeae65f0e5e504794
  -- if needed you will need to add more settings:
  https://blog.51cto.com/u_15936016/6006760

```bash
Host github.com
User xxxyouremail@qq.com
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/xxxyour_private_key
Port 443
```

## Frontend

You will need to do this in both user and admin repositories

1. clone common, shared, documentation, user and admin repository
2. switch to `development` branches in each repo and create a custom branch for you.
3. go to root project folder (user and admin) and create symlink to public folder and docs.

```bash
  mklink /D public ..\donde-frontend-common\public
  mklink /D docs ..\donde-documentation\docs
```

4. go to app folder (user and admin) and create symlink to common and shared folder

```bash
  mklink /D common ..\..\donde-frontend-common\common
  mklink /D shared ..\..\donde-shared\shared
```

> `mklink` only works in symbol of system (not powershell nor gitbash)

or use `cp -r`

5. create env.local file from sample.env

If you **DONT HAVE ACCESS TO BACKEND** then you will need to install CORS extension (https://mybrowseraddon.com/access-control-allow-origin.html) into your browser and set this value in your env file

```
NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header
NEXT_PUBLIC_API_ENDPOINT='https://api.test.dondelobusco.com'
NEXT_PUBLIC_WS_ENDPOINT='wss://api.test.dondelobusco.com'
```

> If you dont find this extension in your browser you may try installing the chrome extension version with this other plugin: **Install Chrome Extensions**

> `NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header` will allow you to work with a local version of you frontend while you communicate with backend hosted in the cloud

6. Install all dependencies with `yarn install`
7. Run frontend server in development mode with `yarn run dev`

> In case you have problems running this command in vscode powershell then do this: https://www.youtube.com/watch?v=gm0gexHWDy0

8. Go to http://localhost:3000

- user site
  - user: user regular 1
  - password: password1234.
- admin site
  - user: user govinda
  - password: password1234.

## Backend

1. clone backend and documentation repo
2. switch to `development` branch in backend repo and create a custom branch for you
3. go to root project folder and create symlink for docs folder

```bash
  mklink /D docs ..\donde-documentation\docs
```

4. create `.env` file from `sample.env`

5. create a local server for database (prefered to use pgadmin and connection data from `DATABASE_URL` in `.env` file)
   a. host: localhost
   b. username: postgres
   c. port: 5432
   d. maintenance database: postgres

6. install dependencies with `yarn install`
7. create database

   1. You first need to create the database: dondelobusco
   2. Then apply prisma command to create tables and relations based on schema
      https://www.prisma.io/docs/concepts/components/prisma-migrate/db-push#choosing-db-push-or-prisma-migrate

   ```bash
     prisma db push or yarn run prisma db push
   ```

   > `prisma migrate or prisma db push` says database name will be created if not found but its not true so you must create the database (7.1)

   3. seed data with

   ```bash
   yarn run prisma:db-seed
   ```

8. start server
   `yarn run dev`

9. go to http://localhost:8000/graphql and test this graphql query

```graphql
query ExampleQuery {
  stores {
    name
  }
}
```

## Documentation

You should create a symlink of documentation repository under each project so you will have access to that repo under the same project

1. clone documentation repository: https://github.com/MaxiSantos/donde-documentation

2. create symlink

```bach
  mklink /D ./path_to_destiny_project/docs ./path_to_documentation_repo./docs
```

3. go to docs folder and run
   `docsify serve -- port 3020`
