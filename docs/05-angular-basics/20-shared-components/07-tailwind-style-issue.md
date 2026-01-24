# Tailwind Style Issue

I have a multi-project angular monorepo workspace. I have a library project to share re-usable components. I have a re-usable header component. I have another project in the same monorepo to test the components in the library project. The header component styles and functionality are working fine when tested in the monorepo. I have used tailwind css to style the header component. Then I have another project in another location outside of the mono repo. I have run pnpm link in the dist/lousing-ui of the mono-repo. And ran pnpm link lousing-ui the project consuming it. I have also updated and angular.json of the consuming app to preserve symlinks, vendor sourcemap set to true, excluded lousing-ui from prebundle. I could import and use the header component. But the tailwind styles are broken for the header component. The tailwind styles used in the consuming app are working fine. how to ensure styles used in re-usable components are not broke in consuming apps?

Below is the angular.json of the consuming app
```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "cli": {
    "packageManager": "npm",
    "analytics": false
  },
  "newProjectRoot": "projects",
  "projects": {
    "frontend": {
      "projectType": "application",
      "schematics": {},
      "root": "",
      "sourceRoot": "src",
      "prefix": "app",
      "architect": {
        "build": {
          "builder": "@angular/build:application",
          "options": {
            "preserveSymlinks": true, // added this property
            "browser": "src/main.ts",
            "tsConfig": "tsconfig.app.json",
            "assets": [
              {
                "glob": "**/*",
                "input": "public"
              }
            ],
            "styles": [
              "src/material-theme.scss",
              "src/styles.css",
              "node_modules/@lousing/ui/src/assets/styles.css" // added this property
            ]
          },
          "configurations": {
            "production": {
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "500kB",
                  "maximumError": "1MB"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "4kB",
                  "maximumError": "8kB"
                }
              ],
              "outputHashing": "all"
            },
            "development": {
              "optimization": false,
              "extractLicenses": false,
              "sourceMap": {
                "scripts": true,
                "styles": true,
                "vendor": true // added this property
              }
            }
          },
          "defaultConfiguration": "production"
        },
        "serve": {
          "builder": "@angular/build:dev-server",
          "options": {
            "prebundle": {
              "exclude": ["lousing-ui"] // added this property
            }
          },
          "configurations": {
            "production": {
              "buildTarget": "frontend:build:production"
            },
            "development": {
              "buildTarget": "frontend:build:development"
            }
          },
          "defaultConfiguration": "development"
        },
        "test": {
          "builder": "@angular/build:unit-test"
        }
      }
    }
  }
}
```


Solution: 
1. run the below command in the root of monorepo.
```sh
tailwindcss -i ./projects/lousing-ui/src/styles.css -o ./dist/lousing-ui/src/styles.css --minify"
```
2. update `angular.json`'s styles to 
```
"styles": [
  "src/material-theme.scss",
  "src/styles.css",
  "node_modules/lousing-ui/src/styles.css"
]
```

