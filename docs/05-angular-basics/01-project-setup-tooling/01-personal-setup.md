# Personal Setup

## Project Metadata

- Repository: https://github.com/neutral-00/practice-angular
- branch: main

## Learning Objective

1. [x] Setup base project

## Pre-requisites

- First install nvm, nodejs, pnpm and angular cli. Google it, you can do it.
- Also install vs code and the extension: Angular Language Service
- At the time of writing, I have
  - NodeJS: 22.x
  - Angular CLI: 21.x
  - pnpm: 10.x

**⚠️ WARNING**

> look out for node and angular version compatibility

## Create the project - standalone way(default after v17)

```sh
ng new practice-angular --skip-install --package-manager=pnpm
cd practice-angular && pnpm install
```

## Create the project the old way - module way

If you want to fall back to the older module approach then run the below command

```sh
ng new practice-angular-old --skip-install --package-manager=pnpm --no-standalone
cd practice-angular-old && pnpm install
```

## Run

```
pnpm start
```
