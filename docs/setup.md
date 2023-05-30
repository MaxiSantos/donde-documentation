# Setup

## Permission

You need to be added as collaborator in private repos to clone them. Then we suggest to use ssh to communicate with github

#### configure ssh

1. Generating ssh keys
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

2. Troubleshooting

+ Connection timed out:
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

1. clone common, user and admin repository
2. switch to development branches in each repo
3. go to root project folder (user and admin) and create symlink to public folder
```bach
  mklink /D public ..\donde-frontend-common\public
```
4. go to app folder (user and admin) and create symlink to common folder
```bach
  mklink /D common ..\..\donde-frontend-common\common
```

> ```mklink``` only works in symbol of system (not powershell nor gitbash)

or use `cp -r`

5. create env.local file from sample.env

If you **DONT HAVE ACCESS TO BACKEND** then you will need to install CORS extension (https://mybrowseraddon.com/access-control-allow-origin.html) into your browser and set this value in your env file
```
NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header
NEXT_PUBLIC_ENDPOINT='https://api.test.dondelobusco.com'
NEXT_PUBLIC_WS_ENDPOINT='wss://api.test.dondelobusco.com'
```

> If you dont find this extension in your browser you may try installing the chrome extension version with this other plugin: **Install Chrome Extensions**

> `NEXT_PUBLIC_TOKEN_PAYLOAD_STRATEGY=header` will allow you to work with a local version of you frontend while you communicate with backend hosted in the cloud

6. Install all dependencies with `yarn install`
7. Run frontend server in development mode with `yarn run dev`

> In case you have problems running this command in vscode powershell then do this: https://www.youtube.com/watch?v=gm0gexHWDy0
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
