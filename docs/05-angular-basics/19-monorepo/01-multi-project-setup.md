# Multi-project setup

## What is mono repo?
It is a single repository workspace containing multiple angular projects with global configuration.

## Why mono repo?
- Simplifies code sharing. You can create libraries that can be share across projects


## How to setup?
Run the below command to create an empty workspace. Later add projects and libraries.
```sh
ng new lousing-ng-workspace --no-create-application --package-manager=pnpm --skip-install 
cd lousing-ng-workspace
code .
pnpm install
ng generate library lousing-ui
ng generate application lib-tester
```


## Reference
> https://angular.dev/reference/configs/file-structure#multiple-projects
> https://angular.dev/tools/libraries/creating-libraries
> https://angular.dev/tools/libraries/creating-libraries#publishing-your-library
> https://github.com/ng-packagr/ng-packagr/blob/main/docs/copy-assets.md


