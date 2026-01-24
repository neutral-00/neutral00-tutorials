# Configure library assets

Update ng-package.json as shown below:
```json
{
  "$schema": "../../node_modules/ng-packagr/ng-package.schema.json",
  "dest": "../../dist/lousing-ui",
  "lib": {
    "entryFile": "src/public-api.ts"
  },
  "assets": ["src/assets/**/*"]
}
```
