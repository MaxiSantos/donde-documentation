# Setup

## Permission

- get ssh keys
- configure your git

## Frontend

You will need to do this in both user and admin repositories

1. clone common repository
2. clone user or admin repository
3. create symlink to common folders into main project

```bach
  mklink /D ./app/common ./common/common
  mklink /D ./public ./common/public
```

or use `cp -r`

4. create env.local file from sample.env

If you **DONT HAVE ACCESS TO BACKEND** then you will need to install CORS extension (https://mybrowseraddon.com/access-control-allow-origin.html) into your browser and set this value in your env file
`NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header`

> If you dont find this extension in your browser you may try installing the chrome extension version with this other plugin: **Install Chrome Extensions**

> `NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header` will allow you to work with a local version of you frontend while you communicate with backend hosted in the cloud

5. Install all dedpendencies with `yarn install`
6. Run frontend server in development mode with `yarn run dev`

## Backend

You need to prepare database and then install backend

### Database

### Backend

## Documentation

You should create a symlink of documentation repository under each project so you will have access to that repo under the same project

1. clone documentation repository: https://github.com/MaxiSantos/donde-documentation

2. create symlink

```bach
  mklink /D ./path_to_destiny_project/docs ./path_to_documentation_repo./docs
```
