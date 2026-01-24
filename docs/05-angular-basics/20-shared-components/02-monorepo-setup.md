# Mono Repo Setup

🔥**WARNING**
- I had issue on copying assets in nx monorepo
- So I resorted to monorepo setup via angular/cli
- First I generated an empty workspace
- Then I generated a library project

```sh
ng new lousing-ng-workspace --no-create-application --package-manager=pnpm --skip-install
cd lousing-ng-workspace
pnpm install
ng generate library lousing-ui
```

## Make sure the library build is configure properly in the root's tsconfig.json
```json
{
  "compilerOptions": {
    "paths": {
      "@lousing/ui": [
        "./dist/@lousing/ui"
      ]
    }
  }
}
```


## Reference
> https://angular.dev/tools/libraries/creating-libraries

