# Publish to npm registry

I have 
- updated the project name as `@lousing/ui` in the package.json and ng-package.json
- build the library with `ng build @lousing/ui`
- compiled tailwindcss
```
tailwindcss -i ./projects/lousing-ui/src/assets/styles.css -o ./dist/@lousing/ui/src/assets/styles.css -
-minify"
```
- opened browser and created an account in `https://registry.npmjs.org/`
- Visited `https://www.npmjs.com/org/create`
- created an organization name `lousing` since my package is scoped at `@lousing`
- 🔥**WARNING**
- Adding new TOTP (time-based one-time password) two-factor authentication is no longer supported.
- Visited https://npmjs.com/settings/neutral-00/tfa and generated a security key for 2FA.
- finally published with
  ```bash
  cd dist/@lousing/ui
  npm publish --access public
  ```


## INFO
  Or for private scope:
  ```bash
  npm publish --access restricted
  ```

- **Consume in other projects**:
  ```bash
  npm install @lousing/ui
  ```

👉 Best for: Sharing across machines/teams with versioning and easy installation.

---
