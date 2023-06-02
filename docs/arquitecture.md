# Arquitecture

## About the project

The project is divided in 4 github repositories.

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
